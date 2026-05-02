# CMS Multimedia - NoSQL Data Model
## Collections Design
```mermaid
erDiagram

    USERS {
        ObjectId _id PK
        string username "unique"
        string email "unique"
        string password_hash
        string avatar_url
        string bio
        date created_at
    }

    POSTS {
        ObjectId _id PK
        ObjectId author_id FK
        string author_username "snapshot"
        string author_avatar_url "snapshot"
        string content
        string media_url
        array tags
        array editors "embebido: [{user_id, username, role}]"
        number likes_count
        date created_at
    }

    LIKES {
        ObjectId _id PK
        ObjectId post_id FK
        ObjectId user_id FK
        date created_at
    }

    USERS ||--o{ POSTS : "author (1:N)"
    USERS ||--o{ LIKES : "user_id (1:N)"
    POSTS ||--o{ LIKES : "post_id (1:N)"
