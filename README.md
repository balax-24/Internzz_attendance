# Internzz: Smart Attendance Pro 🎓

Internzz is a high-security, professional-grade attendance management system designed for colleges and universities. It replaces traditional manual entry with a cutting-edge **Mobile-to-Mobile Bluetooth Beacon** system, reinforced by triple-layer security.

---

## 🚀 Key Features

### 📡 Presence Verification (iBeacon)
- **Faculty:** Broadcasts a unique Bluetooth signal (iBeacon) derived from a custom hashing algorithm of Department and Section.
- **Student:** Scans for the specific signal. Presence is only marked if the student is physically within the teacher's range.

### 🔐 Triple-Layer Security (Anti-Proxy)
1. **Hardware Locking (Device Binding):** Accounts are permanently bound to the student's physical phone's unique hardware ID (`AndroidId` / `identifierForVendor`). Prevents "Buddy Marking."
2. **Biometric Authentication:** Requires a Fingerprint or Face ID scan before the attendance signal is finalized.
3. **Geo-fencing:** GPS coordinates are verified to ensure the student is within the campus radius (e.g., 500m).

### 📊 Comprehensive Faculty Hub
- **Dynamic Classes:** Staff can switch between various Departments, Sections, Years, and Periods on the fly.
- **Real-time Monitoring:** Live percentage indicator and student list that updates instantly as students scan.
- **Manual Overrides:** Faculty can manually mark students as **Present**, **Absent**, or **OD (On Duty)**.
- **Excel Export:** Generate and download attendance reports directly to the device's Downloads folder.

### 🌙 Modern UX/UI
- Trendy **Material 3** design with custom gradients and soft shadows.
- Full **Dark Mode** and Light Mode support.
- **Local Profile Picture:** Users can set a profile photo that is stored locally on the device for privacy.
- **Smooth Animations:** Integrated Lottie animations for successful marking.

---

## 🛠 Tech Stack

- **Framework:** Flutter (Agile Iterative Modular Architecture)
- **Backend:** Supabase (PostgreSQL, Real-time Streams, Secure Auth)
- **Database Logic:** Historical row-based session management (ready for future web integration).
- **Offline Engine:** Local SQLite storage with automatic synchronization when internet returns.

---

## 📦 Core Dependencies

- `supabase_flutter`: Backend & Realtime
- `dchs_flutter_beacon`: iBeacon Signal management
- `android_id` & `device_info_plus`: Hardware Security
- `local_auth`: Biometric verification
- `geolocator`: GPS Geofencing
- `excel`: Data reporting
- `lottie`: Trendy animations
- `shared_preferences`: Local caching & UI persistence

---

## 📂 Project Structure

```text
lib/
├── core/        # Global constants and utils (Beacon Hashing, Device Helpers)
├── services/    # Logic for Auth, Supabase, Offline storage, and Updates
├── models/      # Data structures (UserModel)
├── screens/     # UI broken down by feature (Auth, Profile, Dashboards)
└── widgets/     # Reusable UI components (Toasts, Dialogs)
```

## 🛠 Future Ready
The database is structured specifically to support a **Student/Admin Web Portal**. Every class session creates a unique historical record, allowing for day-wise and period-wise attendance summaries.

---

**Developed by Balaharish S**  
[GitHub](https://github.com/balax-24) | [Instagram](https://www.instagram.com/balax.24/)
