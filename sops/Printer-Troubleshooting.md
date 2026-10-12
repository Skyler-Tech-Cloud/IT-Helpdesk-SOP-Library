# SOP-202: Network Printer Spooler & Driver Resolution

**Applies To:** Tier 1 Helpdesk Support  
**Environment:** Windows 10/11, Network Print Servers  
**Objective:** Resolve common local print queue jams, offline printer states, and driver errors.

---

## 1. Initial Assessment
* Ask the user:
  * *"Is the printer showing offline, or is the print job sitting in the queue with an error?"*
  * *"Is this affecting just your computer, or everyone in your office/floor?"*

---

## 2. Step-by-Step Troubleshooting Workflow

### Step 1: Check Connection & Restart Print Spooler Service
If print jobs are stuck or failing to send, reset the local print service:
1. Open **Services.msc** via the Windows Run dialog (`Win + R`).
2. Scroll down to **Print Spooler**, right-click, and select **Stop**.
3. Open File Explorer and navigate to: `C:\Windows\System32\spool\PRINTERS`
4. Delete all files inside this folder (these are corrupted/stuck print jobs).
5. Return to **Services.msc**, right-click **Print Spooler**, and select **Start** (ensure startup type is set to *Automatic*).

### Step 2: Re-add Network Printer via Print Server
1. Go to **Settings** ➔ **Bluetooth & devices** ➔ **Printers & scanners**.
2. Locate the problematic printer and click **Remove device**.
3. Click **Add device** to search for and reinstall the network printer via the corporate print server.

---

## 3. Ticket Closure
* Print a test page successfully and confirm with the user before closing the ticket.
