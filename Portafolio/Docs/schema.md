# CMS Multimedia - NoSQL Data Model
## Collections Design
```mermaid
flowchart LR

    USERS["USERS<br>_id (PK)<br>nombre<br>email"]

    INTERACCION["INTERACCION<br>_idUsuario (FK)<br>postId (FK)<br>rol"]

    POSTS["POSTS<br>_id (PK)<br>title<br>type<br>slug<br>tags"]

    USERS -- "1:N" --> INTERACCION
    POSTS -- "1:N" --> INTERACCION

    USERS -- "1:N autores" --> POSTS
