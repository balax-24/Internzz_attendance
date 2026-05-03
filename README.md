# Internzz: Smart Attend Pro

Smart Attend is a professional attendance and campus-operations platform built for colleges and universities. It combines a Flutter mobile app, a Next.js operator web portal, Supabase-backed role security, offline recovery, Face ID workflows, device binding, Bluetooth beacon presence checks, reports, notifications, and audit-ready administration.

Current mobile version: **4.1.2+40102**

---

## Key Features

### Presence Verification

- **Staff session broadcast:** Faculty can start class sessions and broadcast attendance availability through Bluetooth beacon flows.
- **Student scan flow:** Students mark attendance only through the approved session and class scope.
- **Manual attendance:** Staff/admin/owner can mark Present, Absent, or OD when policy allows.
- **Attendance history:** Students, parents, staff, admins, and owners get role-aware attendance views.
- **Correction workflow:** Students can request attendance corrections; staff/admin/owner can review and approve/reject them.

### Security and Anti-Proxy Protection

1. **Device Binding:** Student accounts are tied to the registered device identity to reduce buddy marking.
2. **Face ID / Face Registration:** Camera, ML Kit, and TFLite flows support face registration and verification.
3. **Biometric Gate:** `local_auth` is used for device-level biometric confirmation where required.
4. **Location and Permission Guardrails:** Bluetooth, location, camera, notification, and biometric permission flows use clearer education and recovery states.
5. **Audit Logs:** Sensitive actions are logged for owner/admin review.
6. **Secure Local State:** Sensitive identity/security paths use secure storage patterns instead of plain local fallback.

### Role-Based Mobile App

- **Student:** Attendance marking, history, analytics, leave/OD requests, correction requests, notifications, profile, virtual ID, and update checks.
- **Staff:** Session start/end, live monitoring, manual attendance, leave review, fines, reports, notifications, outbox, and class operations.
- **Admin:** College-level users, staff/student management, Face ID approval queue, suspicious activity, subjects, feature flags, reports, audit views, and settings.
- **Owner:** Global dashboard across colleges, institution onboarding, global audit visibility, operations, reports, notifications, feature flags, and policy surfaces.
- **Parent:** Linked-student overview, attendance visibility, notification inbox, and student status monitoring.

### Offline and Sync Engine

- Local SQLite outbox for pending attendance and operational actions.
- Offline attendance recovery when a staff session has not synced yet.
- Retry and reconciliation flows for pending marks.
- Clear outbox/status screens for staff and operator review.

### Smart Attend Operator OS

The repo also includes `admin-portal/`, a Next.js web portal for staff, admins, and owners.

- Role-gated dashboard routes.
- Owner global access with institution/class scope filters.
- Staff sessions, students, attendance logs, manual attendance, leaves, fines, notifications, reports, search, sync health, corrections, and campaigns.
- Admin-only Face ID approvals, suspicious activity, audit logs, staff management, subjects, and settings.
- Owner-only college onboarding and global institution visibility.
- Tailwind CSS, shadcn-style primitives, lucide-react icons, Supabase Auth, and system/light/dark themes.

### Modern UI/UX

- Premium Material 3 mobile UI.
- Smart Attend branding with updated app icons and logo assets.
- DM Sans body typography and Space Grotesk heading/metric helpers.
- Shared design system widgets: app shell, headers, metric cards, status pills, gradient buttons, action tiles, timeline tiles, empty states, skeleton loading, and permission explainer sheets.
- Light and dark mode support.
- Polished role-specific dashboards and operational screens.

---

## Tech Stack

### Mobile App

- **Framework:** Flutter / Dart
- **Backend:** Supabase Auth, PostgreSQL, Realtime, Storage, and Edge Functions
- **Push:** Firebase Cloud Messaging plus local notifications
- **Offline:** SQLite through `sqflite`
- **Security:** `flutter_secure_storage`, `local_auth`, `android_id`, `device_info_plus`, `crypto`
- **Presence:** Bluetooth beacon support through `dchs_flutter_beacon`
- **Face Flows:** Camera, Google ML Kit face detection, and TFLite
- **Reports:** Excel, PDF, CSV/export-oriented flows
- **UI:** Material 3, Google Fonts, Flutter Animate, SVG, Lottie, Font Awesome

### Web Operator Portal

- **Framework:** Next.js 16 App Router
- **UI:** Tailwind CSS, shadcn-style components, lucide-react
- **Theme:** `next-themes`
- **Backend:** Shared Supabase project and role model

### Backend

- Supabase migrations for attendance records, attempts, admin RLS, anti-proxy security, push tokens, fines, audit logs, corrections, delivery tracking, feature flags, operational events, subjects, colleges RLS, and notification/settings hardening.
- Supabase Edge Function: `send-push`

---

## Core Dependencies

- `supabase_flutter`: Supabase Auth, database, and realtime access
- `firebase_core` / `firebase_messaging`: Push notification transport
- `flutter_local_notifications`: Local notification display
- `sqflite`: Offline persistence and outbox recovery
- `flutter_secure_storage`: Secure local secrets/state
- `dchs_flutter_beacon`: Bluetooth beacon flows
- `android_id` / `device_info_plus`: Device identity support
- `local_auth`: Biometric verification
- `geolocator`: Location-aware checks
- `camera`, `google_mlkit_face_detection`, `tflite_flutter`: Face registration and verification
- `excel`, `pdf`, `share_plus`: Reports and exports
- `google_fonts`, `flutter_animate`, `flutter_svg`, `lottie`: Premium UI layer

---

## Project Structure

```text
.
|-- lib/
|   |-- core/          # Constants, theme, permissions, shared app config
|   |-- controllers/   # Stateful attendance and feature controllers
|   |-- env/           # Generated environment bindings
|   |-- models/        # Domain models and typed data objects
|   |-- screens/       # Role and feature screens
|   |   |-- analytics/
|   |   |-- attendance/
|   |   |-- auth/
|   |   |-- dashboard/
|   |   |-- leave/
|   |   |-- notifications/
|   |   |-- operations/
|   |   |-- outbox/
|   |   |-- parent/
|   |   |-- profile/
|   |   |-- reports/
|   |   |-- search/
|   |   |-- settings/
|   |   `-- student/
|   |-- services/      # Supabase, offline sync, security, push, reports, updates
|   `-- widgets/       # Reusable app widgets and shared UI system
|
|-- admin-portal/
|   `-- src/
|       |-- app/        # Next.js routes for Operator OS
|       |-- components/ # UI primitives, mode toggle, scope filter
|       |-- hooks/      # Web hooks
|       `-- lib/        # Access control, filters, Supabase clients
|
|-- supabase/
|   |-- migrations/     # Database schema, RLS, security, feature tables
|   `-- functions/      # Edge functions, including push delivery
|
|-- assets/             # Logos, icons, ML model, app assets
|-- docs/               # Reports, role matrix, PRD tracker, developer guide
`-- test/               # Focused Flutter regression tests
```

---

## Setup

### Mobile Requirements

- Flutter SDK
- Android Studio / Android SDK
- Xcode for iOS builds
- Supabase project
- Firebase project if push delivery is enabled

### Mobile Environment

Client environment bindings live in `lib/env/`.

Expected values:

- Supabase URL
- Supabase anon key
- College beacon UUID

Never place service-role keys or Firebase private keys inside the Flutter app.

### Run Mobile App

```bash
flutter pub get
flutter run
```

### Build Android APK

```bash
flutter build apk --release
```

Generated APK:

```text
build/app/outputs/flutter-apk/app-release.apk
```

For production signing, create `android/key.properties` and point it to your release keystore. Local test builds can still install using the fallback debug keystore configuration.

---

## Admin Portal Setup

```bash
cd admin-portal
npm install
```

Create `admin-portal/.env.local`:

```bash
NEXT_PUBLIC_SUPABASE_URL=your-supabase-project-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-supabase-anon-key
```

Run locally:

```bash
npm run dev
```

Build:

```bash
npm run build
```

---

## Backend Notes

Apply Supabase migrations from `supabase/migrations/` in order.

Push delivery requires:

- `FCM_PROJECT_ID`
- `FCM_SERVICE_ACCOUNT_JSON`
- deployed Supabase Edge Function: `send-push`

Privileged roles are intended to be preprovisioned. Student self-registration happens in the app; staff, admin, and owner accounts should be created/administered through trusted operator flows or manual SQL.

---

## Quality Commands

```bash
flutter analyze
flutter test
```

Admin portal:

```bash
cd admin-portal
npm run build
```

---

## APK Download

Download the latest published APK from GitHub releases:

[Download the Latest APK](https://github.com/balax-24/Internzz_attendance/releases/latest)

---

## Author

<div align="center">

Made with love by [Balaharish](https://balaharish.netlify.app)  
GitHub: [Balax-24](https://github.com/balax-24)

</div>
