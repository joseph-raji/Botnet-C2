# **Botnet C2 Project – Exploiting File Upload Vulnerabilities for Remote Control**  

## **Project Overview**  
This project demonstrates the creation of a **botnet with a Command & Control (C2) server** by exploiting a **file upload vulnerability** in a web application.  
The botnet consists of multiple compromised machines (**bots**) that connect to a centralized **C2 server**, allowing remote execution of commands and **DDoS attacks (SYN flood & ICMP flood)**.  

The attack chain involves:  
✅ **PHP-based remote code execution**  
✅ **Python-based bot communication**  
✅ **DDoS attack execution**  

⚠️ **This project is strictly for ethical hacking and educational purposes. Do not use it for illegal activities.**  

---

## **How It Works**  

### 1️⃣ **Initial Exploitation – Gaining Access**  
🔹 A **vulnerable web application** is hosted on an Apache server (XAMPP on Ubuntu 20.04).  
🔹 The server lacks **file upload validation**, allowing an attacker to upload **malicious PHP files** (`malware.php`).  
🔹 The uploaded PHP script is then executed remotely, which **installs a Python-based bot on the target machine**.  

### 2️⃣ **Establishing the Botnet**  
🔹 The bot machine executes `threaded_client.py`, which:  
   - **Collects system details** (hostname, private/public IP, OS, username).  
   - **Establishes a persistent TCP connection** with the C2 server.  
   - **Registers itself as a bot** by sending its details to the C2.  
   - **Waits for remote commands** from the C2 server.  

### 3️⃣ **Remote Control via C2 Server**  
🔹 The **C2 server (running on Kali Linux)** sends instructions to connected bots, such as:  
   - **File Management:** Upload/download files between C2 and bots.  
   - **Shell Command Execution:** Run system commands remotely.  
   - **DDoS Attacks:** Instruct bots to launch large-scale network attacks.  

### 4️⃣ **Distributed Denial of Service (DDoS) Attacks**  
 **SYN Flood Attack:**  
   - Bots generate **fake TCP SYN requests** with **spoofed IP addresses**.  
   - Overloads the target’s TCP stack, exhausting available connections.  

 **ICMP Flood Attack:**  
   - Bots send a massive number of **ICMP echo requests (ping requests)** to overwhelm the target’s network and CPU.  

---

##  **Technical Stack**  

### **Botnet Components**  
- **C2 Server:**  
  - Python-based backend to **control bots**.  
  - Runs on **Kali Linux** with a Flask-based web interface.  

- **Bot (Infected Machines):**  
  - Virtual machines running **Ubuntu 20.04**.  
  - Python script (`threaded_client.py`) establishes a **TCP connection** to C2.  

- **Exploitation Mechanism:**  
  - Vulnerable **PHP web application** on **XAMPP (Apache Server)**.  
  - Allows **arbitrary file uploads** without extension validation.  

---

## Defenses & Mitigation Strategies  

### 🔹 Preventing Exploitation  
- **Validate file uploads** (restrict allowed file extensions).  
- **Rename uploaded files** to prevent direct execution.  

### 🔹 Detecting Botnet Activity  
- **Monitor unexpected outbound traffic** to C2 servers.  
- Use **Intrusion Detection Systems (IDS)** to detect anomalous network behavior.  

### 🔹 DDoS Mitigation  
- **Implement SYN cookies** to defend against SYN floods.  
- Use **rate limiting** and **firewalls** to block ICMP floods.  

