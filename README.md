# Metrics and Log Scraper

Collecting metrics and logs from a self-managed Docker environment for Grafana Dashboards.

## Prerequisites

- Docker, Docker compose
- Grafana Cloud
  - set up prometheus datasource and dashboards
  - set up loki datasource and dashboards

## prepare

- fill template variables with Grafana datasource configuration
  - grafana_prom_host
  - grafana_loki_host
  - grafana_user
  - grafana_key
- start system `docker-compose up -d`

## Stack

- Prometheus
  - node-exporter # collecting VM stats
  - localhost:3033/api/metrics # custom metrics route
- Promtail
  - scrapes docker logs
