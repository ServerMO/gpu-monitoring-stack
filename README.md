# 📊 NVIDIA GPU Monitoring Stack (Prometheus + Grafana + DCGM)

A production-ready Docker Compose template to monitor NVIDIA GPUs (VRAM, Power, Temp) using the official DCGM Exporter, Prometheus, and Grafana. 

Provided by **[ServerMO](https://www.servermo.com/)** - High-Performance Bare Metal GPU Servers.



## ⚠️ The Problem We Are Solving
Running AI workloads (LLMs, Model Training, Inference) blind is dangerous. Standard server tools like `htop` cannot see GPU metrics. This stack helps you prevent:
- **OOM (Out of Memory) Crashes:** Monitor VRAM usage in real-time.
- **Thermal Throttling:** Alert when your GPU hits 85°C+.
- **Power Limit Drops:** Track wattage and PCIe bandwidth bottlenecks.

📖 **Read the full step-by-step tutorial here:** [How to Monitor NVIDIA GPUs with Prometheus & Grafana](https://www.servermo.com/howto/monitor-nvidia-gpu-prometheus-grafana/)

---

## 🛠️ Prerequisites
Before running this stack, your host machine MUST have:
1. NVIDIA Drivers installed.
2. Docker & Docker Compose installed.
3. **NVIDIA Container Toolkit** installed and configured:
   ```bash
   sudo nvidia-ctk runtime configure --runtime=docker
   sudo systemctl restart docker
   ```
   
## 🚀 Quick Start Guide

**1. Clone the repository**
```bash
  git clone [https://github.com/ServerMO-Official/gpu-monitoring-stack.git](https://github.com/ServerMO-Official/gpu-monitoring-stack.git)
  cd gpu-monitoring-stack
```

**2. Set permissions for Grafana**
```bash
sudo chown -R 472:472 grafana_data
```

**3. Start the stack**
```bash
docker compose up -d
```

## 🛑 CRITICAL WARNING: The Disk Bloat Trap
Many online guides tell you to set `DCGM_EXPORTER_INTERVAL=30`. **Do not do this!** The interval is in milliseconds. Setting it to `30` will fill up your hard drive with logs in days. 
In our `docker-compose.yml`, we have safely set it to `15000` (15 seconds) which is optimal for production.

---

## 📈 Grafana Dashboard Setup
1. Open `http://<YOUR_SERVER_IP>:3000`
2. Default Login: `admin` / `admin`
3. Add Data Source: `Prometheus` (URL: `http://prometheus:9090`)
4. Go to **Dashboards > Import** and enter ID: **`12239`** (Official NVIDIA Dashboard).

---

### 🖥️ Need More GPU Power?
Is your Grafana dashboard showing 99% VRAM usage? Stop throttling your AI agents. Upgrade to unshared, dedicated power.
👉 **[Deploy a Bare Metal GPU Server with ServerMO](https://www.servermo.com/gpu-servers/)**

---
*Note: This repository is provided by ServerMO as an educational resource and template. It is provided 'as-is' without active support. For enterprise GPU server hosting, visit [ServerMO.com](https://www.servermo.com).*


