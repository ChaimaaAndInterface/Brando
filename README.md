# AI-Powered Social Interaction Chatbot

This project outlines the development of a Conversational AI Application designed for web and WordPress platforms. It focuses on a phased approach to building a robust and interactive chatbot.

## Table of Contents

1.  [Introduction](#introduction)
2.  [Core Functionality & User Experience](#core-functionality--user-experience)
    * [User Flow](#user-flow)
    * [Dialogue Engine](#dialogue-engine)
3.  [Technical Stack](#technical-stack)
4.  [Data Management & Analytics](#data-management--analytics)
    * [Database Architecture](#database-architecture)
    * [Conversation Logging, Learning, Analytics](#conversation-logging-learning-analytics)
    * [User Feedback](#user-feedback)
5.  [Infrastructure & Deployment](#infrastructure--deployment)
    * [Local Development & CI/CD](#local-development--cicd)
    * [Environment Configuration](#environment-configuration)
6.  [Security Measures](#security-measures)
    * [Data Encryption](#data-encryption)
    * [Anonymization or Pseudonymization of Personal Data](#anonymization-or-pseudonymization-of-personal-data)
    * [User Authentication](#user-authentication)
    * [Audit Trail / Security Logs](#audit-trail--security-logs)
7.  [Project Schedule (Approximate Phases)](#project-schedule-approximate-phases)
8.  [Deliverables](#deliverables)

## 1. Introduction

This project aims to build an AI-powered conversational chatbot that provides natural and effortless interactions for users on web and potentially WordPress platforms. The development will proceed in distinct phases, ensuring a structured and manageable approach.

## 2. Core Functionality & User Experience

### User Flow

The user interaction is designed to be intuitive and conversational:

1.  **Open the App**: User accesses the web application, presenting a chat window.
2.  **AI Greets**: The system provides a warm welcome, prompting the user to start chatting.
3.  **User Inputs Query**: User types questions or commands into the chat box.
4.  **System Processes Input**: Input is sent to the AI backend for processing.
5.  **AI Generates Response**: The AI processes the input, understands the intent, and crafts a helpful text response.
6.  **Answer Appears**: The AI's reply is displayed in the chat window.
7.  **Continue Conversation**: Users can continue the dialogue by repeating steps 3-6.

Future enhancements include context retention, clarification capabilities, and actionable responses.

### Dialogue Engine

The dialogue engine will evolve through phases:

* **Phase 1: Rules & Keyword Matching**: The AI will identify specific keywords or patterns to trigger pre-defined responses.
* **Phase 2: Basic Intent Recognition**: Utilizing NLP libraries (e.g., scikit-learn), the system will categorize user phrases into "intents" (e.g., "greet," "ask_order_status") linked to specific responses. Simple session state will be maintained for context.

## 3. Technical Stack

* **Frontend**: React.js (JavaScript)
* **Backend**: Python (Flask or FastAPI)
* **Database**: Google Cloud Firestore (NoSQL)
* **Containerization**: Docker
* **Version Control**: Git (GitHub)
* **NLP Libraries**: NLTK, SpaCy, scikit-learn

## 4. Data Management & Analytics

### Database Architecture

A NoSQL document-oriented database, Google Cloud Firestore, is chosen for its flexibility and scalability, especially for conversational data.

**Proposed Collections:**

* `users`: Stores user authentication details (encrypted passwords, unique IDs, signup timestamps).
* `conversations`: Each document represents a complete chat session, including `startTime`, `endTime`, `topic`, and a `messages` sub-collection (or linked separately if conversations are very long).
* `analytics_logs`: Raw conversation data for insights.
* `feedback`: Stores user feedback submissions.

### Conversation Logging, Learning, Analytics

* **Conversation Logging**: Every user message and AI response will be logged with details like `messageId`, `conversationId`, `userId`, `sender`, `text`, `timestamp`, `sentiment`, `detectedIntent`, and `context_variables`.
* **Learning**: Initial learning will be manual, involving reviewing logs to refine rules and simple classification models.
* **Analytics**: Key metrics tracked will include active conversations, average conversation length, common user intents, AI response accuracy (manual review initially), and user satisfaction. Simple Python scripts will be used for data processing and reporting.

### User Feedback

An in-app feedback form will allow users to provide ratings and comments, which will be saved to Firestore for analysis to improve the chatbot.

## 5. Infrastructure & Deployment

### Local Development & CI/CD

* **Local Development**: Docker Compose will be used for setting up the local development environment (frontend, backend, local database if applicable).
* **CI/CD**: GitHub Actions will be implemented for Continuous Integration/Continuous Deployment. The pipeline will include triggers on code pushes, building Docker images, running tests, and deploying to a container registry (e.g., Google Container Registry) and target environments (e.g., Google Cloud Run/Firebase Hosting).

### Environment Configuration

Configuration settings (API keys, database URLs, logging levels) will be managed using environment variables (`os.environ.get()` in Python, `.env` files/Webpack's DefinePlugin in React) to ensure separation between development, testing, and production environments.

## 6. Security Measures

Security is a core aspect of the project.

### Data Encryption (TLS, SSL)

* **In Transit**: All communication will be encrypted using TLS/SSL, handled automatically by deployment platforms like Firebase Hosting and Google Cloud Run.
* **At Rest**: Firestore automatically encrypts data at rest.

### Anonymization or Pseudonymization of Personal Data

* **User IDs**: Randomly generated UUIDs will be used for users in conversation logs instead of directly identifiable information.
* **Conversation Content**: Efforts will be made to avoid storing sensitive personal information directly in chat logs, with future improvements for masking sensitive data.
* **Pseudonymization**: `conversationId` and `userId` will be linked to analytics data, but the `users` collection (containing real user info) will be kept separate with controlled access.

### User Authentication (JWT)

JSON Web Tokens (JWT) will be used for stateless user authentication. The flow involves:

1.  User logs in/signs up, providing credentials to the backend.
2.  Backend verifies credentials against Firestore.
3.  Backend generates a JWT containing `userId` and non-sensitive info.
4.  JWT is sent to the frontend and securely stored (localStorage, sessionStorage, or httpOnly cookies).
5.  Frontend includes JWT in `Authorization` header for future API requests.
6.  Backend validates the JWT's signature and expiration, extracting `userId` for authorization.

### Audit Trail / Security Logs

Important security-related events (login attempts, new registrations, data changes, API errors) will be logged using Python's logging module and stored in a dedicated system like Google Cloud Logging for analysis and alerts. Logs will include `timestamp`, `event_type`, `userId`, `source_IP`, `outcome`, and a `description`.

## 7. Project Schedule (Approximate Phases)

* **Phase 1: Foundation & Basic Chat (Weeks 1-3)**
    * React frontend setup.
    * Simple Flask backend setup.
    * User authentication (signup/login).
    * Firestore connection for basic user data.
    * Initial rule-based/keyword matching AI.
    * Basic conversation logging.
* **Phase 2: Refinement & Initial Deployment (Weeks 3-8)**
    * Improve chat interface and user experience.
    * Set up Dockerfiles and Docker Compose for local development.
    * Implement GitHub Actions for CI/CD.
    * Deploy prototype to Google Cloud Run/Firebase Hosting.
    * Refine existing AI rules.
* **Phase 3: Analytics & Feedback (Weeks 3-12)**
    * Integrate Google Analytics for frontend tracking.
    * Implement in-app feedback form and save data to Firestore.
    * Develop simple Python scripts for basic analytics reporting.
    * Explore basic intent recognition using NLP libraries.
* **Phase 4: Future Enhancements & Polish (Ongoing)**
    * Context retention for AI.
    * Clarification capabilities.
    * Actionable responses.
    * Continuous AI model refinement based on feedback and analytics.

## 8. Deliverables

* **Functional Prototype**: Web-based chat interface, basic conversational AI, user authentication, conversation logging to Firestore.
* **Codebase**: Frontend (React) source code, Backend (Python Flask) source code, Dockerfiles, GitHub Actions CI/CD workflow.
* **Documentation**: Basic `README.md` with setup instructions, API documentation (if FastAPI is used).
* **Deployment**: Live application accessible via a public URL (e.g., Google Cloud Run/Firebase Hosting).
