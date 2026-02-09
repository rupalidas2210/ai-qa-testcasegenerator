
# Spectrum App – Comprehensive Functional Requirements (Employee Login, Password Flows, Facility Configuration, Device Setup, Permissions, Scanner Pairing)

## 1. Overview
This document consolidates **all flows extracted from the provided Figma text**, including:
- Employee Login
- Password Expiration & Password Errors
- Temporary Password & Change Password Flow
- Forgot Password Flow
- Facility ID Configuration & Change Facility Flow
- Device Permissions Prompts
- Device Not Checked Out Flow
- First-Time Setup
- Scanner Pairing
- Battery Alerts
- App Navigation

---

# 2. Employee Login Flow

## 2.1 Login Screen Elements
- User ID input
- Password input (masked)
- Log In button
- Exit button
- Error messages displayed inline or as banners
- Alerts such as password expiration
- Version label (v1.0 / Spectrum 1.0.0)

## 2.2 Password Expiration Alerts
- Alert appears when password expires in **10 days** (orange).
- Alert appears when password expires in **5 days** (red).
- Alert can be dismissed but no actions may be taken from within the alert.
- Alert reappears after every login until password is changed.

## 2.3 Incorrect Password Attempts
- Error states:
  - "Incorrect password. 3 sign‑in attempts left."
  - "Incorrect password. 2 sign‑in attempts left."
  - "Incorrect password. 1 sign‑in attempt left."
- After third failed attempt:
  - User gets locked out.
  - Message: "Access denied. Too many failed log-in attempts. Find a facility manager to reset your password."
  - Facility manager receives alert and resets password to temporary value.

## 2.4 Account Lockout States
- Standard lockout: "Your account has been locked. Find a facility manager to reset your password."
- Expired password lockout: "Account locked – expired password. Find a facility manager to reset your password."
- Device not checked out: "This device is not checked out to you. Please find a facility manager to check out this device."

---

# 3. Temporary Password + Change Password Flow

## 3.1 Conditions
- When locked out, user receives temporary password from manager.
- Logging in with this temporary password **forces** Change Password process.

## 3.2 Change Password Screen
Fields:
- User ID
- New Password
- Confirm Password
- SAVE button (disabled until valid)

Password Validity Rules:
- Must contain **10–128 characters**
- Must contain at least:
  - **1 uppercase letter**
  - **1 lowercase letter**
  - **2 numbers**
  - **2 special characters**
- Disallowed symbols: `# + & |`
- Cannot contain the **User ID** or **User’s name**
- Cannot reuse passwords from last **6 generations (~18 months)**

## 3.3 Password Mismatch / Error States
- "Passwords don’t match."
- "Passwords cannot contain User ID or user’s name."
- Specific rule violations (uppercase, lowercase, numbers, specials, banned symbols).

## 3.4 Successful Password Update
- Message: **"Password changed successfully."**
- User must re-login using new password.

## 3.5 Edge Case – Closing App
- If user closes app during Change Password flow:
  - Temporary password still works.
  - Flow restarts from beginning.

---

# 4. Forgot Password Flow
- User attempts login.
- After lockout, associate retrieves temporary password from manager.
- Manager resets password and marks task complete.
- User logs in with temporary password → begins Change Password flow.

---

# 5. Facility Configuration (Manual Flow)

## 5.1 First-Time Setup
If device has **no facility configured**:
- User is prompted: "A facility has not been configured yet. Please set up a facility to continue."
- User must type **3-letter facility ID** manually.
- Must press ENTER to accept.

## 5.2 Facility ID Rules
- Facility ID must be **3 characters**.
- Error: "Facility ID should be 3 characters."
- Confirmation step: User enters ID again.
- If mismatch: "Facility IDs do not match."
- If incorrect/not recognized: "Facility not recognized."
- If user doesn’t have access: "User does not have access to this facility."
- If device already configured to same facility: "Device is already configured to this facility."

## 5.3 Successful Configuration
Messages:
- "Facility ID successfully configured to device."
- "Device configured to Zone successfully."
- Facility name (ex: Braintree, MA (GDT)) displayed.
- Device info such as MAC, IP, server shown.

---

# 6. Device Settings & Permissions

## 6.1 Android / Native Permission Modals
Device will show **native OS modals**, not Spectrum UI.
Prompts include:
- "Allow Spectrum to access photos, media, and files?"
- "Allow Spectrum to take pictures and record video?"
Options:
- Allow
- Deny
- Don’t ask again

---

# 7. Scanner Pairing Flow

## 7.1 Accessing Scanner Pairing
- From top status bar, select Bluetooth icon.
- Screen shows:
  - "Scanner connected" OR
  - "No scanner connected"
- If not connected, select **PAIR** to display pairing barcode.
- User scans barcode using handheld scanner.
- After connection, user proceeds to login.

---

# 8. Battery Alerts

## 8.1 Battery Levels
- If battery <20%:
  - Display "Low Battery" state.
- If battery ≥20%:
  - Display normal battery indicator (example: 56%).

---

# 9. App Navigation After Login
After successful login, user sees list of apps in Spectrum:
- Shop
- Expedite
- Staging
- Audit
- Load
- Verify
- Equipment
- Inventory
- Cycle Count
- Adjust Inventory
- Slotting
- Replenish
- Lean
- Returns
- P‑Cube
- Prep
- Putaway

Side Menu Always Includes:
- About
- Change Password
- Scanner Pairing
- Logout

---

# 10. Complete Error Message Library
- "Incorrect password. 3 sign-in attempts left."
- "Incorrect password. 2 sign-in attempts left."
- "Incorrect password. 1 sign-in attempt left."
- "Access denied. Too many failed log-in attempts."
- "Your account has been locked. Find a facility manager to reset your password."
- "Account locked – expired password. Find a facility manager to reset your password."
- "This device is not checked out to you."
- "Device is already configured to this facility."
- "Facility ID should be 3 characters."
- "Facility IDs do not match."
- "User does not have access to this facility."
- "Passwords don’t match."
- "Passwords cannot contain User ID or user’s name."
- Rule errors for uppercase/lowercase/numbers/special characters.

---

# End of Document
