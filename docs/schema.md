# CMS Multimedia - NoSQL Data Model

## Collections Design
```mermaid
erDiagram
POSTS {
    string _id PK
    string type
    string title
    string slug
    string[] tags
    
}

MEDIA_TEXT {
    int id PK
    string body
    string post_id FK
}

MEDIA_IMAGE {
    int id PK
    string imageUrl
    string altText
    string caption
    string image_id FK
}

MEDIA_VIDEO {
    int id PK
    string videoUrl
    string provider
    number durationSeconds
    string video_id FK

}

POSTS ||--o| MEDIA_TEXT : "embedded type=text"
POSTS ||--o| MEDIA_IMAGE : "embedded type=image"
POSTS ||--o| MEDIA_VIDEO : "embedded type=video"


