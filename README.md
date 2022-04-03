# Metrics and Logs Scraper

Collecting metrics and logs of a self-managed Docker environment and the VM for Grafana Dashboards.

## Prerequisites

- Linux VM, Docker, Docker compose
- Grafana Cloud
  - set up prometheus datasource and dashboards
  - set up loki datasource and dashboards

## Prepare

- Fill template variables with Grafana datasource configuration
  - grafana_prom_host
  - grafana_loki_host
  - grafana_prom_user
  - grafana_loki_user
  - grafana_key

## Start system

`docker-compose up -d`

## Stack

- Prometheus
  - VM stats: Prometheus scrapes stat, collected by node-exporter
  - API metrics: Prometheus requests metrics (e.g. exposed by prom-client) from custom route `api:3033/api/metrics` 
    hint: Using a common network, the main system which is a docker-compose project is located separately, example configuration:
    ```yml
    services:
      api:
        ...
        networks:
          - monitoring
    networks:
      monitoring:
        name: monitoring
        driver: bridge
    ```
- Promtail
  - System logs: from /var/logs
  - Docker logs: from /var/lib/docker/containers
