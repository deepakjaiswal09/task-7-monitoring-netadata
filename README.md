# 🚀 DevOps Internship — Task 7

## System Resource Monitoring with Netdata (Docker on Windows)

---

## 📌 Objective

Set up **Netdata** using Docker and demonstrate system monitoring (CPU, Memory, Disk, Network, Processes) and Docker container metrics (if available). Provide evidence (screenshots) and a short explanation of the steps taken.

---

## 🔧 Environment

* Host: **Windows 10/11** running Docker Desktop (Linux containers) with **WSL2** recommended.
* Tools used: Docker, PowerShell (or WSL2/Ubuntu terminal), Web browser (Chrome/Edge).

---

## 🗂️ Project structure (recommended)

```
devops_task-7/
├─ screenshots/
│  ├─ 01_docker_ps.png
│  ├─ 02_dashboard_system_overview.png
│  ├─ 03_dashboard_network.png
│  ├─ 04_dashboard_processes.png
│  ├─ 05_dashboard_docker_containers.png  (optional)
│  └─ 06_dashboard_alarms.png
├─ run-netdata.ps1   (PowerShell run file)
├─ run-netdata.sh    (WSL/Bash run file)
└─ README.md         (this file)
```

---

## ✅ Step-by-step execution (detailed)

> **Tip:** If you want full host and per-container metrics, use the **WSL2** terminal. If you only need a quick dashboard screenshot, PowerShell single-line is fine.

### 1) Create persistent volumes (optional but recommended)

**PowerShell / WSL**

```powershell
# Create volumes (run once)
docker volume create netdata_lib
docker volume create netdata_cache
docker volume create netdata_log
```

**Expected result:** command prints the names of the created volumes (e.g. `netdata_lib`).

**Screenshot:** save as `screenshots/01_docker_ps.png` after verifying container (see step 3).

---

### 2) Start Netdata (PowerShell - quick method)

If you are in PowerShell and want the simplest command (no host mounts):

```powershell
docker run -d --name netdata `
  -p 19999:19999 `
  -v netdata_lib:/var/lib/netdata `
  -v netdata_cache:/var/cache/netdata `
  -v netdata_log:/var/log/netdata `
  --restart unless-stopped `
  netdata/netdata:stable
```

**What this does:** runs Netdata and exposes its dashboard on port **19999**. This is sufficient for the dashboard screenshots required by the task.

---

### 3) Verify container is running (CLI evidence)

**PowerShell / WSL**

```powershell
docker ps --filter "name=netdata" --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"
```

**Screenshot:** take and save the output as `screenshots/01_docker_ps.png`. This proves the container is up and port `19999` is mapped.

---

### 4) Open Netdata dashboard

* Open browser and visit: `http://localhost:19999`
* Wait a few seconds for the dashboard to populate charts.

**Screenshot (System Overview):** capture the top of the dashboard showing CPU, Memory, Load, Disk I/O. Save as `screenshots/02_dashboard_system_overview.png`.

**Screenshot (Network):** scroll to the network section and save as `screenshots/03_dashboard_network.png`.

**Screenshot (Processes/Applications):** scroll to processes and save as `screenshots/04_dashboard_processes.png`.

**Screenshot (Alarms/Health):** open the alarms/health panel and save as `screenshots/06_dashboard_alarms.png`.

---

### 5) (Optional) Show Docker containers panel (per-container metrics)

To see per-container metrics in Netdata, run Netdata with access to the Docker socket and host files. **Run this in WSL2** (Ubuntu terminal) for best results:

```bash
# ensure volumes exist
docker volume create netdata_lib
docker volume create netdata_cache
docker volume create netdata_log

# run Netdata with host mounts (recommended in WSL2)
docker run -d --name=netdata \
  -p 19999:19999 \
  -v netdata_lib:/var/lib/netdata \
  -v netdata_cache:/var/cache/netdata \
  -v netdata_log:/var/log/netdata \
  -v /etc/passwd:/host/etc/passwd:ro \
  -v /etc/group:/host/etc/group:ro \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  -v /var/run/docker.sock:/var/run/docker.sock:ro \
  --cap-add SYS_PTRACE \
  --security-opt apparmor=unconfined \
  --restart unless-stopped \
  netdata/netdata:stable
```

**If you run this command from WSL2**, you should then see a **Docker** section in Netdata showing CPU/Memory/IO for each container.

**Screenshot:** If visible, save the Docker containers panel as `screenshots/05_dashboard_docker_containers.png`.

---

### 6) View logs (optional but useful for debugging)

**PowerShell / WSL**

```powershell
# show last 50 lines
docker logs netdata --tail 50

# follow logs
docker logs -f netdata
```

**Or inside the container:**

```bash
docker exec -it netdata tail -n 200 /var/log/netdata/error.log
```

---

### 7) Stop and remove (cleanup)

```powershell
docker stop netdata
docker rm -f netdata
```

---

## 🧾 README checklist (for submission)

* [ ] `docker ps` screenshot → `screenshots/01_docker_ps.png`
* [ ] System Overview screenshot → `screenshots/02_dashboard_system_overview.png`
* [ ] Network screenshot → `screenshots/03_dashboard_network.png`
* [ ] Processes screenshot → `screenshots/04_dashboard_processes.png`
* [ ] Docker containers screenshot (optional) → `screenshots/05_dashboard_docker_containers.png`
* [ ] Alarms screenshot → `screenshots/06_dashboard_alarms.png`

Place these images inside the `screenshots/` folder at the repository root.

---

## 🗂️ How to add & push to GitHub

```bash
git init
git add .
git commit -m "Task 7: Netdata monitoring - README + screenshots"
# create repo on GitHub and then:
git remote add origin <your-github-repo-url>
git branch -M main
git push -u origin main
```

---

## 🔎 Notes & Troubleshooting

* If the Docker Containers panel is missing in Netdata, it usually means the container started without access to `/var/run/docker.sock` or `/proc`/`/sys`. To get per-container metrics, run Netdata from WSL2 with the command shown in Step 5.
* If `http://localhost:19999` doesn't load, ensure Docker Desktop is running and the container is `Up` (check `docker ps`).
* On Windows, PowerShell uses the backtick (`) for line continuation. In WSL/Bash, use ``.

---

## 📌 Deliverables (what to upload)

1. `README.md` (this file)
2. `screenshots/` folder with all required images (names as above)
3. (Optional) `run-netdata.ps1` and `run-netdata.sh` scripts used to launch Netdata

---

## 🙏 Acknowledgement

I would like to express my sincere gratitude to my mentor and the DevOps internship coordinators for guiding me through this task. I also thank the maintainers of Netdata and Docker for their excellent tools which made monitoring and debugging simple and effective.

---

**Submitted by:** [Your Name]

**Date:** [DD-MM-YYYY]
