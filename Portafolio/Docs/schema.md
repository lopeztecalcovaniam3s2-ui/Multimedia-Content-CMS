# CMS Multimedia - NoSQL Data Model
## Collections Design
```mermaid

erDiagram

USERS {
     _id PK
     nombre
     email
}

ROLES {
    ObjectId _id PK
    string roleName
    string description
}

POSTS {
    ObjectId _id PK
    string type
    string title
    string slug
    string[] tags
    string author_username
    string author_email
    string author_role
    date createdAt
}

POST_PERMISSIONS {
    ObjectId _id PK
    ObjectId post_id
    ObjectId user_id
    ObjectId role_id
}

MEDIA_TEXT {
    string body
}

MEDIA_IMAGE {
    string imageUrl
    string altText
    string caption
}

MEDIA_VIDEO {
    string videoUrl
    string provider
    number durationSeconds
}

ROLES ||--o{ USERS : "default role"
USERS ||--o{ POSTS : "authors"
POSTS ||--o| MEDIA_TEXT : "type=text"
POSTS ||--o| MEDIA_IMAGE : "type=image"
POSTS ||--o| MEDIA_VIDEO : "type=video"

USERS ||--o{ POST_PERMISSIONS : "has"
POSTS ||--o{ POST_PERMISSIONS : "permissions"
ROLES ||--o{ POST_PERMISSIONS : "assigned role"
