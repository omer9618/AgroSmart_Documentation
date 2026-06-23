# Master Test Suite
## AgroSmart Enterprise Agricultural Intelligence Platform

**Document Identifier:** AS-MTS-V1.0  
**Version:** 1.0 Final  
**Date of Issue:** June 23, 2026  
**Issuing Organization:** Quality Assurance Division  

---

## 1. Introduction
This Master Test Suite compiles the formal test specifications and step-by-step test cases required to verify the operational capabilities of the AgroSmart platform. This suite is structured around the 20 Functional Requirements (`BRD-FR-001` through `BRD-FR-020`) and 9 Non-Functional Requirements (`NF-PU-01` through `NF-ER-02`) mapped in the Requirements Traceability Matrix (RTM). 

All test cases are detailed in table formats, providing preconditions, specific input parameter vectors (incorporating whitelisted data spelling anomalies), execution steps, and expected outputs to facilitate validation checks.

---

## 2. Machine Learning & Core Inference Test Cases

| Test Case ID | Target Requirement | Verification Objective | Preconditions | Input Data / Parameters | Step-by-Step Execution | Expected Output |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-ML-01** | BRD-FR-003 | Validate crop recommendation classification. | Crop recommendation binary model is loaded in server memory. | Nitrogen: 90, Phosphorous: 42, Potassium: 43, Temparature: 20.8, Humidity: 82.0, pH: 6.5, Rainfall: 202.9 | 1. Initialize API client.<br>2. Submit POST request to prediction endpoint with inputs.<br>3. Capture JSON response payload. | Response returns crop label `rice` in under two seconds. |
| **TC-ML-02** | BRD-FR-003 | Validate fertilizer prediction classification. | Fertilizer classification binary model is loaded in server memory. | Soil Type: `Clayey`, Crop Type: `Paddy`, Nitrogen: 80, Phosphorous: 30, Potassium: 35, Moisture: 15.0 | 1. Initialize API client.<br>2. Submit POST request to fertilizer prediction endpoint.<br>3. Capture JSON response. | Response returns fertilizer recommendation formula in under two seconds. |
| **TC-MAINT-02** | NF-ER-02 | Verify serialization handling of schema spelling anomalies. | Django model serializers are configured for input parameter parsing. | Soil form input fields matching: `Temparature`, `Humidity `, `Phosphorous` | 1. Send soil payload with misspelled parameters.<br>2. Inspect API parsing log entries.<br>3. Verify model scoring function execution. | Serializers parse parameters successfully without raising serialization errors. |

---

## 3. User Interface, Layouts & Usability Test Cases

| Test Case ID | Target Requirement | Verification Objective | Preconditions | Input Data / Parameters | Step-by-Step Execution | Expected Output |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-UI-01** | BRD-FR-001 | Verify Urdu and English interface translations. | User is on the login view. | Localization capsule widget toggle | 1. Toggle language switch to Urdu.<br>2. Inspect form titles and text guides.<br>3. Toggle language switch to English.<br>4. Inspect text. | All UI text translates instantly between Urdu and English. |
| **TC-UI-02** | BRD-FR-002 | Verify keyboard view safety padding. | Form inputs are active. | Root scaffold viewport settings | 1. Tap input text field to raise soft keyboard.<br>2. Observe card layouts and form scaling. | Viewport remains stable and forms do not experience card collapses. |
| **TC-UI-03** | BRD-FR-011 | Verify soil data guidance overlays. | User is on crop entry screen. | Range guide overlays | 1. Inspect display on N, P, and K input fields.<br>2. Tap range info button. | Input field bounds display valid chemical ranges. |
| **TC-UI-04** | BRD-FR-018 | Verify network state alerting display. | Connection state changes. | Offline network state trigger | 1. Disconnect device cellular network.<br>2. Observe dashboard warning banners. | Persistent orange warning banner displays indicating offline fallback mode. |
| **TC-UI-05** | BRD-FR-012 | Verify advisory logs parameter expansion. | User is on history view. | Log parameter details card | 1. Tap historical recommendation log card.<br>2. Verify details list. | Detail drawer expands displaying full soil chemical inputs and outputs. |
| **TC-UI-06** | BRD-FR-014 | Verify advisory dashboard widgets. | User dashboard is active. | Dashboard panels | 1. Open home view.<br>2. Inspect weather widget and recommended crop cards. | Combined weather and recommendation panels render with correct layout alignment. |

---

## 4. Local Storage & History Cache Test Cases

| Test Case ID | Target Requirement | Verification Objective | Preconditions | Input Data / Parameters | Step-by-Step Execution | Expected Output |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-DB-01** | BRD-FR-008 | Verify automatic SQLite caching of logs. | SQLite database is initialized. | DiagnosticHistory row data | 1. Submit prediction request.<br>2. Query local sandboxed cache file.<br>3. Check row records. | Recommendation data is written automatically to local cache. |
| **TC-DB-02** | BRD-FR-015 | Verify historical search queries. | Local database contains multiple records. | Search term keyword `rice` | 1. Open history screen.<br>2. Enter keyword in search field.<br>3. Observe listed records. | Display filters instantly, listing matching records containing crop name. |
| **TC-DB-03** | BRD-FR-016 | Verify category chips filtering. | Local database contains various record types. | Category filter chips (`Crop`, `Fertilizer`) | 1. Navigate to history view.<br>2. Tap the `Fertilizer` filter chip.<br>3. Tap the `Crop` filter chip. | History list displays matching categories only. |
| **TC-COMP-02** | NF-LC-01 | Verify sandbox SQLite database file isolation. | Application is running on device simulator. | Cache directory sandbox path | 1. Open sandboxed application document path.<br>2. Access cache files.<br>3. Attempt reading cache files from external app. | Cache files are read-write restricted to the sandboxed application process. |

---

## 5. User Security, Authentication & Session Test Cases

| Test Case ID | Target Requirement | Verification Objective | Preconditions | Input Data / Parameters | Step-by-Step Execution | Expected Output |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-AU-01** | BRD-FR-009 | Verify password complexity checks during signups. | User is on signup screen. | Username: `farmer_test`, Password: `123` | 1. Input credentials.<br>2. Click register.<br>3. Input strong password (uppercase, digit, symbol).<br>4. Click register. | System rejects weak password with complexity alert, and allows strong password register. |
| **TC-AU-02** | BRD-FR-010 | Verify persistent session auto-logins. | Secure cache holds valid session token. | Encrypted JWT token | 1. Launch application.<br>2. Observe splash routing path. | App reads secure storage token, bypasses login, and opens Dashboard. |
| **TC-AU-03** | BRD-FR-017 | Verify session sign-out functionality. | User is authenticated. | Sign-out action event | 1. Navigate to settings.<br>2. Click sign-out.<br>3. Attempt back navigation. | Session token is cleared, user is redirected to login, and back operations are blocked. |
| **TC-SEC-02** | NF-SS-01 | Verify Keychain/Keystore token encryption. | Authentication session is established. | JWT token storage write | 1. Perform login validation.<br>2. Intercept local memory token writes.<br>3. Verify security configurations. | Tokens are encrypted using device Keychain or Keystore APIs. |

---

## 6. Decentralized Ledger Logging Test Cases

| Test Case ID | Target Requirement | Verification Objective | Preconditions | Input Data / Parameters | Step-by-Step Execution | Expected Output |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-BC-01** | BRD-FR-005 | Verify asynchronous Celery queue handoffs. | Celery background task environment is running. | Audit sync queue job | 1. Submit prediction payload.<br>2. Inspect API response logs.<br>3. Monitor Redis task queue. | Response returns to client in under two seconds; task handoff to Celery executes asynchronously. |
| **TC-BC-02** | BRD-FR-020 | Verify ledger Etherscan links. | Audit record status is `Synchronized`. | Sepolia transaction hash | 1. Open result history view.<br>2. Locate transaction verification link.<br>3. Click hyperlink. | App opens web browser routing to the correct Sepolia transaction receipt details page. |
| **TC-SEC-01** | NF-SA-01 | Verify Sepolia ledger audit logs security. | Sync task executes. | Ethereum ABI contract parameters | 1. Trigger sync task execution.<br>2. Monitor transaction payload.<br>3. Confirm contract log call parameters. | Worker signs transaction with secure wallet keys and commits log payload to smart contract. |
| **TC-PF-03** | NF-PB-01 | Verify Celery sync task execution latency. | Network connection is online. | Background task signing job | 1. Dispatch sync task to queue.<br>2. Measure elapsed execution time to transaction confirmation. | Queue task signs and broadcasts transactions to Sepolia RPC node in under thirty seconds. |

---

## 7. External Integrations, Weather & LLM Test Cases

| Test Case ID | Target Requirement | Verification Objective | Preconditions | Input Data / Parameters | Step-by-Step Execution | Expected Output |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-AI-01** | BRD-FR-006 | Verify Google Gemini advisory formatting. | Gemini API endpoint is online. | Cognitive prompts parameters | 1. Submit advisory query request.<br>2. Inspect API response payload. | Response parses into 4 structured advisor output cards on the dashboard screen. |
| **TC-WE-01** | BRD-FR-013 | Verify GPS coordinate fallback coordinates. | Device GPS service is disabled. | Coords request events | 1. Disable device geolocator location permissions.<br>2. Request advisory weather tips. | System falls back to default coordinates (Islamabad latitude/longitude) to query weather inputs. |
| **TC-DV-01** | BRD-FR-019 | Verify global endpoint config toggles. | App config settings are active. | Environment endpoint configuration toggles | 1. Set environment flag configuration parameter to `staging`.<br>2. Set configuration parameter to `production`. | System routes API requests to emulated staging endpoints and production endpoints. |
| **TC-MAINT-01** | NF-ER-01 | Verify Postgres error log and Slack alerting alerts. | Integration exception occurs (e.g. Sepolia outage). | Outage simulation context | 1. Simulate three failed connection retries to RPC node.<br>2. Inspect PostgreSQL logs database.<br>3. Monitor Slack alerts channel. | Worker records exception code in database and dispatches automated crash notification to Slack. |

---

## 8. Performance & Device Compatibility Test Cases

| Test Case ID | Target Requirement | Verification Objective | Preconditions | Input Data / Parameters | Step-by-Step Execution | Expected Output |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-PF-01** | NF-PU-01 | Verify system response times under normal load. | System is under normal load conditions. | Transaction execution triggers | 1. Measure API recommendation latency.<br>2. Measure local SQLite transaction response speeds. | ML inference returns in under 2.0s; SQLite read-write tasks execute in under one hundred milliseconds. |
| **TC-PF-02** | NF-PU-02 | Verify system response times under peak load (offline timeout). | Staging slot simulates high network latency. | Five-second API request latency | 1. Trigger recommendation form submit.<br>2. Monitor execution redirection timeline. | Network connection interceptor triggers the offline rules engine in under five hundred milliseconds. |
| **TC-OF-01** | BRD-FR-004 | Verify high-availability offline rules engine. | Network connection is disabled. | Temperature: 42.0, Humidity: 85.0 | 1. Input weather telemetry offline.<br>2. Trigger local advice evaluations.<br>3. Observe result page UI. | Advice is calculated offline using deterministic rules and displays on results page. |
| **TC-COMP-01** | NF-CC-01 | Verify native compile compatibility. | Native build profiles are configured. | Android SDK 28+ binary, iOS 15.0+ binary | 1. Compile native Android builds.<br>2. Compile native iOS builds.<br>3. Install and run on target emulators. | Native application packages compile, install, and execute successfully without system errors. |
