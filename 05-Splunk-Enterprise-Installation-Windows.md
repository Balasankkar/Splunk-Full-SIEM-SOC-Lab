# 🧩 Lab 5 — Installing Splunk Enterprise on Windows

In this lab, I installed and configured **Splunk Enterprise** on a Windows virtual machine.  
This step expands on the previous Linux-based setup by adding a Windows environment to collect and analyze system logs, application data, and web activity.

---

## ⚙️ Step 1: Overview

The objective of this task was to:
- Install **Splunk Enterprise 9.0.4** on Windows.
- Set up an administrator account.
- Launch and verify access to the Splunk Web interface.
- Prepare for configuring a **Windows Universal Forwarder** in the next lab.

---

## ⚙️ Step 2: Download Splunk Enterprise

The installer was obtained from the official Splunk website.

**Steps:**
1. Logged into the [Splunk download portal](https://www.splunk.com/en_us/download.html).  
2. Selected the **Windows 64-bit** package (`.msi`).
3. Version used: **9.0.4**.

The installer was pre-downloaded into the `Downloads` folder for convenience.

```bash
C:\Users\<username>\Downloads\

```


⚙️ Step 3: Run the Splunk Installer
I launched the .msi installer by double-clicking it and accepted the default settings.

Default installation path:

makefile
Copy code
C:\Program Files\Splunk
Installer steps:

Checked “Accept the License Agreement”.

Chose to install Splunk Enterprise for all users (Local System account).

Selected the default installation directory.



⚙️ Step 4: Create an Administrator Account
During setup, I created the Splunk admin user:

makefile
Copy code
Username: Analyst
Password: ********
This account will be used to log into Splunk Web and manage dashboards, data inputs, and searches.


⚙️ Step 5: Installation Progress and Completion
The installer verified dependencies and installed Splunk Enterprise.
The setup process took approximately 5–8 minutes.

Once complete, the installer displayed the success message:

nginx
Copy code
Splunk Enterprise was successfully installed.


⚙️ Step 6: Access the Splunk Web Interface
By default, Splunk Web runs on port 8000.

To access the instance, I opened a browser and entered:

cpp
Copy code
http://127.0.0.1:8000
or (if connected to VPN)

cpp
Copy code
http://10.48.184.120:8000
I then logged in with the previously created administrator credentials:

makefile
Copy code
Username: Analyst
Password: ********

⚙️ Step 7: Explore the Splunk Dashboard
After logging in, the Splunk Enterprise dashboard loaded successfully, confirming a functional installation.

From here, I can:

Add and configure data inputs,

Create dashboards,

Install apps,

Or connect forwarders from other systems.


✅ Outcome
Successfully installed Splunk Enterprise 9.0.4 on Windows 10.

Created and verified an administrator account.

Confirmed Splunk Web access on port 8000.

Ready for the next step: installing a Windows Universal Forwarder and forwarding Windows Event Logs into Splunk.

🔜 Next Step
Proceed to Lab 6 — Configuring the Windows Universal Forwarder, where the forwarder will be set up to transmit Windows Event Logs (System, Security, and Application) to this Splunk Enterprise instance for centralized analysis.
