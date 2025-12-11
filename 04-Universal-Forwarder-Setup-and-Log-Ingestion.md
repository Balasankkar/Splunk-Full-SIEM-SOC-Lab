# 🧩 Lab 4 — Setting Up Splunk Universal Forwarder (Linux)

In this lab, I set up the **Splunk Universal Forwarder** on the Linux server to forward logs to the main Splunk Enterprise instance.  
The Universal Forwarder is a lightweight Splunk agent designed to collect and send data securely to an indexer or another forwarder.

---

## ⚙️ Step 1: Understanding Splunk Forwarders

Splunk provides two main types of forwarders:

- **Heavy Forwarder:** Used when log data needs to be filtered or parsed before forwarding.  
- **Universal Forwarder:** A lightweight agent that forwards logs without local indexing or filtering.  

For this task, I used the **Universal Forwarder** to ingest logs from the Linux machine into the Splunk instance.

The latest version at the time of this setup was **9.0.3**.

---

## ⚙️ Step 2: Locate the Forwarder Package

The forwarder installer was already available in the lab environment under:

~/Downloads/splunk/


Before starting the installation, I switched to root privileges:

```bash
sudo su
```

Then verified the files:

ls

Output included:

splunk_installer.tgz
splunkforwarder.tgz

⚙️ Step 3: Install the Forwarder

I extracted and installed the Universal Forwarder using the following command:

tar xvzf splunkforwarder.tgz

This created a new folder named splunkforwarder/, containing all the binaries and configuration files.

Next, I moved the folder to the /opt/ directory:

mv splunkforwarder /opt/

⚙️ Step 4: Start the Splunk Forwarder

I navigated to the forwarder’s binary directory and started the service with the license acceptance flag:

cd /opt/splunkforwarder
./bin/splunk start --accept-license

As this was the first startup, I was prompted to create admin credentials:

Username: splunkadmin
Password: ********

During initialization, the system detected that port 8089 was already in use and asked to use an alternate port.
I set the management port to 8090.

After configuration, Splunk confirmed that the Universal Forwarder was running successfully.

Figure 1 — Overview of Splunk Universal Forwarder setup.


Figure 2 — Extracting and moving the forwarder directory.


Figure 3 — Creating credentials and running the forwarder on port 8090.

✅ Outcome

Installed and configured the Splunk Universal Forwarder on Linux.

Successfully created admin credentials for the forwarder instance.

Verified the forwarder service is running on port 8090.

Prepared for the next step — configuring the forwarder to send logs to the Splunk indexer.

# 🧩 Lab 4 — Setting Up Splunk Universal Forwarder and Ingesting Linux Logs

In this lab, I set up the **Splunk Universal Forwarder** on a Linux machine and configured it to forward system logs into the main **Splunk Enterprise** instance for analysis.  
This setup demonstrates end-to-end data ingestion — from log forwarding to visualization in Splunk.

---

## ⚙️ Step 1: Understanding Splunk Forwarders

Splunk forwarders are responsible for sending data from endpoints to the Splunk indexer.  
There are two main types of forwarders:

- **Heavy Forwarder** — Parses, filters, and modifies log data before sending it to Splunk.
- **Universal Forwarder** — A lightweight agent that forwards raw logs without parsing or indexing.

In this setup, I used the **Universal Forwarder (v9.0.3)** for Linux.

---

## ⚙️ Step 2: Locate and Install the Forwarder

The forwarder installer was pre-downloaded in the following directory:

~/Downloads/splunk/

mathematica
Copy code

First, I verified the files:

```bash
ls

```
Output:

Copy code
splunk_installer.tgz
splunkforwarder.tgz
Then switched to root privileges and extracted the forwarder:

bash
Copy code
sudo su
tar xvzf splunkforwarder.tgz
mv splunkforwarder /opt/
Next, I started the forwarder and accepted the license:

bash
Copy code
cd /opt/splunkforwarder
./bin/splunk start --accept-license
I created admin credentials and assigned a custom management port 8090, since port 8089 was already in use.




⚙️ Step 3: Configure Splunk to Receive Data
Now that the forwarder is running, the Splunk Enterprise instance must be configured to receive incoming data.

Navigate in Splunk Web to:

nginx
Copy code
Settings → Forwarding and receiving → Configure receiving
Then add a new receiving port — the default port is 9997.


After saving, port 9997 becomes active and is ready to accept data from forwarders.

⚙️ Step 4: Create a Custom Index
Next, I created a dedicated index called Linux_host to store incoming logs.

Path:

pgsql
Copy code
Settings → Indexes → New Index
Name the new index:

nginx
Copy code
Linux_host
Click Save to finalize.



⚙️ Step 5: Configure the Forwarder Output
On the Linux host, I configured the Universal Forwarder to send data to the Splunk instance’s receiving port.

Command executed from:

bash
Copy code
/opt/splunkforwarder/bin
bash
Copy code
./splunk add forward-server 10.48.142.158:9997
The command successfully added the forwarder target:

nginx
Copy code
Added forwarding to: 10.48.142.158:9997
⚙️ Step 6: Specify Log Sources
Linux stores most system logs under /var/log/.
For this lab, I chose to monitor syslog and send it to the Linux_host index.

bash
Copy code
./splunk add monitor /var/log/syslog -index Linux_host
Result:

nginx
Copy code
Added monitor of '/var/log/syslog'.
⚙️ Step 7: Verify Configuration in inputs.conf
I checked the inputs.conf file to confirm the monitored log source and index mapping.

Path:

swift
Copy code
/opt/splunkforwarder/etc/apps/search/local
Commands:

bash
Copy code
ls
cat inputs.conf
Output:

ini
Copy code
[monitor:///var/log/syslog]
disabled = false
index = Linux_host

⚙️ Step 8: Generate and Verify Log Data
To simulate live log data, I used the logger utility to create a test message inside syslog:

bash
Copy code
logger "coffely-has-the-best-coffee-in-town"
Verified entry with:

bash
Copy code
tail -1 /var/log/syslog
Then confirmed it appeared in Splunk under the index Linux_host.



✅ Outcome
Successfully installed and configured Splunk Universal Forwarder on Linux.

Configured Splunk Enterprise to receive data on port 9997.

Created a custom Linux_host index for segregated log storage.

Monitored /var/log/syslog and verified log forwarding through the Splunk Search dashboard.

Confirmed successful ingestion and visualization of test log data.

🔚 Summary
This lab established the foundation for log collection and centralization using Splunk.
I now have a fully functional setup where Linux logs are continuously forwarded to Splunk for real-time monitoring and analysis.




