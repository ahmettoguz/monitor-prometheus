<h1 id="top" align="center">Monitor Prometheus <br/> 🚢 v1.0.0 🚢</h1>

<br>

<div align="center">
    <img height=150 src="assets/banner/banner.png">
</div>

<br>

## 🔍 Table of Contents

- [Features](#features)
- [System Startup](#system-startup)

<br/>

<h2 id="features">🔥 Features</h2>

- **Docker Containerization:** The application is containerized using Docker to ensure consistent deployment, scalability, and isolation across different environments.
- **Persistent Data:** Utilizes bind mounts to persist data on the host machine, preventing data loss during container restarts.
- **Docker Compose Deployment:** Simplifies deployment with Docker Compose configuration, enabling easy setup and service orchestration without complex commands.
- **Customizable Configuration:** Easily modify Prometheus configuration via bind mounts to adjust settings such as scrape intervals, alert rules, and more.
- **Traefik Metrics Integration:** Prometheus can be configured to scrape metrics provided by Traefik, enabling monitoring of your reverse proxy's performance, request counts, error rates, and other important statistics. This helps to get a comprehensive view of your application's traffic and routing.
- **cAdvisor Integration:** Integrates with cAdvisor to scrape container metrics and track resource usage (CPU, memory, network, disk) across running containers.
- **Node-Exporter Integration:** Scrapes node metrics, including system-level statistics like CPU usage, memory consumption, disk I/O, and network statistics for overall server health monitoring.

<br/>

<h2 id="system-startup">🚀 System Startup</h2>

- Create a new directory named `monitor`.

```
mkdir monitor
cd monitor
```

- Clone project.

```
git clone https://github.com/ahmettoguz/monitor-prometheus
```

- Create configuration file `./config/prometheus.yml` with reference to one of the following file according to needs:

- `./config/prometheus.all.yml`
- `./config/prometheus.cadvisor.yml`
- `./config/prometheus.node-exporter.yml`
- `./config/prometheus.traefik.yml`

```
cp ./config/prometheus.all.yml ./config/prometheus.yml
```

- Create `network-monitor` network if not exists.

```
docker network create network-monitor
```

- Run Container.

```
docker stop                             monitor-prometheus-c
docker rm                               monitor-prometheus-c
docker compose -p monitor up --build -d prometheus
docker compose -p monitor up -d         prometheus
docker logs -f                          monitor-prometheus-c
```

- Test connection.

```
curl -vkL https://micro-local.net/prometheus/api/v1/query?query=up
curl -vkL https://micro-local.net/prometheus/api/v1/metadata
```

- Refer to [`Node-Export`](https://github.com/ahmettoguz/monitor-node-export) repository to expose node metrics.

- Refer to [`cAdvisor`](https://github.com/ahmettoguz/monitor-cadvisor) repository to expose contianer metrics.

- Refer to [`Grafana`](https://github.com/ahmettoguz/monitor-grafana) repository to integrate grafana to visualize node exporter data.

- Refer to [`Traefik`](https://github.com/ahmettoguz/core-traefik) repository to expose traefik metrics and also launch reverse proxy.

<br/>

### [🔝](#top)
