# SOC Lab in Azure - Security Operations Lab

This project is a **hands-on SOC Lab** built in **Azure** to simulate real-world Security Operations Center (SOC) tasks, including **log collection, analysis, and attack visualization**. The lab includes setting up **Virtual Machines, Log Forwarding, KQL queries, and Sentinel dashboards**.

---

## 📌 Part 1: Setting Up Azure Subscription

1. **Create an Azure Free Subscription**
   - [Azure Free Account](https://azure.microsoft.com/en-us/free/)
   - If a free account isn’t available, consider **pay-as-you-go** (be mindful of costs).

2. **Login to Azure Portal**
   - Access the Azure portal: [https://portal.azure.com](https://portal.azure.com)

---

## 📌 Part 2: Setting Up the Honeypot (Azure VM)

1. **Create a Windows 10 Virtual Machine**
   - Go to **Azure Portal** → Search for **Virtual Machines**
   - Create a **new VM**
   - Choose an appropriate **size** based on available resources.
   - Set a **username and password** (store safely).

2. **Modify Network Security Group (NSG)**
   - Navigate to **NSG settings** for the VM.
   - Create a rule to **allow all inbound traffic** (for testing purposes only).

3. **Disable Windows Firewall (Temporarily)**
   - Open **Run (`Win + R`)** → Type `wf.msc`
   - Go to **Properties** → Set all profiles (**Domain, Private, Public**) to **Off**.

---

## 📌 Part 3: Generating Logs for Analysis

1. **Simulate Failed Login Attempts**
   - Try **failing 3 logins** using the username `employee`.

2. **Check Security Logs in Event Viewer**
   - Open **Event Viewer** → Navigate to **Windows Logs > Security**.
   - Find **Event ID: 4625** (Failed login attempts).

---

## 📌 Part 4: Log Forwarding & KQL Queries

### 1️⃣ Create Log Analytics Workspace
   - Search for **Log Analytics Workspaces** in Azure.
   - Create a new **workspace**.

### 2️⃣ Connect Azure Sentinel to Log Analytics
   - Search for **Azure Sentinel** and link it to the Log Analytics Workspace.

### 3️⃣ Enable Log Collection
   - Configure **Windows Security Events via AMA** to send logs to Sentinel.

### 4️⃣ Querying Logs with KQL
   Run this query in **Log Analytics Workspace (LAW)** to find failed login attempts:
   ```kql
   SecurityEvent
   | where EventId == 4625
📌 Part 5: Log Enrichment - Adding Geolocation Data
Import an IP-to-Geo Watchlist

Download the GeoIP CSV file (or use an external service).
Upload it as a Sentinel Watchlist:
Name: geoip
Source Type: Local File
Search Key: network
Enrich Logs with Geolocation Data
