# SOP-102: Account Lockout Triage & Self-Service MFA Reset

**Applies To:** Tier 1 Helpdesk Support  
**Environment:** Microsoft Entra ID / Azure AD, M365 Admin Center  
**Objective:** Safely verify user identity and resolve account lockouts or multi-factor authentication (MFA) registration blocks.

---

## 1. Identity Verification (Crucial Security Step)
- **Never** reset a password or MFA method without verifying the user's identity via an out-of-band secure method (e.g., verifying their employee ID, direct manager confirmation, or a secure video/phone callback to their official office number).

---

## 2. Step-by-Step Resolution Workflow

### Step 1: Check Account Status
1. Navigate to **Microsoft 365 Admin Center** ➔ **Users** ➔ **Active users**.
2. Locate the user and check if the account is blocked due to repeated failed login attempts.
3. If blocked, uncheck "Block this user from signing in" or clear the sign-in session.

### Step 2: Temporary Password Reset
1. Click **Reset password** in the user's profile panel.
2. Select "Auto-generate password" or create a temporary complex password.
3. Check the box to **"Require this user to change their password when they first sign in."**

### Step 3: Reset MFA Authentication Methods
If the user lost their phone or got a new device and cannot pass MFA:
1. Go to the user's account details ➔ **Authentication methods**.
2. Click **Require re-register MFA**. This revokes their existing tokens and prompts them to set up a new authenticator app or phone number upon their next login.

---

## 3. Common Exceptions & Troubleshooting

* **Immediate Re-Lockout Loop:** If an account locks out again immediately after a password reset, it is almost always caused by a background mobile device (smartphone mail app) or Outlook client caching old credentials. 
  * *Resolution:* Instruct the user to temporarily close Outlook and disconnect/pause active email sync on mobile devices until the new password is updated everywhere.
* **Risk-Based Sign-In Blocks:** If Entra ID flags the login as "Risky Sign-In" due to unusual location or travel patterns, a standard password reset may not clear the block.
  * *Resolution:* Review the Entra ID Protection sign-in logs and dismiss user risk if identity is confirmed, or escalate to Tier 2.

---

## 4. Escalation Matrix

* **Tier 1 (Helpdesk):** Out-of-band identity verification, account unblocking, temporary password generation, and MFA re-registration triggers.
* **Tier 2 / SysAdmin:** Risk-based sign-in blocks, Azure AD Identity Protection alerts, persistent sync loops, or Conditional Access Policy overrides.

---

## 5. Documentation & Ticket Closure
- Log the specific identity verification method and exception codes used in the ticket notes.
- Advise the user to test their login and confirm they can access corporate resources successfully before closing the ticket.
