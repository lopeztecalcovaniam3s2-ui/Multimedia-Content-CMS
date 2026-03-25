# CMS Multimedia - NoSQL Data Model
## Collections Design
```mermaid
erDiagram

USERS {
    ObjectId _id PK
    string nombre
    string email
}

INTERACCION {
    ObjectId _idUsuario FK
    ObjectId postId FK
    string rol
}

POSTS {
    ObjectId _id PK
    string title
    string type
    string slug
    string[] tags
}

USERS ||--o{ INTERACCION : "1:N"
POSTS ||--o{ INTERACCION : "1:N"

USERS ||--o{ POSTS : "1:N autores"
