# 🧩 Lab 6 — Windows Universal Forwarder Setup and Log Integration

In this lab, I configured the **Splunk Universal Forwarder** on a Windows system to send system event logs to the **Splunk Enterprise** instance.  
This demonstrates how Splunk can centralize log collection across both Linux and Windows environments.

---

## ⚙️ Step 1: Configure Splunk to Receive Data

Before installing the forwarder, I ensured that the **Splunk Enterprise** instance is configured to receive data on **port 9997**.

**Path in Splunk Web:**

Settings → Forwarding and receiving → Configure receiving

arduino
Copy code

Then, click **Add new** and enter the receiving port:

9997

yaml
Copy code

Click **Save**.

![Forwarding and Receiving Settings](../images/siemlab/28-forwarding-menu.png)
![Receiving Port Configuration](../images/siemlab/29-receive-port.png)

---

## ⚙️ Step 2: Download Splunk Universal Forwarder

I downloaded **Splunk Universal Forwarder 9.0.4** for Windows from the [official Splunk website](https://www.splunk.com/en_us/download/universal-forwarder.html).

**Selected version:**
Windows 64-bit (.msi)

yaml
Copy code

The downloaded installer was placed in the `Downloads` folder.

![Forwarder Download Page](../images/siemlab/30-forwarder-download.png)
![Forwarder Installer in Downloads Folder](../images/siemlab/31-forwarder-downloads-folder.png)

---

## ⚙️ Step 3: Begin Installation

Launched the installer by double-clicking it.

Checked the **License Agreement** and selected:

Use this Universal Forwarder with:
→ An on-premises Splunk Enterprise instance

yaml
Copy code

![License Agreement & On-Premises Selection](../images/siemlab/32-forwarder-license.png)

---

## ⚙️ Step 4: Configure Splunk Listener

Specified the **Receiving Indexer** details to allow the forwarder to send logs to the Splunk instance:

Hostname or IP: 127.0.0.1
Port: 9997

yaml
Copy code

This ensures that data is sent to the same machine running Splunk Enterprise (for lab setup).

![Receiving Indexer Configuration](../images/siemlab/33-receiving-indexer.png)

---

## ⚙️ Step 5: Configure Deployment Server

Although optional, I also configured the **Deployment Server** for forwarder management.  
This allows centralized control of multiple forwarders from the Splunk instance.

Hostname or IP: 127.0.0.1
Port: 8089

yaml
Copy code

![Deployment Server Configuration](../images/siemlab/34-deployment-server.png)

---

## ⚙️ Step 6: Create Forwarder Admin Account

Created an administrative account for the forwarder:

Username: Analyst
Password: ********

yaml
Copy code

This will be used to authenticate and manage the forwarder connection with the Splunk Indexer.

![Forwarder Admin Setup](../images/siemlab/35-forwarder-admin.png)

---

## ⚙️ Step 7: Install and Complete Setup

The installation process took 3–5 minutes.  
The wizard displayed progress for copying and installing files.

![Installation Progress](../images/siemlab/36-forwarder-progress.png)
![Installation Completion](../images/siemlab/37-forwarder-complete.png)

---

## ⚙️ Step 8: Verify Forwarder Connection in Splunk

Once the forwarder installation was complete, I navigated to:

Settings → Forwarder Management

markdown
Copy code

The **Windows client (coffelylab)** appeared under the **Clients** tab, confirming a successful connection.

Host Name: coffelylab
IP Address: 127.0.0.1
Machine Type: windows-x64
Deployed Apps: 0
Status: Phoned home a few seconds ago

yaml
Copy code

![Forwarder Management Status](../images/siemlab/38-forwarder-management.png)

---

## ⚙️ Step 9: Configure Data Inputs (Windows Event Logs)

With the forwarder successfully connected, I configured it to collect **Windows Event Logs**.

In Splunk Web:
Settings → Data Inputs → Local Event Logs

yaml
Copy code

I selected the following:
- Application Logs  
- Security Logs  
- System Logs  

Then saved and applied the configuration.

![Windows Event Log Selection](../images/siemlab/39-windows-event-logs.png)
![Data Input Added Confirmation](../images/siemlab/40-event-log-confirm.png)

---

## ⚙️ Step 10: Verify Log Ingestion

Searched in Splunk using the following query:

```spl
index=windows_logs sourcetype="WinEventLog:*"

```
Logs from the Windows endpoint appeared successfully, confirming that event data was being ingested from the Universal Forwarder.


✅ Outcome
Installed and configured Splunk Universal Forwarder on Windows.

Verified successful communication with Splunk Enterprise on port 9997.

Forwarded Windows Event Logs (Application, System, and Security).

Confirmed real-time log ingestion in Splunk Web.

🔚 Summary
With this setup, both Linux and Windows systems now send logs to a centralized Splunk Enterprise instance.
This provides cross-platform visibility for security monitoring, event correlation, and incident investigation.
