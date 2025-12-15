# 🧩 Lab 7 — Event Log Ingestion

In this lab, I completed the configuration of the **Splunk Universal Forwarder** on a Windows endpoint and connected it to the **Splunk Enterprise** instance. After establishing communication, I configured the forwarder to send **Windows Event Logs** (Application, Security, and System) into Splunk for monitoring and analysis.

---

## ⚙️ Step 1: Add Data from Forwarder

To begin ingesting logs from the Windows machine:

1. Navigate to **Settings → Add Data**

![Add Data Menu in Splunk](../images/siemlab/43-add-data-menu.png)
   
2. Select the **Forward** option to pull data from the connected Splunk Forwarder.

![Select Forward Option](../images/siemlab/44-forward-data.png)

---

## ⚙️ Step 2: Select Forwarder Host

In the **Select Forwarders** window:

- The available host `WINDOWS coffelylab` appeared.

- I moved it to **Selected host(s)** and created a **New Server Class Name**: `coffely_lab`

Then clicked **Next**.

---

## ⚙️ Step 3: Choose Data Source — Local Event Logs

Next, I configured the source for log collection.

1. Under **Select Source**, I chose:
Local Event Logs — Collect event logs from this machine.

2. From the list, I selected the following event logs:
- **Application**
- **Security**
- **System**

These represent the primary Windows event channels used for monitoring user activity, system alerts, and security events.

![Select Local Event Logs](../images/siemlab/46-local-eventlogs.png)

---

## ⚙️ Step 4: Create an Index for Event Logs

To organize the incoming data, I created a new index:

`win_logs`

This index will store all incoming events forwarded from the Windows endpoint.

![Create Win_Logs Index](../images/siemlab/47-create-index.png)

---

## ⚙️ Step 5: Review and Confirm Configuration

Before finalizing, I reviewed the configuration:

| Parameter | Value |
|------------|--------|
| Server Class Name | coffelylab |
| Input Type | Windows Event Logs |
| Event Logs | Application, Security, System |
| Index | win_logs |
| Host | WINDOWS coffelylab |

Once verified, I clicked **Submit** to activate the data input.

![Configuration Review Screen](../images/siemlab/48-review-settings.png)

---

## ⚙️ Step 6: Verify Ingestion via Splunk Search

After a few moments, the data began flowing into Splunk. To verify, I ran the following search query:

```spl
source="WinEventLog:*" index="win_logs"

```

Splunk successfully displayed events from all three logs:

- **WinEventLog:Security**

- **WinEventLog:System**

- **WinEventLog:Application**

Over 12,000+ events were indexed within minutes, confirming successful ingestion.


## ✅ Outcome
The Splunk Universal Forwarder successfully connected to the Splunk Enterprise Indexer on port 9997.

Forwarding of Windows Event Logs (Application, Security, and System) was configured and validated.

The win_logs index was created to store and organize Windows events.

Logs were successfully searchable within Splunk’s Search & Reporting App.

## 🔍 Key Commands and Ports
Component	    Port	    Description

Splunk Indexer (Receiver)	9997	Receives forwarded data

Splunk Deployment Server	8089	Manages and deploys configurations

Splunk Web Interface	8000	Administrative GUI access

## 🔚 Summary

This lab demonstrated how to:

Configure Splunk Universal Forwarder on Windows.

Connect it securely to Splunk Enterprise.

Collect and index Windows Event Logs.

Verify end-to-end log ingestion.

This forms the backbone of centralized monitoring for Windows systems in a SOC environment.
