# To-Do App with Observability

This project is a **simple To-Do application** implemented using **Flask** and equipped with observability tools like **Prometheus** and **Grafana** for monitoring and visualizing application metrics. The application is containerized using **Docker** and orchestrated via **Docker Compose**.

---

## ✨ Features

1. **To-Do App:** A simple Python Flask-based application for managing tasks.
2. **Prometheus:** Collects application metrics (e.g., request counts, latencies).
3. **Grafana:** Visualizes metrics collected by Prometheus.
4. **Metrics Endpoint:** Exposes Prometheus-compatible metrics at `/metrics`.

---

## 🛠 Prerequisites

Ensure you have the following installed on your system:

- **Docker Desktop** or **Docker Engine**
- **Docker Compose** (bundled with Docker Desktop)
- **Python 3.x** (if running locally without Docker)

---

## 🚀 Getting Started

### 1️⃣ Clone the Repository

```
git clone https://github.com/rushi2828/todo-app-observability.git
cd todo-app-observability
```

### 2️⃣ Build and Run the Application
Run the following command to build and start the application:
```
docker-compose up --build
```
This will start the following services:
- To-Do App: Accessible at http://localhost:5000
- Prometheus: Accessible at http://localhost:9091
- Grafana: Accessible at http://localhost:3000

### 📌 Application Endpoints
##### To-Do App
- GET http://localhost:5000/todos: Retrieves the list of to-do items.
- POST http://localhost:5000/todos: Adds a new to-do item.
Example payload:
```
{
  "todo": "My task"
}
```
##### Prometheus Metrics
- GET /metrics: Exposes application metrics in Prometheus format.

## 📈 Observability Setup
#### Prometheus
Prometheus is configured to scrape metrics from the To-Do app's **/metrics** endpoint. 
The configuration is specified in **observability/prometheus.yml.**

#### Grafana
1. Default Login:
- Username: admin
- Password: admin

2. Setting Up Dashboards:

- Navigate to http://localhost:3000.
- Add Prometheus as a data source (URL: http://prometheus:9090).
- Import or create dashboards to visualize metrics.

### 🛠 Commands Reference

#### Build and Start Services
```
docker-compose up --build
```
#### Stop Services
```
docker-compose down
```
#### Check Running Containers
```
docker-compose ps
```
#### View Logs
```
docker-compose logs app
```
#### Rebuild and Restart
```
docker-compose up --build
```

## 🔧 Troubleshooting

#### ImportError
```
ImportError: cannot import name 'url_quote' from 'werkzeug.urls' (/usr/local/lib/python3.9/site-packages/werkzeug/urls.py)
```
#### Solution:
1. Check version of Flask and Werkzeug are compatible
```
pip freeze | grep 'Flask\|Werkzeug'
```
#### Port Already in Use
```
Error: Ports are not available: exposing port TCP 0.0.0.0:9090 -> 0.0.0.0:0
```
#### Solution:
1. Check which process is using the port:
```
netstat -aon | findstr :9090  # Windows
lsof -i :9090                 # Linux/macOS
```
2. Stop the conflicting process or modify the port in **docker-compose.yml**

#### Internal Server Error on /todos
- Check application logs for details:
```
docker-compose logs app
```
- Common issues include database initialization or incorrect routes.
#### Grafana Login Issues
- Default credentials are admin/admin.
- If you've changed the password and forgotten it:
```
docker-compose down
docker-compose up --build
```

## 📂 File Structure
```
├── app/
│   ├── app.py               # Main Flask application
│   ├── requirements.txt     # Python dependencies
│   ├── Dockerfile           # Dockerfile for the app
├── observability/
│   ├── prometheus.yml       # Prometheus configuration
├── docker-compose.yml       # Docker Compose configuration
├── README.md                # Project documentation
```
