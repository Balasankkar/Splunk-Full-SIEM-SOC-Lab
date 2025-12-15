# 🧩 Lab 4.1 — Setting Up Splunk Universal Forwarder (Linux)

In this lab, I set up the **Splunk Universal Forwarder** on the Linux server to forward logs to the main Splunk Enterprise instance.  
The Universal Forwarder is a lightweight Splunk agent designed to collect and send data securely to an indexer or another forwarder.

---

## ⚙️ Step 1: Understanding Splunk Forwarders

Splunk forwarders are responsible for sending data from endpoints to the Splunk indexer.  
There are two main types of forwarders:

- **Heavy Forwarder:** Used when log data needs to be filtered or parsed before forwarding.  
- **Universal Forwarder:** A lightweight agent that forwards logs without local indexing or filtering.  

For this task, I used the **Universal Forwarder** to ingest logs from the Linux machine into the Splunk instance.

---

## ⚙️ Step 2: Locate the Forwarder Package

The forwarder installer was already available in the lab environment under:

```bash
~/Downloads/splunk/
```

Before starting the installation, I switched to root privileges:

```bash
sudo su
```

Figure 1 — Overview of Splunk Universal Forwarder setup.

## ⚙️ Step 3: Install the Forwarder

I extracted and installed the Universal Forwarder using the following command:

```bash
tar xvzf splunkforwarder.tgz
```

This created a new folder named splunkforwarder/, containing all the binaries and configuration files.

Next, I moved the folder to the /opt/ directory:

``` bash
mv splunkforwarder /opt/
```

Figure 2 — Extracting and moving the forwarder directory.

## ⚙️ Step 4: Start the Splunk Forwarder

I navigated to the forwarder’s binary directory and started the service with the license acceptance flag:

```bash
cd /opt/splunkforwarder
./bin/splunk start --accept-license

```
As this was the first startup, I was prompted to create admin credentials:

```bash
Username: splunkadmin
Password: ********
```

During initialization, the system detected that port 8089 was already in use and asked to use an alternate port.
I set the management port to 8090.

Figure 3 — Creating credentials and running the forwarder on port 8090.

After configuration, Splunk confirmed that the Universal Forwarder was running successfully.

✅ Outcome

Installed and configured the Splunk Universal Forwarder on Linux.

Successfully created admin credentials for the forwarder instance.

Verified the forwarder service is running on port 8090.

Splunk Forwarder is up and running but does not know what data to send and where. This is what we are going to configure next.

## 🧩 Lab 4.2 — Ingesting Linux Logs

In this task, I set up the **Splunk Universal Forwarder** on a Linux machine and configured it to forward system logs into the main **Splunk Enterprise** instance for analysis. This setup demonstrates end-to-end data ingestion — from log forwarding to visualization in Splunk.

---

## ⚙️ Step 1: Configure Splunk to Receive Data
Now that the forwarder is running, the Splunk Enterprise instance must be configured to receive incoming data.

Navigate in Splunk Web to:

Settings → Forwarding and receiving → Configure receiving


Then add a new receiving port — the default port is 9997.


After saving, port 9997 becomes active and is ready to accept data from forwarders.

⚙️ Step 2 : Create a Custom Index

Next, I created a dedicated index called Linux_host to store incoming logs.

Path: Settings → Indexes → New Index

Name the new index: Linux_host

Click Save to finalize.

## ⚙️ Step 3: Configure the Forwarder Output

On the Linux host, I configured the Universal Forwarder to send data to the Splunk instance’s receiving port.

In the host terminal, I went to the directory `/opt/splunkforwarder/bin` :

```bash
cd /opt/splunkforwarder/bin
```
I then added the forward-server using the command 

```bash
./splunk add forward-server 10.48.142.158:9997
```
The command successfully added the forwarder target:
```bash
Added forwarding to: 10.48.142.158:9997
```
## ⚙️ Step 4: Specify Log Sources

Linux stores most system logs under /var/log/.

For this lab, I chose to monitor syslog and send it to the Linux_host index.

```bash
./splunk add monitor /var/log/syslog -index Linux_host
```

Result:
```bash
Added monitor of '/var/log/syslog'.
```

## ⚙️ Step 5: Verify Configuration in inputs.conf

I checked the inputs.conf file to confirm the monitored log source and index mapping.

Path:

```bash
/opt/splunkforwarder/etc/apps/search/local
```
Commands:

```bash
ls
inputs.conf
cat inputs.conf
```
Output:
```bash
[monitor:///var/log/syslog]
disabled = false
index = Linux_host
```

⚙️ Step 8: Generate and Verify Log Data
To simulate live log data, I used the logger utility to create a test message inside syslog:

```bash
logger "coffely-has-the-best-coffee-in-town"
```
Verified entry with:

```bash
tail -1 /var/log/syslog
```

Then confirmed it appeared in Splunk under the index Linux_host.

## ✅ Outcome
Successfully installed and configured Splunk Universal Forwarder on Linux.

Configured Splunk Enterprise to receive data on port 9997.

Created a custom Linux_host index for segregated log storage.

Monitored /var/log/syslog and verified log forwarding through the Splunk Search dashboard.

Confirmed successful ingestion and visualization of test log data.

## 🔚 Summary
This lab established the foundation for log collection and centralization using Splunk. I now have a fully functional setup where Linux logs are continuously forwarded to Splunk for real-time monitoring and analysis.
