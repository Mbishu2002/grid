---

## 📦 Field Technician Application Documentation (FTApp)

### 🔍 Overview
The **Field Technician App (FTApp)** is a mobile-first utility application built specifically for field technicians working on the electrical grid. It supports real-time task assignment, GPS-guided navigation to assets, fault reporting, and communication with the control center via the PLAS backend.

---

### 🎯 Objectives
- Enable fast and secure access to tasks
- Provide efficient reporting tools for grid faults and maintenance
- Ensure reliable field connectivity (with offline-first capabilities)
- Improve technician response time and data accuracy

---

### 📱 Core Features

#### 1. **Secure Authentication**
- Login using email/username and password
- Two-Factor Authentication (2FA) via OTP or Authenticator app
- Secure token storage via **SecureStore** (React Native)

#### 2. **Task Management**
- View assigned tasks with status (`Pending`, `In Progress`, `Completed`)
- Accept/Reject task assignments
- Mark task as completed with notes, photos, and location metadata
- Real-time task update via WebSocket connection

#### 3. **Fault Reporting**
- Report faults in real-time with:
  - Text description
  - Image upload (camera/gallery)
  - Voice notes (optional transcription)
  - Auto-tagging of GPS location
- Sync offline reports when connectivity is restored

#### 4. **Nearby Asset Discovery**
- Use device GPS to locate nearby assets (transformers, poles, substations)
- View asset details and maintenance history
- Tap to navigate via Google Maps or in-app Mapbox routing

#### 5. **Offline First Support**
- Queue fault reports and tasks while offline
- Sync with backend once reconnected
- View previously downloaded asset and task data without internet

#### 6. **Technician Dashboard**
- Daily stats: Tasks completed, pending, average response time
- Faults resolved vs. reported
- Safety alerts and company broadcasts

#### 7. **Push Notifications**
- Task assignment alerts
- System-wide alerts from the control center
- Nearby fault or hazard detection (planned)

---

### 🌐 Backend Integration (API Endpoints Used)

| Feature | Endpoint |
|--------|----------|
| Login | `POST /auth/login` |
| View assigned tasks | `GET /technicians/tasks` *(planned)* |
| Accept/Reject tasks | `PUT /technicians/task/{id}/status` *(planned)* |
| Submit fault report | `POST /faults/report` |
| Submit task report | `POST /technicians/report` |
| Nearby assets | `GET /technicians/nearby-assets` |
| Get asset details | `GET /assets/{id}` |
| Get real-time alerts | `GET /alerts` |
| Send location ping | `POST /technicians/location` *(planned)* |

---

### 🎨 UI/UX Design Language

- **Framework**: React Native
- **Design System**: Material Design 3 + Tailwind-like styles (via NativeWind)
- **Primary Color**: Electric Blue `#0F52BA`
- **Secondary**: Utility Orange `#FF6B00`
- **Themes**: Dark & Light mode
- **Maps**: Mapbox GL JS + location marker clustering

---

### 🧩 Architecture

- **Client**: React Native
- **State Management**: Zustand or Redux Toolkit
- **Offline Support**: MMKV for local storage + queue management
- **Sync Engine**: Background task + retry mechanism
- **Media Upload**: Multipart API (support for compression before upload)

---

### 🔐 Security

- All requests authenticated via JWT
- Secure keychain/token storage
- Field audit log created on every task/fault report
- Encrypted local storage

---

### 🚀 Future Enhancements

1. **AR Asset Tagging**
   - Overlay maintenance instructions and fault info in real-world view

2. **QR/Barcode Scanner**
   - Identify asset via scan for quick access

3. **Gamification**
   - Scoreboard for task performance, monthly rewards

4. **Chat with Dispatch**
   - Real-time messaging between technician and control center

5. **Drone Companion App**
   - Pair with drone for aerial inspections

6. **Wearable Support**
   - Notifications and task previews on smartwatches

7. **Voice-First Mode**
   - Full task and fault logging using only voice commands

---

### ⚙️ Deployment and Updates

- Distributed via Play Store / Enterprise MDM (Mobile Device Management)
- OTA (Over-the-Air) updates using Expo EAS Updates
- Crash/error tracking with Sentry
- Analytics for usage insights via Firebase or Segment

---

### 📘 Summary

| Feature | Status |
|--------|--------|
| Fault Reporting | ✅ |
| Task Management | ✅ |
| Asset Lookup | ✅ |
| GPS-based Asset Discovery | ✅ |
| Offline Support | ✅ |
| Technician Dashboard | ✅ |
| Push Notifications | 🔜 |
| QR Scan, AR Overlay | 🔜 |
| Drone & Wearable Integration | 🔜 |

---
