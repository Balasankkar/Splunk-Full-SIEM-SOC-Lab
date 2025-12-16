# 🧩 Lab 6 — Windows Universal Forwarder Setup

In this lab, I configured the **Splunk Universal Forwarder** on a Windows system to send system event logs to the **Splunk Enterprise** instance. This demonstrates how Splunk can centralize log collection across both Linux and Windows environments.

---

## ⚙️ Step 1: Configure Splunk to Receive Data

Before installing the forwarder, I ensured that the **Splunk Enterprise** instance is configured to receive data on **port 9997**.

Settings → Forwarding and receiving → Configure receiving

![Image Alt](https://github.com/Balasankkar/Splunk-Full-SIEM-SOC-Lab/blob/ad0d4a1953af59ee0dd5e54fd9f1c9c153b9777e/Screenshots/Figure60.png)

Then, click **Add new** 

![Image Alt](https://github.com/Balasankkar/Splunk-Full-SIEM-SOC-Lab/blob/ad0d4a1953af59ee0dd5e54fd9f1c9c153b9777e/Screenshots/Figure61.png)

Enter the receiving port: **9997**

Click **Save**.

![Image Alt](https://github.com/Balasankkar/Splunk-Full-SIEM-SOC-Lab/blob/ad0d4a1953af59ee0dd5e54fd9f1c9c153b9777e/Screenshots/FIgure63.png)


---

## ⚙️ Step 2: Download Splunk Universal Forwarder

I downloaded **Splunk Universal Forwarder 9.0.4** for Windows from the [official Splunk website](https://www.splunk.com/en_us/download/universal-forwarder.html).

**Selected version:**
Windows 64-bit (.msi)

The downloaded installer was placed in the `Downloads` folder.

![Image Alt](https://github.com/Balasankkar/Splunk-Full-SIEM-SOC-Lab/blob/ad0d4a1953af59ee0dd5e54fd9f1c9c153b9777e/Screenshots/Figure1%2CL5.png)

---

## ⚙️ Step 3: Begin Installation

Launched the installer by double-clicking it.

Checked the **License Agreement** and select:

Use this Universal Forwarder with:
→ An on-premises Splunk Enterprise instance

![Image Alt](https://github.com/Balasankkar/Splunk-Full-SIEM-SOC-Lab/blob/2fb41d1163016269e22e359acfd14502b79afd38/Screenshots/Figure64.png)

---

## ⚙️ Step 4: Create Forwarder Admin Account

Created an administrative account for the forwarder:

Username: Analyst
Password: ********

This will be used to authenticate and manage the forwarder connection with the Splunk Indexer.

![Forwarder Admin Setup](https://github.com/Balasankkar/Splunk-Full-SIEM-SOC-Lab/blob/2fb41d1163016269e22e359acfd14502b79afd38/Screenshots/Figure65.png)

---

## ⚙️ Step 5: Configure Deployment Server

Although optional, I also configured the **Deployment Server** for forwarder management.  
This allows centralized control of multiple forwarders from the Splunk instance.

Hostname or IP: 127.0.0.1
Port: 8089

---

## ⚙️ Step 6: Configure Splunk Listener

Specify the **Receiving Indexer** details to allow the forwarder to send logs to the Splunk instance:

Hostname or IP: 127.0.0.1
Port: 9997

This ensures that data is sent to the same machine running Splunk Enterprise (for lab setup).

## ⚙️ Step 7: Install and Complete Setup

The installation process took 3–5 minutes.  
The wizard displayed progress for copying and installing files.

![Installation Completion](https://github.com/Balasankkar/Splunk-Full-SIEM-SOC-Lab/blob/2fb41d1163016269e22e359acfd14502b79afd38/Screenshots/Figure66.png)

---

## ⚙️ Step 8: Verify Forwarder Connection in Splunk

Once the forwarder installation was complete, I navigated to:

Settings → Forwarder Management

![Image Alt](https://github.com/Balasankkar/Splunk-Full-SIEM-SOC-Lab/blob/2fb41d1163016269e22e359acfd14502b79afd38/Screenshots/Figure67.png)

The **Windows client (coffelylab)** appeared under the **Clients** tab, confirming a successful connection.

Host Name: coffelylab

IP Address: 127.0.0.1

Machine Type: windows-x64

Deployed Apps: 0

Status: Phoned home a few seconds ago

![Forwarder Management Status](https://github.com/Balasankkar/Splunk-Full-SIEM-SOC-Lab/blob/2fb41d1163016269e22e359acfd14502b79afd38/Screenshots/Figure68.png)

---

## ✅ Outcome
Installed and configured Splunk Universal Forwarder on Windows.

Verified successful communication with Splunk Enterprise on port 9997.

🔚 Summary
With this setup, both Linux and Windows systems now send logs to a centralized Splunk Enterprise instance. This provides cross-platform visibility for security monitoring, event correlation, and incident investigation.
