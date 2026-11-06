#import csv
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
    
    # Default fallback profile for unmapped departments
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
        with open(csv_filepath, mode='r', encoding='utf-8') as file
