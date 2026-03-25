# CMS Multimedia - NoSQL Data Model
## Collections Design
```mermaid
flowchart LR

    USERS["<b>USERS</b><br>------------------<br>
    _id: ObjectId (PK)<br>
    nombre: string<br>
    email: string"]

    INTERACCION["<b>INTERACCION</b><br>------------------<br>
    _idUsuario: ObjectId (FK)<br>
    postId: ObjectId (FK)<br>
    rol: string"]

    POSTS["<b>POSTS</b><br>------------------<br>
    _id: ObjectId (PK)<br>
    title: string<br>
    type: string<br>
    slug: string<br>
    tags: string[]"]

    USERS -- "1:N" --> INTERACCION
    POSTS -- "1:N" --> INTERACCION

    USERS -- "1:N autores" --> POSTS
