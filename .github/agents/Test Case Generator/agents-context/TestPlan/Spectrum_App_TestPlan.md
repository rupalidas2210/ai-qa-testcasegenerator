# Spectrum App - Comprehensive Test Plan

**Document Version:** 1.0  
**Date Created:** February 5, 2026  
**Project:** Spectrum App  
**Testing Scope:** Employee Login, Password Flows, Facility Configuration, Device Setup, Permissions, Scanner Pairing

---

## 1. Purpose and Quality Objectives

### 1.1 Testing Goals
- Ensure all Employee Login flows function correctly across all scenarios
- Validate password security policies and expiration mechanisms
- Verify facility configuration and device management workflows
- Confirm proper device permissions and scanner pairing functionality
- Achieve 100% requirements traceability with zero missing test scenarios
- Ensure error handling and validation messages are accurate and user-friendly

### 1.2 Success Criteria
- 100% RTM coverage with all requirements mapped to test scenarios
- All critical paths tested (login, password management, facility setup)
- Zero critical defects in production
- All error states properly validated
- Complete coverage of positive, negative, and edge case scenarios

### 1.3 Definition of Complete Coverage
- Every requirement has at least one mapped test scenario
- All user workflows have end-to-end test coverage
- All validation rules tested with valid and invalid inputs
- All error messages verified
- All state transitions validated
- All permission and access control scenarios tested

---

## 2. Scope

### 2.1 In-Scope Features
1. **Employee Login Flow**
   - User authentication (User ID and Password)
   - Login validation and error handling
   - Version display

2. **Password Management**
   - Password expiration alerts (10-day and 5-day warnings)
   - Failed login attempts tracking (3 attempts)
   - Account lockout mechanisms
   - Temporary password flow
   - Change password workflow
   - Password validation rules
   - Forgot password process

3. **Facility Configuration**
   - First-time facility setup
   - Manual 3-character facility ID entry
   - Facility ID validation and confirmation
   - Facility change workflow
   - Device zone configuration

4. **Device Permissions**
   - Android native permission modals
   - Photo/media/file access permissions
   - Camera and video recording permissions

5. **Scanner Pairing**
   - Bluetooth scanner connection status
   - Scanner pairing via barcode
   - Connection success/failure states

6. **Battery Alerts**
   - Low battery warning (<20%)
   - Battery level display

7. **App Navigation**
   - Post-login app list display
   - Side menu navigation
   - About, Change Password, Scanner Pairing, Logout options

### 2.2 Out-of-Scope
- Individual app functionality (Shop, Expedite, Staging, etc.) - testing limited to app list display only
- Backend API performance testing
- Database testing
- Network layer testing
- Specific device hardware testing beyond permissions
- Multi-language support (if not specified in requirements)

### 2.3 Assumptions
- Testing will be performed on Android devices
- Device has Bluetooth capability for scanner pairing
- Network connectivity is available
- Facility IDs are pre-configured in the backend system
- User accounts and permissions are set up in the backend

### 2.4 Constraints
- Testing dependent on backend API availability
- Scanner hardware required for pairing tests
- Physical Android device required for native permission testing

### 2.5 Dependencies
- Backend user authentication service
- Facility management system
- Password policy enforcement service
- Device management system
- Bluetooth scanner hardware

---

## 3. Requirements Traceability Matrix (RTM)

| Req ID | Requirement Description | Acceptance Criteria | Test Scenario IDs | Test Case IDs |
|--------|------------------------|---------------------|-------------------|---------------|
| REQ-001 | Login Screen UI Elements | Display User ID, Password, Log In, Exit buttons, error messages, version label | TS-001, TS-002 | TBD |
| REQ-002 | Password Expiration Alert (10 days) | Display orange alert when password expires in 10 days | TS-003 | TBD |
| REQ-003 | Password Expiration Alert (5 days) | Display red alert when password expires in 5 days | TS-004 | TBD |
| REQ-004 | Password Alert Dismissal | Alert can be dismissed but reappears on next login | TS-005 | TBD |
| REQ-005 | Failed Login Attempt 1 | Display "Incorrect password. 3 sign-in attempts left." | TS-006 | TBD |
| REQ-006 | Failed Login Attempt 2 | Display "Incorrect password. 2 sign-in attempts left." | TS-007 | TBD |
| REQ-007 | Failed Login Attempt 3 | Display "Incorrect password. 1 sign-in attempt left." | TS-008 | TBD |
| REQ-008 | Account Lockout After 3 Failures | Display "Access denied. Too many failed log-in attempts. Find a facility manager to reset your password." | TS-009 | TBD |
| REQ-009 | Facility Manager Alert on Lockout | Facility manager receives alert and can reset password | TS-010 | TBD |
| REQ-010 | Standard Account Lockout Message | Display "Your account has been locked. Find a facility manager to reset your password." | TS-011 | TBD |
| REQ-011 | Expired Password Lockout | Display "Account locked – expired password. Find a facility manager to reset your password." | TS-012 | TBD |
| REQ-012 | Device Not Checked Out | Display "This device is not checked out to you. Please find a facility manager to check out this device." | TS-013 | TBD |
| REQ-013 | Temporary Password Flow | Login with temporary password forces Change Password process | TS-014 | TBD |
| REQ-014 | Change Password Screen UI | Display User ID, New Password, Confirm Password, SAVE button (disabled until valid) | TS-015 | TBD |
| REQ-015 | Password Length Validation | Password must contain 10-128 characters | TS-016, TS-017, TS-018 | TBD |
| REQ-016 | Password Uppercase Requirement | Password must contain at least 1 uppercase letter | TS-019, TS-020 | TBD |
| REQ-017 | Password Lowercase Requirement | Password must contain at least 1 lowercase letter | TS-021, TS-022 | TBD |
| REQ-018 | Password Number Requirement | Password must contain at least 2 numbers | TS-023, TS-024 | TBD |
| REQ-019 | Password Special Character Requirement | Password must contain at least 2 special characters | TS-025, TS-026 | TBD |
| REQ-020 | Password Banned Symbols | Password cannot contain # + & \| symbols | TS-027, TS-028, TS-029, TS-030 | TBD |
| REQ-021 | Password User ID Restriction | Password cannot contain User ID | TS-031, TS-032 | TBD |
| REQ-022 | Password User Name Restriction | Password cannot contain User's name | TS-033, TS-034 | TBD |
| REQ-023 | Password History Check | Cannot reuse passwords from last 6 generations (~18 months) | TS-035, TS-036 | TBD |
| REQ-024 | Password Mismatch Error | Display "Passwords don't match." when New Password ≠ Confirm Password | TS-037 | TBD |
| REQ-025 | Password User ID/Name Error | Display "Passwords cannot contain User ID or user's name." | TS-038 | TBD |
| REQ-026 | Password Rule Violation Errors | Display specific error for each validation rule violation | TS-039 | TBD |
| REQ-027 | Successful Password Change | Display "Password changed successfully." and require re-login | TS-040 | TBD |
| REQ-028 | Change Password App Closure | Temporary password remains valid if app closed during change process | TS-041 | TBD |
| REQ-029 | Forgot Password Flow | User gets temporary password from manager after lockout | TS-042 | TBD |
| REQ-030 | First-Time Facility Setup | Prompt "A facility has not been configured yet. Please set up a facility to continue." | TS-043 | TBD |
| REQ-031 | Facility ID Manual Entry | User must type 3-letter facility ID and press ENTER | TS-044 | TBD |
| REQ-032 | Facility ID Length Validation | Display "Facility ID should be 3 characters." if not exactly 3 characters | TS-045, TS-046, TS-047 | TBD |
| REQ-033 | Facility ID Confirmation | User must enter Facility ID twice for confirmation | TS-048 | TBD |
| REQ-034 | Facility ID Mismatch Error | Display "Facility IDs do not match." when entries don't match | TS-049 | TBD |
| REQ-035 | Facility Not Recognized Error | Display "Facility not recognized." if ID doesn't exist in system | TS-050 | TBD |
| REQ-036 | Facility Access Denied | Display "User does not have access to this facility." | TS-051 | TBD |
| REQ-037 | Facility Already Configured | Display "Device is already configured to this facility." | TS-052 | TBD |
| REQ-038 | Successful Facility Configuration | Display "Facility ID successfully configured to device." | TS-053 | TBD |
| REQ-039 | Successful Zone Configuration | Display "Device configured to Zone successfully." | TS-054 | TBD |
| REQ-040 | Facility Name Display | Display facility name (e.g., "Braintree, MA (GDT)") | TS-055 | TBD |
| REQ-041 | Device Info Display | Display device MAC, IP, and server information | TS-056 | TBD |
| REQ-042 | Photo/Media Permission Prompt | Display "Allow Spectrum to access photos, media, and files?" with Allow/Deny/Don't ask again | TS-057 | TBD |
| REQ-043 | Camera Permission Prompt | Display "Allow Spectrum to take pictures and record video?" with Allow/Deny/Don't ask again | TS-058 | TBD |
| REQ-044 | Scanner Status Display | Display "Scanner connected" or "No scanner connected" | TS-059, TS-060 | TBD |
| REQ-045 | Scanner Pairing Access | Access scanner pairing via Bluetooth icon in status bar | TS-061 | TBD |
| REQ-046 | Scanner Pairing Barcode Display | Display pairing barcode when PAIR selected | TS-062 | TBD |
| REQ-047 | Scanner Connection Success | Connect scanner after barcode scan | TS-063 | TBD |
| REQ-048 | Low Battery Alert | Display "Low Battery" when battery <20% | TS-064 | TBD |
| REQ-049 | Battery Level Display | Display normal battery percentage when ≥20% | TS-065 | TBD |
| REQ-050 | App List Display | Display all 17 apps after successful login | TS-066 | TBD |
| REQ-051 | Side Menu Options | Display About, Change Password, Scanner Pairing, Logout in side menu | TS-067 | TBD |
| REQ-052 | Exit Button Functionality | Exit button closes login screen | TS-068 | TBD |
| REQ-053 | Password Masking | Password input field displays masked characters | TS-069 | TBD |
| REQ-054 | Successful Login | Valid credentials allow successful login and navigation to app list | TS-070 | TBD |

**Total Requirements:** 54  
**Total Test Scenarios:** 70+

---

## 4. System Overview and Test Boundaries

### 4.1 High-Level Architecture
```
┌─────────────────────────────────────────┐
│         Spectrum Mobile App             │
│  (Android UI - React Native/Native)     │
├─────────────────────────────────────────┤
│  ┌───────────┐  ┌──────────────────┐   │
│  │  Login    │  │  Facility Setup  │   │
│  │  Module   │  │  Module          │   │
│  └───────────┘  └──────────────────┘   │
│  ┌───────────┐  ┌──────────────────┐   │
│  │ Password  │  │  Scanner Pairing │   │
│  │ Management│  │  Module          │   │
│  └───────────┘  └──────────────────┘   │
└─────────────────────────────────────────┘
            ↓ API Calls
┌─────────────────────────────────────────┐
│      Backend Services (REST API)        │
├─────────────────────────────────────────┤
│  • Authentication Service               │
│  • User Management Service              │
│  • Password Policy Service              │
│  • Facility Management Service          │
│  • Device Management Service            │
└─────────────────────────────────────────┘
            ↓
┌─────────────────────────────────────────┐
│         Database Layer                  │
│  • User Accounts                        │
│  • Facility Configurations              │
│  • Device Registry                      │
│  • Password History                     │
└─────────────────────────────────────────┘
```

### 4.2 Data Flow
1. User enters credentials → UI validation → API call to Authentication Service
2. Backend validates against database → Returns success/failure + user context
3. Password expiration checked → Alert triggered if applicable
4. Facility configuration checked → Setup flow triggered if needed
5. Scanner status checked → Display connection status

### 4.3 External Dependencies
- **Android OS**: Native permission dialogs, Bluetooth stack
- **Backend REST API**: All authentication and configuration operations
- **Bluetooth Scanner**: Hardware device for pairing functionality
- **Network**: Required for all backend communication

### 4.4 Test Boundaries
- **In Boundary**: UI interactions, validation logic, workflow transitions, error handling, state management
- **Out of Boundary**: Backend API logic (black box), database operations, network infrastructure
- **Mocked Components**: Backend API responses (for isolated UI testing)
- **Real Components**: Android permissions, Bluetooth stack (for integration testing)

---

## 5. Feature and Business Rule Breakdown

### 5.1 Employee Login

#### Sub-Features
- User credential input (User ID, Password)
- Login validation
- Error display
- Version display
- Exit functionality

#### Business Rules
- BR-001: User ID is required (cannot be empty)
- BR-002: Password is required (cannot be empty)
- BR-003: Password input must be masked
- BR-004: Version label must display "v1.0" or "Spectrum 1.0.0"
- BR-005: Exit button must close the login screen
- BR-006: Login button triggers authentication

#### Field-Level Validations
| Field | Type | Mandatory | Format | Length | Special Rules |
|-------|------|-----------|--------|--------|---------------|
| User ID | Text | Yes | Alphanumeric | Variable | - |
| Password | Masked Text | Yes | Mixed | 10-128 | Must meet complexity rules |

#### State Transitions
```
[Not Logged In] → [Credentials Entered] → [Validating] → [Success/Failure]
                                              ↓
                            [Failure] → [Error State] → [Retry/Lockout]
                                              ↓
                            [Success] → [Password Check] → [Expired?] → [Change Password Flow]
                                              ↓
                                        [Not Expired] → [App List Screen]
```

---

### 5.2 Password Expiration Alerts

#### Sub-Features
- 10-day expiration warning (orange alert)
- 5-day expiration warning (red alert)
- Alert dismissal
- Alert persistence

#### Business Rules
- BR-007: Orange alert appears when password expires in exactly 10 days
- BR-008: Red alert appears when password expires in exactly 5 days
- BR-009: Alert can be dismissed by user
- BR-010: Alert has no actionable buttons (informational only)
- BR-011: Alert reappears after every subsequent login until password changed

#### State Transitions
```
[Password X Days to Expiry] → [X = 10 days] → [Show Orange Alert]
[Password X Days to Expiry] → [X = 5 days] → [Show Red Alert]
[Alert Displayed] → [User Dismisses] → [Alert Hidden]
[Next Login] → [Still Within Alert Period] → [Alert Reappears]
```

---

### 5.3 Failed Login Attempts & Account Lockout

#### Sub-Features
- Failed attempt tracking
- Progressive error messages
- Account lockout
- Facility manager notification
- Password reset workflow

#### Business Rules
- BR-012: System tracks failed login attempts per user account
- BR-013: After 1st failure: Display "3 sign-in attempts left"
- BR-014: After 2nd failure: Display "2 sign-in attempts left"
- BR-015: After 3rd failure: Display "1 sign-in attempt left"
- BR-016: After 3rd consecutive failure: Lock account
- BR-017: Locked account displays: "Access denied. Too many failed log-in attempts. Find a facility manager to reset your password."
- BR-018: Facility manager receives alert notification
- BR-019: Only facility manager can reset locked account
- BR-020: Reset sets temporary password

#### State Transitions
```
[Active Account] → [Failed Attempt 1] → [Warning: 3 attempts left]
[Warning: 3 attempts left] → [Failed Attempt 2] → [Warning: 2 attempts left]
[Warning: 2 attempts left] → [Failed Attempt 3] → [Warning: 1 attempt left]
[Warning: 1 attempt left] → [Failed Attempt 4] → [Account Locked]
[Account Locked] → [Manager Resets] → [Temporary Password Issued]
```

---

### 5.4 Account Lockout States

#### Sub-Features
- Standard lockout (failed attempts)
- Expired password lockout
- Device not checked out restriction

#### Business Rules
- BR-021: Standard lockout shows: "Your account has been locked. Find a facility manager to reset your password."
- BR-022: Expired password lockout shows: "Account locked – expired password. Find a facility manager to reset your password."
- BR-023: Device checkout restriction shows: "This device is not checked out to you. Please find a facility manager to check out this device."
- BR-024: Each lockout type requires facility manager intervention

---

### 5.5 Temporary Password & Change Password Flow

#### Sub-Features
- Temporary password login
- Forced password change
- Password validation
- Password confirmation
- Success confirmation
- Re-login requirement

#### Business Rules
- BR-025: Login with temporary password must force Change Password screen
- BR-026: Change Password screen displays: User ID (read-only), New Password, Confirm Password, SAVE button
- BR-027: SAVE button is disabled until all validations pass
- BR-028: Password must be 10-128 characters
- BR-029: Password must contain at least 1 uppercase letter
- BR-030: Password must contain at least 1 lowercase letter
- BR-031: Password must contain at least 2 numbers
- BR-032: Password must contain at least 2 special characters
- BR-033: Password cannot contain symbols: # + & |
- BR-034: Password cannot contain User ID
- BR-035: Password cannot contain User's name
- BR-036: Password cannot match any of last 6 passwords (~18 months)
- BR-037: New Password and Confirm Password must match
- BR-038: If passwords don't match: Display "Passwords don't match."
- BR-039: If password contains User ID/name: Display "Passwords cannot contain User ID or user's name."
- BR-040: If validation rule violated: Display specific rule error
- BR-041: On successful change: Display "Password changed successfully."
- BR-042: After successful change: User must re-login with new password
- BR-043: If app closed during change: Temporary password remains valid, flow restarts

#### Field-Level Validations
| Field | Type | Mandatory | Min Length | Max Length | Special Rules |
|-------|------|-----------|------------|------------|---------------|
| User ID | Text (Read-only) | Yes | - | - | Display only |
| New Password | Masked Text | Yes | 10 | 128 | Complexity rules apply |
| Confirm Password | Masked Text | Yes | 10 | 128 | Must match New Password |

#### Password Complexity Matrix
| Rule | Required | Error Message |
|------|----------|---------------|
| Length 10-128 | Yes | "Password must be 10-128 characters" |
| ≥1 Uppercase | Yes | "Password must contain at least 1 uppercase letter" |
| ≥1 Lowercase | Yes | "Password must contain at least 1 lowercase letter" |
| ≥2 Numbers | Yes | "Password must contain at least 2 numbers" |
| ≥2 Special Chars | Yes | "Password must contain at least 2 special characters" |
| No # + & \| | Yes | "Password cannot contain # + & \| symbols" |
| No User ID | Yes | "Passwords cannot contain User ID or user's name" |
| No User Name | Yes | "Passwords cannot contain User ID or user's name" |
| Not in last 6 | Yes | "Password cannot be reused from last 6 passwords" |

---

### 5.6 Facility Configuration (Manual Flow)

#### Sub-Features
- First-time facility setup
- Facility ID entry
- Facility ID confirmation
- Facility validation
- Access control
- Success confirmation
- Device information display

#### Business Rules
- BR-044: If no facility configured: Display "A facility has not been configured yet. Please set up a facility to continue."
- BR-045: User must manually type 3-letter facility ID
- BR-046: User must press ENTER to accept entry
- BR-047: Facility ID must be exactly 3 characters
- BR-048: If length ≠ 3: Display "Facility ID should be 3 characters."
- BR-049: User must enter Facility ID twice (confirmation step)
- BR-050: If entries don't match: Display "Facility IDs do not match."
- BR-051: If facility not in system: Display "Facility not recognized."
- BR-052: If user lacks access: Display "User does not have access to this facility."
- BR-053: If device already configured to same facility: Display "Device is already configured to this facility."
- BR-054: On success: Display "Facility ID successfully configured to device."
- BR-055: On success: Display "Device configured to Zone successfully."
- BR-056: Display facility name (e.g., "Braintree, MA (GDT)")
- BR-057: Display device MAC, IP, and server information

#### Field-Level Validations
| Field | Type | Mandatory | Format | Length | Special Rules |
|-------|------|-----------|--------|--------|---------------|
| Facility ID (Entry 1) | Text | Yes | Alphanumeric | Exactly 3 | Must press ENTER |
| Facility ID (Entry 2) | Text | Yes | Alphanumeric | Exactly 3 | Must match Entry 1 |

#### State Transitions
```
[No Facility Configured] → [Prompt User]
[User Enters Facility ID] → [Validate Length] → [Pass: 3 chars] → [Request Confirmation]
                                              → [Fail: ≠3 chars] → [Show Error]
[Confirmation Entry] → [Match?] → [Yes] → [Validate Facility in Backend]
                                → [No] → [Show Mismatch Error]
[Backend Validation] → [Recognized?] → [Yes] → [Check Access]
                                     → [No] → [Show Not Recognized Error]
[Check Access] → [Has Access?] → [Yes] → [Check If Already Configured]
                               → [No] → [Show No Access Error]
[Already Configured?] → [No] → [Configure Device] → [Success Messages]
                      → [Yes] → [Show Already Configured Error]
```

---

### 5.7 Device Permissions

#### Sub-Features
- Photo/media/files permission
- Camera/video permission
- Permission dialog display
- User choice capture

#### Business Rules
- BR-058: Android displays native OS permission modals (not Spectrum UI)
- BR-059: Photo permission: "Allow Spectrum to access photos, media, and files?"
- BR-060: Camera permission: "Allow Spectrum to take pictures and record video?"
- BR-061: Options provided: Allow, Deny, Don't ask again
- BR-062: User choice persisted by Android OS

---

### 5.8 Scanner Pairing

#### Sub-Features
- Scanner connection status display
- Bluetooth icon access
- Pairing barcode generation
- Scanner connection establishment

#### Business Rules
- BR-063: Access scanner pairing via Bluetooth icon in top status bar
- BR-064: Display "Scanner connected" if scanner is paired
- BR-065: Display "No scanner connected" if no scanner paired
- BR-066: If not connected, show PAIR button
- BR-067: Clicking PAIR displays pairing barcode
- BR-068: User scans barcode with handheld scanner
- BR-069: After successful scan, connection established
- BR-070: User can proceed to login after connection

#### State Transitions
```
[Scanner Not Connected] → [User Clicks Bluetooth Icon] → [Display Status: No scanner connected]
[Display Status] → [User Clicks PAIR] → [Display Pairing Barcode]
[Display Barcode] → [User Scans Barcode] → [Connection Established]
[Connection Established] → [Display Status: Scanner connected]
```

---

### 5.9 Battery Alerts

#### Sub-Features
- Battery level monitoring
- Low battery alert
- Battery percentage display

#### Business Rules
- BR-071: If battery <20%: Display "Low Battery" state
- BR-072: If battery ≥20%: Display normal battery percentage (e.g., "56%")

---

### 5.10 App Navigation

#### Sub-Features
- Post-login app list
- Side menu
- App selection
- Menu options

#### Business Rules
- BR-073: After successful login, display list of 17 apps
- BR-074: Apps listed: Shop, Expedite, Staging, Audit, Load, Verify, Equipment, Inventory, Cycle Count, Adjust Inventory, Slotting, Replenish, Lean, Returns, P-Cube, Prep, Putaway
- BR-075: Side menu always includes: About, Change Password, Scanner Pairing, Logout
- BR-076: User can select any app from the list
- BR-077: User can access menu options from side menu

---

## 6. Coverage Model

### 6.1 Functional Coverage

#### Happy Path Scenarios
- Successful login with valid credentials
- Password expiration alerts displayed correctly
- Change password with all valid rules met
- Facility setup completed successfully
- Scanner paired successfully
- App list displayed after login

#### Alternate Path Scenarios
- Login with credentials about to expire (10-day, 5-day alerts)
- Change password after temporary password
- Facility configuration when user has multiple facility access
- Dismiss password expiration alert
- App closure during change password flow

#### Negative Scenarios
- Login with invalid credentials (1st, 2nd, 3rd attempt)
- Password change with validation rule violations
- Facility ID entry with wrong length
- Facility ID mismatch during confirmation
- Unrecognized facility ID
- User without facility access
- Device not checked out to user

---

### 6.2 Data Coverage

#### Boundary Value Analysis

**Password Length:**
- Below minimum: 9 characters (Invalid)
- Minimum: 10 characters (Valid)
- Valid mid-range: 50 characters (Valid)
- Maximum: 128 characters (Valid)
- Above maximum: 129 characters (Invalid)

**Facility ID Length:**
- Below minimum: 2 characters (Invalid)
- Valid: 3 characters (Valid)
- Above maximum: 4 characters (Invalid)

**Failed Login Attempts:**
- 1st attempt (Invalid)
- 2nd attempt (Invalid)
- 3rd attempt (Invalid)
- 4th attempt → Lockout

**Password Expiration Days:**
- 11 days (No alert)
- 10 days (Orange alert)
- 6 days (Orange alert)
- 5 days (Red alert)
- 1 day (Red alert)
- 0 days → Expired lockout

**Battery Level:**
- 19% (Low battery)
- 20% (Normal)
- 50% (Normal)
- 100% (Normal)

#### Equivalence Classes

**User ID:**
- Valid alphanumeric
- Invalid: Empty/null
- Invalid: Special characters only

**Password:**
- Valid: Meets all complexity rules
- Invalid: Missing uppercase
- Invalid: Missing lowercase
- Invalid: <2 numbers
- Invalid: <2 special chars
- Invalid: Contains banned symbols
- Invalid: Contains User ID
- Invalid: Contains User name
- Invalid: Too short
- Invalid: Too long
- Invalid: Reused from history

**Facility ID:**
- Valid: 3 alphanumeric chars
- Invalid: <3 chars
- Invalid: >3 chars
- Invalid: Empty
- Invalid: Special characters
- Valid but not recognized in system
- Valid but user has no access

---

### 6.3 State and Workflow Coverage

#### User Account States
- Active & Not Locked
- Active & Password Expiring Soon (10 days)
- Active & Password Expiring Soon (5 days)
- Locked due to failed attempts
- Locked due to expired password
- Locked due to device not checked out
- Using temporary password

#### Device Configuration States
- Not configured (first-time setup)
- Configured to facility
- Configured to different facility (change scenario)

#### Scanner Connection States
- Not connected
- Pairing in progress
- Connected

#### App States
- Login screen
- Change password screen
- Facility setup screen
- App list screen
- Individual app screens (out of scope for detailed testing)

---

### 6.4 Role and Permission Coverage

#### User Roles
- Standard Employee (login, use apps)
- Facility Manager (reset passwords, check out devices, manage alerts)

#### Access Control Scenarios
- User with single facility access
- User with multiple facility access
- User without facility access
- User with device checked out
- User without device checked out

---

### 6.5 Platform Coverage
- Android OS version compatibility (specific versions TBD)
- Different Android device manufacturers (Samsung, Google Pixel, etc.)
- Different screen sizes and resolutions

---

### 6.6 Integration Coverage

#### Success Scenarios
- Successful authentication API call
- Successful password change API call
- Successful facility configuration API call
- Successful device checkout validation
- Successful scanner pairing via Bluetooth

#### Failure Scenarios
- Network timeout during login
- API error response (500, 503)
- Backend service unavailable
- Bluetooth connection failure
- Scanner hardware not responding

---

### 6.7 Non-Functional Coverage

#### Performance
- Login response time (<3 seconds)
- Password validation real-time feedback
- Facility configuration response time

#### Security
- Password masking in UI
- Password complexity enforcement
- Account lockout mechanism
- Password history tracking
- Temporary password expiration

#### Usability
- Error message clarity
- Alert dismissal functionality
- Input field validation feedback
- Button enable/disable states

#### Accessibility (If Applicable)
- Screen reader compatibility
- Text size scalability
- Color contrast for alerts

---

## 7. Test Scenario Catalog

### 7.1 Login Flow Scenarios

| Scenario ID | Description | Preconditions | Input/Data | Expected Result | Req ID |
|-------------|-------------|---------------|------------|-----------------|--------|
| TS-001 | Verify login screen UI elements | App launched | None | Display User ID field, Password field, Log In button, Exit button, version label | REQ-001 |
| TS-002 | Verify version label display | Login screen displayed | None | Version shows "v1.0" or "Spectrum 1.0.0" | REQ-001 |
| TS-069 | Verify password masking | Login screen displayed | Type password "Test123" | Password field shows masked characters (****) | REQ-053 |
| TS-068 | Verify Exit button functionality | Login screen displayed | Click Exit | Login screen closes/app exits | REQ-052 |
| TS-070 | Successful login with valid credentials | User account active, not locked | UserID: valid, Password: valid | Login successful, navigate to app list | REQ-054 |

---

### 7.2 Password Expiration Alert Scenarios

| Scenario ID | Description | Preconditions | Input/Data | Expected Result | Req ID |
|-------------|-------------|---------------|------------|-----------------|--------|
| TS-003 | 10-day password expiration alert | User password expires in 10 days | UserID: valid, Password: valid | Orange alert displayed: Password expires in 10 days | REQ-002 |
| TS-004 | 5-day password expiration alert | User password expires in 5 days | UserID: valid, Password: valid | Red alert displayed: Password expires in 5 days | REQ-003 |
| TS-005 | Alert dismissal and persistence | Alert displayed | Dismiss alert, logout, login again | Alert dismissed, reappears on next login | REQ-004 |

---

### 7.3 Failed Login Attempt Scenarios

| Scenario ID | Description | Preconditions | Input/Data | Expected Result | Req ID |
|-------------|-------------|---------------|------------|-----------------|--------|
| TS-006 | First failed login attempt | Account active, 0 previous failures | UserID: valid, Password: incorrect | Error: "Incorrect password. 3 sign-in attempts left." | REQ-005 |
| TS-007 | Second failed login attempt | Account active, 1 previous failure | UserID: valid, Password: incorrect | Error: "Incorrect password. 2 sign-in attempts left." | REQ-006 |
| TS-008 | Third failed login attempt | Account active, 2 previous failures | UserID: valid, Password: incorrect | Error: "Incorrect password. 1 sign-in attempt left." | REQ-007 |
| TS-009 | Account lockout after 3 failed attempts | Account active, 3 previous failures | UserID: valid, Password: incorrect | Account locked, Error: "Access denied. Too many failed log-in attempts. Find a facility manager to reset your password." | REQ-008 |
| TS-010 | Facility manager receives lockout alert | Account locked due to failures | N/A | Facility manager receives notification alert | REQ-009 |

---

### 7.4 Account Lockout State Scenarios

| Scenario ID | Description | Preconditions | Input/Data | Expected Result | Req ID |
|-------------|-------------|---------------|------------|-----------------|--------|
| TS-011 | Standard account lockout message | Account locked (not due to expiration) | UserID: locked account | Error: "Your account has been locked. Find a facility manager to reset your password." | REQ-010 |
| TS-012 | Expired password lockout | Account locked due to expired password | UserID: expired account | Error: "Account locked – expired password. Find a facility manager to reset your password." | REQ-011 |
| TS-013 | Device not checked out error | Device not checked out to user | UserID: valid, Device: not checked out | Error: "This device is not checked out to you. Please find a facility manager to check out this device." | REQ-012 |

---

### 7.5 Temporary Password & Change Password Scenarios

| Scenario ID | Description | Preconditions | Input/Data | Expected Result | Req ID |
|-------------|-------------|---------------|------------|-----------------|--------|
| TS-014 | Login with temporary password forces change | Account has temporary password | UserID: valid, Password: temporary | Change Password screen displayed | REQ-013 |
| TS-015 | Change Password screen UI elements | Change Password screen displayed | None | Display User ID (read-only), New Password, Confirm Password, SAVE button (disabled) | REQ-014 |
| TS-016 | Password minimum length validation | Change Password screen | New Password: "Test@12" (7 chars) | Error: Password must be 10-128 characters | REQ-015 |
| TS-017 | Password maximum length validation | Change Password screen | New Password: 129 characters | Error: Password must be 10-128 characters | REQ-015 |
| TS-018 | Password valid length | Change Password screen | New Password: "Test@12345" (11 chars, meets all rules) | No length error, other validations apply | REQ-015 |
| TS-019 | Password missing uppercase | Change Password screen | New Password: "test@12345##" | Error: Password must contain at least 1 uppercase letter | REQ-016 |
| TS-020 | Password contains uppercase | Change Password screen | New Password: "Test@12345##" | No uppercase error, other validations apply | REQ-016 |
| TS-021 | Password missing lowercase | Change Password screen | New Password: "TEST@12345##" | Error: Password must contain at least 1 lowercase letter | REQ-017 |
| TS-022 | Password contains lowercase | Change Password screen | New Password: "Test@12345##" | No lowercase error, other validations apply | REQ-017 |
| TS-023 | Password missing numbers | Change Password screen | New Password: "TestTest@##" | Error: Password must contain at least 2 numbers | REQ-018 |
| TS-024 | Password contains 2+ numbers | Change Password screen | New Password: "Test@12345##" | No number error, other validations apply | REQ-018 |
| TS-025 | Password missing special characters | Change Password screen | New Password: "Test1234567" | Error: Password must contain at least 2 special characters | REQ-019 |
| TS-026 | Password contains 2+ special characters | Change Password screen | New Password: "Test@12345##" | No special char error, other validations apply | REQ-019 |
| TS-027 | Password contains banned symbol # | Change Password screen | New Password: "Test#12345@@" | Error: Password cannot contain # + & \| symbols | REQ-020 |
| TS-028 | Password contains banned symbol + | Change Password screen | New Password: "Test+12345@@" | Error: Password cannot contain # + & \| symbols | REQ-020 |
| TS-029 | Password contains banned symbol & | Change Password screen | New Password: "Test&12345@@" | Error: Password cannot contain # + & \| symbols | REQ-020 |
| TS-030 | Password contains banned symbol \| | Change Password screen | New Password: "Test\|12345@@" | Error: Password cannot contain # + & \| symbols | REQ-020 |
| TS-031 | Password contains User ID | Change Password screen, UserID: "john123" | New Password: "john123@Test12@@" | Error: "Passwords cannot contain User ID or user's name." | REQ-021 |
| TS-032 | Password does not contain User ID | Change Password screen, UserID: "john123" | New Password: "Valid@12345##" | No User ID error, other validations apply | REQ-021 |
| TS-033 | Password contains User name | Change Password screen, User name: "John Doe" | New Password: "JohnDoe@12345##" | Error: "Passwords cannot contain User ID or user's name." | REQ-022 |
| TS-034 | Password does not contain User name | Change Password screen, User name: "John Doe" | New Password: "Valid@12345##" | No User name error, other validations apply | REQ-022 |
| TS-035 | Password reused from history | Change Password screen, Last 6 passwords stored | New Password: Matches one of last 6 | Error: Cannot reuse password from last 6 generations | REQ-023 |
| TS-036 | Password not in history | Change Password screen, Last 6 passwords stored | New Password: New unique password | No history error, other validations apply | REQ-023 |
| TS-037 | Password mismatch error | Change Password screen | New Password: "Test@12345##", Confirm: "Test@12345@@" | Error: "Passwords don't match." | REQ-024 |
| TS-038 | Password contains User ID/name error display | Change Password screen | New Password contains UserID | Error: "Passwords cannot contain User ID or user's name." | REQ-025 |
| TS-039 | Specific validation rule violation errors | Change Password screen | Various invalid inputs | Specific error for each rule violation | REQ-026 |
| TS-040 | Successful password change | Change Password screen | New Password: valid, Confirm: matches, all rules met | Message: "Password changed successfully.", Return to login | REQ-027 |
| TS-041 | App closure during password change | Change Password screen | Close app, reopen, login with temp password | Temporary password still valid, Change Password flow restarts | REQ-028 |
| TS-042 | Forgot password flow | Account locked | Manager resets → temp password issued | User logs in with temp → Change Password flow starts | REQ-029 |

---

### 7.6 Facility Configuration Scenarios

| Scenario ID | Description | Preconditions | Input/Data | Expected Result | Req ID |
|-------------|-------------|---------------|------------|-----------------|--------|
| TS-043 | First-time facility setup prompt | No facility configured on device | Login successful | Prompt: "A facility has not been configured yet. Please set up a facility to continue." | REQ-030 |
| TS-044 | Manual facility ID entry | Facility setup prompted | Type "GDT", press ENTER | Facility ID captured, request confirmation | REQ-031 |
| TS-045 | Facility ID too short | Facility setup prompted | Type "GD" (2 chars) | Error: "Facility ID should be 3 characters." | REQ-032 |
| TS-046 | Facility ID too long | Facility setup prompted | Type "GDTA" (4 chars) | Error: "Facility ID should be 3 characters." | REQ-032 |
| TS-047 | Facility ID valid length | Facility setup prompted | Type "GDT" (3 chars) | No length error, proceed to confirmation | REQ-032 |
| TS-048 | Facility ID confirmation prompt | First entry valid | Second entry requested | System requests re-entry for confirmation | REQ-033 |
| TS-049 | Facility ID mismatch | First entry: "GDT", Second entry: "ABC" | GDT, ABC | Error: "Facility IDs do not match." | REQ-034 |
| TS-050 | Facility not recognized | Matching entries, facility not in system | Facility ID: "XYZ" | Error: "Facility not recognized." | REQ-035 |
| TS-051 | User no access to facility | Matching entries, facility exists, no user access | Valid facility ID | Error: "User does not have access to this facility." | REQ-036 |
| TS-052 | Device already configured to facility | Device already configured, same facility entered | Current facility ID | Error: "Device is already configured to this facility." | REQ-037 |
| TS-053 | Successful facility configuration | Matching entries, facility valid, user has access | Valid facility ID | Message: "Facility ID successfully configured to device." | REQ-038 |
| TS-054 | Successful zone configuration | Facility configured successfully | N/A | Message: "Device configured to Zone successfully." | REQ-039 |
| TS-055 | Facility name display | Facility configured | Facility: GDT | Display: "Braintree, MA (GDT)" | REQ-040 |
| TS-056 | Device info display | Facility configured | N/A | Display: Device MAC, IP, Server information | REQ-041 |

---

### 7.7 Device Permission Scenarios

| Scenario ID | Description | Preconditions | Input/Data | Expected Result | Req ID |
|-------------|-------------|---------------|------------|-----------------|--------|
| TS-057 | Photo/media permission prompt | App requires photo access, first time | N/A | Android modal: "Allow Spectrum to access photos, media, and files?" with Allow/Deny/Don't ask again | REQ-042 |
| TS-058 | Camera permission prompt | App requires camera access, first time | N/A | Android modal: "Allow Spectrum to take pictures and record video?" with Allow/Deny/Don't ask again | REQ-043 |

---

### 7.8 Scanner Pairing Scenarios

| Scenario ID | Description | Preconditions | Input/Data | Expected Result | Req ID |
|-------------|-------------|---------------|------------|-----------------|--------|
| TS-059 | Scanner connected status | Scanner already paired | Click Bluetooth icon | Display: "Scanner connected" | REQ-044 |
| TS-060 | Scanner not connected status | No scanner paired | Click Bluetooth icon | Display: "No scanner connected" | REQ-044 |
| TS-061 | Access scanner pairing | Top status bar visible | Click Bluetooth icon | Scanner pairing screen opens | REQ-045 |
| TS-062 | Display pairing barcode | Scanner not connected | Click PAIR button | Pairing barcode displayed | REQ-046 |
| TS-063 | Scanner connection success | Pairing barcode displayed | Scan barcode with scanner | Scanner connects, status changes to "Scanner connected" | REQ-047 |

---

### 7.9 Battery Alert Scenarios

| Scenario ID | Description | Preconditions | Input/Data | Expected Result | Req ID |
|-------------|-------------|---------------|------------|-----------------|--------|
| TS-064 | Low battery alert | Battery level <20% | Battery at 15% | Display: "Low Battery" | REQ-048 |
| TS-065 | Normal battery display | Battery level ≥20% | Battery at 56% | Display: "56%" | REQ-049 |

---

### 7.10 App Navigation Scenarios

| Scenario ID | Description | Preconditions | Input/Data | Expected Result | Req ID |
|-------------|-------------|---------------|------------|-----------------|--------|
| TS-066 | App list display after login | Successful login | Valid credentials | Display 17 apps: Shop, Expedite, Staging, Audit, Load, Verify, Equipment, Inventory, Cycle Count, Adjust Inventory, Slotting, Replenish, Lean, Returns, P-Cube, Prep, Putaway | REQ-050 |
| TS-067 | Side menu options | App list displayed | Open side menu | Display: About, Change Password, Scanner Pairing, Logout | REQ-051 |

---

## 8. Test Data Strategy

### 8.1 User Account Data

#### Valid User Accounts
- **User1**: Active, password valid for >30 days, single facility access
- **User2**: Active, password expires in 10 days, multiple facility access
- **User3**: Active, password expires in 5 days, single facility access
- **User4**: Locked due to failed attempts
- **User5**: Locked due to expired password
- **User6**: Active with temporary password
- **User7**: Device not checked out to this user
- **User8**: No facility access

#### User IDs
- Valid format: "emp001", "johnsmith", "user123"
- Invalid: Empty, null

#### Passwords
- Valid current passwords for test users
- Invalid passwords for negative testing
- Password history data (last 6 passwords) for history validation
- Temporary passwords for reset scenarios

---

### 8.2 Facility Data

#### Valid Facilities
- **GDT**: Braintree, MA (GDT) - Zone configured
- **LAX**: Los Angeles, CA (LAX) - Zone configured
- **CHI**: Chicago, IL (CHI) - Zone configured

#### Invalid Facilities
- **XYZ**: Not in system (for "not recognized" test)
- **ABC**: In system but User has no access

---

### 8.3 Password Change Test Data

#### Valid Password Examples
- "Valid@12345##"
- "Test@Password99!!"
- "Secure$Pass123*"

#### Invalid Password Examples (Each violates one rule)
- "short@1#" (Too short - 8 chars)
- "test@12345##" (No uppercase)
- "TEST@12345##" (No lowercase)
- "TestTest@##" (Only 0 numbers)
- "Test1234567" (No special chars)
- "Test#12345@@" (Contains banned #)
- "Test+12345@@" (Contains banned +)
- "Test&12345@@" (Contains banned &)
- "Test|12345@@" (Contains banned |)
- Contains UserID/Username (varies per user)
- Matches password history (varies per user)

---

### 8.4 Edge Case Data

#### Boundary Values
- Password: 9 chars, 10 chars, 128 chars, 129 chars
- Facility ID: 2 chars, 3 chars, 4 chars
- Failed attempts: 1, 2, 3, 4
- Days to expiry: 11, 10, 6, 5, 1, 0
- Battery: 19%, 20%, 100%

#### Special Characters
- Password test with all allowed special chars: ! @ $ % ^ * ( ) - _ = [ ] { } ; : ' " , . < > ? / ~ `
- Facility ID with numbers: "G01", "L2X"
- Facility ID with letters only: "GDT", "LAX"

---

### 8.5 Data Setup and Cleanup

#### Setup Requirements
- Create test user accounts in backend
- Configure facility records in backend
- Assign user-facility access mappings
- Populate password history for test users
- Set password expiration dates for test scenarios
- Lock/unlock accounts as needed
- Check out devices to specific users

#### Cleanup Requirements
- Reset failed login attempt counters after tests
- Unlock test accounts
- Remove temporary passwords after tests
- Reset device facility configurations
- Clear password history (if needed for retest)

---

## 9. Test Environment and Configuration

### 9.1 Test Environments

#### Environment 1: Local Dev
- **Purpose**: Unit and component testing
- **Backend**: Mock API responses
- **Database**: Local test DB
- **Devices**: Android emulators
- **Network**: Localhost

#### Environment 2: QA
- **Purpose**: Integration and E2E testing
- **Backend**: QA API server
- **Database**: QA database
- **Devices**: Physical Android devices (multiple models)
- **Network**: QA network

#### Environment 3: Staging
- **Purpose**: Pre-production validation
- **Backend**: Staging API server (production-like)
- **Database**: Staging database
- **Devices**: Physical Android devices
- **Network**: Production-like network

---

### 9.2 Device Configurations

#### Android Devices
- **Model 1**: Samsung Galaxy Tab (Android 11)
- **Model 2**: Google Pixel (Android 12)
- **Model 3**: Android emulator (Android 13)

#### Screen Sizes
- Small: 5-6 inches
- Medium: 7-8 inches
- Large: 10+ inches

---

### 9.3 Feature Flags and Configuration
- Password expiration feature: ON
- Facility configuration feature: ON
- Scanner pairing feature: ON
- Battery alerts feature: ON
- Permission prompts feature: ON

---

### 9.4 External Dependencies

#### Backend API Endpoints
- `/auth/login` - User authentication
- `/auth/change-password` - Password change
- `/auth/reset-password` - Password reset
- `/facility/configure` - Facility setup
- `/device/checkout` - Device checkout validation
- `/user/alerts` - User alerts (password expiration)

#### Third-Party Services
- Android OS permission system
- Bluetooth stack for scanner pairing

---

### 9.5 Versioning
- **App Version**: v1.0 / Spectrum 1.0.0
- **Android OS**: 11, 12, 13 (minimum support TBD)
- **Backend API**: v2.0

---

## 10. Entry and Exit Criteria

### 10.1 Entry Criteria

#### Pre-Testing Requirements
✅ All test environments (Dev, QA, Staging) are set up and accessible  
✅ Backend API services are deployed and operational  
✅ Test user accounts and facility data are created  
✅ Android devices (physical and emulators) are available  
✅ Bluetooth scanners are available for pairing tests  
✅ Test Plan is reviewed and approved  
✅ Test cases are created and reviewed  
✅ Test data is prepared and validated  
✅ Defect tracking system is ready  
✅ App build is deployed to test environment  

#### Build Quality Gates
✅ Build is smoke-test ready (app launches without crashes)  
✅ No P0/P1 known defects from previous builds  
✅ Release notes available with changes documented  

---

### 10.2 Exit Criteria

#### Test Execution Completion
✅ 100% RTM coverage - all requirements mapped to executed test cases  
✅ 100% of Functional test cases executed  
✅ 100% of Regression test cases executed  
✅ 100% of Smoke test cases executed  
✅ 95%+ of Integration test cases executed  
✅ 90%+ of E2E test cases executed  

#### Quality Metrics
✅ Zero P0 (Critical) defects open  
✅ <5 P1 (High) defects open  
✅ All P1 defects have workarounds or timelines  
✅ <20 P2 (Medium) defects open  
✅ Test pass rate ≥95%  
✅ Regression test pass rate = 100%  

#### Documentation Completion
✅ All test cases executed and results logged  
✅ All defects logged with reproducible steps  
✅ Test summary report created  
✅ Known issues documented  
✅ Sign-off from QA lead and stakeholders  

---

## 11. Defect Management

### 11.1 Severity Definitions

| Severity | Definition | Example |
|----------|------------|---------|
| P0 - Critical | System unusable, blocks all users, data loss | App crashes on launch, authentication completely broken |
| P1 - High | Major functionality broken, affects most users, no workaround | Cannot login, password change fails, facility setup blocked |
| P2 - Medium | Functionality partially broken, workaround exists | Error message incorrect, UI misalignment, performance degraded |
| P3 - Low | Minor issue, cosmetic, rare scenario | Typo in text, color inconsistency, edge case behavior |

---

### 11.2 Priority Definitions

| Priority | Definition | SLA |
|----------|------------|-----|
| Immediate | Must fix before release | 24 hours |
| High | Fix in current sprint | 3 days |
| Medium | Fix in next sprint | 1 week |
| Low | Fix in backlog | TBD |

---

### 11.3 Retest and Regression Rules
- **P0/P1 defects**: Retest immediately after fix
- **P2 defects**: Retest in next build
- **Regression scope**: Run full regression suite after any P0/P1 fix
- **Smoke tests**: Run after every new build
- **Failed test cases**: Retest after defect fix

---

### 11.4 Stop-Ship Criteria
- Any P0 defect exists
- >5 P1 defects exist
- Critical workflow blocked (login, password change, facility setup)
- Data security vulnerability identified
- Performance degradation >50% from baseline

---

## 12. Test Levels and Types

### 12.1 Test Distribution by Type

| Test Type | Description | Coverage % | Execution |
|-----------|-------------|------------|-----------|
| Functional | Core feature validation (login, password, facility, scanner) | 35% | Manual + Automated |
| Smoke | Critical path sanity after build | 8% | Automated |
| Regression | Ensure existing functionality not broken | 20% | Automated |
| Integration | Backend API integration, Bluetooth integration | 12% | Manual + Automated |
| E2E | End-to-end user workflows (login to app selection) | 10% | Manual |
| Negative | Invalid inputs, error states, lockouts | 10% | Manual + Automated |
| Edge | Boundary values, special characters, concurrency | 5% | Manual |

---

### 12.2 Manual vs Automated Scope

#### Automated Testing (60%)
- Login happy path
- Password validation rules
- Facility ID validations
- Failed login attempt counter
- Error message assertions
- Smoke tests
- Regression tests

#### Manual Testing (40%)
- First-time user flows
- Android native permission prompts
- Bluetooth scanner pairing
- Complex multi-step workflows
- Visual UI validation
- Usability testing
- Exploratory testing

---

## 13. Risk-Based Testing

### 13.1 High-Risk Areas

| Risk Area | Impact | Probability | Mitigation | Mandatory Tests |
|-----------|--------|-------------|------------|-----------------|
| Account Lockout Logic | Critical - Users unable to work | Medium | Extensive testing of failed attempt counter | TS-006 to TS-013 |
| Password Change Flow | Critical - Security vulnerability | Medium | Validate all 11 password rules | TS-015 to TS-042 |
| Facility Configuration | High - Device unusable if misconfigured | Medium | Test all validation rules and error states | TS-043 to TS-056 |
| Temporary Password Security | Critical - Unauthorized access | Low | Ensure temp password forces change | TS-013, TS-014, TS-041 |
| Scanner Pairing | Medium - Operational inefficiency | Medium | Test Bluetooth connection in various states | TS-059 to TS-063 |
| Password Expiration Alerts | Medium - Users locked out unexpectedly | Low | Test 10-day, 5-day, and expired states | TS-003, TS-004, TS-012 |
| Backend API Failures | High - Service unavailable | Low | Integration tests with error simulation | N/A - Integration testing |
| Data Persistence | High - Loss of configuration | Low | Test app closure/restart scenarios | TS-041, TS-028 |

---

### 13.2 Risk Mitigation Strategies
- **Priority 1**: Test all account lockout scenarios before release
- **Priority 2**: Validate all 11 password complexity rules with positive and negative cases
- **Priority 3**: Test facility configuration error handling exhaustively
- **Priority 4**: Perform E2E testing of complete user journeys
- **Priority 5**: Conduct security review of password handling and storage

---

## 14. Test Execution Schedule

### Phase 1: Smoke Testing (1 day)
- App launch
- Login happy path
- Basic navigation

### Phase 2: Functional Testing (5 days)
- Login flows (1 day)
- Password management (2 days)
- Facility configuration (1 day)
- Scanner pairing, battery, permissions (1 day)

### Phase 3: Integration Testing (2 days)
- Backend API integration
- Bluetooth integration

### Phase 4: Regression Testing (2 days)
- Full regression suite

### Phase 5: E2E Testing (2 days)
- Complete user workflows
- Multi-scenario testing

### Phase 6: Exploratory Testing (1 day)
- Ad-hoc testing
- Edge case discovery

**Total Duration: 13 days**

---

## 15. Roles and Responsibilities

| Role | Responsibility |
|------|----------------|
| QA Lead | Test Plan approval, resource allocation, sign-off |
| QA Engineer | Test case creation, execution, defect logging |
| Automation Engineer | Automated test script development |
| Backend Developer | API fixes, test data setup |
| Mobile Developer | App fixes, build deployment |
| Facility Manager (Test User) | Password reset testing, device checkout testing |
| Product Owner | Requirements clarification, acceptance |

---

## 16. Appendix

### 16.1 Acronyms and Abbreviations
- **RTM**: Requirements Traceability Matrix
- **E2E**: End-to-End
- **API**: Application Programming Interface
- **UI**: User Interface
- **OS**: Operating System
- **P0/P1/P2/P3**: Priority levels
- **QA**: Quality Assurance

---

### 16.2 References
- Requirements Document: `requirement.md`
- Figma Design Specifications (referenced in requirements)
- Backend API Documentation
- Android OS Permission Guidelines

---

### 16.3 Change Log

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-05 | QA Team | Initial Test Plan created from requirements |

---

## 17. Next Steps

✅ **Test Plan Approved** → Ready for Test Case Generation

**Next Action**: Use **"Generate Zephyr Test Case"** skill to create Zephyr-ready test cases from this Test Plan.

---

**End of Test Plan**
