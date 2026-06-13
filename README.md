# INNOVEGA Mobile Application

INNOVEGA is a Flutter mobile application for smart agriculture. It connects a farmer or administrator to an IoT irrigation platform, displays real-time gateway/device data, supports manual and scheduled irrigation, provides AI recommendations, detects plant disease from images, and centralizes alerts, weather, maps, preferences, and activity history.

## Technical Goal

The mobile application is the user-facing layer of a larger INNOVEGA system:

- Flutter app: mobile interface, local preferences, navigation, charts, maps, notifications, and AI screens.
- NestJS backend: authentication, users, gateways, sensors, schedules, notifications, and MQTT/socket coordination.
- IoT gateway: sends real-time packets for pumps, valves, sensors, and node status.
- AI services: irrigation recommendation, water consumption prediction, AgroBot assistant, and disease detection.

## Application Architecture

The Flutter code follows a simple layered architecture:

```text
lib/
  main.dart                  App bootstrap, providers, themes, and routes
  config/                    Environment, translations, design system
  models/                    Data structures parsed from APIs/local storage
  screens/                   Full pages shown to the user
  services/                  API, socket, AI, storage, and business logic
  widgets/                   Reusable UI components and dialogs
  utils/                     Pure helpers and validation logic
```

The main dependency direction is:

```text
Screens -> Services -> Backend / local storage / sockets
Screens -> Models
Screens -> Widgets
Services -> Models + Config
```

This keeps UI code separate from API and business logic, which makes the project easier to explain during the technical defense.

## Runtime Flow

1. `main.dart` initializes Flutter bindings, notification channels, local storage, and preferences.
2. `MyApp` creates the global `MaterialApp`, applies the selected theme/language, and registers app routes.
3. `StartupScreen` decides whether the user should see onboarding, PIN setup, login, or the main app.
4. `LoginScreen` authenticates the user through `AuthService`.
5. `GatewaySelectionScreen` lets the user choose a gateway.
6. `RootShell` loads the persistent bottom navigation, drawer, socket initializer, and main feature screens.
7. Feature screens call services to load/update data and display the result.

## Important Files

| File | Role |
| --- | --- |
| `lib/main.dart` | Starts the app, initializes global services, defines routes, themes, and localization. |
| `lib/screens/startup_screen.dart` | Chooses the first screen according to saved user/session/PIN state. |
| `lib/screens/login_screen.dart` | User authentication screen. |
| `lib/screens/gateway_selection_screen.dart` | Lists available gateways after login. |
| `lib/screens/root_shell.dart` | Main navigation container with bottom bar, drawer, sockets, and feature pages. |
| `lib/screens/dashboard_screen.dart` | Real-time irrigation dashboard for pumps, valves, sensors, and gateway state. |
| `lib/screens/schedule_config_screen.dart` | Irrigation planning and schedule configuration. |
| `lib/screens/ai_mode_screen.dart` | AI irrigation and smart recommendation entry point. |
| `lib/screens/ai_section_config_screen.dart` | Detailed crop/section configuration used by AI recommendations. |
| `lib/screens/disease_detection_screen.dart` | Plant disease image detection workflow. |
| `lib/screens/agrobot_screen.dart` | Chat UI for the AgroBot agricultural assistant. |
| `lib/screens/map_screen.dart` | OpenStreetMap-based device map with node control. |
| `lib/screens/google_maps_screen.dart` | Google Maps alternative device map. |
| `lib/screens/weather_screen.dart` | Weather forecast UI used by irrigation decisions. |
| `lib/screens/water_consumption_screen.dart` | Water consumption analytics and PDF report export. |
| `lib/screens/settings_page.dart` | User preferences, profile, security PIN, language, theme, and feedback. |
| `lib/screens/admin_screen.dart` | Administration screen for users, gateways, sensors, and reference data. |
| `lib/services/auth_service.dart` | Login, logout, password reset, and profile API calls. |
| `lib/services/dashboard_service.dart` | Gateway configuration, node state, and node command API calls. |
| `lib/services/socket_service.dart` | Real-time socket.io connection and gateway packet streams. |
| `lib/widgets/socket_initializer.dart` | Connects sockets/notifications around the authenticated app shell. |
| `lib/services/notification_service.dart` | Local notification list, unread count, display logic, and alert logging. |
| `lib/services/ai_service.dart` | AI irrigation, anomaly, and disease API integration. |
| `lib/services/chatbot_service.dart` | AgroBot/Gemini/local fallback conversation orchestration. |
| `lib/services/smart_chatbot_service.dart` | Builds smart farm context for AgroBot answers. |
| `lib/services/water_consumption_service.dart` | Water usage data and prediction API logic. |
| `lib/services/preferences_service.dart` | Saves and exposes app language, theme, notifications, and UI preferences. |
| `lib/services/storage_service.dart` | Persists authenticated user/session/gateway data locally. |
| `lib/config/environment.dart` | Central API URLs and environment configuration. |
| `lib/config/design_system.dart` | Shared colors, typography, spacing, app bars, and visual components. |

## Main Modules

### Authentication and Security

The user authenticates with email and password. The app stores the user, token, and selected gateway locally. Sensitive actions are protected by a local security PIN.

Key files:

- `screens/login_screen.dart`
- `screens/reset_password_screen.dart`
- `screens/security_pin_setup_screen.dart`
- `services/auth_service.dart`
- `services/security_pin_service.dart`
- `services/storage_service.dart`

### Dashboard and Irrigation Control

The dashboard loads gateway configuration from the backend, listens to socket packets, displays node status, and sends open/close commands for valves and pumps.

Key files:

- `screens/dashboard_screen.dart`
- `services/dashboard_service.dart`
- `services/gateway_connectivity_service.dart`
- `services/socket_service.dart`
- `widgets/pump_valve_details_form.dart`

### Scheduling and AI Irrigation

The scheduling module lets the farmer configure automatic irrigation. The AI module generates recommendations from crop, section, soil, weather, and irrigation data.

Key files:

- `screens/schedule_config_screen.dart`
- `screens/ai_mode_screen.dart`
- `screens/ai_section_config_screen.dart`
- `services/schedule_service.dart`
- `services/ai_service.dart`
- `utils/irrigation_validation.dart`

### Maps

The app has two map implementations. The default map uses `flutter_map`; a Google Maps screen is also available. Both show device locations and support control actions.

Key files:

- `screens/map_screen.dart`
- `screens/google_maps_screen.dart`
- `services/map_service.dart`
- `services/location_service.dart`
- `widgets/map_device_values_form.dart`

### Notifications and Activity History

Socket and polling services receive notifications from the backend. The notification service stores them locally, tracks unread count, shows UI alerts, and writes important alerts to the farm activity log.

Key files:

- `services/notification_service.dart`
- `services/polling_notification_service.dart`
- `services/alert_listener_service.dart`
- `screens/notification_history_page.dart`
- `screens/farm_activity_log_screen.dart`
- `services/farm_activity_log_service.dart`

### AgroBot Assistant

AgroBot is the conversational assistant. It can call the Flask AgroBot API, direct Gemini fallback, or local fallback logic depending on configuration.

Key files:

- `screens/agrobot_screen.dart`
- `services/chatbot_service.dart`
- `services/agrobot_api_service.dart`
- `services/smart_chatbot_service.dart`
- `services/chat_context_builder.dart`

### Reports and Analytics

The app displays water consumption charts and can generate PDF reports.

Key files:

- `screens/water_consumption_screen.dart`
- `services/water_consumption_service.dart`
- `services/pdf_generation_service.dart`
- `models/report_model.dart`

## Data Models

The `models/` folder contains plain Dart classes used to parse backend data and pass structured data between screens and services.

Important examples:

- `login_model.dart`: authenticated user and roles.
- `gateway_model.dart`: selected gateway.
- `dashboard_model.dart`: sections, nodes, sensor values, pump/valve state.
- `schedule_model.dart`: irrigation schedules.
- `ai_models.dart`: AI request/response structures.
- `notification_model.dart`: alert and notification types.
- `water_model.dart`: consumption points and summaries.
- `weather_model.dart`: current weather and forecast data.

## How To Run

```bash
flutter pub get
flutter run
```

To analyze code quality:

```bash
flutter analyze
```

To format Dart files:

```bash
dart format lib test
```

## Soutenance Technique: Explanation Script

For a technical presentation, explain the project in this order:

1. INNOVEGA is a smart agriculture IoT platform.
2. The Flutter app is the mobile client used by farmers and administrators.
3. The app is organized by layers: screens, services, models, widgets, and config.
4. `main.dart` initializes services and routes.
5. `RootShell` is the authenticated application shell with navigation and sockets.
6. The dashboard communicates with the backend and receives real-time gateway packets through socket.io.
7. Services isolate API calls, so screens stay focused on UI and user actions.
8. AI modules add value through irrigation recommendations, disease detection, anomaly detection, and AgroBot assistance.
9. Security is handled by JWT authentication, local storage, and PIN protection.
10. The app supports preferences such as language, theme, notifications, and units.

## Cleanup Notes

During the cleanup pass, unused private Flutter UI helpers and stale local debug prints were removed from the touched files. No full screen or service file was deleted because the analyzer did not prove any whole Dart file was unused.
