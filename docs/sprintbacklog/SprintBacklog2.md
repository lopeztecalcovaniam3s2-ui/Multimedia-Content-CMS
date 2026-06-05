# Sprint Backlog — Sprint Alpha "Product Base"
## Social Network

---

## Context

This sprint covers the full frontend development and its integration with the REST API built in Sprint 0. By the end of this sprint the social network is fully functional locally and deployed to production on Railway and Netlify.

---

## Sprint Alpha — "Product Base"

**Duration:** 4 weeks
**Objective:** Build all HTML pages, connect them to the backend API, deploy the full system to production and validate the complete user flow end to end.

---

## Sprint Parameter & Capacity Plan

| Parameter | Value |
|-----------|-------|
| Sprint Duration | 4 weeks |
| Daily Commitment | 2 hours (Monday – Friday) |
| Total Sprint Capacity | 200 hours |
| Estimated Workload | 170 hours |
| Buffer | 30 hours |

---

## Sprint Goal

> Deliver a fully deployed social network accessible from any device, where users can register, log in, create posts, explore content, search, like publications and view profiles.

---

## Sprint Backlog

| ID | Story | Description | Priority | Estimate | Epic |
|----|-------|-------------|----------|----------|------|
| SPA-01 | Login page | Build `login.html` connected to `POST /api/auth/login` — validate fields, store JWT in localStorage, redirect to index | High | 3 pts | E1 |
| SPA-02 | Registration page | Build `registro.html` connected to `POST /api/auth/register` — validate fields, confirm password, store JWT, redirect | High | 3 pts | E1 |
| SPA-03 | Logout functionality | Implement logout on all pages — clear localStorage token and user, redirect to login | High | 2 pts | E1 |
| SPA-04 | Post gallery page | Build `index.html` — fetch and render all posts dynamically from `GET /api/posts` with image, tags and likes | High | 4 pts | E2 |
| SPA-05 | Create post page | Build `crear-post.html` — content, tags, optional media link, send to `POST /api/posts` with JWT | High | 3 pts | E2 |
| SPA-06 | Post detail page | Build `post-detalle.html` — full post view with image, author, date, tags, likes and View Profile button | Medium | 4 pts | E2 |
| SPA-07 | Search page | Build `posts.html` — receive `?q=` URL param, filter posts by content, author and tags | Medium | 3 pts | E4 |
| SPA-08 | Own profile page | Build `perfil.html` — show logged-in user data from localStorage, filter and display their posts | Medium | 3 pts | E3 |
| SPA-09 | Other user profile page | Build `perfil-usuario.html` — receive `?id=` URL param, filter posts by author_id, display user info | Medium | 3 pts | E3 |
| SPA-10 | Like button on gallery | Add like/unlike button to each post card in `index.html` — toggle liked state, update counter visually | Medium | 3 pts | E3 |
| SPA-11 | Like button on post detail | Add like/unlike button to `post-detalle.html` — same logic as gallery | Medium | 2 pts | E3 |
| SPA-12 | Session protection | Redirect to login if no token on protected pages — `crear-post.html`, `perfil.html` | High | 2 pts | E1 |
| SPA-13 | Responsive design — index | Apply responsive CSS to `index.html` — 3 columns desktop, 2 tablet, 1 mobile | Medium | 2 pts | E2 |
| SPA-14 | Responsive design — forms | Apply responsive CSS to `login.html`, `registro.html` and `crear-post.html` | Medium | 2 pts | E1 |
| SPA-15 | Responsive design — profiles | Apply responsive CSS to `perfil.html`, `perfil-usuario.html` and `posts.html` | Medium | 2 pts | E3 |
| SPA-16 | Git repository setup | Initialize Git, create GitHub repository, configure `.gitignore`, push first commit | High | 1 pt | E5 |
| SPA-17 | Railway backend deployment | Deploy Node.js backend to Railway — connect GitHub repo, configure environment variables | High | 3 pts | E5 |
| SPA-18 | Railway MongoDB deployment | Deploy MongoDB service on Railway — obtain public connection string, connect to backend | High | 3 pts | E5 |
| SPA-19 | Netlify frontend deployment | Deploy `frontend/` folder to Netlify — update all API URLs from localhost to Railway public URL | High | 2 pts | E5 |
| SPA-20 | End to end production testing | Test full user flow on Netlify — register, login, create post, like, search, view profile, logout | High | 3 pts | E5 |

**Total:** 53 points

---

## Sprint Acceptance Criteria

```gherkin
Feature: Login page connected to API

  Scenario: Successful login from browser
    Given the user is on login.html served by Live Server
    When they enter valid email and password
    And click "Iniciar sesión"
    Then the browser sends POST to /api/auth/login
    And stores the JWT token in localStorage
    And redirects to index.html

  Scenario: Invalid credentials from browser
    Given the user is on login.html
    When they enter wrong credentials
    And click "Iniciar sesión"
    Then the page shows an error message in red
    And no token is stored in localStorage
```

```gherkin
Feature: Post gallery loads dynamically

  Scenario: Posts exist in the database
    Given the user is on index.html
    When the page loads
    Then the browser fetches GET /api/posts
    And renders each post as a card with content, author and like count
    And posts with media_url show the image
    And posts without image but with tags show tag badges

  Scenario: No posts in database
    Given the posts collection is empty
    When the user opens index.html
    Then the page shows "No hay posts aún"
```

```gherkin
Feature: Create post connected to API

  Scenario: Authenticated user creates a post
    Given the user has a valid token in localStorage
    And is on crear-post.html
    When they fill the content field and click "Crear post"
    Then the browser sends POST to /api/posts with the JWT in the Authorization header
    And the post appears in index.html after redirect

  Scenario: Unauthenticated access to create post
    Given no token exists in localStorage
    When the user opens crear-post.html
    Then the page immediately redirects to login.html
```

```gherkin
Feature: Search filters posts

  Scenario: Search by content keyword
    Given the user is on index.html
    When they type "gatos" in the search bar and click "Buscar"
    Then the browser redirects to posts.html?q=gatos
    And posts.html shows only posts containing "gatos" in content, author or tags

  Scenario: Search with no results
    Given the user searches for "xyznotexist"
    Then posts.html shows "No se encontraron posts para xyznotexist"
```

```gherkin
Feature: Own profile shows user posts

  Scenario: User views their profile
    Given the user has an active session stored in localStorage
    When they open perfil.html
    Then the page reads username and email from localStorage
    And fetches GET /api/posts
    And filters posts where author_id matches the logged-in user id
    And displays only those posts

  Scenario: Unauthenticated access to profile
    Given no token in localStorage
    When the user opens perfil.html
    Then the page redirects to login.html
```

```gherkin
Feature: Production deployment

  Scenario: Backend accessible via Railway URL
    Given the backend is deployed on Railway
    When a POST request is sent to https://social-network-production-59ef.up.railway.app/api/auth/login
    Then the server responds with status 200 and a JWT token

  Scenario: Frontend accessible via Netlify URL
    Given the frontend is deployed on Netlify
    When a user opens https://incomparable-yeot-45f845.netlify.app
    Then login.html loads correctly
    And all fetch calls point to the Railway backend URL
```

---

## Technical Tasks by Week

### Week 1 — Core Pages

| Day | DEV-1 | DEV-2 | DEV-3 | DEV-4 | DEV-5 |
|-----|-------|-------|-------|-------|-------|
| Monday | SPA-01: Build login.html structure and CSS | SPA-01: Connect login form to POST /api/auth/login | SPA-02: Build registro.html structure and CSS | SPA-02: Connect register form to POST /api/auth/register | SPA-02: Add password confirmation validation |
| Tuesday | SPA-01: Store JWT and user in localStorage | SPA-01: Add error message display | SPA-02: Store JWT and user in localStorage | SPA-02: Add error message display | SPA-03: Implement logout — clear localStorage and redirect |
| Wednesday | SPA-12: Add session check on crear-post.html | SPA-12: Add session check on perfil.html | SPA-04: Build index.html structure and CSS | SPA-04: Fetch GET /api/posts and render post cards | SPA-04: Handle empty posts state |
| Thursday | Test login flow end to end with Live Server | Test register flow end to end with Live Server | Test logout from index.html | Test session protection redirects | SPA-04: Display image if media_url exists |
| Friday | Week 1 review — verify auth pages working | Week 1 review — verify gallery loads posts | Week 1 review — team sync | Fix bugs found in testing | Document localStorage data structure |

### Week 2 — Extended Features

| Day | DEV-1 | DEV-2 | DEV-3 | DEV-4 | DEV-5 |
|-----|-------|-------|-------|-------|-------|
| Monday | SPA-05: Build crear-post.html — textarea, tags, radio button | SPA-05: Connect form to POST /api/posts with JWT | SPA-07: Build posts.html — read ?q= param from URL | SPA-07: Filter posts by content, author and tags | SPA-08: Build perfil.html — read user from localStorage |
| Tuesday | SPA-05: Convert #tag string to array before sending | SPA-05: Show success message and redirect after 1.5s | SPA-07: Show filtered results as post cards | SPA-07: Handle no results state | SPA-08: Fetch and filter posts by author_id |
| Wednesday | SPA-06: Build post-detalle.html — full post view | SPA-06: Read ?id= param and find post from API | SPA-09: Build perfil-usuario.html — read ?id= param | SPA-09: Fetch and filter posts by author_id | SPA-09: Display author username and avatar initials |
| Thursday | SPA-06: Display author avatar, date, tags and content | SPA-06: Add View Profile button pointing to perfil-usuario.html | Test search page with multiple queries | Test own profile with posts and without posts | Test other user profile navigation from post detail |
| Friday | Week 2 review — verify all pages connected | Week 2 review — team sync | Fix search bugs | Fix profile bugs | Document complete page navigation flow |

### Week 3 — Likes, Responsive and Git

| Day | DEV-1 | DEV-2 | DEV-3 | DEV-4 | DEV-5 |
|-----|-------|-------|-------|-------|-------|
| Monday | SPA-10: Add like button to each post card in index.html | SPA-10: Connect like button to POST and DELETE /api/posts/:id/like | SPA-11: Add like button to post-detalle.html | SPA-11: Connect like button with same logic as gallery | SPA-16: Initialize Git and create GitHub repository |
| Tuesday | SPA-10: Toggle liked class and update counter visually | SPA-10: Redirect to login if no token when liking | SPA-11: Toggle liked class on post detail | SPA-16: Push first commit to GitHub | SPA-13: Apply responsive CSS to index.html |
| Wednesday | SPA-13: Test index.html on mobile viewport | SPA-14: Apply responsive CSS to login.html and registro.html | SPA-14: Apply responsive CSS to crear-post.html | SPA-15: Apply responsive CSS to perfil.html | SPA-15: Apply responsive CSS to perfil-usuario.html and posts.html |
| Thursday | Test likes on index and post detail | Test likes without session — verify redirect | Test all pages on mobile viewport | Test all pages on tablet viewport | Add viewport meta tag to all HTML files |
| Friday | Week 3 review — verify likes and responsive working | Week 3 review — team sync | Fix responsive issues found in testing | Fix like bugs found in testing | Verify GitHub repo has all files except .env |

### Week 4 — Deployment and Production Testing

| Day | DEV-1 | DEV-2 | DEV-3 | DEV-4 | DEV-5 |
|-----|-------|-------|-------|-------|-------|
| Monday | SPA-17: Create Railway project and deploy from GitHub | SPA-17: Configure environment variables in Railway — PORT, MONGO_URI, JWT_SECRET | SPA-18: Add MongoDB service to Railway project | SPA-18: Obtain MONGO_PUBLIC_URL and update MONGO_URI in Railway variables | SPA-18: Verify backend connects to Railway MongoDB |
| Tuesday | SPA-19: Replace all localhost:3000 with Railway URL using VS Code find and replace | SPA-19: Push URL changes to GitHub | SPA-19: Deploy frontend folder to Netlify via drag and drop | SPA-19: Verify all fetch calls point to Railway URL | SPA-19: Test Netlify URL opens correctly in browser |
| Wednesday | SPA-20: Full end to end test — register new user on Netlify | SPA-20: Full end to end test — login and create post | SPA-20: Full end to end test — search and view post detail | SPA-20: Full end to end test — like posts and view profile | SPA-20: Full end to end test — logout and session protection |
| Thursday | Sprint Alpha demo — present login, register and gallery | Sprint Alpha demo — present create post and search | Sprint Alpha demo — present profiles and likes | Sprint Alpha demo — present deployment on Railway and Netlify | Sprint Alpha demo — coordinate and document feedback |
| Friday | Sprint retrospective — what went well | Sprint retrospective — what to improve | Sprint 1 planning — review User Experience backlog | Sprint 1 planning — assign stories | Sprint 1 planning — team sync |

---

## Impediments

| ID | Description | Impact | Owner |
|----|-------------|--------|-------|
| IMP-01 | Telmex DNS blocks MongoDB Atlas port 27017 | Forces Railway MongoDB as production database instead of Atlas | External — ISP |
| IMP-02 | Railway free trial limited to 30 days or $5.00 credit | Backend and database will go offline when trial expires | Developer |
| IMP-03 | CORS errors when frontend on Live Server calls backend on localhost | Requires CORS middleware properly configured in Express | Developer |
| IMP-04 | localStorage not available in some private browser modes | May cause session issues for some users | External — Browser |
| IMP-05 | Railway MongoDB service deleted automatically due to disk space constraints | Required recreating the MongoDB service and updating connection strings | External — Railway |

---

## Dependencies

| ID | Story | Depends on | Type |
|----|-------|------------|------|
| DEP-01 | All frontend stories | Sprint 0 must be complete — all API endpoints must be working | Cross-sprint |
| DEP-02 | SPA-04 Post gallery | SPA-01 Login must be complete — token needed to test protected posts | Internal |
| DEP-03 | SPA-05 Create post | SPA-01 Login must be complete — JWT required in Authorization header | Internal |
| DEP-04 | SPA-08 Own profile | SPA-01 Login must be complete — user data read from localStorage | Internal |
| DEP-05 | SPA-10 Like button | SPA-04 Gallery must be complete — like buttons rendered per post | Internal |
| DEP-06 | SPA-19 Netlify deployment | SPA-16 GitHub repo must be complete — all files pushed | Internal |
| DEP-07 | SPA-17 Railway deployment | SPA-16 GitHub repo must be connected to Railway | Internal |
| DEP-08 | SPA-20 E2E testing | SPA-17, SPA-18 and SPA-19 must all be complete | Internal |

---

## Risk Mitigation

| Impediment | Mitigation Strategy |
|------------|-------------------|
| IMP-01 | Use Railway MongoDB for all production connections. Keep local MongoDB for development. |
| IMP-02 | Monitor Railway credit usage. Evaluate upgrading to paid plan or migrating to Render free tier before expiration. |
| IMP-03 | Ensure `app.use(cors())` is present in `app.js` before all routes. |
| IMP-05 | Document Railway MongoDB connection string in a secure location outside the codebase. Recreate service if deleted and update all environment variables. |

---

## Definition of Done

- [ ] All pages load correctly on Netlify production URL
- [ ] All fetch calls point to Railway backend URL — no localhost references
- [ ] Full user flow tested end to end — register, login, post, like, search, profile, logout
- [ ] All pages responsive on mobile and desktop
- [ ] No unhandled errors in browser console
- [ ] JWT token stored and cleared correctly in localStorage
- [ ] GitHub repository up to date with latest changes
- [ ] `.env` file not committed to GitHub
