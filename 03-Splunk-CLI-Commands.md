# 🧩 Lab 3 — Exploring Splunk Through the CLI

After successfully installing and running **Splunk Enterprise** on the Linux server, I explored how to manage and interact with Splunk using its **Command-Line Interface (CLI)**.  
The CLI allows administrators to perform key operations such as starting, stopping, restarting, and monitoring the Splunk service — as well as executing searches directly from the terminal.

---

## ⚙️ Step 1: Navigating to Splunk’s CLI

All Splunk administrative commands are executed from within the Splunk installation directory:


I switched to this directory before running any CLI commands:

```bash
cd /opt/splunk/bin

```

## ⚙️ Step 2: Common Splunk CLI Commands
1. Start Splunk

The splunk start command initializes the Splunk service and makes it accessible via the web interface (http://coffely:8000).


```bash

./splunk start

```
This command launches the necessary processes and opens key ports:

HTTP: 8000

Management: 8089

App Server: 8065

KV Store: 8191

Once startup checks are complete, Splunk displays:

```bash

The Splunk web interface is at http://coffely:8000

```

2. Stop Splunk

The splunk stop command stops all running Splunk services safely.

```bash

./splunk stop

```
This ensures all background Splunk processes are properly terminated.

3. Restart Splunk

Used when changes are made to configuration files or apps.
It first stops all running processes and then starts them again.

```bash

./splunk status

```
Example output: 

```bash

splunkd is running (PID: 2158)
splunk helpers are running (PIDs: 2159 2301 2351 2437)

```

5. Add One-Shot Event

The splunk add oneshot command is used to manually add a single event to the Splunk index — helpful for testing log ingestion.

```bash

./splunk add oneshot

```

6. Search Data via CLI

Splunk’s search command allows quick searches directly from the terminal using Splunk’s Search Processing Language (SPL).

```bash

./splunk search coffely

```

7. Help Command

The splunk help command displays all available CLI options and syntax information.

```bash

./splunk help

```

This is the most important command for troubleshooting or exploring available functionality.


Figure 1 — Starting the Splunk service via CLI.


Figure 2 — Using stop, restart, and status commands.


Figure 3 — Performing searches and viewing help options from the CLI.

✅ Outcome

Learned key Splunk CLI commands for managing services and performing searches.

Verified that Splunk can be controlled entirely through the terminal.

Successfully ran test searches and confirmed system operation via CLI.

🔜 Next Step

Proceed to Lab 4: Installing and Configuring the Splunk Universal Forwarder —
where I’ll deploy a lightweight forwarder on a remote system to send Linux logs to this Splunk instance for centralized monitoring.

