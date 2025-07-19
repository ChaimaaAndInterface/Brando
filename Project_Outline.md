# AI Chat Application

This project plan outlines the development of a full-stack AI-powered chat application. The plan is broken down into distinct phases, each with specific goals, action items, and the necessary knowledge required for successful implementation.

## Technologies

* **Backend:** Python, Flask
* **Frontend:** HTML, CSS, JavaScript
* **Database:** Google Firestore
* **Authentication:** bcrypt, PyJWT
* **Deployment:** Google Cloud

## Project Plan

### Phase 1: Backend Foundation

[cite_start]The primary goal of this phase is to establish a fundamental web server capable of handling requests[cite: 4].

---

#### **Micro-Phase 1.1: Set Up Your Local Environment**

**Action Items:**
* [cite_start]Install Python on your computer[cite: 7].
* [cite_start]Create a new project folder and add your `index.html`, `login.html`, `signup.html`, and `style.css` files[cite: 8].
* [cite_start]In your project folder's terminal or command prompt, install the Flask framework by executing: `pip install Flask Flask-Cors`[cite: 9].

**Required Knowledge:**
* [cite_start]**Basic Command Line:** Familiarity with navigating folders (`cd`), listing files (`ls` or `dir`), and running commands like `pip` is essential for installing software and running the server[cite: 11, 12].
* [cite_start]**Python Fundamentals:** A foundational understanding of Python syntax, variables, and functions is necessary to develop the server-side code[cite: 13].

---

#### **Micro-Phase 1.2: Create a "Hello World" Flask Server**

**Action Items:**
* [cite_start]Inside your project folder, create a new file named `app.py`[cite: 16].
* [cite_start]Develop a simple Flask application to ensure the server can listen for requests[cite: 17].
* [cite_start]Establish a test endpoint (a "route") that provides a simple message[cite: 18].
* [cite_start]Execute the server from the command line using: `python app.py`[cite: 19].
* [cite_start]Open a web browser and go to `http://127.0.0.1:5000/api/test` to verify that your message is displayed[cite: 20].

**Required Knowledge:**
* [cite_start]**Flask Basics:** Understanding application initialization, routes (`@app.route(...)`), and returning responses is at the core of the backend[cite: 22, 23].
* [cite_start]**APIs (Conceptual):** Grasping that an API (Application Programming Interface) facilitates communication between the frontend (browser) and the backend (server) is crucial[cite: 24]. [cite_start]This test route serves as the initial API endpoint[cite: 25].

### Phase 2: Database & User Sign-Up

[cite_start]The objective of this phase is to connect to a database and enable new users to create accounts[cite: 27].

---

#### **Micro-Phase 2.1: Set Up Firestore & Connect**

**Action Items:**
* [cite_start]Navigate to the Google Cloud Console to create a project and activate the Firestore database[cite: 30].
* [cite_start]Generate a secure "service account key" (a JSON file) for your project; this file should not be shared[cite: 31].
* [cite_start]Install the Python library for Firestore by running: `pip install firebase-admin`[cite: 32].
* [cite_start]In `app.py`, incorporate the necessary code to initialize the database connection using the service account key[cite: 33].

**Required Knowledge:**
* [cite_start]**Cloud Console Navigation:** Basic proficiency in using a cloud provider's dashboard to create projects and manage services is required[cite: 35].
* [cite_start]**NoSQL Concepts:** An understanding of NoSQL databases like Firestore, which store data in documents organized into collections, is necessary[cite: 36]. [cite_start]This differs from traditional SQL tables[cite: 37].

---

#### **Micro-Phase 2.2: Build the Sign-Up Backend**

**Action Items:**
* [cite_start]Install a library for password security: `pip install bcrypt`[cite: 40].
* [cite_start]In `app.py`, create a new API route: `/api/signup`[cite: 41]. [cite_start]This route will accept a username, email, and password[cite: 42].
* [cite_start]Within the route, hash the provided password using bcrypt[cite: 43].
* [cite_start]Store the new user's information (username, email, and the hashed password) in a `users` collection in Firestore[cite: 44].

**Required Knowledge:**
* [cite_start]**Password Hashing:** It is critical for security to understand why passwords should never be stored in plain text[cite: 46]. [cite_start]`bcrypt` is a one-way function that transforms a password into a secure hash[cite: 47]. [cite_start]This is a fundamental concept in cybersecurity[cite: 48].
* [cite_start]**Flask Requests:** Knowledge of how to retrieve data (like JSON) from a frontend request using Flask's `request` object is required[cite: 49].

---

#### **Micro-Phase 2.3: Connect the Sign-Up Frontend**

**Action Items:**
* [cite_start]Create a new JavaScript file (e.g., `auth.js`) and link it to your `signup.html`[cite: 52].
* Write JavaScript code that:
    * [cite_start]Listens for the "submit" event on the sign-up form[cite: 54].
    * [cite_start]Prevents the default form submission[cite: 55].
    * [cite_start]Retrieves the values from the username, email, and password input fields[cite: 56].
    * [cite_start]Utilizes the `fetch()` function to send this data to your `/api/signup` backend endpoint[cite: 57].
    * [cite_start]Displays a success or error message to the user based on the server's response[cite: 58].

**Required Knowledge:**
* [cite_start]**JavaScript DOM Manipulation:** You will need to know how to select HTML elements (`document.getElementById`) and retrieve their values (`.value`)[cite: 60].
* [cite_start]**JavaScript Events:** Understanding how to listen for user actions such as clicks or form submissions (`.addEventListener`) is necessary[cite: 61].
* [cite_start]**JavaScript fetch() API:** This is the contemporary method for making API calls from the browser to your backend[cite: 62]. [cite_start]You must know how to execute a POST request and manage the returned Promise[cite: 63].

### Phase 3: Login & Authentication

[cite_start]This phase focuses on enabling existing users to log in and authenticate their identity for subsequent requests[cite: 65].

---

#### **Micro-Phase 3.1: Build the Login Backend**

**Action Items:**
* [cite_start]Install the JWT library by running: `pip install PyJWT`[cite: 68].
* [cite_start]Create a new API route: `/api/login`[cite: 69]. [cite_start]This route will accept an email and password[cite: 70].
* [cite_start]The system will look up the user in Firestore by their email[cite: 71].
* [cite_start]If the user exists, bcrypt will be used to compare the submitted password with the stored hash[cite: 72].
* [cite_start]If the credentials match, a JSON Web Token (JWT) containing the user's ID will be generated and sent back to the frontend[cite: 73].

**Required Knowledge:**
* [cite_start]**Authentication vs. Authorization:** It is important to understand that authentication is the process of verifying a user's identity (logging in), while authorization determines what actions a user is permitted to perform[cite: 75].
* [cite_start]**JWT (JSON Web Tokens):** Learning what JWTs are and their application in stateless authentication is key[cite: 76]. [cite_start]A JWT acts as a temporary, secure ID card that the user includes with every request to confirm they are logged in[cite: 77].

---

#### **Micro-Phase 3.2: Connect the Login Frontend**

**Action Items:**
* [cite_start]In your `auth.js` file, implement the logic for the `login.html` page[cite: 80].
* [cite_start]Use `fetch()` to send the email and password to the `/api/login` endpoint[cite: 81].
* [cite_start]Upon a successful login, receive the JWT from the server[cite: 82].
* [cite_start]Store the JWT in the browser's `localStorage`[cite: 83].
* [cite_start]Redirect the user to the main `index.html` page[cite: 84].

**Required Knowledge:**
* [cite_start]**Browser Storage (localStorage):** An understanding of how `localStorage` works is needed to store small amounts of data, like the JWT, in the user's browser, ensuring it persists even if the tab is closed[cite: 86].

### Phase 4: Core Chat Functionality

[cite_start]The goal of this phase is to create a secure chat endpoint and make the chat interface operational[cite: 88].

---

#### **Micro-Phase 4.1: Build the Secure Chat Backend**

**Action Items:**
* [cite_start]Create a new API route: `/api/chat`[cite: 91].
* [cite_start]Secure this route by requiring a JWT to be sent in the request headers[cite: 92].
* [cite_start]The route will first validate the JWT; if it is invalid or absent, an error will be returned[cite: 93].
* [cite_start]If the JWT is valid, it will be decoded to retrieve the `userId`[cite: 94].
* [cite_start]Implement basic keyword-matching logic (e.g., if the message contains "hello," respond with "Hi there!")[cite: 95].
* [cite_start]Log the user's message and the AI's response to a `conversations` collection in Firestore, including the `userId`[cite: 96].

**Required Knowledge:**
* [cite_start]**HTTP Headers:** You should understand that headers are additional pieces of information sent with an API request[cite: 98]. [cite_start]The `Authorization` header is the standard location for a JWT[cite: 99].
* [cite_start]**Python Dictionaries/JSON:** The AI logic will heavily depend on manipulating dictionaries to formulate responses[cite: 100].

---

#### **Micro-Phase 4.2: Activate the Chat Frontend**

**Action Items:**
* [cite_start]Create a JavaScript file for `index.html` (e.g., `chat.js`)[cite: 103].
* When the page loads, check for a JWT in `localStorage`. [cite_start]If it is not present, redirect to `login.html`[cite: 104].
* [cite_start]If a JWT is present, display the chat container and hide the prompt view[cite: 105].
* When a user sends a message:
    * [cite_start]Display their message on the right side of the chat window[cite: 107].
    * [cite_start]Use `fetch()` to send the message and the JWT (in the `Authorization` header) to your `/api/chat` endpoint[cite: 108].
    * [cite_start]When a response is received, display the AI's message on the left side[cite: 109].

**Required Knowledge:**
* [cite_start]**JavaScript Functions:** You will be writing functions to manage sending messages, receiving responses, and updating the user interface[cite: 111].
* [cite_start]**Dynamic HTML:** Knowledge of how to use JavaScript to create new HTML elements and append them to the page is required[cite: 112]. [cite_start]This is how the chat messages will be rendered[cite: 113].

---

[cite_start]This detailed plan provides a clear path forward[cite: 114]. [cite_start]It is recommended to tackle one micro-phase at a time, ensuring you are comfortable with the "Required Knowledge" before beginning to code[cite: 115]. [cite_start]Good luck! [cite: 116]