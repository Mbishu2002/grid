# 📦 PLAS Backend Documentation – Power Line Analytics Software

## Overview
The PLAS (Power Line Analytics Software) backend provides a modular, scalable, and real-time platform for monitoring and analyzing power grid infrastructure. This document outlines the architecture, key modules, technologies, and API endpoints necessary for managing and simulating grid operations.

---

## 🛠️ Tech Stack
- **Language**: Python 3.11+
- **Framework**: FastAPI (REST + WebSockets)
- **Database**: PostgreSQL (with PostGIS for spatial data)
- **Real-Time**: WebSockets via Starlette / Redis PubSub
- **Task Queue**: Celery + Redis
- **Authentication**: JWT + OAuth2
- **Simulation Engine**: PyPower + GridCal (combined)
- **Monitoring**: Prometheus + Grafana
- **Testing**: Pytest + HTTPX

---

## 🧱 Architecture
- **Monorepo** (using Poetry)
- **Domain-driven structure** (auth, assets, analytics, etc.)
- **Async-first** (all endpoints are async)
- **OpenAPI docs** available at `/docs`
- **Dockerized** services

---

## 🔧 Key Modules

### 1. **Authentication & Authorization**
- Handles user login, JWT token issuance, 2FA
- Role-based permissions (Admin, Technician, Analyst)

### 2. **Asset Management**
- CRUD for substations, transformers, lines
- Maintenance logs
- Performance metrics from IoT sensors

### 3. **Grid Topology**
- Manages nodes, lines, transformers
- Built-in GIS mapping support (PostGIS)

### 4. **Fault Management**
- Logging and assigning faults
- Tracking theft alerts
- Real-time resolution updates

### 5. **Analytics Engine**
- Load forecasting (via ML models)
- Energy loss detection
- Transformer health score

### 6. **Alerts & Notification System**
- Critical grid event alerts (via WebSockets and email)
- Configurable thresholds and notification rules

### 7. **Monitoring Dashboard API**
- Real-time grid status
- Asset condition monitoring
- Regional load heatmap data

### 8. **Simulation Engine**
- Hybrid engine using **PyPower** for power flow
- **GridCal** for control analysis
- Input: Network state, demand profile, weather
- Output: Fault prediction, load stability
- API-first simulation execution

### 9. **Technician Support API**
- Task assignment
- Field logs
- GPS-based nearby asset listing

### 10. **Reporting & Exports**
- Daily/weekly export of fault and performance
- Data export in CSV/JSON
- Visuals export (PNG, SVG, PDF)

---

## 🌐 API Summary
Follows RESTful conventions:
- `GET` for retrieval
- `POST` for creation
- `PUT` for updates
- `DELETE` for removal
- `WebSocket` endpoints for real-time monitoring

See separate [API Endpoints Document] for full route list.

---

## 🧪 Simulation Workflow
1. Admin/Analyst configures simulation inputs:
    - Load forecast, node parameters, weather data
2. API `/simulation/run` is triggered
3. Backend queues task using Celery
4. PyPower + GridCal are used to simulate
5. Results (JSON + visual) stored and published via WebSocket

---

## 🔐 Security
- Role-based access control
- Token expiration with refresh tokens
- Input validation via Pydantic
- Rate limiting and audit logs

---

## 📦 Deployment
- Docker Compose for local dev
- K8s manifests for cloud deployment
- CI/CD via GitHub Actions
- Logging with ELK stack (Elasticsearch, Logstash, Kibana)

---

## 📚 Future Enhancements
- Integration with SCADA/AMI
- AI model for predictive fault analytics
- Offline mode for mobile technician app
- Blockchain-based fault attestation

---

**Last Updated:** April 2025

