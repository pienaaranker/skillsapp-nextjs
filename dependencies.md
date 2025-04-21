# Modulern Dependencies

This file tracks the key libraries and tools used in the Modulern project and their purpose.

## Core Framework & Hosting

*   **Next.js:** React framework for frontend (UI, routing, SSR/SSG) and backend (API Routes).
*   **React:** UI library for building components.
*   **Vercel:** Hosting platform optimized for Next.js deployment.

## Backend & Database

*   **Firebase:** Backend-as-a-Service platform providing:
    *   **Authentication:** Handling user sign-up, sign-in, and session management (using Firebase Auth).
    *   **Firestore Database:** (Potentially used later) NoSQL database for storing user data, curricula, progress, etc.
    *   **Storage:** (Potentially used later for assignment submissions).
*   **firebase:** Official JavaScript SDK for interacting with Firebase services.

## AI / Language Model

*   **Google Gemini:** Large Language Model used for curriculum generation and assignment creation via its API.
    *   *(Note: All Gemini API calls are routed through `https://proxy-chi-plum.vercel.app/`)*

## Frontend UI & Styling

*   **Tailwind CSS:** Utility-first CSS framework for styling. (Assuming standard Next.js setup includes it)
*   **firebaseui:** (Recommended) Pre-built UI components for Firebase authentication forms.
*   **lucide-react:** Library for simple, consistent line icons (as per `style_guide.md`).

## Development Tools

*   **Node.js / npm:** JavaScript runtime and package manager.
*   **Git:** Version control system.
*   **ESLint / Prettier:** (Likely included in Next.js setup) For code linting and formatting. 