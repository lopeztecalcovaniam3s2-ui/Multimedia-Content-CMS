### Diseñando para la Escala: MongoDB vs Google Firestore

A simple vista, guardar un "Me Gusta" o registrar una "Visita" parece la misma tarea sin importar la base de datos que utilicemos. Sin embargo, en el mundo NoSQL, el diseño de nuestra información depende directamente de los **límites físicos** y las **fortalezas** del motor que estamos usando. 

Si no diseñamos pensando en la escala, una publicación que se vuelva viral puede consumir todos los recursos o bloquear nuestra aplicación. A continuación, analizaremos cómo resolver esto en dos bases de datos diferentes y el porqué de cada decisión arquitectónica.

---

#### 1. Solución en MongoDB (Aprovechando su motor de actualización)

**Justificación del Diseño:**
* **Visitas (Views):** MongoDB es extremadamente eficiente para realizar actualizaciones matemáticas (atómicas) en un mismo documento. Usar el operador `$inc` para sumar 1 a un contador (`views_count`) es la opción más rápida y limpia. No necesitamos saber *quién* vio el post ni *cuándo*, solo el total, por lo que un número entero basta.
* **Me Gusta (Likes):** ¿Por qué no guardar los *Likes* en un arreglo dentro del post? Porque MongoDB tiene un límite estricto: **ningún documento puede pesar más de 16 MB**. Si el post se vuelve viral y guardamos los IDs de un millón de usuarios dentro del documento del post, el arreglo crecerá infinitamente (conocido como el anti-patrón de *Unbounded Array*) y romperemos la base de datos. Por eso, los *Likes* se extraen a su propia colección, ya que nos interesa saber exactamente *quién* dio like y *cuándo*.

```javascript
// ---
// Core Entity: POST (with a simple integer for views)
// ---
// MongoDB can handle thousands of increments per second on this document.
db.POSTS.insertOne({
  "_id": "post_101",
  "title": "Implementando bases de datos no relacionales",
  "content": "En este proyecto...",
  "user_id": "usr_001",
  "views_count": 0, // A simple number, no need for a separate collection
  "tags": [ { "id": "tag_1", "name": "NoSQL" } ]
});

// ---
// Core Entity: POST_LIKE
// ---
// Likes go to a separate collection because they track WHO liked it.
// If we embedded them, a viral post would hit the 16 MB limit.
db.POST_LIKES.insertOne({
  "_id": "like_992",
  "post_id": "post_101",
  "user_id": "usr_005", // The user who clicked 'Like'
  "created_at": new ISODate("2026-03-16T08:00:00Z")
});

```

---

#### 2. Solución en Google Firestore (Evitando el cuello de botella de escritura)

**Justificación del Diseño:**

* **El problema del límite de escritura:** A diferencia de MongoDB, Firestore tiene una regla estricta para garantizar la sincronización en tiempo real en los dispositivos móviles: **solo puedes actualizar un mismo documento 1 vez por segundo**. Si usáramos un contador de visitas dentro del documento principal y 50 usuarios abren el post al mismo tiempo, 49 de ellos recibirían un error por exceder la cuota y la app fallaría.
* **La solución (Subcolecciones y Eventos):** Para evitar este bloqueo, cambiamos la estrategia a un patrón llamado *Event Logging* (Registro de eventos). A Firestore le cuesta mucho actualizar *el mismo* documento simultáneamente, pero tiene una capacidad masiva para **crear documentos nuevos**. Por lo tanto, cada Visita y cada Like se convierte en la inserción de un documento nuevo dentro de una subcolección (`LIKES` y `VIEWS`). Cuando necesitemos mostrar el total en la pantalla, simplemente le pedimos a Firestore que cuente cuántos documentos hay en la subcolección, una operación que este motor hace de manera optimizada.

```dart
// ---
// Subcollection: LIKES
// Path: /USERS/usr_001/POSTS/post_101/LIKES/like_992
// ---
await db
    .collection('USERS').doc('usr_001')
    .collection('POSTS').doc('post_101')
    .collection('LIKES') // New Subcollection for Likes
    .doc('like_992')
    .set({
  // We save who liked it and when
  'user_id': 'usr_005',
  'created_at': FieldValue.serverTimestamp(),
});

// ---
// Subcollection: VIEWS
// Path: /USERS/usr_001/POSTS/post_101/VIEWS/view_8834
// ---
// Instead of updating a counter, we log an event. 
// Later, to know total views, we just ask Firestore: "Count the documents in this subcollection"
await db
    .collection('USERS').doc('usr_001')
    .collection('POSTS').doc('post_101')
    .collection('VIEWS') // New Subcollection for Views (Event Logging)
    .doc() // Leaving this empty generates an automatic random ID
    .set({
  'created_at': FieldValue.serverTimestamp(),
});

```
