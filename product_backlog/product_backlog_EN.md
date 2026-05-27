
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

---

## E1 — User Authentication

### US-01 Account Registration

**As** a new user  
**I want** to create an account with username, email and password  
**So that** I can access the social network features


**Acceptance criteria:**
```gherkin


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

  Scenario: Username already registred
    Given a user with username "juan" already exists
    When another user has that username
    Then the system shows "Username or email already registered"

  Scenario: Lag on Network
    Given the user is on the registration page
    When they enter his data whith network lag
    And click on "Create account"
    Then The system continue the process

  Scenario: Invalid email
    Given the user enter a email
    When the email has a invalid format
    Then the system shows "Invalid Username or email"
 
```

---

### US-02 Login

**As** a registered user  
**I want** to log in with my email and password  
**So that** I can access my account and private features


**Acceptance criteria:**
```gherkin


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


**Acceptance criteria:**
```gherkin


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


**Acceptance criteria:**
```gherkin


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


**Acceptance criteria:**
```gherkin


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

**Acceptance criteria:**
```gherkin


  Scenario: View post in detail
    Given the user is on index.html
    When they click on a post
    Then the system redirects to post-detalle.html?id={postId}
    And shows full content, image, author, date and likes

  Scenario: Post not found
    Given the user accesses post-detalle.html with an invalid id
    When the post is visible
    Then the system shows "Post not found"
```

---

## E3 — Social Interactions

### US-07 Like a Post

**As** an authenticated user  
**I want** to like a post  
**So that** I can express that I enjoyed the content


**Acceptance criteria:**
```gherkin


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


**Acceptance criteria:**
```gherkin


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


**Acceptance criteria:**
```gherkin


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


**Acceptance criteria:**
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
    When the user click on search
    Then the system shows "No posts found for xyzabc123"
```

---

