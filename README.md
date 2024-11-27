# Prometheus Grafana Monitoring

Prometheus Exporters and integrations: 
https://prometheus.io/docs/instrumenting/exporters/

Grafana Dashboards Library:
https://grafana.com/grafana/dashboards/


# Deploying the Monitoring and Visualization Stack with Docker Compose

This project sets up a monitoring and visualization stack using Docker Compose, including Prometheus, Grafana, and optional tools like Node Exporter and cAdvisor for enhanced monitoring.

## Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Services](#services)
  - [Prometheus](#prometheus)
  - [Grafana](#grafana)
  - [Optional Services](#optional-services)
    - [Node Exporter](#node-exporter)
    - [cAdvisor](#cadvisor)
- [Setup](#setup)
  - [Clone the Repository](#clone-the-repository)
  - [Configuration](#configuration)
  - [Run the Stack](#run-the-stack)
- [Accessing the Services](#accessing-the-services)
- [Stopping the Stack](#stopping-the-stack)

---

## Overview

This stack includes:
- **Prometheus**: A monitoring system and time-series database for metrics aggregation.
- **Grafana**: A visualization tool for monitoring dashboards.
- **Optional**:
  - **Node Exporter**: Collects system-level metrics.
  - **cAdvisor**: Provides resource usage and performance metrics for running containers.

The stack uses persistent volumes for data retention and runs with `restart: unless-stopped` for resilience.

---

## Prerequisites

Ensure you have the following installed:
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

---

## Services

### Prometheus
- **Purpose**: Collect and aggregate metrics from various sources.
- **Image**: `prom/prometheus:v2.55.1`
- **Configuration**: Defined in `./config/prometheus.yaml`.
- **Ports**: Exposes port `9090` for web UI access.
- **Data Volume**: `prometheus-data` (stores time-series data).

### Grafana
- **Purpose**: Dashboard visualization for monitoring data.
- **Image**: `grafana/grafana-oss:11.3.1`
- **Ports**: Exposes port `3000` for the Grafana web interface.
- **Data Volume**: `grafana-data` (stores dashboard and user data).

### Optional Services

#### Node Exporter
- **Purpose**: Collects system metrics (e.g., CPU, memory, disk usage).
- **Image**: `quay.io/prometheus/node-exporter:v1.8.2`
- **Additional Configuration**: Maps host root filesystem for metrics collection.

#### cAdvisor
- **Purpose**: Provides metrics for Docker containers.
- **Image**: `gcr.io/cadvisor/cadvisor:v0.51.0`
- **Ports**: Exposes port `8080` for web UI access.
- **Additional Configuration**: Requires privileged access and specific volumes for container inspection.

---

## Setup

### Clone the Repository

Clone this repository to your local machine:
```bash
git clone <repository-url>
cd <repository-directory>
```

### Configuration

Ensure the `./config/prometheus.yaml` file is properly configured for your use case. Update any scrape targets as needed.

### Run the Stack

Start the stack with the following command:
```bash
docker-compose up -d
```

---

## Accessing the Services

- **Prometheus**: [http://localhost:9090](http://localhost:9090)
- **Grafana**: [http://localhost:3000](http://localhost:3000)
  - Default login: 
    - Username: `admin`
    - Password: `admin` (you will be prompted to change this on first login).
- **Node Exporter (if enabled)**: Metrics available to Prometheus.
- **cAdvisor (if enabled)**: [http://localhost:8080](http://localhost:8080)

---

## Stopping the Stack

To stop and remove the stack, run:
```bash
docker-compose down
```

---

## Notes

- Persistent volumes (`prometheus-data` and `grafana-data`) are defined for data storage.
- Node Exporter and cAdvisor are optional but recommended for comprehensive monitoring.
- Use this setup to monitor system health, application performance, and container metrics effectively.

---

Maintainer: milan.dima@vives.be


