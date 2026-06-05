# Sprint Backlog — Sprint 0 "Foundations"
## Social Network

---

## Context

This sprint covers the initial setup of the project — database design, backend architecture, authentication system and local development environment configuration. This work was completed before any frontend integration.

---

## Sprint 0 — "Foundations"

**Duration:** 4 weeks
**Objective:** Design and implement the data model, set up the Node.js + Express + MongoDB backend, and deliver a fully functional REST API with authentication.

---

## Sprint Parameter & Capacity Plan

| Parameter | Value |
|-----------|-------|
| Sprint Duration | 4 weeks |
| Daily Commitment | 2 hours (Monday – Friday) |
| Total Sprint Capacity | 200 hours |
| Estimated Workload | 160 hours |
| Buffer | 40 hours |

---

## Sprint Goal

> Deliver a fully functional and tested REST API with user authentication, post management and likes, connected to a MongoDB database and running locally.

---

## Sprint Backlog

| ID | Story | Description | Priority | Estimate | Epic |
|----|-------|-------------|----------|----------|------|
| SP0-01 | Project folder structure | Create the folder structure: `src/config`, `src/models`, `src/routes`, `src/controllers`, `src/middleware` | High | 1 pt | E5 |
| SP0-02 | Node.js and npm initialization | Install Node.js, run `npm init -y` and configure `package.json` with start and dev scripts | High | 1 pt | E5 |
| SP0-03 | Install dependencies | Install `express`, `mongoose`, `dotenv`, `bcryptjs`, `jsonwebtoken`, `cors` and `nodemon` | High | 1 pt | E5 |
| SP0-04 | Environment variables setup | Create `.env` file with `PORT`, `MONGO_URI` and `JWT_SECRET`. Add `.env` to `.gitignore` | High | 1 pt | E5 |
| SP0-05 | MongoDB connection | Create `src/config/db.js` with Mongoose connection and error handling | High | 2 pts | E5 |
| SP0-06 | Express app configuration | Create `src/app.js` with CORS, JSON middleware and route mounting | High | 2 pts | E5 |
| SP0-07 | Server entry point | Create `server.js` that loads `.env`, imports app and starts listening on the configured port | High | 1 pt | E5 |
| SP0-08 | USERS schema design | Design and implement `User.js` Mongoose schema with username, email, password_hash, avatar_url, bio and timestamps | High | 3 pts | E1 |
| SP0-09 | POSTS schema design | Design and implement `Post.js` Mongoose schema with Snapshot Pattern for author data, tags array, editors array, likes_count and timestamps | High | 3 pts | E2 |
| SP0-10 | LIKES schema design | Design and implement `Like.js` Mongoose schema with post_id, user_id, compound unique index and timestamps | High | 2 pts | E3 |
| SP0-11 | Register endpoint | Implement `POST /api/auth/register` — validate fields, check duplicates, hash password with bcryptjs, create user, return JWT | High | 4 pts | E1 |
| SP0-12 | Login endpoint | Implement `POST /api/auth/login` — find user by email, compare password with bcryptjs, return JWT | High | 3 pts | E1 |
| SP0-13 | Auth middleware | Create `auth.middleware.js` — verify JWT token, fetch full user from MongoDB, attach to `req.user` | High | 3 pts | E1 |
| SP0-14 | Create post endpoint | Implement `POST /api/posts` — protected route, create post with author snapshot from `req.user` | High | 3 pts | E2 |
| SP0-15 | Get all posts endpoint | Implement `GET /api/posts` — return all posts sorted by most recent | High | 2 pts | E2 |
| SP0-16 | Like post endpoint | Implement `POST /api/posts/:id/like` — protected, create like document, increment likes_count | Medium | 3 pts | E3 |
| SP0-17 | Unlike post endpoint | Implement `DELETE /api/posts/:id/like` — protected, delete like document, decrement likes_count | Medium | 2 pts | E3 |
| SP0-18 | API testing with Thunder Client | Install Thunder Client in VS Code, test all endpoints manually — register, login, create post, get posts, like, unlike | High | 3 pts | E5 |
| SP0-19 | Local MongoDB setup | Install MongoDB Community Server, configure PATH, create `/data/db` directory, run `mongod` as local service | Medium | 2 pts | E5 |
| SP0-20 | MongoDB Shell setup | Install `mongosh`, verify connection to local MongoDB, run basic queries on all collections | Medium | 1 pt | E5 |

**Total:** 43 points

---

## Sprint Acceptance Criteria

```gherkin
Feature: User registration via API

  Scenario: Successful registration
    Given the API is running on localhost:3000
    When a POST request is sent to /api/auth/register with valid username, email and password
    Then the response status is 201
    And the response contains a JWT token
    And the user is created in the MongoDB users collection
    And the password is stored as a bcryptjs hash

  Scenario: Duplicate email registration
    Given a user with email "test@test.com" already exists
    When a POST request is sent to /api/auth/register with the same email
    Then the response status is 400
    And the response contains "El usuario o email ya está registrado"
```

```gherkin
Feature: User login via API

  Scenario: Successful login
    Given a registered user with email "test@test.com" and password "123456"
    When a POST request is sent to /api/auth/login with those credentials
    Then the response status is 200
    And the response contains a JWT token
    And the token encodes the user id

  Scenario: Wrong password
    Given a registered user with email "test@test.com"
    When a POST request is sent to /api/auth/login with wrong password "000000"
    Then the response status is 400
    And the response contains "Credenciales incorrectas"
```

```gherkin
Feature: Create post via API

  Scenario: Authenticated user creates a post
    Given the user is authenticated with a valid JWT token
    When a POST request is sent to /api/posts with content, tags and optional media_url
    Then the response status is 201
    And the post is saved in the MongoDB posts collection
    And the post includes author_username and author_avatar_url from the user snapshot

  Scenario: Unauthenticated request to create post
    Given no Authorization header is sent
    When a POST request is sent to /api/posts
    Then the response status is 401
    And the response contains "No autorizado, token requerido"
```

```gherkin
Feature: Like and unlike a post

  Scenario: Like a post
    Given the user is authenticated
    And a post with id "abc123" exists with likes_count 0
    When a POST request is sent to /api/posts/abc123/like
    Then the response status is 200
    And a like document is created in the likes collection
    And the post likes_count is updated to 1

  Scenario: Unlike a post
    Given the user has previously liked post "abc123"
    When a DELETE request is sent to /api/posts/abc123/like
    Then the response status is 200
    And the like document is removed from the likes collection
    And the post likes_count is decremented by 1
```

```gherkin
Feature: MongoDB local connection

  Scenario: Successful connection
    Given mongod is running on localhost:27017
    When the Node.js server starts
    Then the console shows "MongoDB conectado"
    And Mongoose is connected to the social-network database

  Scenario: Connection failure
    Given mongod is not running
    When the Node.js server starts
    Then the console shows "Error de conexión"
    And the process exits with code 1
```

---

## Technical Tasks by Week

### Week 1 — Environment & Data Model

| Day | DEV-1 | DEV-2 | DEV-3 | DEV-4 | DEV-5 |
|-----|-------|-------|-------|-------|-------|
| Monday | SP0-01: Create folder structure | SP0-02: Install Node.js and initialize npm | SP0-03: Install all dependencies | SP0-04: Configure .env and .gitignore | SP0-19: Install MongoDB locally |
| Tuesday | SP0-07: Create server.js | SP0-06: Create app.js with Express config | SP0-05: Create db.js with Mongoose connection | SP0-20: Install mongosh and test connection | SP0-19: Configure PATH and /data/db |
| Wednesday | SP0-08: Design User.js schema | SP0-08: Review and validate User.js schema | SP0-09: Design Post.js schema with Snapshot Pattern | SP0-09: Review and validate Post.js schema | SP0-10: Design Like.js schema with unique index |
| Thursday | Test server startup — verify MongoDB connected message | Test all three models load without errors | Review schema decisions — embedding vs referencing | Document data model decisions | SP0-10: Validate unique index on Like.js |
| Friday | Week 1 review — verify full project structure | Week 1 review — verify all dependencies installed | Week 1 review — verify all schemas correct | Week 1 review — verify local MongoDB running | Week 1 review — team sync |

### Week 2 — Authentication

| Day | DEV-1 | DEV-2 | DEV-3 | DEV-4 | DEV-5 |
|-----|-------|-------|-------|-------|-------|
| Monday | SP0-11: Create auth.routes.js | SP0-11: Create auth.controller.js — register function | SP0-11: Implement bcryptjs password hashing | SP0-12: Implement login function | SP0-13: Create auth.middleware.js |
| Tuesday | SP0-11: Implement JWT token generation on register | SP0-12: Implement JWT token generation on login | SP0-12: Implement bcryptjs password comparison | SP0-13: Implement JWT verification in middleware | SP0-13: Fetch full user from MongoDB in middleware |
| Wednesday | SP0-11: Test register endpoint with Thunder Client | SP0-12: Test login endpoint with Thunder Client | SP0-13: Test middleware with valid token | SP0-13: Test middleware with invalid token | SP0-13: Test middleware with no token |
| Thursday | Fix register bugs found in testing | Fix login bugs found in testing | Fix middleware bugs found in testing | Document authentication flow | Review JWT expiration and secret configuration |
| Friday | Week 2 review — verify register, login and middleware working | Week 2 review — verify all auth tests passing | Week 2 review — team sync | Update .env with strong JWT_SECRET | Verify .env is properly in .gitignore |

### Week 3 — Posts and Likes

| Day | DEV-1 | DEV-2 | DEV-3 | DEV-4 | DEV-5 |
|-----|-------|-------|-------|-------|-------|
| Monday | SP0-14: Create post.routes.js | SP0-14: Create post.controller.js — createPost function | SP0-15: Implement getPosts function | SP0-16: Implement likePost function | SP0-17: Implement unlikePost function |
| Tuesday | SP0-14: Connect author snapshot from req.user to post creation | SP0-15: Sort posts by created_at descending | SP0-16: Increment likes_count with $inc operator | SP0-17: Decrement likes_count with $inc operator | Mount post routes in app.js |
| Wednesday | SP0-14: Test create post with Thunder Client | SP0-15: Test get all posts with Thunder Client | SP0-16: Test like post with Thunder Client | SP0-17: Test unlike post with Thunder Client | Test full posts and likes flow end to end |
| Thursday | Fix create post bugs — verify author snapshot is correct | Fix get posts bugs — verify sort order | Fix like bugs — verify likes_count increments correctly | Fix unlike bugs — verify likes_count decrements correctly | Verify duplicate like returns error |
| Friday | Week 3 review — verify all post and like endpoints working | Week 3 review — team sync | Document all available API endpoints | Test all endpoints in sequence — register, login, post, like | Verify JWT protection on all private routes |

### Week 4 — Testing and Validation

| Day | DEV-1 | DEV-2 | DEV-3 | DEV-4 | DEV-5 |
|-----|-------|-------|-------|-------|-------|
| Monday | SP0-18: Full API test suite with Thunder Client — all endpoints | SP0-18: Full API test suite with Thunder Client — all endpoints | SP0-18: Full API test suite with Thunder Client — all endpoints | SP0-18: Full API test suite with Thunder Client — all endpoints | SP0-18: Full API test suite with Thunder Client — all endpoints |
| Tuesday | Verify all MongoDB collections created correctly | Run mongosh queries — verify users, posts and likes data | Test error handling — missing fields, wrong credentials | Test error handling — expired token, invalid token | Test error handling — duplicate email, duplicate like |
| Wednesday | Bug fixing — address all issues found in testing | Bug fixing — address all issues found in testing | Bug fixing — address all issues found in testing | Bug fixing — address all issues found in testing | Bug fixing — address all issues found in testing |
| Thursday | Sprint 0 demo — present register and login endpoints | Sprint 0 demo — present create and get posts endpoints | Sprint 0 demo — present like and unlike endpoints | Sprint 0 demo — present MongoDB data via mongosh | Sprint 0 demo — coordinate and document feedback |
| Friday | Sprint retrospective — what went well | Sprint retrospective — what to improve | Sprint 1 planning — review frontend integration backlog | Sprint 1 planning — assign stories | Sprint 1 planning — team sync |

---

## Impediments

| ID | Description | Impact | Owner |
|----|-------------|--------|-------|
| IMP-01 | Node.js not installed on Windows machines | Blocks all backend development until resolved | Developer |
| IMP-02 | MongoDB Atlas unreachable due to Telmex DNS blocking port 27017 | Forces local MongoDB as development database | External — ISP |
| IMP-03 | PowerShell does not recognize `mkdir -p` syntax | Minor friction during folder structure setup | Developer |
| IMP-04 | mongosh not included in MongoDB Server installer | Requires separate installation for database shell access | Developer |

---

## Dependencies

| ID | Story | Depends on | Type |
|----|-------|------------|------|
| DEP-01 | SP0-05 MongoDB connection | Local MongoDB must be running before server starts | Internal |
| DEP-02 | SP0-11 Register endpoint | SP0-08 User.js schema must be complete | Internal |
| DEP-03 | SP0-14 Create post endpoint | SP0-13 Auth middleware must be complete | Internal |
| DEP-04 | SP0-16 Like endpoint | SP0-14 and SP0-10 must be complete | Internal |
| DEP-05 | All stories | SP0-02 and SP0-03 must be complete — Node.js and dependencies required | Internal |

---

## Risk Mitigation

| Impediment | Mitigation Strategy |
|------------|-------------------|
| IMP-01 | Download Node.js LTS from nodejs.org and add to Windows PATH |
| IMP-02 | Use local MongoDB for development. Switch to Railway MongoDB for production deployment |
| IMP-04 | Download mongosh separately from mongodb.com/try/download/shell |

---

## Definition of Done

- [ ] All endpoints return correct HTTP status codes
- [ ] All endpoints tested manually with Thunder Client
- [ ] JWT authentication works on all protected routes
- [ ] MongoDB collections created and populated with test data
- [ ] No unhandled errors in the Node.js console
- [ ] `.env` file is in `.gitignore` and not committed to GitHub
- [ ] `nodemon` restarts server correctly on file changes
