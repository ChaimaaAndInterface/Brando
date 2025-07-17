# Brando AI - Conversational Assistant

Brando AI is a web-based, intelligent conversational assistant designed to handle complex questions and tasks. This project combines a modern web interface with a powerful AI backend, with a special focus on topics related to AI and Cyber Security.

This application is being built following a phased development plan, starting with a foundational chat prototype and evolving into a more sophisticated and feature-rich platform.

---

## Core Technologies

The project leverages a modern and scalable technology stack to deliver a robust and responsive experience.

| Category           | Technology                                                     | Purpose                                                      |
| ------------------ | -------------------------------------------------------------- | ------------------------------------------------------------ |
| **Frontend** | [React.js](https://reactjs.org/)                               | Building a dynamic and interactive user interface.           |
| **Backend** | [Flask](https://flask.palletsprojects.com/)                    | A lightweight Python framework for the API and AI logic.     |
| **Database** | [Google Cloud Firestore](https://firebase.google.com/docs/firestore) | A scalable NoSQL database for user and conversation data.    |
| **Styling** | [Tailwind CSS](https://tailwindcss.com/)                       | A utility-first CSS framework for rapid UI design.           |
| **Authentication** | [JSON Web Tokens (JWT)](https://jwt.io/)                       | Secure, stateless user authentication between services.      |
| **Containerization** | [Docker](https://www.docker.com/)                              | Packaging the app into containers for consistent environments. |
| **CI/CD** | [GitHub Actions](https://github.com/features/actions)          | Automating testing and deployment workflows.                 |

---

## Project Structure

The project is organized into two main directories in the root folder:

```
/brando-ai-project
|
├── 📁 frontend/      # Contains the React.js application
|   ├── src/
|   ├── public/
|   ├── package.json
|   └── ...
|
├── 📁 backend/       # Contains the Python Flask API
|   ├── venv/
|   ├── app.py
|   ├── requirements.txt
|   └── ...
|
└── 📄 README.md       # You are here!
```

---

## Local Development Setup

To run this project on your local machine, you will need to set up and run both the frontend and backend services simultaneously.

### Prerequisites

* [Node.js](https://nodejs.org/en/) (v16 or later)
* [Python](https://www.python.org/downloads/) (v3.8 or later) and `pip`
* A Google Cloud account with a Firestore database enabled.
* Your Google Cloud Service Account JSON key file.

### 1. Backend Setup

First, set up and run the Python Flask server.

```bash
# 1. Navigate to the backend directory
cd backend

# 2. Create and activate a Python virtual environment
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`

# 3. Install the required Python packages
pip install -r requirements.txt

# 4. Create a .env file and add your credentials (see below)

# 5. Run the Flask development server
flask run
```
> The backend API will now be running at `http://127.0.0.1:5000`.

### 2. Frontend Setup

Next, in a **new terminal window**, set up and run the React application.

```bash
# 1. Navigate to the frontend directory
cd frontend

# 2. Install the required npm packages
npm install

# 3. Run the React development server
npm start
```
> The frontend application will open in your browser at `http://localhost:3000`.

### Environment Variables

You must create a `.env` file in the `backend` directory to store your secret keys.

**`backend/.env`:**
```
# Path to your Google Cloud service account JSON file
GOOGLE_APPLICATION_CREDENTIALS="path/to/your/serviceAccountKey.json"

# Secret key for signing JWTs (use a long, random string)
JWT_SECRET_KEY="your-super-secret-key-that-is-long-and-random"
```

---

## Practical Development Plan (Day-by-Day)

This schedule is designed for focused, 30-minute daily sessions.

### **Phase 1: Foundation & MVP**

* **Day 1:** Convert static `login.html` into a React component (`Login.js`).
* **Day 2:** Convert static `signup.html` into a React component (`Signup.js`).
* **Day 3:** Install `react-router-dom` and set up basic routes for `/login` and `/signup`.
* **Day 4:** Create a placeholder `/chat` route and a basic `ChatContainer.js` component.
* **Day 5:** Convert the static chat UI from `index.html` into the `ChatContainer.js` component.
* **Day 6:** Set up the Flask backend folder, virtual environment, and install Flask.
* **Day 7:** Connect the Flask backend to Firestore using your service account credentials.
* **Day 8:** Create the `/api/signup` endpoint in Flask.
* **Day 9:** Implement password hashing (e.g., with `werkzeug.security`) in the signup endpoint.
* **Day 10:** Implement the `/api/login` endpoint, checking the user and hashed password.
* **Day 11:** Implement JWT creation on the backend and return the token on a successful login.
* **Day 12:** Install and configure `Flask-CORS` on the backend to allow requests from the frontend.
* **Day 13:** Connect the React `Signup.js` form to the `/api/signup` endpoint.
* **Day 14:** Connect the React `Login.js` form to the `/api/login` endpoint.
* **Day 15:** On successful login, store the received JWT in the browser's `localStorage`.
* **Day 16:** Create a "protected route" component in React that checks for the JWT.
* **Day 17:** Use the protected route to guard the `/chat` page, redirecting to `/login` if no JWT is found.
* **Day 18:** Create a basic `/api/chat` endpoint in Flask that requires a valid JWT and returns a hardcoded response.
* **Day 19:** In `ChatContainer.js`, use the `useState` hook to manage an array of chat messages.
* **Day 20:** On chat form submission, send the user's message and JWT to the `/api/chat` endpoint.
* **Day 21:** Display the user's message and the AI's response in the UI by updating the state.

### **Phase 2: Deployment & Core Features**

* **Day 22:** Write a `Dockerfile` for the Flask backend.
* **Day 23:** Test building the backend Docker image locally.
* **Day 24:** Write a `Dockerfile` for the React frontend (using a multi-stage build).
* **Day 25:** Test building the frontend Docker image locally.
* **Day 26:** Create a `docker-compose.yml` file to define the `frontend` and `backend` services.
* **Day 27:** Run the entire application locally using `docker-compose up`.
* **Day 28:** Debug any networking issues between the containers.
* **Day 29:** Set up a basic GitHub Actions workflow file (`.github/workflows/ci.yml`).
* **Day 30:** Configure the CI workflow to build the Docker images on every push to the `main` branch.
* **Day 31:** Deploy the backend Docker image to Google Cloud Run.
* **Day 32:** Configure environment variables in the Cloud Run service.
* **Day 33:** Deploy the frontend to Firebase Hosting or Netlify.
* **Day 34:** Update the backend CORS policy to accept requests from the deployed frontend URL.
* **Day 35:** Test the live, deployed application from end to end.
* **Day 36:** Modify the backend chat endpoint to log user messages to a `conversations` collection in Firestore.
* **Day 37:** Modify the backend chat endpoint to also log the AI's response.
* **Day 38:** Create a new backend endpoint `/api/history` to fetch the chat history for a logged-in user.
* **Day 39:** In the `ChatContainer.js` component, use a `useEffect` hook to call the `/api/history` endpoint when the component loads.
* **Day 40:** Populate the chat state with the fetched history, displaying it in the UI.

### **Phase 3: AI & Security Enhancements**

* **Day 41:** Integrate a basic NLP library (like `spaCy`) into the backend.
* **Day 42:** Create a simple intent recognition system using keyword matching within the `/api/chat` endpoint.
* **Day 43:** Define 3-5 common cyber security questions and create detailed, pre-written answers.
* **Day 44:** Train your basic intent model to recognize and respond to the defined cyber security questions.
* **Day 45:** Add another 2-3 AI-related questions and answers to expand the knowledge base.
* **Day 46:** Implement input validation on the login and signup endpoints to sanitize data.
* **Day 47:** Set up basic security headers (like `Content-Security-Policy`) on the Flask response.
* **Day 48:** Implement rate limiting on the `/api/login` endpoint to protect against brute-force attacks.
* **Day 49:** Add a "Was this helpful?" (thumbs up/down) UI element to AI responses in React.
* **Day 50:** Create a new backend endpoint to receive and store this feedback in Firestore, linked to the specific conversation and message.
* **Day 51+:** Continue to review the UI/UX, fix bugs, clean up the codebase, and research more advanced NLP techniques.
