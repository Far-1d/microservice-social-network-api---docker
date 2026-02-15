# Service Docker Startup

---

## 🛠️ Tech Stack

- **Framework**: FastAPI - Django
- **Database**: Sqlite3
- **Metric**: Prometheus
- **Logging**: Promtail - Loki
- **Monitoring DashBoard**: Grafana 
- **Authentication**: JWT
- **Testing**: Pytest - Django Test

---

## 🚦 services

### docker-compose.yml
+ post <small>**Fastapi**</small>
+ user <small>**Django**</small>
+ user_consumer <small>**Django**</small>
+ redis <small>**redis**</small>
+ kafka <small>**confluentinc/cp-kafka**</small>

### docker-compose.monitoring.yml
+ prometheus <small>**prom/prometheus**</small>
+ loki <small>**grafana/loki**</small>
+ promtail <small>**grafana/promtail**</small>
+ grafana <small>**grafana/grafana**</small>

---

## 🌐 Network
All services are under the same network to be able to access each other. 
Because two docker-compose files are used, and docker-compose.yml is started first, the network in monitoring file is tagged as *external*.


## 📁 File Structure

```
├── .env.docker                        # docker env file
├── docker-compose.yml                 # Main docker-compose file
├── docker-compose.monitoring.yml         # docker-compose file for monitoring
├── monitoring/                         # Monitoring stack
│   ├── datasources.yaml                # Grafana datasources
│   ├── loki-config.yaml                 # Loki logging config
│   ├── prometheus.yml                   # Prometheus config
│   └── promtail-config.yaml             # Promtail config
├── post/                                # Post service
│   ├── backend/                          # Post backend (FastAPI)
│   │   ├── .env                          # Environment variables
│   │   ├── Dockerfile                     # Backend Dockerfile
│   │   ├── requirements.txt                # Python dependencies
│   │   └── app/                            # Application code
│   │       ├── main.py                      # Entry point
│   │       ├── core/                         # Core functionality
│   │       ├── db/                            # Database models
│   │       ├── internal/                      # Internal logic
│   │       ├── models/                        # Pydantic models
│   │       ├── routers/                       # API routes
│   │       ├── schemas/                       # Data schemas
│   │       └── tests/                          # Tests
│   └── frontend/                           # Post frontend (empty)
└── user/                                 # User service
    ├── backend/                           # User backend (Django)
    │   ├── .env                             # Environment variables
    │   ├── Dockerfile                        # Backend Dockerfile
    │   ├── manage.py                          # Django manage.py
    │   ├── requirements.txt                   # Python dependencies
    │   ├── apps/                              # Django apps
    │   │   ├── base/                            # Base app
    │   │   ├── communications/                   # Communications app
    │   │   ├── profiles/                         # Profiles app
    │   │   ├── relationships/                    # Relationships app
    │   │   └── users/                            # Users app
    │   ├── logs/                               # Log files
    │   └── settings/                           # Django settings
    │       ├── asgi.py                           # ASGI config
    │       └── settings/                         # Settings modules
    │           ├── base.py                        # Base settings
    │           ├── dev.py                          # Development settings
    │           └── prod.py                         # Production settings
    └── frontend/                            # User frontend (empty)
```

> [!NOTE]
> ###### please note that most files are not shown in this structure and only main files required for docker and monitoring are displayed. 

> [!NOTE]
> ###### if you see the file naming is inconvenient feel free to rename them but be careful to also change their names in docker and config files


## ⚙️ Setup Steps

### 1. Install docker
install docker from [docker](https://www.docker.com/get-started)


### 2. Start Fastapi and Django
```
docker compose -f ./docker-compose.yml up
```
>[!NOTE]
> kafka takes around 30s to fully initialize and post service waits this time for kafka to run. so the total time can take up to a minute each time you restart the compose.

### 3. Start monitoring services
```bash
docker compose -f docker-compose.monitoring.yml up
```

### 4. Open Grafana
- URL: http://localhost:3000
- Login: admin / admin
- Prometheus and Loki are auto-connected

>[!TIP]
>grafana asks for changing the password after first login, but if you want to change the credentials before starting the container, edit these two lines in docker-compose.monitoring.yml file
```
- GF_SECURITY_ADMIN_USER=admin
- GF_SECURITY_ADMIN_PASSWORD=admin
```

## 🤩 What You Get


### Fastapi and Django services
Access them under
- http://localhost:8000 (django)  
- http://localhost:8001 (fastapi)


### Grafana
- URL: http://localhost:3000
- Login: admin / admin
- Prometheus and Loki are auto-connected

---

## Feedback

You are encouraged to test the API thoroughly and help improve it by reporting any bugs or issues you encounter.

Please send your feedback or bug reports via:

- **Email:** farid.zarie.000@gmail.com
- **Telegram:** [@el_fredoo](https://t.me/el_fredoo)

Your contributions and feedback are highly appreciated!


---

Thank you for using the Social Network project! 🙏
