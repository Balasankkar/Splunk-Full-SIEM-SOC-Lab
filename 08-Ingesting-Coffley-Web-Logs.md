# 🧩 Lab 8 — Splunk Forwarder Configuration and Log Ingestion

In this lab, I configured the Splunk Universal Forwarder on a Windows machine, connected it to the Splunk Enterprise Indexer, and set up log ingestion for both Windows Event Logs and Coffely IIS Web Logs. This establishes the foundation for collecting endpoint and web application logs for centralized security monitoring.

---

## ⚙️ Step 1: Ingest Coffely Web Logs (IIS)

The same Windows host also ran the Coffely web application, accessible at: http://coffely.thm

This local site simulates an e-commerce platform used to generate web traffic for log collection.

## ⚙️ Step 2: Add Data from Forwarder

Navigated to:

Settings → Add Data → Forward

Selected Forward data from a Splunk forwarder.

Selected WINDOWS coffelylab as the host and proceeded.

## ⚙️ Step 3: Configure Source Path

Select Files & Directories as the source input method.

Specified the IIS log path:

`C:\inetpub\logs\LogFiles\W3SVC2`

## ⚙️ Step 4: Set Source Type and Index

Under Input Settings, selected:

Source Type: **iis**

This automatically applies Microsoft IIS log parsing during ingestion.

Created a new index for web data:

`web_logs`

## ⚙️ Step 5: Verify Web Log Ingestion

After setup, I accessed the Coffely site to generate logs (navigating through menus and placing mock orders).

Within 4–5 minutes, logs began populating in Splunk.

Search query:

`index="web_logs" sourcetype="iis"`

Results included HTTP requests, response codes, timestamps, and client IPs — confirming successful ingestion.


✅ Outcome
By the end of this lab:

Splunk Universal Forwarder was successfully installed and connected to Splunk Enterprise.

Windows Event Logs and IIS Web Logs were ingested and indexed.

Verified both log sources via Splunk Search queries:

index="win_logs"
index="web_logs" sourcetype="iis"

🔍 Key Insights
Component	Log Source	Index	Verification Query
Windows Host	Event Logs (Application, Security, System)	win_logs	source="WinEventLog:*"
Coffely Web Server	IIS Access Logs	web_logs	index="web_logs" sourcetype="iis"

This lab demonstrated end-to-end log forwarding and ingestion across both system and web sources, a fundamental capability in SOC environments for threat monitoring and analysis.

## 🔚 Summary

After completing this setup:

The Splunk environment is now receiving logs from multiple sources.

Data normalization through source types (WinEventLog, IIS) allows seamless querying and dashboard creation.
