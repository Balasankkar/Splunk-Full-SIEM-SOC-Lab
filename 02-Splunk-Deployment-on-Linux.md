# 🧩 Lab 2 — Splunk Deployment on Linux Server

In this task, I deployed **Splunk Enterprise** on the Linux (Ubuntu) server and verified that it was running successfully through the web interface.  
The goal of this lab was to install Splunk, start the service, and access the Splunk dashboard to ensure that the platform is ready for log ingestion and monitoring.

---

## ⚙️ Step 1: Splunk Installer Setup

Splunk supports multiple operating systems, but in this lab, the deployment focused on **Ubuntu Linux**.  
The required installation files — `splunk_installer.tgz` and `splunkforwarder.tgz` — were already available in the lab environment at the following path:


Before starting the installation, I switched to the root user to ensure sufficient permissions for setup:

## ⚙️ Step 2: Extract and Install Splunk

To begin the installation, I extracted the Splunk installer package using the following command:

tar xvzf splunk_installer.tgz

This command unpacked the archive and created a new folder named splunk/, containing all required binaries and configuration files.
Next, I moved the Splunk directory to the /opt/ directory, which is a standard location for optional software installations on Linux:

mv splunk /opt/

## ⚙️ Step 3: Start Splunk Service

Once installation was complete, I started Splunk for the first time using:

cd /opt/splunk/bin
./splunk start --accept-license

During the initial startup, Splunk prompted for the creation of an administrator account, which will be used to access the Splunk Web UI.

I created the following credentials:

Username: splunkadmin

Password: custom secure password

Splunk then initialized its web server and confirmed successful startup with the following message:

The Splunk web interface is at http://coffely:8000

## ⚙️ Step 4: Access Splunk Web Interface

Once the service was running, I accessed the Splunk dashboard through the browser within the lab environment by visiting:

http://coffely:8000

Using the admin credentials created earlier, I logged in successfully to the Splunk Enterprise dashboard, confirming that the deployment was successful and ready for further configuration.

Figure 1 — Splunk installer setup and extraction on Ubuntu server.


Figure 2 — Extracting and moving Splunk directory to /opt/.


Figure 3 — Starting Splunk service and creating admin credentials.


Figure 4 — Accessing the Splunk web interface at http://coffely:8000
.

✅ Outcome

Successfully installed and configured Splunk Enterprise on the Linux server.

Verified successful startup and web interface access.

Created an administrator account (splunkadmin) for dashboard management.

Confirmed readiness for log ingestion and monitoring in the next lab.


