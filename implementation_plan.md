# Modulern: Implementation Plan

This document outlines the implementation plan for the Modulern, based on the provided architecture and requirements document. Check off tasks as they are completed.

**Goal:** To develop a web application that uses Google Gemini to generate personalized learning curricula from free online resources.

**Technology Stack:**
* **Frontend:** Next.js
* **Backend:** Next.js API Routes
* **Database:** Firebase Firestore
* **Auth:** Firebase Authentication
* **Storage:** Firebase Storage (Optional)
* **LLM:** Google Gemini
* **Hosting:** Vercel

---

## Phase 1: Foundation & Setup (Estimated: 1 Week)

**Objective:** Establish the development environment, project structure, and essential service integrations.

- [x] **Task 1.1: Environment Setup**
    - [x] Install Node.js and npm/yarn.
    - [x] Install Next.js CLI.
- [x] **Task 1.2: Project Initialization**
    - [x] Create a new Next.js project (`npx create-next-app@latest`).
    - [x] Set up Git repository and version control.
- [ ] **Task 1.3: Firebase Project Setup**
    - [ ] Create a Firebase project via the Firebase console.
    - [ ] Enable Firestore Database, Firebase Authentication, and optionally Firebase Storage.
    - [ ] Configure basic Firestore security rules (start restrictive).
    - [ ] Obtain Firebase configuration credentials (apiKey, authDomain, projectId, etc.).
- [x] **Task 1.4: API Key Acquisition**
    - [x] Obtain API keys for Google Gemini.
    - [x] Review Gemini API documentation and usage limits.
- [ ] **Task 1.5: Basic Integration**
    - [x] Install Firebase client SDK (`firebase`) in the Next.js project.
    - [ ] Install Firebase Admin SDK (`firebase-admin`) for backend use.
    - [x] Configure environment variables for Firebase credentials (both client config and service account for admin).
    - [ ] Initialize Firebase client SDK in the Next.js app (e.g., in `_app.tsx` or a dedicated config file).
    - [ ] Establish helper functions or context for interacting with Firestore and Auth.

---

## Phase 2: Core Feature Development - Authentication & Curriculum (Estimated: 2-3 Weeks)

**Objective:** Implement user management and the core curriculum generation functionality.

- [ ] **Task 2.1: User Authentication**
    - [ ] Implement frontend UI for user registration and login using Firebase Authentication (e.g., `firebaseui-web` or custom email/password, Google Sign-In flows).
    - [ ] Set up protected routes/pages in Next.js based on Firebase Auth state.
    - [ ] Handle user sessions and state management (e.g., using React Context with Firebase Auth listeners).
    - [ ] Store additional user profile information in a Firestore 'users' collection upon signup.
- [ ] **Task 2.2: Skill & Experience Selection UI**
    - [ ] Create frontend components for users to input the desired skill.
    - [ ] Implement UI for selecting experience level (Beginner, Intermediate, Advanced, Custom).
- [ ] **Task 2.3: Backend Curriculum Generation API**
    - [ ] Create a Next.js API route (`/api/generate-curriculum`).
    - [ ] Secure the API route (ensure only authenticated users can call it).
    - [ ] Accept `skill` and `experienceLevel` (or `quizResults`) as input.
    - [ ] **Crucial:** Develop robust prompt engineering strategies for the Gemini API call to request structured curriculum data (JSON preferred) based on input, emphasizing free resources.
    - [ ] Handle potential errors from the Gemini API.
- [ ] **Task 2.4: Gemini API Integration (Backend)**
    - [ ] Install necessary libraries for making API calls (e.g., `axios` or `node-fetch`).
    - [ ] Implement the call to the Gemini API within the backend route using the obtained API key. **Note:** All Gemini API calls should be routed through the proxy server at `https://proxy-chi-plum.vercel.app/`. See `https://github.com/pienaaranker/proxy` for details.
    - [ ] Parse the Gemini response (expecting structured JSON).
- [ ] **Task 2.5: Curriculum Display & Storage**
    - [ ] Create frontend components to display the generated curriculum (modules, steps, resource links) fetched from the backend.
    - [ ] Store the generated curriculum in Firestore (e.g., a 'curricula' collection), linking it to the user ID and skill. Structure the data appropriately for efficient querying.

---

## Phase 3: Core Feature Development - Tracking & Assignments (Estimated: 2-3 Weeks)

**Objective:** Enable users to track their learning progress and receive generated assignments.

- [ ] **Task 3.1: Progress Tracking Logic**
    - [ ] Implement backend logic (API route or direct Firestore calls from frontend/server components using security rules) to mark curriculum steps as complete/incomplete.
    - [ ] Update user-specific progress data in Firestore (e.g., within the user's document or a separate 'progress' subcollection).
- [ ] **Task 3.2: Progress Visualization UI**
    - [ ] Develop frontend components to visually represent progress (e.g., checkmarks on steps, progress bars per module/curriculum) by reading data from Firestore.
    - [ ] Create a basic User Dashboard page summarizing active curricula and overall progress fetched from Firestore.
- [ ] **Task 3.3: Backend Assignment Generation API**
    - [ ] Create a Next.js API route (`/api/generate-assignment`).
    - [ ] Secure the API route.
    - [ ] Accept context (e.g., `curriculum_id`, `step_id` or `module_id`) as input.
    - [ ] Develop prompts for Gemini requesting relevant practice exercises or assignments based on the learning context.
    - [ ] Handle Gemini API calls and responses. **Note:** Ensure these calls also use the proxy server `https://proxy-chi-plum.vercel.app/`.
- [ ] **Task 3.4: Assignment Display & Storage**
    - [ ] Create frontend components to allow users to request an assignment for a specific step/module.
    - [ ] Display the generated assignment content received from the backend.
    - [ ] Store generated assignments in Firestore (e.g., an 'assignments' collection), linking them to the user, curriculum, and specific step/module.

---

## Phase 4: Advanced Features & Refinement (Estimated: 2 Weeks)

**Objective:** Enhance the user experience with custom features and refine existing ones.

- [ ] **Task 4.1: Custom Experience Level Quiz**
    - [ ] Design the logic and questions for the custom experience assessment quiz. This likely requires further LLM prompting or a predefined question bank structure stored in Firestore.
    - [ ] Implement the quiz UI on the frontend.
    - [ ] Integrate quiz results into the curriculum generation prompt context (Task 2.3).
- [ ] **Task 4.2: Resource Link Validation & Handling**
    - [ ] Implement basic checks or allow user reporting for broken/incorrect resource links (store reports possibly in Firestore).
    - [ ] Refine prompts to improve the quality and relevance of free resources found by Gemini.
- [ ] **Task 4.3: User Dashboard Enhancement**
    - [ ] Flesh out the User Dashboard with more details fetched from Firestore (completed skills, suggested next steps, etc.).
- [ ] **Task 4.4: (Optional) Assignment Submission/Feedback**
    - [ ] Implement UI for users to submit assignment answers (text stored in Firestore or file upload via Firebase Storage).
    - [ ] *Advanced:* Explore using Gemini for basic feedback on submitted assignments (requires careful prompt design and handling, potentially storing feedback in Firestore).

---

## Phase 5: Testing, Deployment & Iteration (Ongoing)

**Objective:** Ensure application quality, deploy to production, and establish a feedback loop.

- [ ] **Task 5.1: Testing**
    - [ ] Component/Unit testing for critical UI and logic parts.
    - [ ] Integration testing for API routes and Firestore interactions (consider Firebase Local Emulator Suite).
    - [ ] End-to-End (E2E) testing for key user flows (signup, curriculum generation, progress tracking).
    - [ ] Manual testing focusing on usability and curriculum quality.
    - [ ] Test Firestore security rules thoroughly.
- [ ] **Task 5.2: Address Challenges**
    - [ ] Implement strategies to mitigate LLM hallucinations (e.g., user flagging, cross-referencing).
    - [ ] Monitor and refine prompts based on testing results.
    - [ ] Optimize parsing of LLM output.
    - [ ] Monitor Firestore costs and optimize queries/data structures.
- [ ] **Task 5.3: Deployment**
    - [ ] Configure Vercel for deployment.
    - [ ] Set up environment variables in Vercel for Firebase client config, Firebase Admin SDK credentials (as secrets), and Gemini API key.
    - [ ] Deploy the application.
- [ ] **Task 5.4: Monitoring & Iteration**
    - [ ] Monitor application performance and costs (Vercel, Firebase usage, Gemini API usage).
    - [ ] Set up basic logging and error tracking (e.g., Vercel logs, Sentry).
    - [ ] Gather user feedback through surveys or feedback forms.
    - [ ] Plan for iterative updates based on feedback and testing.

---

**Disclaimer:** Timelines are estimates and may vary based on complexity, team size, and unforeseen challenges. Prompt engineering for the LLM is a critical and potentially time-consuming aspect requiring significant iteration. Firebase setup and security rules configuration also require careful attention.
