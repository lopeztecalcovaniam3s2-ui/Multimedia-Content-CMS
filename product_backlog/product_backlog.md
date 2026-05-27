# Product Backlog — Red Social
 
---
 
## Product Goal
 
Desarrollar una red social web funcional y desplegada en la nube donde los usuarios puedan registrarse, autenticarse, publicar contenido multimedia, interactuar mediante likes y explorar publicaciones de otros usuarios, desde cualquier dispositivo con acceso a internet.
 
---
 
## Épicas
 
| ID | Épica | Descripción |
|----|-------|-------------|
| E1 | Autenticación de usuarios | Registro, inicio y cierre de sesión con seguridad |
| E2 | Gestión de publicaciones | Crear, visualizar y explorar posts |
| E3 | Interacciones sociales | Likes y visualización de perfiles |
| E4 | Búsqueda y navegación | Buscar posts por texto y tags |
| E5 | Infraestructura y despliegue | Backend, base de datos y frontend en la nube |
 
---
 
## E1 — Autenticación de usuarios
 
### US-01 Registro de cuenta
 
**Como** usuario nuevo  
**Quiero** crear una cuenta con username, email y contraseña  
**Para** acceder a las funciones de la red social
 
**Criterios de aceptación:**
- El sistema valida que todos los campos estén llenos
- El sistema valida que las contraseñas coincidan
- El email y username deben ser únicos en la base de datos
- La contraseña se almacena encriptada con bcryptjs
- Al registrarse exitosamente el usuario recibe un token JWT y es redirigido al inicio
**Gherkin:**
```gherkin
Feature: Registro de usuario
 
  Scenario: Registro exitoso
    Given el usuario está en la página de registro
    When ingresa username "juanito", email "juan@test.com" y contraseña "123456"
    And confirma la contraseña "123456"
    And hace click en "Crear cuenta"
    Then el sistema crea la cuenta en la base de datos
    And guarda el token JWT en localStorage
    And redirige al usuario a index.html
 
  Scenario: Contraseñas no coinciden
    Given el usuario está en la página de registro
    When ingresa contraseña "123456" y confirma "654321"
    And hace click en "Crear cuenta"
    Then el sistema muestra el mensaje "Las contraseñas no coinciden"
    And no crea ningún registro en la base de datos
 
  Scenario: Email ya registrado
    Given existe un usuario con email "juan@test.com"
    When otro usuario intenta registrarse con el mismo email
    Then el sistema muestra el mensaje "El usuario o email ya está registrado"
```
 
---
 
### US-02 Inicio de sesión
 
**Como** usuario registrado  
**Quiero** iniciar sesión con mi email y contraseña  
**Para** acceder a mi cuenta y funciones privadas
 
**Criterios de aceptación:**
- El sistema valida que los campos no estén vacíos
- El sistema compara la contraseña ingresada con la encriptada en la base de datos
- Al iniciar sesión exitosamente el usuario recibe un token JWT
- El token y los datos del usuario se guardan en localStorage
- Credenciales incorrectas muestran mensaje de error sin revelar cuál campo falló
**Gherkin:**
```gherkin
Feature: Inicio de sesión
 
  Scenario: Login exitoso
    Given el usuario está en la página de login
    When ingresa email "juan@test.com" y contraseña "123456"
    And hace click en "Iniciar sesión"
    Then el sistema verifica las credenciales
    And guarda el token JWT en localStorage
    And redirige al usuario a index.html
 
  Scenario: Credenciales incorrectas
    Given el usuario está en la página de login
    When ingresa email "juan@test.com" y contraseña incorrecta "000000"
    And hace click en "Iniciar sesión"
    Then el sistema muestra "Credenciales incorrectas"
    And no guarda ningún token
 
  Scenario: Campos vacíos
    Given el usuario está en la página de login
    When deja el campo de contraseña vacío
    And hace click en "Iniciar sesión"
    Then el sistema muestra "Todos los campos son obligatorios"
```
 
---
 
### US-03 Cierre de sesión
 
**Como** usuario autenticado  
**Quiero** cerrar mi sesión  
**Para** proteger mi cuenta en dispositivos compartidos
 
**Criterios de aceptación:**
- Al cerrar sesión se eliminan el token y los datos del usuario de localStorage
- El usuario es redirigido al login
- Las rutas privadas son inaccesibles tras cerrar sesión
**Gherkin:**
```gherkin
Feature: Cierre de sesión
 
  Scenario: Cerrar sesión exitosamente
    Given el usuario tiene sesión activa
    When hace click en "Cerrar sesión"
    Then el sistema elimina el token de localStorage
    And redirige al usuario a login.html
 
  Scenario: Acceso a ruta privada sin sesión
    Given el usuario no tiene sesión activa
    When intenta acceder a crear-post.html directamente
    Then el sistema redirige automáticamente a login.html
```
 
---
 
## E2 — Gestión de publicaciones
 
### US-04 Crear publicación
 
**Como** usuario autenticado  
**Quiero** crear una publicación con texto, tags e imagen opcional  
**Para** compartir contenido con otros usuarios
 
**Criterios de aceptación:**
- El campo de contenido es obligatorio
- Los tags se ingresan con formato #tag y se convierten a array
- El link de imagen/video es opcional
- La publicación guarda automáticamente el username y avatar del autor como snapshot
- Tras publicar exitosamente redirige al inicio después de 1.5 segundos
- Si no hay sesión activa redirige al login
**Gherkin:**
```gherkin
Feature: Crear publicación
 
  Scenario: Publicación exitosa con texto y tags
    Given el usuario tiene sesión activa
    And está en crear-post.html
    When escribe "Mi primera publicación" en el campo de contenido
    And escribe "#test #primero" en el campo de tags
    And hace click en "Crear post"
    Then el sistema guarda el post en la base de datos
    And muestra el mensaje "¡Post creado exitosamente!"
    And redirige a index.html después de 1.5 segundos
 
  Scenario: Publicación sin contenido
    Given el usuario tiene sesión activa
    When deja el campo de contenido vacío
    And hace click en "Crear post"
    Then el sistema muestra "El contenido del post es obligatorio"
    And no guarda ningún post
 
  Scenario: Intento de publicar sin sesión
    Given el usuario no tiene sesión activa
    When accede a crear-post.html
    Then el sistema redirige automáticamente a login.html
```
 
---
 
### US-05 Ver galería de publicaciones
 
**Como** visitante o usuario autenticado  
**Quiero** ver todas las publicaciones de la red social  
**Para** explorar el contenido disponible
 
**Criterios de aceptación:**
- Los posts se cargan automáticamente al entrar a index.html
- Se muestran ordenados del más reciente al más antiguo
- Cada post muestra contenido, autor, likes y tags si los tiene
- Si el post tiene imagen se muestra, si tiene tags se muestran como badges
- Si no hay posts muestra un mensaje informativo
- La página es responsiva — 3 columnas en desktop, 2 en tablet, 1 en móvil
**Gherkin:**
```gherkin
Feature: Galería de publicaciones
 
  Scenario: Cargar posts exitosamente
    Given existen publicaciones en la base de datos
    When el usuario entra a index.html
    Then el sistema hace GET a /api/posts
    And muestra cada post en una tarjeta con contenido, autor y likes
 
  Scenario: Sin publicaciones
    Given no existen publicaciones en la base de datos
    When el usuario entra a index.html
    Then el sistema muestra "No hay posts aún"
```
 
---
 
### US-06 Ver publicación en detalle
 
**Como** usuario  
**Quiero** ver una publicación en tamaño completo  
**Para** leer el contenido completo y ver la imagen sin recortes
 
**Criterios de aceptación:**
- Al hacer click en un post redirige a post-detalle.html con el id en la URL
- Muestra imagen completa sin recorte
- Muestra autor con avatar, fecha de publicación y tags
- Incluye botón de like funcional
- Incluye botón "Ver perfil" del autor
**Gherkin:**
```gherkin
Feature: Detalle de publicación
 
  Scenario: Ver post en detalle
    Given el usuario está en index.html
    When hace click en una publicación
    Then el sistema redirige a post-detalle.html?id={postId}
    And muestra el contenido completo, imagen, autor, fecha y likes
 
  Scenario: Post no encontrado
    Given el usuario accede a post-detalle.html con un id inválido
    Then el sistema muestra "Post no encontrado"
```
 
---
 
## E3 — Interacciones sociales
 
### US-07 Dar like a una publicación
 
**Como** usuario autenticado  
**Quiero** dar like a una publicación  
**Para** expresar que me gustó el contenido
 
**Criterios de aceptación:**
- Solo usuarios autenticados pueden dar like
- Al dar like el contador incrementa en 1 visualmente
- Al quitar like el contador decrementa en 1 visualmente
- Si no hay sesión activa redirige al login al intentar dar like
- El backend registra el like en la colección likes y actualiza likes_count en el post
**Gherkin:**
```gherkin
Feature: Sistema de likes
 
  Scenario: Dar like exitosamente
    Given el usuario tiene sesión activa
    And está viendo un post con 5 likes
    When hace click en el botón de like
    Then el sistema hace POST a /api/posts/{id}/like
    And el contador muestra 6
    And el botón cambia a color rojo
 
  Scenario: Quitar like
    Given el usuario ya dio like a un post
    When hace click en el botón de like nuevamente
    Then el sistema hace DELETE a /api/posts/{id}/like
    And el contador decrementa en 1
    And el botón regresa a color gris
 
  Scenario: Like sin sesión
    Given el usuario no tiene sesión activa
    When hace click en el botón de like
    Then el sistema redirige a login.html
```
 
---
 
### US-08 Ver perfil propio
 
**Como** usuario autenticado  
**Quiero** ver mi perfil  
**Para** revisar mis publicaciones y datos de cuenta
 
**Criterios de aceptación:**
- Muestra el username y email del usuario logueado
- Muestra únicamente las publicaciones del usuario logueado
- Cada publicación muestra su contador de likes
- Al hacer click en una publicación redirige al detalle
- Si no hay sesión activa redirige al login
**Gherkin:**
```gherkin
Feature: Perfil propio
 
  Scenario: Ver perfil con publicaciones
    Given el usuario tiene sesión activa y tiene posts publicados
    When accede a perfil.html
    Then el sistema muestra su username y email
    And muestra únicamente sus publicaciones
 
  Scenario: Ver perfil sin publicaciones
    Given el usuario tiene sesión activa pero no tiene posts
    When accede a perfil.html
    Then el sistema muestra "Aún no tienes publicaciones"
```
 
---
 
### US-09 Ver perfil de otro usuario
 
**Como** usuario  
**Quiero** ver el perfil de otro usuario  
**Para** explorar su contenido
 
**Criterios de aceptación:**
- Accesible desde el botón "Ver perfil" en post-detalle.html
- Muestra username y avatar del usuario con sus iniciales
- Muestra todas las publicaciones de ese usuario
- Cada publicación muestra su contador de likes
- Al hacer click en una publicación redirige al detalle
**Gherkin:**
```gherkin
Feature: Perfil de otro usuario
 
  Scenario: Ver perfil desde detalle de post
    Given el usuario está en post-detalle.html
    When hace click en "Ver perfil"
    Then el sistema redirige a perfil-usuario.html?id={authorId}
    And muestra el username y publicaciones del autor
```
 
---
 
## E4 — Búsqueda y navegación
 
### US-10 Buscar publicaciones
 
**Como** usuario  
**Quiero** buscar publicaciones por texto  
**Para** encontrar contenido específico
 
**Criterios de aceptación:**
- La búsqueda filtra por contenido del post, nombre del autor y tags
- Al hacer click en "Buscar" redirige a posts.html con el texto como parámetro en la URL
- También funciona presionando Enter
- Si no hay resultados muestra un mensaje informativo
- La búsqueda no distingue mayúsculas de minúsculas
**Gherkin:**
```gherkin
Feature: Búsqueda de publicaciones
 
  Scenario: Búsqueda con resultados
    Given el usuario está en index.html
    When escribe "gatos" en el buscador
    And hace click en "Buscar"
    Then el sistema redirige a posts.html?q=gatos
    And muestra los posts que contienen "gatos" en contenido, autor o tags
 
  Scenario: Búsqueda sin resultados
    Given el usuario busca "xyzabc123"
    Then el sistema muestra "No se encontraron posts para xyzabc123"
```
 
---
 
## E5 — Infraestructura y despliegue
 
### US-11 API REST funcional
 
**Como** desarrollador  
**Quiero** que el backend exponga endpoints REST  
**Para** que el frontend pueda consumir los datos
 
**Criterios de aceptación:**
- `POST /api/auth/register` — registra usuario y devuelve token
- `POST /api/auth/login` — autentica usuario y devuelve token
- `GET /api/posts` — devuelve todos los posts
- `POST /api/posts` — crea post (requiere token)
- `POST /api/posts/:id/like` — da like (requiere token)
- `DELETE /api/posts/:id/like` — quita like (requiere token)
- Rutas privadas devuelven 401 sin token válido
---
 
### US-12 Despliegue en producción
 
**Como** usuario final  
**Quiero** acceder a la red social desde cualquier dispositivo  
**Para** no depender de que el desarrollador tenga su computadora encendida
 
**Criterios de aceptación:**
- Frontend desplegado en Netlify con URL pública
- Backend desplegado en Railway con URL pública
- Base de datos MongoDB alojada en Railway
- El sistema funciona 24/7 sin intervención manual
---
 
## Resumen del backlog
 
| ID | Historia | Épica | Prioridad | Estado |
|----|----------|-------|-----------|--------|
| US-01 | Registro de cuenta | E1 | Alta | ✅ Completado |
| US-02 | Inicio de sesión | E1 | Alta | ✅ Completado |
| US-03 | Cierre de sesión | E1 | Alta | ✅ Completado |
| US-04 | Crear publicación | E2 | Alta | ✅ Completado |
| US-05 | Ver galería | E2 | Alta | ✅ Completado |
| US-06 | Ver detalle de post | E2 | Media | ✅ Completado |
| US-07 | Dar like | E3 | Media | ✅ Completado |
| US-08 | Ver perfil propio | E3 | Media | ✅ Completado |
| US-09 | Ver perfil de otro usuario | E3 | Media | ✅ Completado |
| US-10 | Buscar publicaciones | E4 | Media | ✅ Completado |
| US-11 | API REST funcional | E5 | Alta | ✅ Completado |
| US-12 | Despliegue en producción | E5 | Alta | ✅ Completado |
 
