
# Product Backlog — Social Network

---

## Product Goal

Develop a fully functional web social network deployed in the cloud where users can register, authenticate, publish multimedia content, interact through likes, and explore other users' publications from any internet-connected device.

---

## Epics

| ID | Epic | Description |
|----|------|-------------|
| E1 | User Authentication | Registration, login and logout with security |
| E2 | Post Management | Create, view and explore posts |
| E3 | Social Interactions | Likes and profile viewing |
| E4 | Search and Navigation | Search posts by text and tags |
| E5 | Infrastructure and Deployment | Backend, database and frontend in the cloud |

---

## E1 — User Authentication

### US-01 Account Registration

**As** a new user  
**I want** to create an account with username, email and password  
**So that** I can access the social network features

**Acceptance Criteria:**
- The system validates that all fields are filled
- The system validates that passwords match
- Email and username must be unique in the database
- Password is stored encrypted with bcryptjs
- Upon successful registration the user receives a JWT token and is redirected to the home page

**Gherkin:**
```gherkin
Feature: User registration

  Scenario: Successful registration
    Given the user is on the registration page
    When they enter username "juanito", email "juan@test.com" and password "123456"
    And confirm password "123456"
    And click "Create account"
    Then the system creates the account in the database
    And stores the JWT token in localStorage
    And redirects the user to index.html

  Scenario: Passwords do not match
    Given the user is on the registration page
    When they enter password "123456" and confirm "654321"
    And click "Create account"
    Then the system shows the message "Passwords do not match"
    And no record is created in the database

  Scenario: Email already registered
    Given a user with email "juan@test.com" already exists
    When another user tries to register with the same email
    Then the system shows "Username or email already registered"
```

---

### US-02 Login

**As** a registered user  
**I want** to log in with my email and password  
**So that** I can access my account and private features

**Acceptance Criteria:**
- The system validates that fields are not empty
- The system compares the entered password with the encrypted one in the database
- Upon successful login the user receives a JWT token
- The token and user data are stored in localStorage
- Incorrect credentials show an error message without revealing which field failed

**Gherkin:**
```gherkin
Feature: Login

  Scenario: Successful login
    Given the user is on the login page
    When they enter email "juan@test.com" and password "123456"
    And click "Sign in"
    Then the system verifies the credentials
    And stores the JWT token in localStorage
    And redirects the user to index.html

  Scenario: Incorrect credentials
    Given the user is on the login page
    When they enter email "juan@test.com" and wrong password "000000"
    And click "Sign in"
    Then the system shows "Incorrect credentials"
    And no token is stored

  Scenario: Empty fields
    Given the user is on the login page
    When they leave the password field empty
    And click "Sign in"
    Then the system shows "All fields are required"
```

---

### US-03 Logout

**As** an authenticated user  
**I want** to log out  
**So that** I can protect my account on shared devices

**Acceptance Criteria:**
- Logout removes the token and user data from localStorage
- The user is redirected to the login page
- Private routes are inaccessible after logout

**Gherkin:**
```gherkin
Feature: Logout

  Scenario: Successful logout
    Given the user has an active session
    When they click "Sign out"
    Then the system removes the token from localStorage
    And redirects the user to login.html

  Scenario: Access to private route without session
    Given the user has no active session
    When they try to access crear-post.html directly
    Then the system automatically redirects to login.html
```

---

## E2 — Post Management

### US-04 Create Post

**As** an authenticated user  
**I want** to create a post with text, tags and an optional image  
**So that** I can share content with other users

**Acceptance Criteria:**
- The content field is required
- Tags are entered in #tag format and converted to an array
- The image/video link is optional
- The post automatically stores the author's username and avatar as a snapshot
- After successful publishing redirects to home after 1.5 seconds
- If no active session redirects to login

**Gherkin:**
```gherkin
Feature: Create post

  Scenario: Successful post with text and tags
    Given the user has an active session
    And is on crear-post.html
    When they write "My first post" in the content field
    And write "#test #first" in the tags field
    And click "Create post"
    Then the system saves the post in the database
    And shows the message "Post created successfully!"
    And redirects to index.html after 1.5 seconds

  Scenario: Post without content
    Given the user has an active session
    When they leave the content field empty
    And click "Create post"
    Then the system shows "Post content is required"
    And no post is saved

  Scenario: Attempt to post without session
    Given the user has no active session
    When they access crear-post.html
    Then the system automatically redirects to login.html
```

---

### US-05 View Post Gallery

**As** a visitor or authenticated user  
**I want** to see all posts on the social network  
**So that** I can explore available content

**Acceptance Criteria:**
- Posts load automatically when entering index.html
- Displayed from most recent to oldest
- Each post shows content, author, likes and tags if any
- If the post has an image it is displayed; if it has tags they are shown as badges
- If there are no posts an informative message is shown
- The page is responsive — 3 columns on desktop, 2 on tablet, 1 on mobile

**Gherkin:**
```gherkin
Feature: Post gallery

  Scenario: Successfully load posts
    Given posts exist in the database
    When the user enters index.html
    Then the system makes GET to /api/posts
    And displays each post in a card with content, author and likes

  Scenario: No posts
    Given no posts exist in the database
    When the user enters index.html
    Then the system shows "No posts yet"
```

---

### US-06 View Post in Detail

**As** a user  
**I want** to view a post in full size  
**So that** I can read the full content and see the image without cropping

**Acceptance Criteria:**
- Clicking a post redirects to post-detalle.html with the id in the URL
- Displays full image without cropping
- Shows author with avatar, publication date and tags
- Includes a functional like button
- Includes a "View profile" button for the author

**Gherkin:**
```gherkin
Feature: Post detail

  Scenario: View post in detail
    Given the user is on index.html
    When they click on a post
    Then the system redirects to post-detalle.html?id={postId}
    And shows full content, image, author, date and likes

  Scenario: Post not found
    Given the user accesses post-detalle.html with an invalid id
    Then the system shows "Post not found"
```

---

## E3 — Social Interactions

### US-07 Like a Post

**As** an authenticated user  
**I want** to like a post  
**So that** I can express that I enjoyed the content

**Acceptance Criteria:**
- Only authenticated users can like posts
- Clicking like increments the counter by 1 visually
- Clicking again removes the like and decrements the counter by 1
- If no active session redirects to login when trying to like
- The backend records the like in the likes collection and updates likes_count in the post

**Gherkin:**
```gherkin
Feature: Like system

  Scenario: Successfully like a post
    Given the user has an active session
    And is viewing a post with 5 likes
    When they click the like button
    Then the system makes POST to /api/posts/{id}/like
    And the counter shows 6
    And the button turns red

  Scenario: Remove like
    Given the user has already liked a post
    When they click the like button again
    Then the system makes DELETE to /api/posts/{id}/like
    And the counter decrements by 1
    And the button returns to grey

  Scenario: Like without session
    Given the user has no active session
    When they click the like button
    Then the system redirects to login.html
```

---

### US-08 View Own Profile

**As** an authenticated user  
**I want** to view my profile  
**So that** I can review my posts and account data

**Acceptance Criteria:**
- Shows the logged-in user's username and email
- Shows only the logged-in user's posts
- Each post shows its like counter
- Clicking a post redirects to its detail
- If no active session redirects to login

**Gherkin:**
```gherkin
Feature: Own profile

  Scenario: View profile with posts
    Given the user has an active session and has published posts
    When they access perfil.html
    Then the system shows their username and email
    And shows only their posts

  Scenario: View profile without posts
    Given the user has an active session but no posts
    When they access perfil.html
    Then the system shows "You have no posts yet"
```

---

### US-09 View Another User's Profile

**As** a user  
**I want** to view another user's profile  
**So that** I can explore their content

**Acceptance Criteria:**
- Accessible from the "View profile" button in post-detalle.html
- Shows the user's username and avatar with their initials
- Shows all posts by that user
- Each post shows its like counter
- Clicking a post redirects to its detail

**Gherkin:**
```gherkin
Feature: Another user's profile

  Scenario: View profile from post detail
    Given the user is on post-detalle.html
    When they click "View profile"
    Then the system redirects to perfil-usuario.html?id={authorId}
    And shows the author's username and posts
```

---

## E4 — Search and Navigation

### US-10 Search Posts

**As** a user  
**I want** to search posts by text  
**So that** I can find specific content

**Acceptance Criteria:**
- Search filters by post content, author name and tags
- Clicking "Search" redirects to posts.html with the text as a URL parameter
- Also works by pressing Enter
- If no results an informative message is shown
- Search is case-insensitive

**Gherkin:**
```gherkin
Feature: Post search

  Scenario: Search with results
    Given the user is on index.html
    When they type "cats" in the search bar
    And click "Search"
    Then the system redirects to posts.html?q=cats
    And shows posts containing "cats" in content, author or tags

  Scenario: Search with no results
    Given the user searches for "xyzabc123"
    Then the system shows "No posts found for xyzabc123"
```

---

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
