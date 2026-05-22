# Multimedia Social Network – Project Backlog 📝

## Project Objective 🎯
Desarrollar una plataforma de red social multimedia que permita a los usuarios crear y compartir contenido en distintos formatos (imágenes, videos y textos). La plataforma incluirá interacciones sociales (likes, comentarios) y perfiles de usuario para personalizar la experiencia y fomentar la participación.

---

# Epics & Features

## Epic 1: User Access & Authentication 🔑
**Objetivo:** Permitir que los usuarios se registren, inicien sesión y accedan a funciones básicas del sitio.

### Feature 1.1: Registration & Account Creation
**User Story:**  
Como nuevo usuario, quiero crear una cuenta con credenciales únicas para poder interactuar con el sitio.

**Acceptance Criteria:**
- El formulario de registro debe solicitar nombre, correo electrónico y contraseña.
- La contraseña debe ser única y encriptada en la base de datos.
- Si la contraseña ya existe, la creación de cuenta debe ser rechazada.
- Al registrarse correctamente, el usuario debe ser redirigido al inicio de sesión o inicio de sesión automático.

---

### Feature 1.2: Login / Session Management
**User Story:**  
Como usuario registrado, quiero iniciar sesión para acceder a funcionalidades restringidas.

**Acceptance Criteria:**
- Los usuarios deben ingresar correo y contraseña para iniciar sesión.
- El sistema valida las credenciales antes de permitir el acceso.
- En caso de error, se debe mostrar un mensaje claro (“Correo o contraseña incorrectos”).

---

## Epic 2: User Profiles 👤
**Objetivo:** Permitir que cada usuario tenga un perfil personalizado y gestione su información básica.

### Feature 2.1: View & Edit Profile
**User Story:**  
Como usuario, quiero ver y editar mi perfil para mantener mi información actualizada.

**Acceptance Criteria:**
- Cada perfil debe mostrar nombre, foto de perfil y lista de posts creados.
- El usuario puede actualizar su información básica (nombre, foto, biografía corta).
- Los cambios se reflejan en tiempo real en el perfil.

---

## Epic 3: Content Posting 📸
**Objetivo:** Permitir a los usuarios crear y visualizar contenido multimedia (imagen + texto breve).

### Feature 3.1: Create Post
**User Story:**  
Como usuario, quiero publicar contenido multimedia para compartir ideas o momentos con otros usuarios.

**Acceptance Criteria:**
- El formulario de creación de post permite subir una imagen y un texto breve.
- Usuarios no autenticados que intenten crear un post deben ser redirigidos al inicio de sesión.
- Cada post creado se asocia automáticamente al perfil del usuario que lo publica.

---

### Feature 3.2: Like Posts
**User Story:**  
Como usuario, quiero poder dar “me gusta” a posts para mostrar mi interés.

**Acceptance Criteria:**
- Usuarios no autenticados que intenten dar “me gusta” deben ser redirigidos al login.
- Cada “me gusta” se registra en la base de datos vinculada al usuario.
- Los posts muestran el conteo total de “me gusta” actualizado en tiempo real.

---

## Epic 4: Guest / Anonymous Access 👀
**Objetivo:** Permitir que los nuevos usuarios exploren el sitio sin autenticación, incentivando el registro.

### Feature 4.1: Browse Posts Without Login
**User Story:**  
Como nuevo usuario, quiero explorar posts sin necesidad de registrarme.

**Acceptance Criteria:**
- Los visitantes pueden ver todos los posts y perfiles públicos.
- Interacciones restringidas (like, post creation) deben mostrar un mensaje con opciones de login o registro.

---

## Epic 5: Technical Architecture & Security 🛠️
**Objetivo:** Garantizar un sistema escalable, seguro y funcional desde la primera versión.

**Stack recomendado:**
- **Frontend:** HTML, CSS, JS (opcional React para escalabilidad)
- **Backend:** Node.js (API RESTful)
- **Database:** MongoDB (NoSQL)
- **Seguridad:** Contraseñas encriptadas, validaciones en frontend y backend
- **Escalabilidad:** Estructura modular para futuras funcionalidades (mensajería, notificaciones, recomendaciones)

---

# Priorities for MVP 🚀
| Priority | Epic / Feature | Notes |
|----------|----------------|-------|
| 1 | User Access & Authentication | Essential to allow user interactions |
| 2 | Guest / Anonymous Access | Let new users explore content before registration |
| 3 | Content Posting | Core functionality: create posts and interact |
| 4 | User Profiles | Display user info and posts |
| 5 | Likes | Basic engagement metric |

---

# Sample User Scenarios / Gherkin Style

## Scenario: Explore posts without logging in
