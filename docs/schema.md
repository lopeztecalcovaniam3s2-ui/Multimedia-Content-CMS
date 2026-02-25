# CMS Multimedia - NoSQL Data Model

## Collections Design
```erDiagram
POSTS {
    ObjectId _id PK
    string type
    string title
    string slug
    string[] tags
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

POSTS ||--o| MEDIA_TEXT : "embedded type=text"
POSTS ||--o| MEDIA_IMAGE : "embedded type=image"
POSTS ||--o| MEDIA_VIDEO : "embedded type=video"
` ` `

## Indexes
| Field | Index Type | Purpose |
|-------|-----------|---------|
| `title` | Text Index | Full-text search |
| `body` | Text Index | Full-text search |
| `tags` | Multikey Index | Filter by tag |

## Notes
- `MEDIA_*` are **not** separate collections — they are embedded objects inside `POSTS`
- `type` field acts as a switch: `text` / `image` / `video`
- Max document size: 16MB (MongoDB limit)
```

---
