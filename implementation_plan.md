# Skill Learning App: Implementation Plan

This document outlines the implementation plan for the Skill Learning App, based on the provided architecture and requirements document. Check off tasks as they are completed.

**Goal:** To develop a web application that uses Google Gemini to generate personalized learning curricula from free online resources.

**Technology Stack:**
* **Frontend:** Next.js
* **Backend:** Next.js API Routes
* **Database & Auth:** Supabase
* **LLM:** Google Gemini
* **Hosting:** Vercel

---

## Phase 1: Foundation & Setup (Estimated: 1 Week)

**Objective:** Establish the development environment, project structure, and essential service integrations.

- [x] **Task 1.1: Environment Setup**
    - [x] Install Node.js and npm/yarn.
    - [x] Install Next.js CLI.
    - [x] Install Supabase CLI.
- [x] **Task 1.2: Project Initialization**
    - [x] Create a new Next.js project (`npx create-next-app@latest`).
    - [x] Set up Git repository and version control.
- [x] **Task 1.4: API Key Acquisition**
    - [x] Obtain API keys for Google Gemini.
    - [x] Review Gemini API documentation and usage limits.
- [ ] **Task 1.5: Basic Integration**
    - [x] Install Supabase client library (`@supabase/supabase-js`) in the Next.js project.
    - [x] Configure environment variables for Supabase URL and keys.
    - [ ] Establish basic connectivity between Next.js and Supabase.

---

## Phase 2: Core Feature Development - Authentication & Curriculum (Estimated: 2-3 Weeks)

**Objective:** Implement user management and the core curriculum generation functionality.

- [ ] **Task 2.1: User Authentication**
    - [ ] Implement frontend UI for user registration and login using Supabase Auth UI components or custom forms.
    - [ ] Set up protected routes/pages in Next.js.
    - [ ] Handle user sessions and state management.
- [ ] **Task 2.2: Skill & Experience Selection UI**
    - [ ] Create frontend components for users to input the desired skill.
    - [ ] Implement UI for selecting experience level (Beginner, Intermediate, Advanced, Custom).
- [ ] **Task 2.3: Backend Curriculum Generation API**
    - [ ] Create a Next.js API route (`/api/generate-curriculum`).
    - [ ] Accept `skill` and `experienceLevel` (or `quizResults`) as input.
    - [ ] **Crucial:** Develop robust prompt engineering strategies for the Gemini API call to request structured curriculum data (JSON preferred) based on input, emphasizing free resources.
    - [ ] Handle potential errors from the Gemini API.
- [ ] **Task 2.4: Gemini API Integration (Backend)**
    - [ ] Install necessary libraries for making API calls (e.g., `axios` or `node-fetch`).
    - [ ] Implement the call to the Gemini API within the backend route using the obtained API key. **Note:** All Gemini API calls should be routed through the proxy server at `https://proxy-chi-plum.vercel.app/`. See `https://github.com/pienaaranker/proxy` for details.
    - [ ] Parse the Gemini response (expecting structured JSON).
- [ ] **Task 2.5: Curriculum Display UI**
    - [ ] Create frontend components to display the generated curriculum (modules, steps, resource links) fetched from the backend.
    - [ ] Store the generated curriculum in Supabase, linking it to the user and skill.

---

## Phase 3: Core Feature Development - Tracking & Assignments (Estimated: 2-3 Weeks)

**Objective:** Enable users to track their learning progress and receive generated assignments.

- [ ] **Task 3.1: Progress Tracking Logic**
    - [ ] Implement backend logic (API route or direct Supabase calls from frontend/server components) to mark curriculum steps as complete/incomplete.
    - [ ] Update the `user_progress` table in Supabase.
- [ ] **Task 3.2: Progress Visualization UI**
    - [ ] Develop frontend components to visually represent progress (e.g., checkmarks on steps, progress bars per module/curriculum).
    - [ ] Create a basic User Dashboard page summarizing active curricula and overall progress.
- [ ] **Task 3.3: Backend Assignment Generation API**
    - [ ] Create a Next.js API route (`/api/generate-assignment`).
    - [ ] Accept context (e.g., `step_id` or `module_id`) as input.
    - [ ] Develop prompts for Gemini requesting relevant practice exercises or assignments based on the learning context.
    - [ ] Handle Gemini API calls and responses. **Note:** Ensure these calls also use the proxy server `https://proxy-chi-plum.vercel.app/`.
- [ ] **Task 3.4: Assignment Display UI**
    - [ ] Create frontend components to allow users to request an assignment for a specific step/module.
    - [ ] Display the generated assignment content received from the backend.
    - [ ] Store generated assignments in Supabase, linking it to the user and skill.

---

## Phase 4: Advanced Features & Refinement (Estimated: 2 Weeks)

**Objective:** Enhance the user experience with custom features and refine existing ones.

- [ ] **Task 4.1: Custom Experience Level Quiz**
    - [ ] Design the logic and questions for the custom experience assessment quiz. This likely requires further LLM prompting or a predefined question bank structure.
    - [ ] Implement the quiz UI on the frontend.
    - [ ] Integrate quiz results into the curriculum generation prompt context (Task 2.3).
- [ ] **Task 4.2: Resource Link Validation & Handling**
    - [ ] Implement basic checks or allow user reporting for broken/incorrect resource links.
    - [ ] Refine prompts to improve the quality and relevance of free resources found by Gemini.
- [ ] **Task 4.3: User Dashboard Enhancement**
    - [ ] Flesh out the User Dashboard with more details (completed skills, suggested next steps, etc.).
- [ ] **Task 4.4: (Optional) Assignment Submission/Feedback**
    - [ ] Implement UI for users to submit assignment answers (text or file upload via Supabase Storage).
    - [ ] *Advanced:* Explore using Gemini for basic feedback on submitted assignments (requires careful prompt design and handling).

---

## Phase 5: Testing, Deployment & Iteration (Ongoing)

**Objective:** Ensure application quality, deploy to production, and establish a feedback loop.

- [ ] **Task 5.1: Testing**
    - [ ] Component/Unit testing for critical UI and logic parts.
    - [ ] Integration testing for API routes and database interactions.
    - [ ] End-to-End (E2E) testing for key user flows (signup, curriculum generation, progress tracking).
    - [ ] Manual testing focusing on usability and curriculum quality.
- [ ] **Task 5.2: Address Challenges**
    - [ ] Implement strategies to mitigate LLM hallucinations (e.g., user flagging, cross-referencing).
    - [ ] Monitor and refine prompts based on testing results.
    - [ ] Optimize parsing of LLM output.
- [ ] **Task 5.3: Deployment**
    - [ ] Configure Vercel for deployment.
    - [ ] Set up environment variables in Vercel.
    - [ ] Deploy the application.
- [ ] **Task 5.4: Monitoring & Iteration**
    - [ ] Monitor application performance and costs (especially Gemini API usage).
    - [ ] Set up basic logging and error tracking.
    - [ ] Gather user feedback through surveys or feedback forms.
    - [ ] Plan for iterative updates based on feedback and testing.

---

**Disclaimer:** Timelines are estimates and may vary based on complexity, team size, and unforeseen challenges. Prompt engineering for the LLM is a critical and potentially time-consuming aspect requiring significant iteration.
