# Complete Setup Guide - Food Nutrition Analyzer

## ✅ Project Status: READY TO BUILD

All code, architecture, and deployment instructions are complete. Follow these steps to build and deploy your app.

---

## 📦 What You're Building

**App Name**: Food Nutrition Analyzer  
**Platform**: Android (Google Play Store ready)  
**Tech Stack**: Flutter + FastAPI + LogMeal AI  
**Cost to Launch**: $25 (Play Store developer account)  

**Core Features**:
- 📸 Camera-based food scanning
- 🧠 AI recognition (1300+ dishes)
- 📊 Nutrition data (calories, protein, carbs, fat)
- 📅 Meal history with SQLite
- ✏️ Manual portion editing

---

## 🚀 QUICK START (30 Minutes)

### Step 1: Install Prerequisites

```bash
# Install Flutter SDK
# Download from: https://docs.flutter.dev/get-started/install
# Add to PATH

# Install Python 3.9+
# Windows: https://www.python.org/downloads/
# Mac: brew install python3
# Linux: sudo apt install python3 python3-pip

# Install Android Studio
# Download from: https://developer.android.com/studio
# Install Android SDK and create an emulator

# Verify installations
flutter doctor
python3 --version
```

### Step 2: Get LogMeal API Key (FREE)

1. Visit https://logmeal.com/api
2. Sign up (email + password)
3. Navigate to **Users** section
4. Copy your **API Token**
5. Save it - you'll need it in Step 4

**Free Tier**: 200 API calls/month

### Step 3: Clone Repository

```bash
git clone https://github.com/sumanthgoli831/food-nutrition-analyzer-app.git
cd food-nutrition-analyzer-app
```

### Step 4: Setup Backend

```bash
cd backend
python3 -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# Mac/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Create .env file with your API key
echo "LOGMEAL_API_KEY=your_api_key_here" > .env

# Run backend server
uvicorn main:app --reload --host 0.0.0.0 --port 8000

# You should see:
# INFO: Uvicorn running on http://0.0.0.0:8000
# Test: Open http://localhost:8000/docs in browser
```

### Step 5: Setup Flutter App

```bash
# Open NEW terminal (keep backend running)
cd flutter_app
flutter pub get

# Get your local IP address
# Windows: ipconfig
# Mac/Linux: ifconfig | grep "inet "

# Edit lib/services/nutrition_service.dart
# Change line 7 to your IP:
static const String apiUrl = 'http://YOUR_IP:8000/analyze';
# Example: 'http://192.168.1.100:8000/analyze'

# Run on emulator or connected device
flutter run

# For Android emulator, use:
static const String apiUrl = 'http://10.0.2.2:8000/analyze';
```

---

## 📁 Complete File Structure to Create

You need to create these files manually:

```
food-nutrition-analyzer-app/
├── backend/
│   ├── main.py
│   ├── requirements.txt
│   └── .env
├── flutter_app/
│   ├── pubspec.yaml
│   ├── lib/
│   │   ├── main.dart
│   │   ├── screens/
│   │   │   ├── camera_screen.dart
│   │   │   └── results_screen.dart
│   │   └── services/
│   │       ├── nutrition_service.dart
│   │       └── database_service.dart
│   └── android/
│       └── app/
│           └── build.gradle
└── README.md
```

---

## 📄 ALL SOURCE CODE FILES

See the complete documentation with all source code:
https://docs.google.com/document/d/1NNjK6Y4yV13_fbrIWLl08Wx5sEor5A0epUDzUYPQVEM/edit

Or download from: https://github.com/sumanthgoli831/food-nutrition-analyzer-app/releases

---

##
