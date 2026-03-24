

## Material Didáctico - Semana 8: CRUD Read (Básico)

¡Bienvenidos a la Semana 8, jóvenes! 

Hasta este punto, hemos trabajado en estructurar nuestra información y diseñar nuestros documentos (JSON/BSON). A partir de hoy, entramos al Segundo Parcial y cambiamos de fase: vamos a empezar a "hablar" con nuestros datos.

El rol protagónico de esta semana es el de **The Query Developer**, pero todo el equipo debe comprender cómo funcionan estas consultas.

Aquí les dejo la guía de trabajo para nuestras sesiones.

---

### 1. Objetivos de la Sesión
* Entender cómo pasamos del clásico `SELECT` de SQL a interactuar con documentos usando **MQL (MongoDB Query Language)**.
* Dominar las operaciones básicas de lectura: `find()` y `findOne()`.
* Aprender a hacer **Proyecciones**, es decir, pedirle a la base de datos exactamente los campos que necesitamos y nada más (para no saturar la red).

### 2. Contexto Teórico: Hablando con la Base de Datos

En este semestre aprendieron que en SQL usamos sentencias estructuradas. En MongoDB, la lógica cambia: le pasamos a la base de datos documentos JSON con las condiciones de lo que estamos buscando.

La estructura básica de una consulta en MQL tiene dos partes principales (ambas son objetos JSON):

1.  **El Filtro (Query):** ¿Qué documentos cumplen la condición? (Es su equivalente al `WHERE`).
2.  **La Proyección (Projection):** ¿Qué datos específicos quiero ver de esos documentos? (Es su equivalente a nombrar las columnas en el `SELECT`).

### 3. Dinámica con su IA (AI Pair Programmer)

Recuerden que la IA es su tutor 24/7. Antes de empezar a tirar código, abran su chat con ChatGPT o Gemini, asegúrense de haber introducido el **Meta-Prompt** del curso (el que definimos en la Semana 0) y envíenle la siguiente instrucción adaptada a su proyecto ABP:

> *"Explain the difference between SQL `SELECT *` and MongoDB `db.collection.find({})`. Show me examples using my schema. My project is about [AQUÍ PONGAN EL TEMA DE SU PROYECTO, ej. RPG Inventory System o Tech Job Board]."*

Lean la explicación, analicen los ejemplos y pregúntenle si algo no queda claro. ¡No copien y peguen sin entender!

### 4. Práctica de Código (El Entregable)

A continuación está la plantilla que deberán adaptar a su proyecto. Este código debe probarse primero en **MongoDB Compass** o en su extensión de VS Code. 

**OJO CON LAS REGLAS:** Recuerden que las colecciones (Entidades) van en `UPPER_SNAKE_CASE` (ej. `STUDENT`, `INVENTORY_ITEM`), los atributos no llevan prefijos (solo `name`, `status`, no `student_name`) y **todo el código y comentarios deben ir estrictamente en inglés**.

Creen este archivo en su repositorio:
**Ruta:** `/project-root/src/queries/01_simple_find.mongodb`

```javascript
// ============================================================================
// FILE: 01_simple_find.mongodb
// DESCRIPTION: Basic Read operations (CRUD) for the project.
// AUTHOR: [Your Name / Team Name]
// ROLE: The Query Developer
// ============================================================================

// 1. Select the database to use. 
// Replace 'my_abp_database' with your actual database name.
use('my_abp_database');

// ============================================================================
// EXERCISE A: Retrieve a single document
// SQL Equivalent: SELECT * FROM STUDENT LIMIT 1;
// USE CASE: Quickly inspect the JSON/BSON structure of a single record.
// ============================================================================
console.log("--- Executing: findOne() ---");
const singleRecord = db.getCollection('STUDENT').findOne({});
console.log(singleRecord);


// ============================================================================
// EXERCISE B: Retrieve all documents (No filters)
// SQL Equivalent: SELECT * FROM STUDENT;
// USE CASE: Fetch the entire collection (Caution: Only for small datasets).
// ============================================================================
// Note: find() returns a cursor. In Compass/VS Code, it displays the results.
db.getCollection('STUDENT').find({});


// ============================================================================
// EXERCISE C: Basic Filtering (Equality Match)
// SQL Equivalent: SELECT * FROM STUDENT WHERE status = 'active';
// USE CASE: Find exact matches for a specific attribute.
// ============================================================================
// The first parameter is the query document { field: value }
db.getCollection('STUDENT').find({ 
    status: "active" 
});


// ============================================================================
// EXERCISE D: Using Projections (Data shaping)
// SQL Equivalent: SELECT name, age FROM STUDENT WHERE status = 'active';
// USE CASE: Reduce network payload by requesting only necessary fields.
// ============================================================================
// The second parameter is the projection document. 
// Use 1 to include a field, 0 to exclude it. 
// Note: The _id field is always included by default unless explicitly excluded.
db.getCollection('STUDENT').find(
    { status: "active" },           // Query filter
    { name: 1, age: 1, _id: 0 }     // Projection (excluding default _id)
);
```

### 5. Instrucciones de Cierre y Commit

Para finalizar la sesión de hoy y asegurar su calificación de la semana, sigan estos pasos:

1.  Asegúrense de que el script se ejecuta correctamente sin errores sintácticos. Si hay errores, pídanle a su IA que les explique qué falló.
2.  Tomen una captura de pantalla de los resultados arrojados por su consulta con proyección (el Ejercicio D) y guárdenla en la ruta `/tests/screenshots/s8_projection_result.png`.
3.  Hagan el commit semántico en inglés usando la terminal:
    * `git add .`
    * `git commit -m "feat(queries): add basic find and projection scripts"`
    * `git push origin main`

¡Cualquier duda, levanten la mano y paso a sus lugares!
