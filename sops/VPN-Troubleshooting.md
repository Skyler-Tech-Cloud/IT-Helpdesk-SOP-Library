# SOP-201: VPN & Remote Access Connectivity Troubleshooting

**Applies To:** Tier 1 Helpdesk Support  
**Environment:** Windows 10/11, Corporate VPN Client  
**Objective:** Provide a systematic methodology for resolving remote user connection failures.

---

## 1. Initial Assessment & User Clarification
* Ask the user: 
  * *"What exact error message or code are you seeing?"*
  * *"Were you able to connect successfully previously, or is this your first time?"*
  * *"Are you connected to a stable home Wi-Fi or cellular hotspot?"*
* **Scope Check:** Determine if the issue affects a single user or multiple users (which may indicate a gateway or server-side outage).

---

## 2. Step-by-Step Troubleshooting Workflow

### Step 1: Physical & Network Layer Check
1. Verify the user has active local internet access by opening a public browser page (e.g., browsing a non-company site).
2. Ensure **Airplane Mode** is toggled **Off**.
3. If on Wi-Fi, advise the user to toggle Wi-Fi off and on, or restart their router/modem if necessary.

### Step 2: Client Application Reset
1. Completely close the corporate VPN client application (check system tray / task manager to ensure no background processes are hung).
2. Relaunch the VPN client as Administrator.
3. Re-enter credentials, ensuring multi-factor authentication (MFA) prompts are approved promptly.

### Step 3: Network Adapter & DNS Flush (Command Line)
If the connection still fails, open **Command Prompt as Administrator** and execute standard diagnostic commands:
cmd
ipconfig /flushdns
ipconfig /release
ipconfig /renew

### Step 4: Credential Manager Verification
1. Verify if the user recently changed their domain password. An outdated cached credential in Windows Credential Manager will cause immediate authentication rejections.
2. Open Windows Credential Manager ➔ Windows Credentials ➔ Remove any stored legacy entries related to the VPN server address.

---

## 3. Escalation Criteria
* If all local steps fail and other users on the network are experiencing the same issue, escalate immediately to Network Infrastructure Tier 2 to check gateway status.
* If individual authentication fails repeatedly despite a confirmed password reset, escalate to Identity & Access Management (IAM).

---

## 4. Documentation & Ticket Closure
* Log all diagnostic steps taken in the IT ticketing system.
* Document the resolution code and confirm user productivity before setting the ticket status to Resolved.
