# Sprint Backlog — Social Network

---

## Context

The base product is complete and deployed in production. The following sprints are focused on improving the user experience, adding deeper social functionalities, and strengthening the system's quality.

---

## Sprint 1 — "User Experience"
**Duration:** 2 weeks
**Objective:** Improve user interaction with the platform — smart likes, smoother navigation, and real-time visual feedback.

---

### Sprint Goal

> Enable users to interact with posts more precisely, seeing at all times if they have liked them, with more intuitive navigation between profiles and posts.

---

### Sprint Backlog

| ID | Story | Description | Priority | Estimate |

|----|----------|-------------|-----------|------------|

| SP1-01 | Smart Likes | When posts load, visually mark which ones have already been liked by the logged-in user | High | 3 pts |

|SP1-02 | Endpoint for likes per user | Create `GET /api/posts/my-likes` that returns the post_ids that the user has already liked |   High | 2 pts |

| SP1-03 | Prevent duplicate likes | Validate on the frontend and backend that a user cannot like the same post twice | High | 3 pts |

| SP1-04 | Post counter on profile | Show how many posts the user has on their profile | Medium | 1 pt |

| SP1-05 | Back button on post details | Improve navigation with a button that returns to the previous page | Low | 1 pt |

| SP1-06 | Welcome message on index page | If the user is logged in, display "Welcome, @username" in the header | Low | 1 pt  |

**Total:** 11 points

---

### Sprint Acceptance Criteria

- The like button displays the correct status (red = already liked, gray = not liked) upon page load
- A user cannot like the same post more than once
- The profile displays the total number of posts
- The back button in post details works correctly on mobile and desktop

---

### Definition of Done

- Functionality manually tested in Netlify
- No errors in the browser console
- Responsive on mobile and desktop
- Changes uploaded to GitHub and redeployed in Railway/Netlify

---

### Technical Tasks

**SP1-01 and SP1-02 — Smart Likes:**
1. Create the `GET /api/posts/mis-likes` endpoint in the backend
2. Add the route to `post.routes.js`
3. Add the controller `getMisLikes` in `post.controller.js`
4. In `index.html`, fetch `/mis-likes` before rendering the posts.
5. Compare each post with the user's like list and mark the button.

**SP1-03 — Prevent Duplicates:**
1. Create a unique index in MongoDB: `{ post_id: 1, user_id: 1 }`
2. On the frontend, disable the like button if it's already marked as liked.

**SP1-04 — Post Counter:**
1. In `perfil.html`, count `misPosts.length` and display it below the username.

**SP1-05 — Back Button:**
1. Change `← Back` in `post-detalle.html` to use `history.back()`.

**SP1-06 — Welcome Message:**
1. In `index.html`, check if there's a user in localStorage and display the message. Greetings

---
