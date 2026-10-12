SOP-203: Local Area Network & Wi-Fi Troubleshooting
Applies To: Tier 1 Helpdesk Support

Environment: Windows 10/11, Corporate Wi-Fi / Ethernet Infrastructure

Objective: Resolve local network adapter failures, IP lease drops, and intermittent gateway disconnects.

1. Initial Assessment
Ask the user:

"Are you connected via Wi-Fi or an Ethernet cable?"

"Is your web browser able to reach internal corporate sites, external public sites, or neither?"

2. Step-by-Step Troubleshooting Workflow
Step 1: Physical Link & Adapter Verification
Verify the physical Ethernet cable is securely clicked into both the endpoint and the wall jack / dock, or ensure Wi-Fi is toggled on.

Open Device Manager ➔ Expand Network adapters ➔ Check for yellow warning triangles indicating driver faults.

Verification: Confirm the adapter status shows "Enabled" and operating normally without driver errors.

Step 2: Release and Renew IP Address (Command Line)
If the local adapter cannot communicate with the default gateway:

Open Command Prompt as Administrator.

Run the following release and renew sequence:

DOS
ipconfig /release
ipconfig /renew
Verification: Confirm the command output returns a valid IPv4 address (e.g., 192.168.x.x or corporate subnet) rather than an APIPA address starting with 169.254.x.x.

Step 3: Reset TCP/IP Stack & Winsock
If network connectivity remains unstable:

In the elevated Command Prompt, execute:

DOS
netsh int ip reset
netsh winsock reset
Restart the computer when prompted.

Verification: Confirm network adapter packet counters increment normally and browser ping requests to 8.8.8.8 succeed after reboot.

3. Documentation & Ticket Closure
Document all executed network repair commands in the ticket notes and confirm stable web browsing with the user.

Copy 2: Paste into sops/User-Offboarding.md
SOP-103: Employee Termination & Account Offboarding
Applies To: Tier 1 / Tier 2 Helpdesk Support

Environment: Microsoft 365 Admin Center, Exchange Online

Objective: Securely disable departing employee access, preserve business data, and reassign mailbox resources.

1. Immediate Account Access Termination
Log into the Microsoft 365 Admin Center as an Administrator.

Navigate to Users ➔ Active users ➔ Select the departing employee.

Click Block sign-in to immediately prevent any further authentication attempts.

Revoke all active session tokens via the user's profile panel to force immediate sign-out across all devices and apps.

Verification: Confirm the user status reflects "Blocked from signing in".

2. Data Preservation & Mailbox Delegation
Convert the user mailbox to a Shared Mailbox to retain historical email access without requiring an active license.

Grant Full Access and Send As permissions to the department manager or designated successor.

Establish a OneDrive data retention hold and transfer ownership of critical shared documents to the manager's workspace.

Verification: Check that the mailbox type displays as "Shared" and delegation permissions appear correctly in the Exchange admin center.

3. License Reclamation
Remove all assigned Microsoft 365 product licenses from the offboarded user profile so they return to the organization's license pool for future onboarding.

Verification: Verify that available organization license counts increase by one.
