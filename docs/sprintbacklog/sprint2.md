## Sprint 2 — "Community"
*Duration:* 2 weeks  
*Goal:* Add features that encourage interaction between users — comments, profile editing and improved search.

---

### Sprint Goal

> Allow users to comment on posts, edit their profile information and find content more precisely with advanced filters.

---

### Sprint Backlog

| ID | User Story | Description | Priority | Estimation |
|----|-----------|-------------|----------|------------|
| SP2-01 | Comments on posts | Add a comments section in post-detalle.html | High | 5 pts |
| SP2-02 | Comments endpoint | Create POST and GET routes for comments in the backend | High | 4 pts |
| SP2-03 | Edit profile | Allow the user to change their username, bio and avatar_url | Medium | 4 pts |
| SP2-04 | Edit profile endpoint | Create route PUT /api/users/me in the backend | Medium | 3 pts |
| SP2-05 | Filter by tags in search | In posts.html allow filtering only by tags using the # prefix | Medium | 2 pts |
| SP2-06 | Post pagination | Load posts 9 at a time with a "Load more" button in index.html | Low | 3 pts |

*Total:* 21 points

---

### Sprint Acceptance Criteria

- An authenticated user can write and publish comments on any post
- Comments show the author and the date
- The user can update their username and bio from their profile
- Searching with #tag filters only by that tag
- The index loads the first 9 posts and allows loading more

---

### Definition of Done

- Feature manually tested on Netlify
- New endpoints documented
- No errors in the browser console
- Responsive on mobile and desktop
- Changes pushed to GitHub and redeployed on Railway/Netlify

---

### Technical Tasks

*SP2-01 and SP2-02 — Comments:*
1. Create comments collection in MongoDB with fields: post_id, user_id, author_username, content, created_at
2. Create Comment.js in src/models/
3. Create comment.controller.js with functions addComment and getComments
4. Create comment.routes.js with routes POST /api/comments and GET /api/comments/:postId
5. Add the comments section in post-detalle.html

*SP2-03 and SP2-04 — Edit profile:*
1. Create route PUT /api/users/me in the backend protected with JWT
2. Create controller that updates username, bio and avatar_url
3. Add an edit form in perfil.html with editable fields
4. On save, also update localStorage with the new data

*SP2-05 — Filter by tags:*
1. In posts.html detect if the query starts with #
2. If so filter only by tags, not by content or author

*SP2-06 — Pagination:*
1. In index.html show only the first 9 posts
2. Add a "Load more" button that loads the next 9
3. Hide the button when there are no more posts

---

## Sprint Summary

| Sprint | Goal | Stories | Points | Duration |
|--------|------|---------|--------|----------|
| Sprint 1 | User Experience | 6 | 11 pts | 2 weeks |
| Sprint 2 | Community | 6 | 21 pts | 2 weeks |
