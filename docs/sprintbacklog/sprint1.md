# Sprint Backlog — Social Network

---

## Context

The base product is complete and deployed in production. The following sprints are focused on improving the user experience, adding deeper social functionalities, and strengthening the system's quality.

---
## Team

 
| Member | Code |
|--------|------|
| Arzabal Flores| DEV-1 |
| Damian Tepole | DEV-2 |
| Gil GUzman | DEV-3 |
| Olivares Luengas | DEV-4 |
| Lopez Tecalco | DEV-5 |
 

---

## Sprint 1 — "User Experience"
**Duration:** 2 weeks
**Objective:** Improve user interaction with the platform — smart likes, smoother navigation, and real-time visual feedback.

---
## Sprint Parameter & Capacity Plan
* Sprint Duration: 2 weeks
* Daily Commitment: 2 Hours (Monday - Friday)
* Total Sprint Capacity: 100 Hours
* Estimated Workload: 20 Horus
* Buffer: 80 Hours

---
 
### Week 1
 
| Day | DEV-1 | DEV-2 | DEV-3 | DEV-4 | DEV-5 |
|-----|-------|-------|-------|-------|-------|
| Monday | Project onboarding — review codebase and repo setup | Project onboarding — review codebase and repo setup | Project onboarding — review codebase and repo setup | Project onboarding — review codebase and repo setup | Project onboarding — review codebase and repo setup |
| Tuesday | SP1-02: Create `GET /api/posts/my-likes` route in `post.routes.js` | SP1-02: Create `getMisLikes` controller in `post.controller.js` | SP1-03: Research duplicate like prevention strategy | SP1-04: Add post counter logic in `perfil.html` | SP1-06: Add welcome message logic in `index.html` |
| Wednesday | SP1-02: Test endpoint with Thunder Client | SP1-02: Deploy backend changes to Railway via GitHub push | SP1-03: Disable like button on frontend after first click | SP1-04: Style post counter in `perfil.css` | SP1-06: Style welcome message in `styles.css` |
| Thursday | SP1-01: Fetch `/my-likes` before rendering posts in `index.html` | SP1-01: Compare post list against liked post IDs | SP1-03: Validate duplicate prevention with multiple test accounts | SP1-04: Test post counter with 0 and multiple posts | SP1-06: Test welcome message with and without active session |
| Friday | SP1-01: Mark liked buttons with class "liked" and red color | SP1-01: Test smart likes on Netlify | SP1-03: Document frontend duplicate prevention approach | SP1-04 + SP1-06: Integration testing on Netlify | Team sync — review Week 1 progress and adjust Week 2 plan |
 
**Week 1 hours per developer: 10h | Team total: 50h**
 
---
 
### Week 2
 
| Day | DEV-1 | DEV-2 | DEV-3 | DEV-4 | DEV-5 |
|-----|-------|-------|-------|-------|-------|
| Monday | SP1-05: Implement `history.back()` on post-detalle.html | SP1-05: Handle direct URL access fallback to index.html | SP1-01: Fix any bugs found in Week 1 smart likes | SP1-03: Final validation of duplicate like prevention | SP1-04 + SP1-06: Fix any styling issues found in Week 1 |
| Tuesday | SP1-05: Test back button on mobile and desktop | SP1-05: Deploy and test on Netlify | Full regression testing — test all SP1 stories end to end | Full regression testing — test all SP1 stories end to end | Full regression testing — test all SP1 stories end to end |
| Wednesday | Bug fixing — address issues found in regression testing | Bug fixing — address issues found in regression testing | Bug fixing — address issues found in regression testing | Update sprint backlog with actual story status | Update impediments and dependencies document |
| Thursday | Sprint 1 demo preparation — prepare walkthrough of all features | Sprint 1 demo preparation — prepare walkthrough of all features | Sprint 1 demo — present SP1-01, SP1-02, SP1-03 | Sprint 1 demo — present SP1-04, SP1-05, SP1-06 | Sprint 1 demo — coordinate and document feedback |
| Friday | Sprint retrospective — what went well | Sprint retrospective — what to improve | Sprint retrospective — what to improve | Sprint 2 planning — review backlog and assign stories | Sprint 2 planning — review backlog and assign stories |
 
**Week 2 hours per developer: 10h | Team total: 50h**
 
---
 
## Sprint 2 — "Community"
**Sprint Goal:** Allow users to comment on posts, edit their profile and find content more precisely with advanced filters.
 
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
 
```gherkin
Feature: Prevent duplicate likes
 
  Scenario: Attempt to like an already liked post
    Given the user has an active session
    And the user has already liked post "abc123"
    When they click the like button of post "abc123"
    Then the system makes DELETE to /api/posts/abc123/like
    And the counter decrements by 1
    And the button returns to grey
 
  Scenario: Backend rejects duplicate like
    Given the user has an active session
    And the unique index exists in the likes collection
    When the frontend sends POST /api/posts/abc123/like for a post already liked
    Then the backend returns status 400
    And the message "You have already liked this post"
```
 
```gherkin
Feature: Post counter on profile
 
  Scenario: User with publications
    Given the user has an active session
    And has 5 published posts
    When they access perfil.html
    Then the system shows "5 posts" below the username
 
  Scenario: User without publications
    Given the user has an active session
    And has no published posts
    When they access perfil.html
    Then the system shows "0 posts" below the username
```
 
```gherkin
Feature: Back button on post detail
 
  Scenario: Navigate back from post detail
    Given the user came from index.html
    And is on post-detalle.html
    When they click the back button
    Then the browser returns to the previous page
    And the scroll position is preserved
 
  Scenario: Direct access to post detail
    Given the user accessed post-detalle.html directly via URL
    When they click the back button
    Then the browser navigates to index.html
```
 
```gherkin
Feature: Welcome message on index
 
  Scenario: Authenticated user enters index
    Given the user has an active session with username "juanito"
    When they enter index.html
    Then the header shows "Welcome, @juanito"
 
  Scenario: Unauthenticated user enters index
    Given the user has no active session
    When they enter index.html
    Then the header shows the "Sign in" button instead of the welcome message
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
