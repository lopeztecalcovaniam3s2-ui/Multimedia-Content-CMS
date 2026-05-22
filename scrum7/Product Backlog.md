- Project Objective 🎯

Develop a multimedia social network platform that allows users to create and share content in different formats, such as images, videos, and text posts.

The platform should include social interaction features, such as reactions, likes, and comments,
to encourage participation and communication among users.

In addition, a profile tracking system will be integrated so that each user can connect with others
and stay up-to-date on their posts. We will also aim to offer a more personalized experience by
displaying content tailored to each user's interests and preferences,
thus improving interaction and engagement on the platform.

- Epics 🥇

To prevent the project from becoming complex or difficult to maintain in its early stages,
the first version will focus solely on essential functionalities.

The goal is to develop a solid, functional, and easily scalable foundation for future updates.

The first version will include:

• Registration and login:
Users will be able to create an account and securely access the platform using basic authentication.

This will allow for the identification of each user and the maintenance of their personalized information.

• User profile:
Each user will have a profile where they can view and manage their basic information within the application,

providing a more personalized experience.

• Content posting (image + minimal text):
Users will be able to create posts that include an image accompanied by a brief description or text.

This feature will be the core of interaction within the platform.

• Likes:
A "like" system will be implemented so that users can interact with other users' posts,

making it easy to measure the acceptance or interest in the shared content.

These features aim to keep the project organized, functional, and focused on what is truly necessary for a stable first version.

It does not include (for now):

Private messaging
Complex recommendation algorithms
Live streaming
Real-time notifications

- User Story 📄
➊ Story 1: Welcome to the Site➋
As a new user, I want to use all the site's features. The user will be able to freely explore posts without obstacles, perform searches, and check profiles.

When the user tries to like a post, the site returns their request with a login form or, failing that, an account creation form.

And when they try to create a post, their request will be rejected with a login form.

➊ Evaluation Criteria Story 1: ➊
* The system should have simple options that do not require any validation.
* The system must validate the user's identity on the page to interact with some special functions.
* The system should present an alternative in case of a lack of identity on the site.

  Feature: Welcome to the Site
  As a new user
  I want to explore the site's content freely
  So that I can view posts, perform searches, and check profiles

  Scenario: Explore posts without logging in
    Given I am a new user on the site
    When I browse posts
    Then I should be able to view all posts without obstacles

  Scenario: Like a post without logging in
    Given I am a new user
    When I try to like a post
    Then I should be prompted with a login form
    And if I have no account, I should see an account creation form

  Scenario: Attempt to create a post without logging in
    Given I am a new user
    When I try to create a post
    Then my request should be rejected
    And I should be shown the login form

➋ Story 2: Login/Creation of Sessions ➋

As a user, I want to become part of the site. The user locates the login button and, upon noticing it, 
enters the corresponding data requested in the form. When a user is new, they will have no data to enter, so they must access a second form to create their account.

The system should perform data checks to verify that the following data is repeated:
* Password

If it is repeated, the system should not allow the creation of any account.

Evaluation Criteria - History 2

* An account creation form
* Password encryption

➋ History 2: Creating posts ➋
As a user, I want to be able to easily create posts. The user is presented with a form to create their post, and they can upload images or GIFs using links.

When the user is not logged in, the system should reject the request and start the corresponding form.

Evaluation Criteria - History 3:
* Post creation form
* Profile validation

Feature: Login and Account Creation
  As a user
  I want to access the site with an account
  So that I can interact with special functions

  Scenario: Login with existing account
    Given I am on the login page
    When I enter valid credentials
    Then I should be logged into my account

  Scenario: Create a new account
    Given I am a new user
    When I navigate to the account creation form
    And I enter my details
    And my password is not repeated
    Then my account should be created successfully
    And my password should be encrypted

  Scenario: Attempt to create an account with a repeated password
    Given I am a new user
    When I enter a password that already exists in the system
    Then the system should not allow account creation
- Proposed architecture 👨‍💻

Frontend: Website (HTML)
Backend: API (Node.js recommended)
Database: MongoDB (NoSQL)
