# SOP-101: New User Provisioning & M365 Onboarding

**Applies To:** Tier 1 Helpdesk Support  
**Environment:** Microsoft 365 Admin Center, Azure Entra ID / Active Directory  
**Objective:** Standardize the creation of new employee accounts, license assignment, and initial security setup.

---

## 1. Prerequisites
* Receive approved HR onboarding ticket containing:
  * Full legal name
  * Job title / Department
  * Manager name
  * Start date

---

## 2. Step-by-Step Provisioning Process

### Step 1: Create User Account in M365 Admin Center
1. Log into the **Microsoft 365 Admin Center** as an Administrator.
2. Navigate to **Users** ➔ **Active users** ➔ Click **Add a user**.
3. Enter the user's first name, last name, and auto-generate or create a standardized display name (e.g., *First.Last@company.com*).
4. Set the initial password to require a reset upon first login.
* **Verification:** Confirm the new user account appears under Active Users with a "Sync status" or "Cloud only" indicator active.

### Step 2: Assign Product Licenses & Location
1. Select the appropriate license assignment based on department requirements (e.g., *Microsoft 365 Business Standard* or *E3*).
2. Set the **Usage location** (e.g., United States) to ensure proper cloud service provisioning.
* **Verification:** Check that service apps (Exchange, Teams, SharePoint) display as assigned under the user's license details.

### Step 3: Assign Group Memberships & Permissions
1. Add the user to relevant department distribution lists and Microsoft Teams channels.
2. Assign the user to baseline security groups (e.g., *All-Staff*, regional office groups).
* **Verification:** Verify group membership lists reflect the newly added user account.

### Step 4: Security & MFA Configuration
1. Ensure **Security Defaults** or **Conditional Access Policies** are enforced for the account.
2. Generate a temporary registration link or communicate temporary credentials securely to the hiring manager for delivery to the new hire.
* **Verification:** Confirm the account shows an active sign-in state pending first-time password change and MFA enrollment.

---

## 3. Verification & Handover
* Send a welcome email to the manager confirming account creation and temporary credentials.
* Schedule a 15-minute Day-1 check-in to assist the new user with initial MFA setup and device sign-in.
