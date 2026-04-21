# PFE-Ino Project: Comprehensive Overview

**Project Name:** Innovega - Agricultural Intelligence IoT Platform  
**Date Generated:** April 21, 2026  
**Primary Technology:** Flutter (Dart) + Python + Machine Learning  
**Purpose:** Smart agricultural irrigation management with AI-powered predictions and anomaly detection

---

## 1. PROJECT PURPOSE & KEY FEATURES

### Core Mission
Innovega is an **Agricultural Intelligence IoT Platform** designed to optimize irrigation management through:
- Real-time sensor data collection from LoRa-based gateways
- AI-powered water demand forecasting
- Automated irrigation scheduling
- Crop health monitoring and anomaly detection
- Farmer guidance via chatbot assistance

### Key Features
- **Professional Login System** - Email/password + social login (Google, Microsoft, Apple)
- **Gateway Management** - Multi-gateway support with device selection
- **Dashboard** - Real-time field monitoring with data visualization
- **AI Mode** - Advanced analytics and recommendations
- **Weather Integration** - Real-time weather and precipitation data
- **Map Interface** - Interactive Google Maps with geolocation
- **Schedule Management** - Create, manage, and automate irrigation schedules
- **Notifications** - Real-time alerts for anomalies and events
- **Water Consumption Tracking** - Historical analysis and optimization
- **Settings & Preferences** - User customization (language: EN/AR, dark mode, etc.)
- **Responsive Design** - Supports Android, iOS, Windows, Linux, macOS, and Web

---

## 2. FLUTTER APP STRUCTURE

### Directory Layout
```
innovega_app/
├── lib/
│   ├── main.dart                          # Application entry point with routing
│   ├── config/
│   │   └── design_system.dart            # Material Design 3 color scheme
│   ├── models/                            # Data models (16 files)
│   │   ├── login_model.dart              # Authentication & user data
│   │   ├── gateway_model.dart            # IoT gateway configuration
│   │   ├── dashboard_model.dart          # Dashboard data structures
│   │   ├── schedule_model.dart           # Irrigation schedule data
│   │   ├── water_model.dart              # Water consumption data
│   │   ├── weather_model.dart            # Weather data structures
│   │   ├── notification_model.dart       # Notification system
│   │   ├── device_location_model.dart    # GPS/location tracking
│   │   ├── preferences_model.dart        # User preferences
│   │   └── ai_models.dart                # AI recommendations
│   ├── services/                          # Business logic & API integration (16 files)
│   │   ├── auth_service.dart             # Authentication & authorization
│   │   ├── gateway_service.dart          # Gateway communication
│   │   ├── dashboard_service.dart        # Dashboard data aggregation
│   │   ├── schedule_service.dart         # Schedule CRUD operations
│   │   ├── weather_service.dart          # Weather API integration
│   │   ├── water_consumption_service.dart # Water data management
│   │   ├── ai_service.dart               # AI model integration
│   │   ├── notification_service.dart     # Notification management
│   │   ├── socket_service.dart           # Real-time WebSocket (Socket.IO)
│   │   ├── alert_listener_service.dart   # Event listener for alerts
│   │   ├── chatbot_service.dart          # AI chatbot integration
│   │   ├── location_service.dart         # GPS/geolocation
│   │   ├── map_service.dart              # Google Maps integration
│   │   ├── storage_service.dart          # Local data persistence
│   │   ├── preferences_service.dart      # User preferences handling
│   │   └── polling_notification_service.dart # Background notifications
│   ├── screens/                           # UI Pages (21 files)
│   │   ├── startup_screen.dart           # App initialization
│   │   ├── login_screen.dart             # User authentication
│   │   ├── gateway_selection_screen.dart # Device selection
│   │   ├── dashboard_screen.dart         # Main dashboard
│   │   ├── dashboard_screen_designed.dart # Alternative design
│   │   ├── ai_mode_screen.dart           # Advanced analytics
│   │   ├── weather_screen.dart           # Weather dashboard
│   │   ├── map_screen.dart               # Interactive map view
│   │   ├── map_screen_designed.dart      # Alternative map design
│   │   ├── water_consumption_screen.dart # Water usage analytics
│   │   ├── schedule_config_screen.dart   # Schedule management
│   │   ├── notification_center_screen.dart # Notifications hub
│   │   ├── notification_history_page.dart # Notification history
│   │   ├── settings_screen.dart          # User settings
│   │   ├── settings_page.dart            # Settings page variant
│   │   ├── edit_profile_screen.dart      # Profile management
│   │   ├── ai_section_config_screen.dart # AI configuration
│   │   ├── app_shell.dart                # App navigation shell
│   │   ├── root_shell.dart               # Root navigation
│   │   ├── socket_diagnostics_screen.dart # WebSocket debugging
│   │   └── google_maps_screen.dart       # Maps integration
│   ├── widgets/                           # Reusable UI components (8 files)
│   │   ├── precision_widgets.dart        # Custom design system widgets
│   │   ├── alert_widgets.dart            # Alert/notification widgets
│   │   ├── notification_widgets.dart     # Notification components
│   │   ├── chat_message_widget.dart      # Chatbot UI
│   │   ├── app_drawer.dart               # Navigation drawer
│   │   ├── socket_initializer.dart       # Socket initialization
│   │   ├── map_device_values_form.dart   # Form for device/map data
│   │   └── pump_valve_details_form.dart  # Device control form
│   └── utils/
│       └── irrigation_validation.dart    # Validation utilities
├── assets/
│   ├── images/                            # UI graphics & backgrounds
│   ├── logos/                             # Innovega brand logos
│   ├── icons/                             # Custom application icons
│   └── img/                               # Additional images
├── test/
│   └── widget_test.dart                  # Flutter widget tests
├── android/                               # Android native code & configuration
├── ios/                                   # iOS native code & configuration
├── windows/                               # Windows desktop support
├── linux/                                 # Linux desktop support
├── macos/                                 # macOS desktop support
├── web/                                   # Web platform support
├── pubspec.yaml                           # Dependencies & configuration
└── README.md                              # Project documentation
```

### pubspec.yaml Dependencies

**Core Framework:**
- `flutter` - UI framework
- `flutter_localizations` - Internationalization (EN, AR)
- `cupertino_icons` - iOS-style icons
- `google_fonts` - Custom typography

**State Management & Data:**
- `provider: ^6.0.0` - State management
- `http: ^1.1.0` - HTTP client for API calls
- `shared_preferences: ^2.2.2` - Local data storage
- `socket_io_client: ^2.0.3` - Real-time WebSocket communication

**UI & Visualization:**
- `flutter_map: ^8.2.2` - Interactive mapping
- `google_maps_flutter: ^2.5.0` - Google Maps integration
- `fl_chart: ^0.68.0` - Data visualization charts
- `convex_bottom_bar: ^3.1.0` - Custom navigation bar
- `font_awesome_flutter: ^10.6.0` - Icon library
- `webview_flutter: ^4.13.1` - Web content embedding

**Location & Geolocation:**
- `geolocator: ^9.0.2` - GPS/geolocation services
- `latlong2: ^0.9.1` - Location coordinate handling

**Utilities:**
- `intl: 0.20.2` - Date/time formatting

---

## 3. AI/ML MODELS DIRECTORY

**Location:** `Model_AI/`

### Available AI/ML Components

#### 3.1 Anomaly Detection Module
**File:** `Model_AI/anomaly_detection/anomaly_detector.dart`

**Purpose:** Detects leaks and abnormal flow patterns in water consumption

**Algorithms:**
- Z-score statistical analysis (threshold: 2.5-3.0 sigma)
- Isolation Forest-like pattern recognition
- Flow meter data analysis

**Key Methods:**
- `detectFlowAnomalies(List<double> flowReadings)` - Identifies outlier readings
- `_calculateSeverity(double zscore)` - Anomaly severity classification
- `_classifyAnomaly(double value, double mean)` - Anomaly type classification

**Output:** `FlowAnomaly` objects with:
- Detection index, value, expected value
- Z-score, severity level
- Timestamp, anomaly type (leak, surge, blockage, etc.)

---

#### 3.2 Chatbot Service
**File:** `Model_AI/chatbot/chatbot_service.dart`

**Purpose:** AI-powered farmer assistance via conversational AI

**Integrations:**
- OpenAI GPT-4o (cloud-based)
- Ollama (local LLM alternative)
- Conversation history management

**Capabilities:**
- Context-aware farming advice
- Irrigation recommendations
- Crop health guidance
- System prompt customization per farmer profile

**Key Methods:**
- `init(apiKey, baseUrl, useLocalLLM)` - Initialize with API config
- `sendMessage(userMessage, farmerContext)` - Chat inference
- `_buildSystemPrompt(farmerContext)` - Dynamic context building
- `_callOpenAI()` / `_callOllama()` - Backend selection

**Features:**
- Persistent conversation history
- Farmer-specific context injection (crop type, location, soil, etc.)
- Multi-turn dialogue support

---

#### 3.3 Crop Health Calculator
**File:** `Model_AI/crop_health_score/crop_health_calculator.dart`

**Purpose:** Computes comprehensive 0-100 crop health scores per field section

**Health Scoring Factors:**
1. **Water Balance (35% weight)**
   - AI-recommended water vs. actual usage
   - Deviation analysis

2. **Soil Moisture (25% weight)**
   - Optimal moisture range assessment
   - Real-time vs. ideal levels

3. **Schedule Adherence (20% weight)**
   - Missed irrigation count
   - Timeliness compliance

4. **Weather Stress (15% weight)**
   - Temperature index (0-100)
   - Rainfall probability

5. **Trend Analysis (5% weight)**
   - Historical soil moisture (7-day)
   - Trajectory assessment

**Key Methods:**
- `calculateSectionHealth(...)` - Main scoring algorithm
- `_calculateWaterScore()` - Water balance component
- `_calculateMoistureScore()` - Soil moisture scoring
- `_calculateScheduleScore()` - Schedule compliance
- `_calculateWeatherScore()` - Weather impact
- `_calculateTrendScore()` - Trend analysis

**Output:** `CropHealthScore` object (0-100) with component breakdown

---

#### 3.4 Irrigation Forecaster
**File:** `Model_AI/forecasting/irrigation_forecaster.dart`

**Purpose:** Predicts water needs for next 7 days using advanced ML models

**Supported Models:**
- LSTM (Long Short-Term Memory)
- Prophet (Facebook's time-series forecasting)
- ARIMA (Statistical forecasting)

**Backend Integration:**
- RESTful API endpoint: `/api/ai/predict/weekly`
- Bearer token authentication
- 30-second timeout

**Input Parameters:**
- Gateway ID
- Section ID
- Crop type
- Historical data

**Key Methods:**
- `getWeeklyForecast(gatewayId, sectionId, cropType, accessToken)` - Main forecast
- Automatic model selection based on data characteristics
- Confidence interval calculation

**Output:** `WeeklyForecast` containing:
- Daily predictions (7 days)
- Confidence scores
- Recommendation thresholds

---

#### 3.5 Research Directory
**Path:** `Model_AI/research/`

Contains experimental models and prototyping code for future features

---

### AI/ML Architecture Notes
- **Singleton Pattern:** All AI services use singleton pattern for memory efficiency
- **Error Handling:** Graceful degradation with fallback values
- **Authentication:** Bearer token-based API calls
- **Async Operations:** All forecasting/predictions use async/await
- **Data Validation:** Input sanitization and bounds checking

---

## 4. TESTING FRAMEWORK (MAESTRO)

**Location:** `maestro/`

### Test Automation Platform
**Maestro** is a mobile app testing framework providing:
- Record & playback UI automation
- Cross-platform testing (Android, iOS)
- Parallel test execution
- Rich reporting with screenshots

### Test Suite Structure

| Test File | Purpose | Duration |
|-----------|---------|----------|
| `00_login_flow.yaml` | User authentication | ~30s |
| `01_navigation_flow.yaml` | Screen navigation | ~45s |
| `02_schedule_flow.yaml` | Irrigation scheduling | ~40s |
| `03_notifications_flow.yaml` | Alert system | ~35s |
| `04_settings_flow.yaml` | User preferences | ~30s |
| `05_error_handling_flow.yaml` | Form validation & errors | ~50s |
| `06_advanced_scenarios.yaml` | Offline mode, sync, performance | ~60s |

### Test Coverage Details

#### 00_login_flow.yaml
```yaml
Steps:
  1. Launch app
  2. Wait for animations
  3. Tap email field → Input: anisbelhadj.contact@gmail.com
  4. Tap password field → Input: anisbelhadj
  5. Tap "Sign In" button
  6. Verify dashboard displays
  7. Select gateway card to proceed
```

**Validates:**
- Email field focus & input
- Password field focus & input
- Button activation
- Authentication response
- Navigation to next screen

#### 01_navigation_flow.yaml
**Screens Tested:**
- Dashboard → Settings → Notifications (bidirectional)
- Back button functionality
- Screen transitions smoothness

#### 02_schedule_flow.yaml
**Features Tested:**
- Create new schedule
- Form field validation
- Save functionality
- Schedule persistence

#### 03_notifications_flow.yaml
**Features Tested:**
- Notification center navigation
- Alert display
- Notification history
- Mark as read/dismiss

#### 04_settings_flow.yaml
**Features Tested:**
- Language switching (EN ↔ AR)
- Dark/Light theme toggle
- Preference persistence
- Profile editing

#### 05_error_handling_flow.yaml
**Error Cases:**
- Empty email submission
- Invalid email format
- Missing password
- Schedule without name/time/frequency
- Network timeout scenarios
- Invalid credentials

#### 06_advanced_scenarios.yaml
**Advanced Tests:**
- Offline mode functionality
- Data synchronization
- Performance under load
- Memory leak detection
- Battery consumption profile

### Maestro Configuration
**File:** `maestro.config.yaml`

```yaml
appId: com.innovega.innovega_app
timeout: 30000ms (30 seconds)
retries: 2
reporting:
  format: junit
  outputDir: test-results/
  screenshotOnFailure: true
  recordScreen: true
environment:
  DEVICE_TYPE: android
  API_URL: https://api.innovega.com
  TEST_EMAIL: test@innovega.com
  TEST_PASSWORD: TestPassword123
```

### Running Tests

```bash
# All tests
maestro test maestro/

# Specific test
maestro test maestro/00_login_flow.yaml

# With specific device
maestro test maestro/ --device <device-id>

# Debug mode
maestro test maestro/ --debug

# Interactive mode
maestro studio
```

### Test Scripts
- `run-tests.ps1` - PowerShell script for Windows
- `run-tests.sh` - Bash script for macOS/Linux
- GitHub Actions CI/CD configuration included

### Test Results
- Location: `maestro/test-results/`
- HTML reports with screenshots
- JSON output for CI/CD integration
- Timestamp-based result organization

---

## 5. ARCHITECTURE & TECHNOLOGY STACK

### Architectural Pattern: MVC + Provider State Management

```
UI Layer (Screens)
    ↓
State Management (Provider)
    ↓
Services Layer (Business Logic)
    ↓
Models Layer (Data Structures)
    ↓
External APIs & Local Storage
```

### Technology Stack

**Frontend:**
- **Framework:** Flutter 3.10.4+
- **Language:** Dart
- **State Management:** Provider 6.0.0
- **UI Design System:** Material Design 3 + Custom "Precision & Earth"

**Backend Integration:**
- **HTTP:** http 1.1.0
- **Real-time:** Socket.IO client 2.0.3
- **Authentication:** Bearer token JWT
- **API Protocol:** RESTful JSON

**Maps & Location:**
- **Maps:** Google Maps Flutter 2.5.0
- **Mapping Library:** Flutter Map 8.2.2
- **Location Services:** Geolocator 9.0.2

**Data Persistence:**
- **Local Storage:** SharedPreferences 2.2.2
- **Session Management:** In-memory caching

**Data Visualization:**
- **Charts:** fl_chart 0.68.0
- **Custom Graphics:** Canvas-based components

**Internationalization:**
- **Localization:** flutter_localizations
- **Supported Languages:** English (en), Arabic (ar)
- **Right-to-Left Support:** Full RTL layout support

**Hardware Integration:**
- **IoT Gateways:** LoRa-based communication
- **MQTT Support:** For gateway communication
- **Sensor Data:** Real-time polling & event-driven

### Design System: "Precision & Earth"

**Philosophy:** "The Digital Agronomist" - authoritative, fluid, natural

**Color Palette:**
- **Primary (Deep Crop):** #006036 → #1A7A4A (vegetation health)
- **Secondary (Harvest Amber):** #855300 (alerts & warnings)
- **Tertiary (Irrigation Teal):** #005D5A (water-related data)
- **Surface Hierarchy:** 10 tonal levels (surface → surface-container-highest)

**Typography:**
- **Display/Headlines:** Manrope (technical, modern)
- **Body/Labels:** Work Sans (high legibility)
- **Typography Scale:** LG Display (3.5rem) → MD Label (0.75rem)

**Design Principles:**
- **No-Line Rule:** Boundaries via color shifts, not borders
- **Glassmorphism:** 70% opacity + 12px blur for overlays
- **Tonal Depth:** Layering without drop shadows
- **Organic Editorialism:** Asymmetric, breathing room, high contrast

### Data Flow

```
Gateway (MQTT) → 
Backend API → 
Flutter App (Socket.IO real-time updates) →
Services (aggregation, transformation) →
State Management (Provider) →
UI Screens (rendered widgets)
```

### Backend Communication

**Authentication Endpoints:**
- POST `/auth/login` - User authentication
- GET `/auth/verify` - Token validation
- POST `/auth/refresh` - Token refresh

**Data Endpoints:**
- GET `/gateways` - List user gateways
- GET `/sections/{sectionId}/data` - Section data
- POST `/schedules` - Create irrigation schedule
- GET `/weather/{location}` - Weather data
- WS `/socket.io` - Real-time event stream

**AI Endpoints:**
- POST `/api/ai/predict/weekly` - Irrigation forecast
- POST `/api/ai/health/calculate` - Crop health score
- POST `/api/ai/anomalies/detect` - Anomaly detection
- POST `/api/chat` - Chatbot inference

### Security Architecture

- **Authentication:** JWT Bearer tokens
- **Storage:** Encrypted SharedPreferences
- **Communication:** HTTPS/TLS
- **Token Lifecycle:** Automatic refresh
- **Sensitive Data:** Never logged
- **Deep Links:** Validated before navigation

---

## 6. DIRECTORY STRUCTURE SUMMARY

```
PFE/
├── innovega/                                    # Main Flutter app
│   └── innovega_app/
│       ├── lib/                                 # Source code
│       ├── android/                             # Android native
│       ├── ios/                                 # iOS native
│       ├── windows/                             # Windows desktop
│       ├── linux/                               # Linux desktop
│       ├── macos/                               # macOS desktop
│       ├── web/                                 # Web platform
│       ├── test/                                # Unit tests
│       ├── build/                               # Build artifacts
│       ├── assets/                              # Images, logos, icons
│       ├── pubspec.yaml                         # Dependencies
│       └── README.md                            # App documentation
│
├── Model_AI/                                    # Machine Learning Models
│   ├── anomaly_detection/                       # Leak & pattern detection
│   ├── chatbot/                                 # AgroBot AI assistant
│   ├── crop_health_score/                       # Health scoring
│   ├── forecasting/                             # 7-day water prediction
│   └── research/                                # Experimental models
│
├── maestro/                                     # QA Automation Tests
│   ├── 00_login_flow.yaml
│   ├── 01_navigation_flow.yaml
│   ├── 02_schedule_flow.yaml
│   ├── 03_notifications_flow.yaml
│   ├── 04_settings_flow.yaml
│   ├── 05_error_handling_flow.yaml
│   ├── 06_advanced_scenarios.yaml
│   ├── maestro.config.yaml
│   ├── TEST_CASES.md
│   ├── test-results/                            # Test reports
│   ├── run-tests.ps1 / run-tests.sh             # Test scripts
│   └── README.md                                # Testing guide
│
├── stitch/                                      # Design Documentation
│   ├── agrotech_precision/
│   │   └── DESIGN.md                            # Design system spec
│   ├── carte_du_champ/
│   ├── contrôle_des_nœuds/
│   ├── données_capteurs/
│   ├── plannings_d_irrigation/
│   └── tableau_de_bord/
│
├── g.py                                         # Gateway simulation script
│   └── MQTT scenarios for testing IoT devices
│
└── PROJECT_OVERVIEW.md                          # This file
```

---

## 7. KEY FILES & THEIR PURPOSES

### Essential Configuration
- `pubspec.yaml` - Dependency management & Flutter config
- `analysis_options.yaml` - Dart linter configuration
- `main.dart` - App entry point & routing setup
- `design_system.dart` - Color & typography definitions

### Core Services
- `auth_service.dart` - User authentication & JWT handling
- `socket_service.dart` - Real-time WebSocket (Socket.IO)
- `gateway_service.dart` - IoT device communication
- `notification_service.dart` - Alert & notification management

### AI/ML Integration
- `ai_service.dart` - Unified AI model access
- `anomaly_detector.dart` - Leak detection algorithm
- `crop_health_calculator.dart` - Health scoring engine
- `irrigation_forecaster.dart` - 7-day prediction model
- `chatbot_service.dart` - AI assistant integration

### Critical Screens
- `login_screen.dart` - Authentication UI
- `dashboard_screen.dart` - Main operational view
- `ai_mode_screen.dart` - Advanced analytics
- `map_screen.dart` - Geolocation visualization
- `schedule_config_screen.dart` - Schedule management

### Testing
- `maestro.config.yaml` - Test configuration
- `*.yaml` files in maestro/ - Individual test cases
- `TEST_CASES.md` - Comprehensive test documentation

---

## 8. DEPLOYMENT & PLATFORM SUPPORT

### Target Platforms
- ✅ **Android** - Primary mobile platform
- ✅ **iOS** - Secondary mobile platform
- ✅ **Windows** - Desktop support
- ✅ **Linux** - Desktop support
- ✅ **macOS** - Desktop support
- ✅ **Web** - Browser-based access

### Build Artifacts
- **Android APK/AAB** - via `android/` directory
- **iOS IPA** - via `ios/` directory
- **Windows EXE** - via `windows/` directory
- **Web Bundle** - via `web/` directory

### Backend Requirements
- REST API with JWT authentication
- WebSocket (Socket.IO) for real-time updates
- MQTT gateway support
- AI model inference service
- Weather API integration

---

## 9. DEVELOPMENT WORKFLOW

### Setup & Initialization
1. Clone repository
2. Navigate to `innovega/innovega_app/`
3. Run `flutter pub get`
4. Configure backend API URL in environment
5. Run `flutter run` on target device

### Testing Workflow
1. Run unit tests: `flutter test`
2. Run Maestro tests: `maestro test maestro/`
3. Generate test reports from `test-results/`
4. Review HTML reports for detailed results

### Deployment Workflow
1. Update version in pubspec.yaml
2. Run tests and validate
3. Build platform-specific artifacts
4. Sign and release

---

## 10. PROJECT STATISTICS

| Metric | Count |
|--------|-------|
| Dart Source Files | ~60 |
| Services | 16 |
| Data Models | 9 |
| Screens | 21 |
| Reusable Widgets | 8 |
| AI/ML Modules | 4 |
| Test Cases | 6+ (maestro) |
| Supported Languages | 2 (EN, AR) |
| Platform Targets | 6 |
| Dependencies | 15+ |

---

## 11. QUICK START COMMANDS

```bash
# Navigate to app directory
cd innovega/innovega_app

# Install dependencies
flutter pub get

# Run on device
flutter run

# Run tests
flutter test

# Run Maestro tests
cd ../../maestro
maestro test maestro/

# Build for Android
flutter build apk

# Build for iOS
flutter build ios

# Build for Web
flutter build web
```

---

## 12. DETAILED SERVICE DOCUMENTATION

### 12.1 Authentication Service (auth_service.dart)

**Purpose:** Manages user authentication, JWT token handling, and session management

**Key Functions:**
```dart
Future<LoginResponse> login(String email, String password)
- Input: email (String), password (String)
- Output: LoginResponse with user data, JWT token, expiry time
- Error Handling: InvalidCredentials, NetworkError, ServerError

Future<bool> logout()
- Clears local token and user session
- Invalidates refresh token on backend

Future<bool> refreshToken()
- Exchanges expired token for new JWT
- Updates local storage automatically

Future<bool> validateToken()
- Verifies if stored token is still valid
- Returns: true if valid, false if expired

Future<UserProfile> getCurrentUser()
- Retrieves logged-in user profile from cache or backend

bool isLoggedIn()
- Returns: boolean indicating authentication state

Future<bool> socialLogin(String provider, String idToken)
- Supports: google, apple, microsoft
- Input: provider name and ID token from social auth SDK
```

**Token Storage:**
- Stored in encrypted SharedPreferences
- Key: `auth_token_${userId}`
- Auto-expiry handling with refresh mechanism
- Token format: Bearer JWT

**Error Codes:**
- `401` - Unauthorized (invalid credentials)
- `403` - Forbidden (token expired)
- `422` - Unprocessable Entity (validation error)
- `500` - Server error

---

### 12.2 Socket Service (socket_service.dart)

**Purpose:** Real-time bi-directional communication via Socket.IO WebSocket

**Configuration:**
```dart
// Initialization
socketService.init(
  serverUrl: 'https://api.innovega.com',
  authToken: jwtToken,
  reconnectDelay: 1000, // milliseconds
  maxReconnectAttempts: 5
);

// Connection states
ConnectionState.connecting
ConnectionState.connected
ConnectionState.disconnected
ConnectionState.error
```

**Real-time Events:**
```dart
// Listen for dashboard updates
socket.on('dashboard:update', (data) {
  // Real-time sensor readings
  // data: { sectionId, sensorType, value, timestamp }
});

// Listen for notifications
socket.on('notification:alert', (data) {
  // data: { alertType, severity, message, timestamp }
});

// Listen for gateway status
socket.on('gateway:status', (data) {
  // data: { gatewayId, status, signalStrength, lastSeen }
});

// Listen for anomaly detection
socket.on('anomaly:detected', (data) {
  // data: { type, severity, description, affectedSection }
});
```

**Emission Methods:**
```dart
// Send command to gateway
socket.emit('device:command', {
  'gatewayId': gatewayId,
  'deviceId': deviceId,
  'command': 'start_pump',
  'parameters': { 'duration': 30 } // minutes
});

// Send schedule update
socket.emit('schedule:update', scheduleData);

// Request manual sync
socket.emit('data:sync', { 'gatewayId': gatewayId });
```

**Error Handling:**
- Auto-reconnection with exponential backoff
- Offline queue for pending commands
- Connection status monitoring

---

### 12.3 Gateway Service (gateway_service.dart)

**Purpose:** Manages IoT gateway discovery, configuration, and communication

**Data Structure:**
```dart
class Gateway {
  String id;
  String name;
  String location;
  GatewayStatus status; // online, offline, error
  List<Section> sections; // field sections connected to gateway
  double latitude;
  double longitude;
  String firmwareVersion;
  DateTime lastSeen;
  int signalStrength; // 0-100 (RSSI)
  List<Device> devices; // pumps, valves, sensors
}

class Section {
  String id;
  String name;
  double area; // hectares
  String cropType;
  SoilType soilType;
  double latitude;
  double longitude;
}

class Device {
  String id;
  String type; // pump, valve, sensor, flowmeter
  String model;
  DeviceStatus status;
  DateTime lastReading;
  dynamic currentValue;
}
```

**Key Methods:**
```dart
Future<List<Gateway>> getUserGateways()
- Returns all gateways belonging to authenticated user

Future<GatewayDetails> getGatewayDetails(String gatewayId)
- Returns full gateway info including sections and devices

Future<bool> configureGateway(Gateway config)
- Updates gateway settings, section names, device mappings

Future<Map<String, dynamic>> getGatewayStats(String gatewayId)
- Returns: uptime %, data transmission rate, error count

Future<List<SensorReading>> getSectionReadings(
  String sectionId, 
  {DateTime? fromDate, DateTime? toDate}
)
- Returns: chronological sensor readings for date range
```

---

### 12.4 AI Service (ai_service.dart)

**Purpose:** Unified interface to all AI/ML models

**Integrated Models:**
```dart
// 1. Anomaly Detection
Future<FlowAnomaly?> detectAnomalies(String sectionId)

// 2. Crop Health Calculation
Future<CropHealthScore> calculateHealth(String sectionId)
- Returns: score (0-100), component breakdown, recommendations

// 3. Weekly Forecasting
Future<WeeklyForecast> getWeeklyForecast(String sectionId)
- Returns: daily water recommendations for 7 days

// 4. Chatbot Query
Future<String> askChatbot(String question, Map<String, dynamic> context)
- context: {cropType, fieldArea, soilType, currentMoisture, ...}
```

---

### 12.5 Notification Service (notification_service.dart)

**Purpose:** Manages notifications, alerts, and reminders

**Notification Types:**
```dart
enum NotificationType {
  ALERT,           // Critical: anomaly, system error
  REMINDER,        // Info: scheduled action due
  RECOMMENDATION,  // Suggestion: AI-generated recommendation
  SCHEDULE,        // Info: schedule execution
  WEATHER,         // Info: weather warning
  ACHIEVEMENT      // Positive: milestone reached
}

class Notification {
  String id;
  NotificationType type;
  String title;
  String message;
  int priority; // 1-5
  bool read;
  DateTime timestamp;
  String? actionUrl;
  Map<String, dynamic>? payload;
}
```

**Methods:**
```dart
Future<List<Notification>> getNotifications({int limit = 50})
- Retrieves recent notifications (paginated)

Future<bool> markAsRead(String notificationId)

Future<bool> deleteNotification(String notificationId)

Future<int> getUnreadCount()

// Subscribe to notification stream
Stream<Notification> onNotificationReceived()
```

---

### 12.6 Chatbot Service (chatbot_service.dart)

**Purpose:** AI-powered conversational assistant for farmers

**System Prompt:**
```
You are AgroBot, an expert agricultural advisor specializing in irrigation management.
You have deep knowledge about:
- Crop water requirements by type and growth stage
- Soil moisture management
- Weather impact on irrigation
- Irrigation system optimization

Context provided:
- Farmer's current crop(s)
- Field soil type and size
- Current weather and forecast
- Historical watering patterns
- Local growing region

Always provide practical, actionable advice specific to the farmer's situation.
```

**Sample Conversation:**
```
Farmer: "My tomato plants are showing yellow leaves"
Bot: "Yellow leaves in tomatoes typically indicate either overwatering causing root 
stress or nutrient deficiency. Based on your recent irrigation schedule showing 40mm 
last week and current soil moisture at 75%, I recommend reducing irrigation frequency 
to 3 times per week. The forecast shows rain coming in 2 days, so pause irrigation 
until after the rainfall. Also check your fertilizer regimen..."
```

---

## 13. DETAILED SCREEN DOCUMENTATION

### 13.1 Login Screen (login_screen.dart)

**Components:**
- Innovega logo and branding
- Email input field (email validation)
- Password input field (masked)
- "Remember me" checkbox
- "Forgot password?" link
- "Sign In" button (primary action)
- Social login buttons (Google, Apple, Microsoft)
- "Create Account" link

**Validation Rules:**
```
Email:
  - Not empty
  - Valid email format (RFC 5322)
  - Max 254 characters

Password:
  - Not empty
  - Min 8 characters
  - Show/hide toggle
```

**State Management:**
```dart
class LoginProvider extends ChangeNotifier {
  String? email;
  String? password;
  bool rememberMe = false;
  bool isLoading = false;
  String? errorMessage;
  
  Future<void> login() async {
    // Email & password validation
    // Call auth_service.login()
    // Handle JWT storage
    // Navigate to gateway selection or dashboard
  }
}
```

---

### 13.2 Dashboard Screen (dashboard_screen.dart)

**Layout Structure:**
```
┌─ Header ────────────────────────┐
│ Welcome, [Farmer Name]           │
│ [Gateway Selector Dropdown]      │
├─ Real-time Metrics ─────────────┤
│ ┌─ Card ┐ ┌─ Card ┐ ┌─ Card ┐ │
│ │Soil %│ │Temp C│ │Flow L/h│ │
│ │ 65%  │ │ 28°  │ │ 12.5   │ │
│ └──────┘ └──────┘ └────────┘ │
├─ Section Status ────────────────┤
│ [Section 1] - Health: 78/100    │
│ [Section 2] - Health: 65/100    │
│ [Section 3] - Health: 82/100    │
├─ Alerts ────────────────────────┤
│ ⚠️ High flow detected (Section 2)│
│ ℹ️ Irrigation due in 2 hours     │
├─ Quick Actions ─────────────────┤
│ [AI Analysis] [Weather] [Charts] │
└─────────────────────────────────┘
```

**Real-time Updates:**
- Refreshes every 5 seconds via Socket.IO
- Shows last update timestamp
- Manual refresh button available

**Data Structure:**
```dart
class DashboardData {
  String gatewayId;
  List<Section> sections;
  List<SensorReading> currentReadings;
  List<CropHealthScore> healthScores;
  List<Alert> activeAlerts;
  WeatherData weather;
  ScheduledAction? nextAction;
  DateTime lastUpdate;
}
```

---

### 13.3 AI Mode Screen (ai_mode_screen.dart)

**Features:**
```
1. Crop Health Dashboard
   - Gauge chart (0-100 score) per section
   - Component breakdown (water, soil, schedule, weather, trend)
   - Trend line (7-day historical)

2. 7-Day Forecast
   - Daily water recommendations
   - Confidence intervals
   - Weather correlation
   - Suggested actions

3. Anomaly Analysis
   - Recent anomalies chart
   - Severity distribution
   - Recommended actions

4. AI Recommendations
   - Top 3 actionable insights
   - Priority ranking
   - Implementation guidance
```

**Data Visualization:**
- Charts library: fl_chart
- Custom gauge widgets
- Line charts for trends
- Bar charts for comparisons

---

### 13.4 Schedule Management Screen (schedule_config_screen.dart)

**Schedule Form Fields:**
```dart
class IrrigationSchedule {
  String id;
  String name;
  List<String> selectedSections;
  DateTime startDate;
  DateTime endDate;
  List<TimeOfDay> wateringTimes; // e.g., [6:00 AM, 6:00 PM]
  Duration duration; // minutes per watering
  int frequency; // days between waterings
  double targetVolume; // liters
  RecurrencePattern pattern; // daily, weekly, monthly, custom
  bool enabled;
  bool aiOptimized; // use AI recommendations
}
```

**Validation:**
- At least one section selected
- End date >= Start date
- Watering time not in past
- Duration 1-180 minutes
- Frequency 1-30 days
- Target volume > 0

**Actions:**
- Create new schedule
- Edit existing schedule
- Delete schedule
- Duplicate schedule
- Test schedule (simulation)
- Enable/disable schedule

---

### 13.5 Weather Screen (weather_screen.dart)

**Data Display:**
```
Current Weather:
  Temperature: 28°C (feels like 31°C)
  Humidity: 65%
  Wind Speed: 12 km/h
  Cloud Cover: 40%
  UV Index: 7 (High)
  Dew Point: 18°C

7-Day Forecast:
  Day | High | Low | Precip | Wind | Condition
  Mon | 30°C | 20°C | 0mm   | 10   | Sunny
  Tue | 28°C | 19°C | 5mm   | 12   | Partly Cloudy
  Wed | 26°C | 18°C | 15mm  | 8    | Rainy
  ...

Irrigation Impact:
  - Evapotranspiration (ET) Rate: 4.2 mm/day
  - Recommended additional water: 2.1 L/m² today
  - Rain expected: 15mm on Wednesday (skip watering)
```

**API Integration:**
- Weather provider: OpenWeatherMap or similar
- 5-day forecast API
- Historical weather data (7 days)

---

### 13.6 Map Screen (map_screen.dart)

**Components:**
```
- Google Maps display
- Gateway markers (colored by status)
- Section boundaries (polygon overlays)
- Sensor location pins
- Zoom controls
- Location service integration
- Info windows on marker tap
```

**Marker Types:**
- 🟢 Online Gateway (green)
- 🔴 Offline Gateway (red)
- 🟡 Low Signal Gateway (yellow)
- 📍 Sensor locations (blue)

**Info Window Content:**
```
Gateway: Main Field
Status: Online
Signal: 85%
Sections: 4
Last Data: 2 minutes ago
[Tap to View Details]
```

---

## 14. API ENDPOINT REFERENCE

### 14.1 Authentication Endpoints

**POST /auth/login**
```json
Request:
{
  "email": "farmer@example.com",
  "password": "SecurePassword123"
}

Response (200):
{
  "success": true,
  "user": {
    "id": "user_12345",
    "name": "John Farmer",
    "email": "farmer@example.com",
    "role": "farmer",
    "avatar": "https://..."
  },
  "accessToken": "eyJhbGciOiJIUzI1NiIs...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIs...",
  "expiresIn": 3600
}

Error (401):
{
  "success": false,
  "error": "Invalid email or password"
}
```

**POST /auth/refresh**
```json
Request (Header):
Authorization: Bearer <refreshToken>

Response (200):
{
  "accessToken": "eyJhbGciOiJIUzI1NiIs...",
  "expiresIn": 3600
}
```

**POST /auth/logout**
```
Request (Header):
Authorization: Bearer <accessToken>

Response (200):
{ "success": true }
```

---

### 14.2 Gateway Endpoints

**GET /gateways**
```json
Response (200):
{
  "success": true,
  "gateways": [
    {
      "id": "gw_001",
      "name": "North Field Gateway",
      "status": "online",
      "location": { "lat": 35.1264, "lng": -106.6055 },
      "signalStrength": 85,
      "firmwareVersion": "2.1.4",
      "lastSeen": "2026-04-21T10:30:00Z",
      "sectionCount": 3,
      "deviceCount": 8
    }
  ]
}
```

**GET /gateways/{gatewayId}/data**
```json
Response (200):
{
  "success": true,
  "gateway": { ... },
  "sections": [ ... ],
  "devices": [ ... ],
  "readings": [
    {
      "sectionId": "sec_001",
      "timestamp": "2026-04-21T10:25:00Z",
      "sensors": {
        "soilMoisture": 65.3,
        "temperature": 28.5,
        "humidity": 62.1,
        "flowRate": 12.5
      }
    }
  ]
}
```

---

### 14.3 Schedule Endpoints

**POST /schedules**
```json
Request:
{
  "name": "Morning Irrigation",
  "gatewayId": "gw_001",
  "sectionIds": ["sec_001", "sec_002"],
  "startDate": "2026-04-21",
  "endDate": "2026-06-30",
  "wateringTimes": ["06:00", "18:00"],
  "duration": 30,
  "frequency": 2,
  "enabled": true
}

Response (201):
{
  "success": true,
  "schedule": {
    "id": "sch_12345",
    "createdAt": "2026-04-21T10:30:00Z",
    ...
  }
}
```

**GET /schedules/{scheduleId}**
```json
Response (200):
{
  "success": true,
  "schedule": { ... },
  "nextExecution": "2026-04-22T06:00:00Z",
  "executionHistory": [ ... ]
}
```

---

### 14.4 AI Endpoints

**POST /api/ai/health/calculate**
```json
Request:
{
  "sectionId": "sec_001",
  "includeBreakdown": true
}

Response (200):
{
  "success": true,
  "score": 78,
  "grade": "B+",
  "breakdown": {
    "waterBalance": 82,
    "soilMoisture": 75,
    "scheduleAdherence": 80,
    "weatherStress": 70,
    "trend": 78
  },
  "recommendations": [
    "Increase watering frequency by 10% for optimal growth",
    "Monitor for heat stress next week",
    "Current soil moisture is ideal for root development"
  ]
}
```

**POST /api/ai/predict/weekly**
```json
Request:
{
  "sectionId": "sec_001"
}

Response (200):
{
  "success": true,
  "forecast": [
    {
      "date": "2026-04-22",
      "recommendedWater": 15.5,
      "confidence": 0.92,
      "reason": "High temperature forecast, low rainfall expected"
    },
    {
      "date": "2026-04-23",
      "recommendedWater": 12.0,
      "confidence": 0.88,
      "reason": "Rain expected in afternoon"
    }
  ]
}
```

**POST /api/ai/chat**
```json
Request:
{
  "message": "My tomato plants look stressed",
  "context": {
    "cropType": "tomato",
    "fieldArea": 2.5,
    "soilType": "loamy",
    "currentMoisture": 65,
    "recentReadings": [ ... ]
  }
}

Response (200):
{
  "success": true,
  "response": "Based on your current soil moisture of 65% and recent weather patterns, your tomatoes appear to be experiencing water stress. I recommend increasing irrigation frequency to daily intervals for the next 5 days, then reassess based on weather conditions...",
  "confidence": 0.95
}
```

---

## 15. DATABASE & DATA MODELS

### 15.1 User Model
```dart
class User {
  String id;
  String name;
  String email;
  String? phone;
  UserRole role; // farmer, admin, technician
  String? avatar;
  String language; // en, ar
  bool darkMode;
  DateTime createdAt;
  DateTime? lastLogin;
  List<String> gatewayIds;
  Preferences preferences;
}

class Preferences {
  bool enableNotifications;
  bool enableEmailAlerts;
  List<String> alertTypes; // anomaly, schedule, weather
  String measurementUnit; // metric, imperial
  String temperatureUnit; // celsius, fahrenheit
}
```

### 15.2 Schedule Execution Log
```dart
class ScheduleExecution {
  String id;
  String scheduleId;
  DateTime executionTime;
  ScheduleStatus status; // success, failed, skipped
  Duration actualDuration;
  double volumeDispensed;
  String? errorMessage;
  Map<String, dynamic>? metadata;
}
```

### 15.3 Sensor Reading
```dart
class SensorReading {
  String id;
  String sectionId;
  DateTime timestamp;
  Map<String, double> values; // {soilMoisture, temperature, humidity, etc}
  double? batteryLevel;
  int signalStrength;
}
```

---

## 16. ENVIRONMENT VARIABLES

**Production (.env.production)**
```
API_URL=https://api.innovega.com
API_TIMEOUT=30000
SOCKET_IO_URL=https://api.innovega.com/socket.io
GOOGLE_MAPS_API_KEY=AIzaSyDxxx...
OPENAI_API_KEY=sk-xxx...
WEATHER_API_KEY=xxx...
ENV=production
LOG_LEVEL=error
ENABLE_DEBUG_MENU=false
```

**Development (.env.development)**
```
API_URL=http://localhost:3000
API_TIMEOUT=60000
SOCKET_IO_URL=http://localhost:3000/socket.io
GOOGLE_MAPS_API_KEY=AIzaSyDxxx...
OPENAI_API_KEY=sk-xxx...
WEATHER_API_KEY=xxx...
ENV=development
LOG_LEVEL=debug
ENABLE_DEBUG_MENU=true
```

---

## 17. INSTALLATION & SETUP GUIDE

### 17.1 Prerequisites
- Flutter SDK 3.10.4 or later
- Dart 3.0+
- Android SDK (for Android development)
- Xcode (for iOS development)
- Git

### 17.2 Step-by-Step Setup

**1. Clone Repository**
```bash
git clone https://github.com/B3lhadj/PFE-Ino.git
cd PFE-Ino
```

**2. Navigate to App Directory**
```bash
cd innovega/innovega_app
```

**3. Get Flutter Dependencies**
```bash
flutter pub get
```

**4. Configure Environment**
```bash
# Copy example env file
cp .env.example .env

# Edit with your API keys
nano .env
```

**5. Generate Code (if needed)**
```bash
# Build Runner for code generation
flutter pub run build_runner build --delete-conflicting-outputs
```

**6. Run on Emulator/Device**
```bash
# List available devices
flutter devices

# Run on specific device
flutter run -d <device-id>
```

---

## 18. GATEWAY SIMULATION (g.py)

**Purpose:** Python script to simulate IoT gateway and MQTT communication for testing

**Features:**
- Generates realistic sensor readings
- Simulates gateway connection/disconnection
- Creates anomalies for testing detection
- Supports multiple gateway simulation

**Usage:**
```bash
python g.py --gateway-id gw_001 --section-count 3 --device-count 8
```

**Simulated Data:**
- Soil moisture: 20-90% (realistic curves)
- Temperature: 15-35°C (seasonal patterns)
- Humidity: 30-80%
- Flow rate: 5-25 L/h with anomalies

---

## 19. TROUBLESHOOTING GUIDE

### Issue: Socket.IO Connection Failed
**Solution:**
- Check backend server is running
- Verify SOCKET_IO_URL in environment
- Check firewall/network restrictions
- Review backend logs

### Issue: Maps Not Showing
**Solution:**
- Verify Google Maps API key is valid
- Check key restrictions (Android/iOS package)
- Enable Maps API in Google Cloud console

### Issue: Notifications Not Received
**Solution:**
- Check notification permissions granted
- Verify notification service is initialized
- Check battery optimization settings
- Review notification center history

### Issue: AI Predictions Returning Null
**Solution:**
- Ensure sufficient historical data (14+ days)
- Check AI backend is reachable
- Verify API credentials
- Check error logs

---

## 20. SECURITY BEST PRACTICES

### Authentication
- Use HTTPS for all API calls
- Store JWT tokens in secure enclave
- Implement token refresh before expiry
- Clear tokens on logout

### Data Protection
- Encrypt sensitive data at rest
- Use TLS 1.2+ for network communication
- Validate all user inputs
- Implement CORS properly

### API Security
- Rate limiting (100 requests/minute per user)
- Input validation on backend
- SQL injection prevention
- XSS protection

### Permissions
- Request location only when needed
- Minimize camera/microphone access
- Clear temporary files
- Implement proper RBAC

---

## 21. PERFORMANCE OPTIMIZATION

### Memory Management
- Use lazy loading for images
- Implement object pooling for frequently-used objects
- Clear caches on low memory
- Monitor for memory leaks

### Network Optimization
- Batch API requests when possible
- Use compression for large payloads
- Implement offline-first strategy
- Cache responses with TTL

### UI Performance
- Use const constructors
- Implement proper ListView builders
- Minimize rebuilds with Provider
- Profile with DevTools

### Data Synchronization
- Only sync changed data (delta sync)
- Batch sync operations
- Implement smart retry logic
- Show sync status to user

---

## 22. CODE EXAMPLES

### 22.1 Using AI Service

```dart
// Get crop health score
final aiService = AIService.instance;
try {
  final healthScore = await aiService.calculateHealth('sec_001');
  print('Health Score: ${healthScore.score}/100');
  print('Grade: ${healthScore.grade}');
  
  healthScore.recommendations.forEach((rec) {
    print('📌 $rec');
  });
} catch (e) {
  print('Error: $e');
}
```

### 22.2 Creating a Schedule

```dart
final schedule = IrrigationSchedule(
  id: 'sch_' + DateTime.now().millisecondsSinceEpoch.toString(),
  name: 'Morning Watering',
  selectedSections: ['sec_001', 'sec_002'],
  startDate: DateTime.now(),
  endDate: DateTime.now().add(Duration(days: 60)),
  wateringTimes: [
    TimeOfDay(hour: 6, minute: 0),
    TimeOfDay(hour: 18, minute: 0),
  ],
  duration: Duration(minutes: 30),
  frequency: 2, // every 2 days
  targetVolume: 100, // liters
  enabled: true,
  aiOptimized: true,
);

await scheduleService.createSchedule(schedule);
```

### 22.3 Real-time Socket Listening

```dart
final socketService = SocketService.instance;

socketService.on('dashboard:update', (data) {
  final reading = SensorReading.fromJson(data);
  dashboardProvider.updateReading(reading);
});

socketService.on('anomaly:detected', (data) {
  notificationService.showAlert(
    title: 'Anomaly Detected',
    message: data['description'],
    severity: AlertSeverity.high,
  );
});
```

---

## 23. DEVELOPMENT GUIDELINES

### Code Style
- Follow Dart style guide (dart.dev/guides/language/effective-dart)
- Use meaningful variable names
- Maximum line length: 80 characters
- Add documentation comments for public APIs

### Testing
- Write unit tests for services
- Write widget tests for UI components
- Maintain >80% code coverage
- Run tests before commit

### Git Workflow
- Create feature branches from `main`
- Commit messages: `feat: description` or `fix: description`
- Create pull request for review
- Delete branch after merge

### Documentation
- Update README for major changes
- Add inline comments for complex logic
- Maintain API documentation
- Document breaking changes

---

## 24. VERSION HISTORY

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-01-15 | Initial release |
| 1.1.0 | 2026-02-20 | Added chatbot integration |
| 1.2.0 | 2026-03-10 | Implemented anomaly detection |
| 1.3.0 | 2026-04-01 | Enhanced UI/UX |
| 1.4.0 | 2026-04-21 | Current (added forecasting) |

---

## 25. CONTACT & SUPPORT

**Development Team:** Innovega Development Team  
**License:** Proprietary (Innovega)  
**Status:** Active Development  
**Last Updated:** April 21, 2026

**Support Channels:**
- Email: support@innovega.com
- GitHub Issues: https://github.com/B3lhadj/PFE-Ino/issues

---

**End of Comprehensive Project Overview**
