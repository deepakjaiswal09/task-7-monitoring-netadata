# 📌 DevOps Internship — Task 7  
## 🖥️ System Resource Monitoring with Netdata (via Docker)

---

## 📖 Project Description
In this task, I deployed **Netdata** inside a Docker container on my Windows system to monitor real-time system resources.  
The monitoring includes **CPU usage, memory utilization, disk I/O, network traffic, processes, and health alarms**.  

All screenshots are attached below in sequence for clarity.  

---

## 📊 Execution Evidence & Screenshots

### 🐳 1. Docker Container Status
**Description:** Verified that the Netdata container is up and running on port `19999`.  
📷 **Screenshot:** *Docker PS output showing running Netdata container*

<img width="1559" height="203" alt="image" src="https://github.com/user-attachments/assets/ec36bfbc-6b94-4cfa-be2b-575531e9ed7a" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/77c861fa-98da-47eb-9189-ce51356d60fa" />

---

### 📈 2. System Overview (CPU, Memory, Disk, Load)
**Description:** Displays key system metrics like CPU usage %, memory utilization, load average, and disk activity.  
📷 **Screenshot:** *Netdata dashboard — System Overview charts*

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/589390dc-062d-4489-be1c-8bf4a65db93a" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f6aacdf6-f526-4276-8752-f8ab3d9d5cf1" />

---

### 🌐 3. Network Metrics
**Description:** Real-time monitoring of incoming and outgoing network traffic, packet rates, and errors.  
📷 **Screenshot:** *Netdata dashboard — Network monitoring charts*

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/94c81c5b-9223-4132-9bcb-b287a1015e81" />


---

### ⚙️ 4. Processes & Applications
**Description:** Shows processes ranked by CPU and memory usage, useful for identifying heavy applications.  
📷 **Screenshot:** *Netdata dashboard — Processes & Applications panel*

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/76895edd-cc77-4580-9020-9b5bfb4610ed" />

---

### 🚨 5. Health / Alarms
**Description:** Shows Netdata’s built-in alerting system with alarms for CPU, memory, and other thresholds.  
📷 **Screenshot:** *Netdata dashboard — Health & Alarms section*

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7f961b68-fb90-4e6e-93ce-a1a59d5aeb30" />

---

## 📑 Final Deliverables
- Step-by-step evidence through screenshots of execution and monitoring  
- Monitoring charts for **system overview, network, processes, containers, and alarms**  

---

## 🌟 Key Learnings
- How to deploy **Netdata** quickly using Docker  
- Gained familiarity with **system-level monitoring metrics**  
- Explored **Docker container metrics** integration via socket binding  
- Understood **real-time alerting & visualization** features of Netdata  

---

## 🙏 Acknowledgement
I sincerely thank my mentor and the DevOps internship team for their continuous support during this task.  
Special thanks to the open-source community for tools like **Docker** and **Netdata**, which made this project achievable and insightful.  

---

**Submitted by:** Deepak Jaiswal 
**Date:** 02/10/2025
