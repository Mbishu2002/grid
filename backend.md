# 📦 PLAS Backend Documentation – Power Line Analytics Software

## Overview
The PLAS (Power Line Analytics Software) backend provides a modular, scalable, and real-time platform for monitoring and analyzing power grid infrastructure. This document outlines the architecture, key modules, technologies, API endpoints, and simulation capabilities.

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

## 🌐 API Endpoints Summary

### 1. **Authentication & User Management**
- `POST /auth/login` – Authenticate user and return JWT token
- `POST /auth/logout` – Invalidate current session
- `GET /auth/me` – Get current user info
- `POST /auth/2fa/setup` – Enable two-factor authentication
- `GET /users/roles` – Get roles and permissions

### 2. **Asset Management**
- `GET /assets` – List all assets
- `POST /assets` – Create a new asset
- `PUT /assets/{id}` – Update asset data
- `DELETE /assets/{id}` – Remove asset
- `GET /assets/{id}/maintenance` – Maintenance logs for asset

### 3. **Network Data**
- `GET /network/topology` – Get power grid structure
- `GET /network/region/{id}` – Get region-specific network data

### 4. **Fault Detection**
- `POST /faults/report` – Report a new fault
- `GET /faults/active` – Get active faults
- `PUT /faults/{id}/resolve` – Mark fault as resolved
- `GET /faults/history` – Fetch historical fault data

### 5. **Analytics**
- `GET /analytics/load` – Load analysis
- `GET /analytics/transformer-health` – Transformer performance
- `GET /analytics/phase-imbalance` – Phase imbalance detection
- `GET /analytics/forecast` – Demand forecasting

### 6. **Alerts & Notifications**
- `GET /alerts` – Get real-time alerts
- `POST /alerts/acknowledge` – Acknowledge alert
- `PUT /alerts/preferences` – Update notification preferences

### 7. **Settings**
- `GET /settings/user` – Get user settings
- `PUT /settings/system` – Update system-wide configuration

### 8. **Reports & Exports**
- `POST /reports/generate` – Generate report (custom)
- `GET /reports/export` – Export data
- `GET /reports/charts` – Export visuals as PNG/SVG

### 9. **Monitoring**
- `GET /monitor/system` – System status
- `GET /monitor/asset/{id}` – Monitor specific asset
- `GET /monitor/region` – Regional grid load overview

### 10. **Field Technician Tools**
- `POST /technicians/assign-task` – Assign task
- `POST /technicians/report` – Submit field report
- `GET /technicians/nearby-assets` – Get GPS-based asset list

### 11. **Simulation Engine**
- `POST /simulation/run` – Trigger power flow simulation
- `GET /simulation/results/{id}` – Retrieve past results
- `GET /simulation/status/{id}` – Get status of a running sim

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
- Integration with SCADA/AMI systems
- Predictive analytics using AI/ML for maintenance
- Mobile offline mode for technicians
- Multi-tenant support for utility companies
- Blockchain for verifiable fault logging
- Real-time video feed integration for substations
- GIS-powered planning and routing for asset upgrades
- Natural language search over logs and reports

---

**Last Updated:** April 2025

