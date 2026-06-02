# Sprint Backlog — Social Network

---

## Context

The base product is complete and deployed in production. The following sprints are focused on improving the user experience, adding deeper social functionalities, and strengthening the system's quality.

---

## Sprint 1 — "User Experience"
**Duration:** 2 weeks
**Objective:** Improve user interaction with the platform — smart likes, smoother navigation, and real-time visual feedback.

---
## Sprint Parameter & Capacity Plan
* Sprint Duration: 2 weeks
* Daily Commitment: 2 Hours (Monday - Friday)
* Total Sprint Capacity: 40 Hours
* Estimated Workload: 20 Horus
* Buffer: 20 Hours

---
## Sprint Goal

> Enable users to interact with posts more precisely, seeing at all times if they have liked them, with more intuitive navigation between profiles and posts.

### Sprint Backlog

| ID | Story | Description | Priority | Estimate |
|----|-------|-------------|----------|----------|
| SP1-01 | Smart Likes | When posts load, visually mark which ones have already been liked by the logged-in user | High | 3 pts |
| SP1-02 | Endpoint for likes per user | Create `GET /api/posts/my-likes` that returns the post_ids that the user has already liked | High | 2 pts |
| SP1-03 | Prevent duplicate likes | Validate on the frontend and backend that a user cannot like the same post twice | High | 3 pts |
| SP1-04 | Post counter on profile | Show how many posts the user has on their profile | Medium | 1 pt |
| SP1-05 | Back button on post details | Improve navigation with a button that returns to the previous page | Low | 1 pt |
| SP1-06 | Welcome message on index page | If the user is logged in, display "Welcome, @username" in the header | Low | 1 pt |

**Total:** 11 points

### Sprint Acceptance Criteria
```gherkin

Feature: Smart likes on page load

  Scenario: User has already liked a post
    Given the user has an active session
    And the user previously liked post "abc123"
    When they enter index.html
    Then the like button of post "abc123" appears in red
    And the button is marked with class "liked"

  Scenario: User has not liked a post
    Given the user has an active session
    And the user has not liked post "xyz456"
    When they enter index.html
    Then the like button of post "xyz456" appears in grey
    And the button does not have the class "liked"

  Scenario: User without session views posts
    Given the user has no active session
    When they enter index.html
    Then all like buttons appear in grey
    And clicking any like button redirects to login.html
```
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


## Impediments
 
| ID | Description | Impact | Owner |
|----|-------------|--------|-------|
| IMP-01 | Railway free tier has insufficient disk space to create unique indexes in MongoDB | Prevents SP1-03 from being fully enforced at the database level | Developer |

 
---
 
## Dependencies
 
| ID | Story | Depends on | Type |
|----|-------|------------|------|
| DEP-01 | SP1-01 Smart likes | SP1-02 must be completed first — needs the `/my-likes` endpoint | Internal |
| DEP-02 | SP1-03 Prevent duplicates | Requires IMP-01 to be resolved or handled via frontend only | Internal |
| DEP-03 | SP1-06 Welcome message | Requires the user to be stored correctly in localStorage after login | Internal |
| DEP-04 | All stories | Active Railway deployment — if the service goes down no story can be tested in production | External |
 
---
### Definition of Done

* [ ] Functionality manually tested in Netlify
* [ ] No errors in the browser console
* [ ] Responsive on mobile and desktop
* [ ] Changes uploaded to GitHub and redeployed in Railway/Netlify

---
