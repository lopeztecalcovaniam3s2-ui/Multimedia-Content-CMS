# CMS Multimedia - NoSQL Data Model
## Collections Design
```mermaid
erDiagram
USERS{
    ObjectId _id PK  
    string username
    string email
    date createdAt
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
USERS ||--o{ POSTS : "authored by" 
POSTS ||--o| MEDIA_TEXT : "embedded type=text"
POSTS ||--o| MEDIA_IMAGE : "embedded type=image"
POSTS ||--o| MEDIA_VIDEO : "embedded type=video"
