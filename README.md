<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
</head>
<body>
  <h1>🛡️ Home Security Operations Center (SOC) in Microsoft Azure</h1>

  <h2>🎯 Project Summary</h2>
  <p>This project demonstrates the setup of a basic Security Operations Center (SOC) in Microsoft Azure using a honeypot virtual machine and Microsoft Sentinel. It involves deploying a Windows VM to capture real-world attack data, forwarding logs to a central Log Analytics Workspace, and analyzing the data with KQL (Kusto Query Language). The goal is to simulate enterprise-grade SOC operations in a cloud environment using only free Azure resources.</p>

  <h2>🧩 Objectives</h2>
  <ul>
    <li>Deploy a vulnerable Windows VM as a honeypot to attract attackers.</li>
    <li>Forward security logs to Azure Log Analytics Workspace.</li>
    <li>Integrate Microsoft Sentinel for log analysis and visualization.</li>
    <li>Detect brute-force and suspicious login attempts using KQL queries.</li>
    <li>Visualize attack data to identify sources, timelines, and methods.</li>
  </ul>

  <h2>⚙️ Tech Stack</h2>
  <ul>
    <li><b>Cloud Platform:</b> Microsoft Azure</li>
    <li><b>SIEM:</b> Microsoft Sentinel</li>
    <li><b>Monitoring:</b> Azure Log Analytics Workspace</li>
    <li><b>Languages:</b> PowerShell, KQL</li>
    <li><b>Operating System:</b> Windows 10 (Honeypot VM)</li>
    <li><b>Security Tools:</b> Azure Defender, NSG, Firewalls</li>
  </ul>

  <h2>🏗️ Architecture</h2>
  
  <img width="1474" height="742" alt="Screenshot 2025-11-11 174729" src="https://github.com/user-attachments/assets/ba1e305a-891a-4a5e-a6de-582160701766" />

  

  <h2>📊 Observations & Results</h2>

<img width="1917" height="845" alt="Screenshot 2025-11-06 214628" src="https://github.com/user-attachments/assets/6e5429a0-6a42-41b8-8af9-18cad64eb473" />

<img width="1920" height="840" alt="Screenshot 2025-11-06 222658" src="https://github.com/user-attachments/assets/93b7d804-3066-414e-a063-7f954d964901" />

<img width="1920" height="1020" alt="Screenshot 2025-11-06 231306" src="https://github.com/user-attachments/assets/0bca77a0-4dd8-4050-b7df-47df4f503992" />



<img width="1920" height="961" alt="Screenshot 2025-11-06 234013" src="https://github.com/user-attachments/assets/399da840-5352-44c9-a614-9a9ba6da0c77" />



  
  <ul>
    <li>Thousands of brute-force RDP login attempts were recorded within 24 hours of deployment.</li>
    <li>Most attacks originated from IP addresses across Asia, Eastern Europe, and North America.</li>
    <li>Frequent targets included usernames like “Administrator” and “Admin”.</li>
    <li>Peak attack activity aligned with specific regional working hours.</li>
    <li>Sentinel dashboards helped visualize top attacking countries and IP ranges.</li>
  </ul>

  <h2>🧠 Key Findings</h2>
  <ul>
    <li>Exposed VMs attract global attacks within minutes of being online.</li>
    <li>Most login attempts are automated, indicating bot-based scanning.</li>
    <li>Effective SIEM dashboards enable fast detection and correlation of incidents.</li>
    <li>Microsoft Sentinel provides valuable real-time insight into attack behavior.</li>
  </ul>
</body>
</html>
