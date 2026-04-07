# 🚀 Real-Time Infrastructure Monitoring using Prometheus & Grafana on AWS EC2

## 📌 Project Overview
This project demonstrates how to build a real-time infrastructure monitoring and alerting system using Prometheus and Grafana on AWS EC2.

Instead of manually checking server health using SSH, this system provides automated monitoring, visualization, and alerting.

---

## 🎯 Objective
- Collect metrics from multiple EC2 instances  
- Centralize monitoring using Prometheus  
- Visualize metrics using Grafana dashboards  
- Trigger alerts when system thresholds exceed limits  

---

## 🏗️ Architecture
```
EC2 (App Server 1) --->|
                      |--> Prometheus Server ---> Grafana Dashboard
EC2 (App Server 2) --->|
```

- Node Exporter → Collects system metrics  
- Prometheus → Stores and queries metrics  
- Grafana → Displays dashboards  

---

## ⚙️ Tech Stack
- AWS EC2
- Prometheus
- Grafana
- Node Exporter
- Linux (Ubuntu)

---

## 🖥️ Setup Steps

### 1️⃣ Launch Monitoring Server (EC2)
- Install Prometheus
- Install Grafana

---

### 2️⃣ Launch Application Servers (2 EC2)
- Install Node Exporter on both servers

```bash
wget https://github.com/prometheus/node_exporter/releases/latest/download/node_exporter.tar.gz
tar -xvf node_exporter.tar.gz
cd node_exporter
./node_exporter
```

---

### 3️⃣ Configure Prometheus

Edit `prometheus.yml`:

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "node_exporter"
    static_configs:
      - targets:
          - "APP_SERVER_1_IP:9100"
          - "APP_SERVER_2_IP:9100"
```

---

### 4️⃣ Start Prometheus

```bash
./prometheus --config.file=prometheus.yml
```

Access:
http://<Prometheus-IP>:9090

---

### 5️⃣ Setup Grafana

Access Grafana:
http://<Grafana-IP>:3000

Default login:
Username: admin  
Password: admin  

- Add Prometheus as Data Source

---

## 📊 Dashboards

### Default Dashboard
- Import Node Exporter Full Dashboard

### Custom Dashboards
- CPU Usage  
- Memory Utilization  
- Disk Usage  

---

## 🚨 Alert Configuration

Example alert rule:

```yaml
groups:
  - name: alert_rules
    rules:
      - alert: HighCPUUsage
        expr: 100 - (avg by(instance)(rate(node_cpu_seconds_total{mode="idle"}[1m])) * 100) > 80
        for: 1m
        labels:
          severity: warning
        annotations:
          summary: "High CPU Usage detected"
```

---



## 💡 Key Learnings
- Real-time monitoring setup  
- Metrics collection using Node Exporter  
- Prometheus configuration  
- Grafana dashboards  
- Alerting setup  

---

## 🔥 Conclusion
This project automates infrastructure monitoring using Prometheus and Grafana, helping detect issues early and improve system reliability.

---

## 👨‍💻 Author
Om Hivarkar

