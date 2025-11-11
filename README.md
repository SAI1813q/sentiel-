<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Home SOC in Azure — Project README</title>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--accent:#06b6d4;--muted:#94a3b8;--glass:rgba(255,255,255,0.03)}
    body{font-family:Inter,ui-sans-serif,system-ui,Segoe UI,Roboto,"Helvetica Neue",Arial;margin:0;background:linear-gradient(180deg,#081121 0%, #071827 100%);color:#e6eef6;line-height:1.55}
    .container{max-width:980px;margin:36px auto;padding:28px;border-radius:12px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));box-shadow:0 6px 30px rgba(2,6,23,0.6)}
    h1{font-size:28px;margin:0 0 6px}
    p.lead{color:var(--muted);margin-top:0}
    .meta{display:flex;gap:12px;flex-wrap:wrap;margin:18px 0}
    .badge{background:var(--glass);padding:6px 10px;border-radius:999px;font-weight:600;color:var(--accent);font-size:13px}
    .grid{display:grid;grid-template-columns:1fr 320px;gap:20px}
    .card{background:rgba(255,255,255,0.02);padding:16px;border-radius:10px}
    .section{margin:18px 0}
    pre{background:#021827;padding:12px;border-radius:8px;overflow:auto;color:#cfeef9}
    code{font-family:Consolas,monaco,monospace;font-size:13px}
    ul{margin:8px 0 8px 18px}
    .yt{width:100%;height:360px;border-radius:8px;overflow:hidden}
    .small{color:var(--muted);font-size:13px}
    .file-structure{background:rgba(0,0,0,0.18);padding:12px;border-radius:8px}
    .footer{display:flex;justify-content:space-between;align-items:center;margin-top:20px;color:var(--muted);font-size:13px}
    a{color:var(--accent)}
    .columns{display:flex;gap:12px}
    @media (max-width:880px){.grid{grid-template-columns:1fr;}.yt{height:220px}}
  </style>
</head>
<body>
  <div class="container">
    <h1>Home Security Operations Center (SOC) in Microsoft Azure</h1>
    <p class="lead">Hands-on SOC built in Azure using a honeypot VM, Log Analytics and Microsoft Sentinel for real-world attack monitoring and KQL-based threat hunting.</p>

<div class="meta">
      <span class="badge">Azure</span>
      <span class="badge">Microsoft Sentinel</span>
      <span class="badge">KQL</span>
      <span class="badge">Cloud Security</span>
      <span class="badge">Threat Hunting</span>
    </div>
  <div class="grid">
      <div>
        <div class="card section">
          <h2>Project Summary</h2>
          <p>I designed and implemented a home SOC in Microsoft Azure. The deployment uses a Windows honeypot VM with exposed RDP to attract automated attack traffic. Events are shipped to a Log Analytics Workspace and analyzed in Microsoft Sentinel using custom Kusto queries.</p>
        </div>
    <div class="card section">
          <h2>Demo Video</h2>
          <div class="yt">
            <!-- Embedded YouTube: change video ID if needed -->
            <iframe width="100%" height="100%" src="https://www.youtube.com/embed/g5JL2RIbThM" title="Project Demo" frameborder="0" allowfullscreen></iframe>
          </div>
          <p class="small">Tip: add an explicit timestamp in the README (e.g., "0:45–2:10 shows the attack walkthrough").</p>
        </div>

   <div class="card section">
          <h2>Objectives</h2>
          <ul>
            <li>Deploy a honeypot VM in Azure and expose RDP/SSH to capture attacker telemetry.</li>
            <li>Forward Windows Security logs to Azure Log Analytics with Azure Monitor Agent.</li>
            <li>Ingest logs into Microsoft Sentinel and create dashboards and detection rules.</li>
            <li>Hunt for indicators of compromise using KQL and create visualizations of attacker sources.</li>
          </ul>
        </div>

   <div class="card section">
          <h2>Architecture</h2>
          <pre><code>[Global Attackers]
      ↓
  [Azure Honeypot VM]
      ↓
[Log Analytics Workspace]
      ↓
 [Microsoft Sentinel]
      ↓
[KQL Analysis & Dashboards]</code></pre>
        </div>

   <div class="card section">
          <h2>Key Findings</h2>
          <ul>
            <li>Honeypot received hundreds of automated RDP brute-force attempts within hours.</li>
            <li>Top attacker IP ranges span Asia, Eastern Europe, and North America.</li>
            <li>Common usernames targeted: Administrator, admin, root.</li>
            <li>Attack spikes align with global active hours of several time zones.</li>
          </ul>
        </div>
    <div class="card section">
          <h2>KQL Examples</h2>
          <pre><code>// Failed RDP Logins
SecurityEvent
| where EventID == 4625
| summarize Count = count() by IPAddress, bin(TimeGenerated, 1h)
| sort by Count desc

// Successful Logins
SecurityEvent
| where EventID == 4624
| summarize Count = count() by Account, bin(TimeGenerated, 1h)

// Attacker Geolocation (example enrichment)
SecurityEvent
| where EventID == 4625
| extend SrcIP = tostring(RemoteIpCountry)
| summarize count() by SrcIP
| sort by count_ desc</code></pre>
          <p class="small">Tip: tweak EventID filters to your VM OS and audit settings.</p>
        </div>
     <div class="card section">
          <h2>Results & Observations</h2>
          <ul>
            <li>High volume of automated scans — indicates mass automated tooling.</li>
            <li>Repeated IPs were observed; consider blocking or enriching with threat feeds.</li>
            <li>Sentinel correlation rules simplified triage and visualization.</li>
          </ul>
        </div>
    <div class="card section">
          <h2>Future Work</h2>
          <ul>
            <li>Automate alerts using Azure Logic Apps for playbook execution.</li>
            <li>Add Linux honeypot and integrate SSH logs for broader coverage.</li>
            <li>Deploy ARM/Terraform templates to reproduce the environment quickly.</li>
            <li>Integrate threat intel for automated IP enrichment and scoring.</li>
          </ul>
        </div>
   </div>

  <aside>
        <div class="card section">
          <h3>Tech Stack</h3>
          <ul>
            <li>Microsoft Azure (VM, Resource Group, Log Analytics)</li>
            <li>Microsoft Sentinel (SIEM)</li>
            <li>Azure Monitor Agent / Log Analytics Agent</li>
            <li>Kusto Query Language (KQL)</li>
            <li>PowerShell / Azure CLI</li>
          </ul>
        </div>

  <div class="card section">
          <h3>Repository Structure</h3>
          <div class="file-structure">
            <pre><code>.
├── images/            (screenshots, dashboards)
├── kql_queries/       (saved KQL scripts)
├── documentation/     (setup notes, how-to)
├── README.html        (this file)
└── LICENSE</code></pre>
          </div>
        </div>
    <div class="card section">
          <h3>How to Reproduce</h3>
          <ol>
            <li>Create a Resource Group in Azure.</li>
            <li>Deploy a Windows VM and allow RDP for the honeypot (use NSG rules carefully).</li>
            <li>Install Azure Monitor Agent and connect the VM to a Log Analytics Workspace.</li>
            <li>Enable Microsoft Sentinel on the workspace and configure data connectors.</li>
            <li>Run KQL queries and create dashboards/workbooks in Sentinel.</li>
          </ol>
          <p class="small">Security note: deploy honeypots in isolated subscriptions and never use credentials you care about.</p>
        </div>

   <div class="card section">
          <h3>Screenshots (placeholder)</h3>
          <p class="small">Add screenshots to <code>/images</code> and reference them here:</p>
          <pre><code>&lt;img src="images/sentinel-dashboard.png" alt="Sentinel dashboard" /&gt;</code></pre>
        </div>

  <div class="card section">
          <h3>Author</h3>
          <p><strong>Sai</strong> — Cybersecurity Student<br/><a href="#">LinkedIn</a> | <a href="#">GitHub</a></p>
        </div>

   </aside>
    </div>
  <div class="footer">
      <div class="small">License: MIT (optional) • Replace placeholders with your screenshots and results.</div>
      <div class="small">Generated: Home SOC README • Copy & paste into your repo as <code>README.html</code></div>
    </div>

  </div>
</body>
</html>

