<h1 align="center">Aahar 🍛🤖</h1>
<p align="center"><b>An AI-Powered Indian Health & Nutrition Ecosystem</b></p>
<p align="center"><i>HackIndia Spark-7 North Region | Team: Udaan</i></p>

## 🚀 Overview
**Aahar** is a cutting-edge, hyper-localized health and fitness mobile application specifically designed for the Indian market. While Western apps struggle with Indian food variations ("Curry Confusion"), **Aahar** uses 2026 Vision-Language AI to "see," understand, and deconstruct complex Indian meals. It goes beyond generic calorie counts by breaking down a cooked meal (like *Paneer Butter Masala*) into raw ingredients (e.g., Atta, Ghee) using the gold-standard ICMR-NIN database.

The app adapts dynamically to user progress, budget, and local environment—providing intelligent macro tracking, budget-adapted diet planning, and goal-oriented workout programming.

## 🎯 The "Indian Context" Problems Solved
*   **The "Curry Confusion"**: Precisely calculates calories based on regional cooking methods instead of generalized estimates.
*   **Calorie Dilution**: Introduces a "Gravy Slider" (Full, Half, Pieces Only) so users don't track the gravy they left behind.
*   **Vernacular Logging**: Allows voice logging in Hinglish (*"Maine 2 katori peeli dal khayi"*).
*   **Budget-Friendly Diets**: Recommends affordable Indian protein sources (Sattu, Soya Chunks) over expensive Western imports.
*   **The Gym Basement Problem**: True "Offline-First" capability using Flutter Isar DB, allowing gym tracking without 4G/5G, auto-syncing when back online.
*   **Context & Privacy**: Features Festive/Fasting Modes (Navratri, Ramadan), weather-aware hydration trackers, and keeps sensitive progress photos locally secured under the DPDP Act.

## ✨ Core Features
*   **Multi-Modal Food Logging**: Photo Thali scans (drawing interactive bounding boxes), Voice notes (Hinglish), Text, or Barcode scans for Indian snacks via `OpenFoodFacts`.
*   **Intelligent Meal Breakdown**: Acts as a "Chef," breaking visual data down into a strict JSON array of raw ingredients rather than guessing a generic final calorie count.
*   **Hyper-Personalization**: Users can edit the AI's deductions, confirm portion sizes using authentic metrics (Katori, Ladle), or dynamically append items (*"Add Dessert"*).
*   **Smart Diet & Workout Engine**: Routes users to scientifically proven workout templates while automatically generating grocery lists that fit their budget.
*   **Gamified Retention**: Apple Watch-style macro rings, celebration streaks, and dynamic macro recalculation upon weight changes.

## 🛠️ Technical Architecture & Stack
Aahar utilizes a highly-optimized **Hybrid AI Architecture**:

*   **Frontend (Mobile App)**: `Flutter` & `Riverpod` — Delivers high-performance UI, custom camera overlays, bounding boxes, and fluid animations.
*   **Local Offline Storage**: `Isar` — A blazing-fast local database for storing workout and diet plans in "Gym Basement Mode".
*   **Backend API**: `Python` + `FastAPI` — Rapid AI integration handling vector embeddings and complex JSON structures.
*   **Cloud & Database**: `Supabase` + `PostgreSQL` — Utilizing `pgvector` for instant semantic matching of extracted ingredients to the **ICMR-NIN database**.
*   **Local Vision AI**: `Gemma 4` (Local Inference) — Provides zero-cloud-cost, highly accurate offline food analysis using the open-source Gemma 4 Vision-Language Model.
*   **Edge AI (On-Device)**: `Google ML Kit` — Instantly verifies and crops food images *on-device* to save bandwidth before sending to the backend.

### 🔄 AI Data Flow (Image Upload)
1. User captures a Thali in Flutter. `Google ML Kit` crops out the background.
2. The compressed image is sent to FastAPI (`POST /analyze/vision`).
3. FastAPI passes the image to the locally-hosted **Gemma 4** Vision-Language Model.
4. AI returns a JSON deconstruction (Raw Ingredients + Bounding Boxes).
5. FastAPI converts ingredients to embeddings and queries `Supabase` (`pgvector`) for accurate ICMR matches.
6. Perfect macros are calculated and returned to Flutter for local `Isar` caching and display.

## 🚀 Setup & Installation (Local Development)

### 1. Frontend (Flutter)
```bash
# Clone the repository
git clone <repository-url>
cd <repository-directory>

# Get dependencies
flutter pub get

# Generate Isar models
dart run build_runner build

# Run the app
flutter run
```

### 2. Backend (FastAPI)
```bash
# Navigate to backend directory
cd backend

# Create a virtual environment
python -m venv venv
venv\Scripts\activate

# Install dependencies
pip install fastapi uvicorn supabase python-dotenv openai sentence-transformers pydantic

# Create a .env file and add your keys
# SUPABASE_URL=...
# SUPABASE_KEY=...

# (Make sure your local Gemma 4 instance is running on your machine)

# Run the FastAPI server
uvicorn main:app --reload
```

## 📜 Documentation
Check out the detailed documentation under the [`docs/`](docs/) folder:
- [System Architecture (LLD)](docs/lld.md)
- [Detailed Project Checklist](docs/Detailed_Checklist.md)
- [Feature Roadmap](docs/feature-to-add-later.md)