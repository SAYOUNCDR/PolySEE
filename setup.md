# PolySEE Local Setup Guide

This guide provides detailed instructions on how to set up and run the PolySEE project locally. The project consists of three main components:
1.  **Frontend**: A React-based user interface.
2.  **Auth Service**: A Node.js/Express service for authentication.
3.  **Backend Core**: A Python/FastAPI service for the AI/RAG functionality.

---

## 🏷️ Tech Stack

**Frontend:**
`React` `Vite` `Tailwind CSS` `Framer Motion` `Lucide React` `Recharts` `Axios`

**Auth Service:**
`Node.js` `Express` `MongoDB` `JWT` `Bcrypt.js`

**Backend Core:**
`Python` `FastAPI` `LangChain` `ChromaDB` `Google Generative AI` `Google Cloud Speech`

---

## 📋 Prerequisites

Before you begin, ensure you have the following installed on your machine:

*   **Node.js** (v18 or higher) & **npm** - [Download](https://nodejs.org/)
*   **Python** (v3.8 or higher) - [Download](https://www.python.org/)
*   **MongoDB** (Local instance or Atlas URI) - [Download](https://www.mongodb.com/try/download/community)
*   **Git** - [Download](https://git-scm.com/)

You will also need a **Google API Key** for the AI features (Gemini).

---

## 🚀 Setup Instructions

### 1. Clone the Repository

```bash
git clone <repository-url>
cd PolySEE
```

### 2. Auth Service Setup (Node.js)

This service handles user authentication and connects to MongoDB.

1.  Navigate to the `Auth` directory:
    ```bash
    cd Auth
    ```

2.  Install dependencies:
    ```bash
    npm install
    ```

3.  Configure environment variables:
    *   Create a `.env` file by copying the example:
        ```bash
        cp .env.example .env
        # On Windows Command Prompt: copy .env.example .env
        ```
    *   Open `.env` and update the values if necessary (especially `MONGO_URI` if your MongoDB is not local).
        ```env
        PORT=4000
        MONGO_URI=mongodb://localhost:27017/chatbot
        JWT_SECRET=your_strong_secret_here
        FRONTEND_ORIGIN=http://localhost:5173
        FASTAPI_URL=http://localhost:8000
        ```

4.  Start the Auth service:
    ```bash
    node index.js
    ```
    *   You should see a message indicating the server is running (e.g., `Server running on port 4000`).

### 3. Backend Core Setup (Python/FastAPI)

This service powers the RAG (Retrieval-Augmented Generation) and AI features.

1.  Navigate to the `backend/core` directory:
    ```bash
    cd ../backend/core
    ```

2.  Create a virtual environment:
    ```bash
    python -m venv .venv
    ```

3.  Activate the virtual environment:
    *   **Windows:**
        ```bash
        .venv\Scripts\activate
        ```
    *   **Mac/Linux:**
        ```bash
        source .venv/bin/activate
        ```

4.  Install Python dependencies:
    ```bash
    pip install -r requirements.txt
    ```

5.  Configure environment variables:
    *   Create a `.env` file:
        ```bash
        cp .env.example .env
        # On Windows Command Prompt: copy .env.example .env
        ```
    *   **Crucial:** Open `.env` and add your Google API Key.
        ```env
        GOOGLE_API_KEY=your_google_api_key_here
        PERSIST_DIR=./chroma_db
        TEMP_MD_DIR=./temp_md
        HOST=127.0.0.1
        PORT=8000
        ```

6.  Start the Backend service:
    ```bash
    uvicorn app:app --reload --host 127.0.0.1 --port 8000
    ```
    *   The API docs will be available at `http://127.0.0.1:8000/docs`.

### 4. Frontend Setup (React/Vite)

1.  Navigate to the `Frontend` directory:
    ```bash
    cd ../../Frontend
    ```

2.  Install dependencies:
    ```bash
    npm install
    ```

3.  Start the development server:
    ```bash
    npm run dev
    ```
    *   The application will typically run at `http://localhost:5173`.

---

## 🔗 Connecting the Services

*   **Frontend** runs on `http://localhost:5173`
*   **Auth Service** runs on `http://localhost:4000`
*   **Backend Core** runs on `http://localhost:8000`

Ensure all three terminals are running simultaneously for the full application to work.

## 🛠️ Troubleshooting

*   **MongoDB Connection Error:** Ensure your MongoDB service is running locally (`mongod`) or your connection string in `Auth/.env` is correct.
*   **Python Module Not Found:** Make sure you activated the virtual environment (`.venv`) before running `pip install`.
*   **CORS Errors:** Check the `FRONTEND_ORIGIN` in `Auth/.env` matches your Frontend URL.
*   **Google API Error:** Verify your `GOOGLE_API_KEY` in `backend/core/.env` is valid and has access to the Generative AI API.

---

Happy Coding! 👨‍💻👩‍💻
