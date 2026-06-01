# Sprint Backlog — Red Social

---

## Contexto

El producto base ya está completo y desplegado en producción. Los siguientes sprints están orientados a mejorar la experiencia del usuario, agregar funcionalidades sociales más profundas y fortalecer la calidad del sistema.

---

## Sprint 1 — "Experiencia de usuario"
**Duración:** 2 semanas  
**Objetivo:** Mejorar la interacción del usuario con la plataforma — likes inteligentes, navegación más fluida y feedback visual en tiempo real.

---

### Sprint Goal

> Que el usuario pueda interactuar con los posts de forma más precisa, viendo en todo momento si ya dio like, con una navegación más intuitiva entre perfiles y publicaciones.

---

### Sprint Backlog

| ID | Historia | Descripción | Prioridad | Estimación |
|----|----------|-------------|-----------|------------|
| SP1-01 | Likes inteligentes | Al cargar los posts, marcar visualmente cuáles ya tienen like del usuario logueado | Alta | 3 pts |
| SP1-02 | Endpoint de likes por usuario | Crear `GET /api/posts/mis-likes` que devuelva los post_ids que el usuario ya likeó | Alta | 2 pts |
| SP1-03 | Prevenir likes duplicados | Validar en frontend y backend que un usuario no pueda dar like dos veces al mismo post | Alta | 3 pts |
| SP1-04 | Contador de posts en perfil | Mostrar cuántas publicaciones tiene el usuario en su perfil | Media | 1 pt |
| SP1-05 | Botón volver en post-detalle | Mejorar la navegación con un botón que regrese a la página anterior | Baja | 1 pt |
| SP1-06 | Mensaje de bienvenida en index | Si el usuario tiene sesión mostrar "Bienvenido, @username" en el header | Baja | 1 pt |

**Total:** 11 puntos

---

### Criterios de aceptación del Sprint

- El botón de like muestra estado correcto (rojo = ya likeado, gris = sin like) al cargar la página
- Un usuario no puede dar like más de una vez al mismo post
- El perfil muestra el número total de publicaciones
- El botón volver en post-detalle funciona correctamente en móvil y desktop

---

### Definition of Done

- Funcionalidad probada manualmente en Netlify
- Sin errores en la consola del navegador
- Responsivo en móvil y desktop
- Cambios subidos a GitHub y redesplegados en Railway/Netlify

---

### Tareas técnicas

**SP1-01 y SP1-02 — Likes inteligentes:**
1. Crear endpoint `GET /api/posts/mis-likes` en el backend
2. Agregar la ruta en `post.routes.js`
3. Agregar el controlador `getMisLikes` en `post.controller.js`
4. En `index.html` hacer fetch a `/mis-likes` antes de renderizar los posts
5. Comparar cada post con la lista de likes del usuario y marcar el botón

**SP1-03 — Prevenir duplicados:**
1. Crear índice único en MongoDB: `{ post_id: 1, user_id: 1 }`
2. En el frontend deshabilitar el botón de like si ya está marcado como liked

**SP1-04 — Contador de posts:**
1. En `perfil.html` contar `misPosts.length` y mostrarlo debajo del username

**SP1-05 — Botón volver:**
1. Cambiar `← Volver` en `post-detalle.html` para usar `history.back()`

**SP1-06 — Mensaje de bienvenida:**
1. En `index.html` verificar si hay usuario en localStorage y mostrar el saludo

---

## Sprint 2 — "Comunidad"
**Duración:** 2 semanas  
**Objetivo:** Agregar funcionalidades que fomenten la interacción entre usuarios — comentarios, edición de perfil y mejoras en la búsqueda.

---

### Sprint Goal

> Que los usuarios puedan comentar publicaciones, editar su información de perfil y encontrar contenido de forma más precisa con filtros avanzados.

---

### Sprint Backlog

| ID | Historia | Descripción | Prioridad | Estimación |
|----|----------|-------------|-----------|------------|
| SP2-01 | Comentarios en posts | Agregar sección de comentarios en post-detalle.html | Alta | 5 pts |
| SP2-02 | Endpoint de comentarios | Crear rutas `POST` y `GET` para comentarios en el backend | Alta | 4 pts |
| SP2-03 | Editar perfil | Permitir al usuario cambiar su username, bio y avatar_url | Media | 4 pts |
| SP2-04 | Endpoint editar perfil | Crear ruta `PUT /api/users/me` en el backend | Media | 3 pts |
| SP2-05 | Filtro por tags en búsqueda | En posts.html permitir filtrar únicamente por tags con prefijo # | Media | 2 pts |
| SP2-06 | Paginación de posts | Cargar posts de 9 en 9 con botón "Ver más" en index.html | Baja | 3 pts |

**Total:** 21 puntos

---

### Criterios de aceptación del Sprint

- Un usuario autenticado puede escribir y publicar comentarios en cualquier post
- Los comentarios muestran el autor y la fecha
- El usuario puede actualizar su username y bio desde su perfil
- La búsqueda con #tag filtra únicamente por esa etiqueta
- El index carga los primeros 9 posts y permite cargar más

---

### Definition of Done

- Funcionalidad probada manualmente en Netlify
- Nuevos endpoints documentados
- Sin errores en la consola del navegador
- Responsivo en móvil y desktop
- Cambios subidos a GitHub y redesplegados en Railway/Netlify

---

### Tareas técnicas

**SP2-01 y SP2-02 — Comentarios:**
1. Crear colección `comments` en MongoDB con campos: `post_id`, `user_id`, `author_username`, `content`, `created_at`
2. Crear `Comment.js` en `src/models/`
3. Crear `comment.controller.js` con funciones `addComment` y `getComments`
4. Crear `comment.routes.js` con rutas `POST /api/comments` y `GET /api/comments/:postId`
5. Agregar la sección de comentarios en `post-detalle.html`

**SP2-03 y SP2-04 — Editar perfil:**
1. Crear ruta `PUT /api/users/me` en el backend protegida con JWT
2. Crear controlador que actualice `username`, `bio` y `avatar_url`
3. Agregar formulario de edición en `perfil.html` con campos editables
4. Al guardar, actualizar también el localStorage con los nuevos datos

**SP2-05 — Filtro por tags:**
1. En `posts.html` detectar si el query empieza con `#`
2. Si es así filtrar únicamente por tags, no por contenido ni autor

**SP2-06 — Paginación:**
1. En `index.html` mostrar solo los primeros 9 posts
2. Agregar botón "Ver más" que cargue los siguientes 9
3. Ocultar el botón cuando no haya más posts

---

## Resumen de sprints

| Sprint | Objetivo | Historias | Puntos | Duración |
|--------|----------|-----------|--------|----------|
| Sprint 1 | Experiencia de usuario | 6 | 11 pts | 2 semanas |
| Sprint 2 | Comunidad | 6 | 21 pts | 2 semanas |
