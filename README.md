# Infrastructure Monitoring Platform

Учебный DevOps/SRE-проект для мониторинга Linux-сервера и Docker-контейнеров с автоматизированным CI/CD.

## Что реализовано

* Мониторинг Linux-сервера
* Мониторинг Docker-контейнеров
* Сбор метрик через Prometheus
* Визуализация в Grafana
* Алерты через Prometheus + Alertmanager
* Автоматическая проверка проекта через GitHub Actions
* Автоматический deployment на VM через Self-hosted Runner
* Запуск всех сервисов через Docker Compose

## Стек

* **Linux / Ubuntu Server**
* **Docker**
* **Docker Compose**
* **Prometheus**
* **Node Exporter**
* **cAdvisor**
* **Grafana**
* **Alertmanager**
* **Git / GitHub**
* **GitHub Actions**

## Архитектура

```text
                    GitHub
                       │
                   git push
                       ▼
              ┌─────────────────┐
              │ GitHub Actions  │
              │                 │
              │      CI         │
              │    validate     │
              └────────┬────────┘
                       │
                    success
                       ▼
              ┌─────────────────┐
              │ Self-hosted     │
              │ Runner          │
              └────────┬────────┘
                       │
                    deploy
                       ▼
              ┌─────────────────┐
              │   Ubuntu VM     │
              │                 │
              │ Docker Compose  │
              ├─────────────────┤
              │ Prometheus      │
              │ Node Exporter   │
              │ cAdvisor        │
              │ Grafana         │
              │ Alertmanager    │
              └─────────────────┘
```

## Project Structure

```text
Monitoring/
├── .github/
│   └── workflows/
│       └── ci.yml
├── alerts/
│   └── alerts.yml
├── alertmanager/
│   └── alertmanager.yml
├── prometheus/
│   └── prometheus.yml
├── docker-compose.yml
└── README.md
```

## CI/CD

При `push` в `main`:

```text
git push
   ↓
CI validation
   ↓
Self-hosted Runner
   ↓
git pull
   ↓
docker compose up -d
```

CI проверяет конфигурацию Docker Compose и структуру проекта.

CD автоматически обновляет проект на VM.

## Запуск

```bash
git clone git@github.com:AITys/Monitoring.git
cd Monitoring
docker compose up -d
```

Проверить состояние:

```bash
docker compose ps
```

## Основные сервисы

| Service       | Port |
| ------------- | ---: |
| Prometheus    | 9090 |
| Grafana       | 3000 |
| cAdvisor      | 8080 |
| Node Exporter | 9100 |
| Alertmanager  | 9093 |

## Что изучил

В процессе проекта получил практический опыт работы с:

* Linux и systemd
* Docker и Docker Compose
* Prometheus и PromQL
* Grafana
* Git и SSH
* GitHub Actions
* Self-hosted Runner
* CI/CD
* мониторингом Docker-контейнеров

## Статус

**Основная инфраструктура и CI/CD работают.**

Проект используется как практическая площадка для дальнейшего изучения DevOps/SRE и автоматизации инфраструктуры.

