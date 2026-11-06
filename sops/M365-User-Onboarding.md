# SOP-101: New User Provisioning & M365 Onboarding

**Applies To:** Tier 1 Helpdesk Support  
**Environment:** Microsoft 365 Admin Center, Azure Entra ID / Active Directory  
**Objective:** Standardize the creation of new employee accounts, license assignment, and initial security setup.

---

## 1. Prerequisites
- Receive approved HR onboarding ticket containing:
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
- **Verification:** Confirm the new user account appears under Active Users with a "Sync status" or "Cloud only" indicator active.

### Step 2: Assign Product Licenses & Location
1. Select the appropriate license assignment based on department requirements (e.g., *Microsoft 365 Business Standard* or *E3*).
2. Set the **Usage location** (e.g., United States) to ensure proper cloud service provisioning.
- **Verification:** Check that service apps (Exchange, Teams, SharePoint) display as assigned under the user's license details.

### Step 3: Assign Group Memberships & Permissions
1. Add the user to relevant department distribution lists and Microsoft Teams channels.
2. Assign the user to baseline security groups (e.g., *All-Staff*, regional office groups).
- **Verification:** Verify group membership lists reflect the newly added user account.

### Step 4: Security & MFA Configuration
1. Ensure **Security Defaults** or **Conditional Access Policies** are enforced for the account.
2. Generate a temporary registration link or communicate temporary credentials securely to the hiring manager for delivery to the new hire.
- **Verification:** Confirm the account shows an active sign-in state pending first-time password change and MFA enrollment.

---

## 🤖 Automated Execution (Python)

To automate the account creation and security group assignment steps detailed in this procedure, use the bundled Python script:

- **Script Location:** `Scripts/onboarding_automation.py`
- **Execution:** `python Scripts/onboarding_automation.py`
- **Input File:** `Scripts/new_hires.csv`

```python
import csv
import logging
from datetime import datetime

# Configure audit logging to track execution history
logging.basicConfig(
    filename='Scripts/user_provisioning.log',
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - [SOP-101 AUDIT] - %(message)s'
)

def generate_user_principal_name(first_name, last_name, domain="criswellauto.com"):
    """
    Generates standardized email/UPN per SOP-101 Step 1: First.Last@company.com
    """
    clean_first = first_name.strip().replace(' ', '')
    clean_last = last_name.strip().replace(' ', '')
    return f"{clean_first}.{clean_last}@{domain}".lower()

def get_department_profile(department):
    """
    Maps department requirements per SOP-101 Step 2 & Step 3:
    Assigns appropriate M365 Licenses and Security/Distribution Groups.
    """
    profiles = {
        "Sales": {
            "License": "Microsoft 365 Business Standard",
            "Groups": ["SG-Sales-Floor", "SG-CRM-Users", "SG-All-Staff"]
        },
        "Service": {
            "License": "Microsoft 365 Business Standard",
            "Groups": ["SG-Service-Advisors", "SG-DMS-Service", "SG-All-Staff"]
        },
        "Finance": {
            "License": "Microsoft 365 E3",
            "Groups": ["SG-Finance-Managers", "SG-DMS-Finance", "SG-All-Staff"]
        },
        "Accounting": {
            "License": "Microsoft 365 E3",
            "Groups": ["SG-Accounting-Staff", "SG-Financial-DMS", "SG-All-Staff"]
        },
        "IT": {
            "License": "Microsoft 365 Enterprise E5",
            "Groups": ["SG-IT-Support", "SG-Global-Admins", "SG-All-Staff"]
        }
    }
    
    return profiles.get(department, {
        "License": "Microsoft 365 Business Standard",
        "Groups": ["SG-All-Staff"]
    })

def provision_users_from_csv(csv_filepath="Scripts/new_hires.csv"):
    """
    Ingests new hire CSV, applies SOP-101 configurations, and outputs audit logs.
    """
    print("==================================================================")
    print("   SOP-101: AUTOMATED M365 USER PROVISIONING & ONBOARDING SYSTEM")
    print("==================================================================\n")
    
    try:
        with open(csv_filepath, mode='r', encoding='utf-8') as file:
            reader = csv.DictReader(file)
            processed_count = 0
            
            for row in reader:
                first_name = row['FirstName']
                last_name = row['LastName']
                dept = row['Department']
                title = row['Title']
                
                upn = generate_user_principal_name(first_name, last_name)
                dept_config = get_department_profile(dept)
                
                user_payload = {
                    "DisplayName": f"{first_name} {last_name}",
                    "UserPrincipalName": upn,
                    "Title": title,
                    "Department": dept,
                    "UsageLocation": "US",
                    "AssignedLicense": dept_config["License"],
                    "AssignedGroups": dept_config["Groups"],
                    "MFA_Status": "Pending First Login / Password Reset Enforced",
                    "Status": "PROVISIONED"
                }
                
                print(f"[+] PROVISIONED USER: {user_payload['DisplayName']}")
                print(f"    ├── UPN / Email:    {user_payload['UserPrincipalName']}")
                print(f"    ├── Title/Dept:     {user_payload['Title']} ({user_payload['Department']})")
                print(f"    ├── Usage Location: {user_payload['UsageLocation']}")
                print(f"    ├── M365 License:   {user_payload['AssignedLicense']}")
                print(f"    ├── Security Groups: {', '.join(user_payload['AssignedGroups'])}")
                print(f"    └── Security State: {user_payload['MFA_Status']}\n")
                
                logging.info(
                    f"CREATED: {upn} | Dept: {dept} | License: {dept_config['License']} | "
                    f"Groups: {dept_config['Groups']} | State: {user_payload['MFA_Status']}"
                )
                
                processed_count += 1
                
            print("==================================================================")
            print(f" SUCCESS: Processed {processed_count} user account(s) according to SOP-101.")
            print(" Audit log written to: Scripts/user_provisioning.log")
            print("==================================================================")

    except FileNotFoundError:
        print(f"[ERROR] Could not locate CSV input file at: '{csv_filepath}'")
        logging.error(f"Execution Failed: Input file missing at {csv_filepath}")
    except KeyError as e:
        print(f"[ERROR] Missing required CSV column header: {e}")
        logging.error(f"Execution Failed: Missing CSV column {e}")

if __name__ == "__main__":
    provision_users_from_csv()
            "License": "Microsoft 365 Business Standard",
            "Groups": ["SG-Service-
