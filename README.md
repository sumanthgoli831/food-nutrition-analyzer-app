# 🍔 Food Nutrition Analyzer App

> **AI-powered mobile app that analyzes food from camera photos and provides instant nutrition data (calories, protein, carbs, fat). Ready for Google Play Store deployment.**

[![Flutter](https://img.shields.io/badge/Flutter-3.38.1-blue.svg)](https://flutter.dev/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-green.svg)](https://fastapi.tiangolo.com/)
[![LogMeal API](https://img.shields.io/badge/LogMeal-Food%20AI-orange.svg)](https://logmeal.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📱 Demo

**Core Features:**
- 📸 Camera-based food scanning
- 🧠 AI food recognition (1300+ dishes)
- 📊 Instant nutrition data (calories, macros)
- 📅 Meal history tracking
- ✏️ Manual portion adjustments
- 🌍 Global food database

---

## 🏗️ Architecture

```
┌─────────────────┐
│  Flutter App    │
│  (Android/iOS)  │
└────────┬────────┘
         │ HTTP
         ▼
┌─────────────────┐
│  FastAPI Backend│
│  (Python)       │
└────────┬────────┘
         │ REST API
         ▼
┌─────────────────┐
│  LogMeal API    │
│  (Food AI)      │
└─────────────────┘
```

**Tech Stack:**
- **Frontend**: Flutter (Dart) - Cross-platform mobile UI
- **Backend**: FastAPI (Python) - High-performance API proxy
- **AI Service**: LogMeal Food Recognition API
- **Database**: SQLite (local meal history)
- **State Management**: Provider pattern

---

## 🚀 Quick Start

### Prerequisites

```bash
# Install Flutter SDK (3.38.1+)
curl -fsSL https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_3.38.1-stable.tar.xz | tar -xJ
export PATH="$PATH:`pwd`/flutter/bin"

# Install Python 3.9+
sudo apt install python3 python3-pip

# Install Android Studio & SDK
# Download from: https://developer.android.com/studio
```

### 1. Clone Repository

```bash
git clone https://github.com/sumanthgoli831/food-nutrition-analyzer-app.git
cd food-nutrition-analyzer-app
```

### 2. Setup Backend

```bash
cd backend
python3 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Get LogMeal API Key
# 1. Sign up at https://logmeal.com/api
# 2. Copy API token from Users section
# 3. Create .env file:
echo "LOGMEAL_API_KEY=your_api_key_here" > .env

# Run backend
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### 3. Setup Flutter App

```bash
cd ../flutter_app
flutter pub get

# Update backend URL in lib/services/nutrition_service.dart:
# Change 'YOUR_BACKEND_IP' to your backend IP (e.g., 192.168.1.100)

# Run app
flutter run
```

---

## 📂 Project Structure

```
food-nutrition-analyzer-app/
├── flutter_app/                # Flutter mobile app
│   ├── lib/
│   │   ├── main.dart           # App entry point
│   │   ├── screens/
│   │   │   ├── camera_screen.dart
│   │   │   └── results_screen.dart
│   │   └── services/
│   │       ├── nutrition_service.dart
│   │       └── database_service.dart
│   ├── android/                # Android-specific config
│   │   └── app/
│   │       └── build.gradle    # API 35 targeting
│   └── pubspec.yaml
├── backend/                    # FastAPI backend
│   ├── main.py                 # API endpoints
│   ├── requirements.txt
│   └── .env                    # API keys (not committed)
├── docs/
│   ├── DEPLOYMENT.md           # Play Store deployment guide
│   └── API.md                  # API documentation
└── README.md
```

---

## 🎯 Core Features Explained

### Food Recognition Flow

1. **User captures photo** → Camera plugin takes picture
2. **Image sent to backend** → HTTP MultipartRequest
3. **Backend calls LogMeal API** → Food recognition + nutrition
4. **Results returned** → JSON with foods array
5. **Display + Save** → Show UI, store in SQLite

### Nutrition Data Structure

```json
{
  "foods": [
    {
      "name": "Chicken Curry",
      "calories": 450,
      "protein": 30,
      "carbs": 35,
      "fat": 20
    }
  ]
}
```

---

## 📱 Google Play Store Deployment

### Android Configuration (API 35)

Edit `android/app/build.gradle`:

```gradle
android {
    compileSdk 35  // Android 15
    defaultConfig {
        minSdk 24
        targetSdk 35  // Required after Aug 31, 2025
        versionCode 1
        versionName "1.0.0"
    }
}
```

### Build Release AAB

```bash
# Generate keystore (first time only)
keytool -genkey -v -keystore ~/upload-keystore.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias upload

# Create android/key.properties:
storePassword=YOUR_PASSWORD
keyPassword=YOUR_PASSWORD
keyAlias=upload
storeFile=/path/to/upload-keystore.jks

# Build AAB
flutter build appbundle --release

# Output: build/app/outputs/bundle/release/app-release.aab
```

### Play Store Checklist

- [ ] Sign up for [Google Play Console](https://play.google.com/console) ($25 one-time)
- [ ] Create app listing (name, description, screenshots)
- [ ] Upload AAB file
- [ ] Complete content rating questionnaire
- [ ] Add privacy policy URL (camera/data usage)
- [ ] Set pricing & distribution (countries)
- [ ] Submit for review (24-48 hours)

---

## 🔑 API Keys & Costs

### LogMeal API

**Free Tier**: 200 API calls/month  
**Pricing**: $0.10 per API call after free tier  
**Sign up**: https://logmeal.com/api

**What you get per API call:**
- Food recognition (1300+ dishes)
- Ingredient detection
- Nutrition data (calories, protein, carbs, fat)
- Portion estimation

**Alternative APIs:**
- **Passio Nutrition-AI SDK**: Flutter plugin, commercial licensing
- **Gemini Vision API**: Custom prompts, requires nutrition DB mapping

---

## 🔧 Development

### Running Backend Locally

```bash
cd backend
uvicorn main:app --reload

# Access Swagger docs: http://localhost:8000/docs
```

### Running Flutter App

```bash
cd flutter_app
flutter run  # Debug mode
flutter run --release  # Release mode
```

### Testing

```bash
# Flutter tests
flutter test

# Backend tests
pytest backend/tests/
```

---

## 🐛 Troubleshooting

### App can't connect to backend

```dart
// Update lib/services/nutrition_service.dart
static const String apiUrl = 'http://YOUR_IP:8000/analyze';

// Get your IP:
// Windows: ipconfig
// Mac/Linux: ifconfig | grep "inet "
// Use 10.0.2.2:8000 for Android Emulator
```

### LogMeal API errors

```bash
# Check API key in backend/.env
cat backend/.env

# Test API directly:
curl -X POST https://api.logmeal.es/v2/image/recognition/complete \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "image=@test.jpg"
```

### Play Store rejection

**Common issues:**
- Missing privacy policy → Add URL explaining camera/data usage
- Wrong API level → Must target API 35 after Aug 31, 2025
- Missing content rating → Complete questionnaire in Play Console

---

## 📚 Documentation

- [Full Deployment Guide](docs/DEPLOYMENT.md)
- [API Documentation](docs/API.md)
- [Flutter Camera Plugin](https://pub.dev/packages/camera)
- [LogMeal API Docs](https://docs.logmeal.com/)
- [Play Store Requirements](https://support.google.com/googleplay/android-developer/answer/11926878)

---

## 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create feature branch (`git checkout -b feature/YourFeature`)
3. Commit changes (`git commit -m 'Add YourFeature'`)
4. Push to branch (`git push origin feature/YourFeature`)
5. Open Pull Request

---

## 📄 License

MIT License - see [LICENSE](LICENSE) file

---

## 👤 Author

**Sumanth Goli**
- GitHub: [@sumanthgoli831](https://github.com/sumanthgoli831)
- Email: [Your Email]

---

## 🙏 Acknowledgments

- [LogMeal](https://logmeal.com/) for food recognition API
- [Flutter](https://flutter.dev/) team for amazing framework
- [FastAPI](https://fastapi.tiangolo.com/) for high-performance backend

---

## 🗺️ Roadmap

- [ ] Barcode scanning for packaged foods
- [ ] Recipe suggestions based on ingredients
- [ ] Daily calorie goal tracking
- [ ] Diet filters (Keto, Vegan, etc.)
- [ ] Cloud sync with user accounts
- [ ] iOS App Store deployment
- [ ] Voice input for food logging
- [ ] Integration with fitness trackers

---

**Built with ❤️ for healthier eating habits**
