## E5 — Infrastructure and Deployment

### US-11 Functional REST API

**As** a developer  
**I want** the backend to expose REST endpoints  
**So that** the frontend can consume the data

**Acceptance Criteria:**
- `POST /api/auth/register` — registers user and returns token
- `POST /api/auth/login` — authenticates user and returns token
- `GET /api/posts` — returns all posts
- `POST /api/posts` — creates post (requires token)
- `POST /api/posts/:id/like` — likes a post (requires token)
- `DELETE /api/posts/:id/like` — removes like (requires token)
- Private routes return 401 without a valid token

---

### US-12 Production Deployment

**As** an end user  
**I want** to access the social network from any device  
**So that** I don't depend on the developer having their computer on

**Acceptance Criteria:**
- Frontend deployed on Netlify with a public URL
- Backend deployed on Railway with a public URL
- MongoDB database hosted on Railway
- The system runs 24/7 without manual intervention

---

## Backlog Summary

| ID | User Story | Epic | Priority | Status |
|----|-----------|------|----------|--------|
| US-01 | Account Registration | E1 | High | ✅ Done |
| US-02 | Login | E1 | High | ✅ Done |
| US-03 | Logout | E1 | High | ✅ Done |
| US-04 | Create Post | E2 | High | ✅ Done |
| US-05 | View Gallery | E2 | High | ✅ Done |
| US-06 | View Post Detail | E2 | Medium | ✅ Done |
| US-07 | Like a Post | E3 | Medium | ✅ Done |
| US-08 | View Own Profile | E3 | Medium | ✅ Done |
| US-09 | View Another User's Profile | E3 | Medium | ✅ Done |
| US-10 | Search Posts | E4 | Medium | ✅ Done |
| US-11 | Functional REST API | E5 | High | ✅ Done |
| US-12 | Production Deployment | E5 | High | ✅ Done |
EOF
