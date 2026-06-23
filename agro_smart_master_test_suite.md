# Master Test Suite
## AgroSmart Enterprise Agricultural Intelligence Platform

**Document Identifier:** AS-MTS-V1.0  
**Version:** 1.0 Final  
**Date of Issue:** June 23, 2026  
**Issuing Organization:** Quality Assurance Division  

---

## 1. Introduction
This Master Test Suite compiles the formal test specifications and step-by-step test cases required to verify the operational capabilities of the AgroSmart platform. This suite spans static requirements audits, unit automation validations, client-server integration runs, end-to-end system testing, and operational deployment checkouts. 

Testers shall execute these test cases in the sequence defined to ensure system integrity, especially when updating machine learning modules or blockchain audit scripts.

---

## 2. Static Design & Requirements Test Cases

### AS-MTS-STA-01: Requirements Traceability Audit
*   **Verification Objective**: Validate that 100% of the requirements mapped in the Requirements Traceability Matrix are traceably resolved in the Functional Specification Document and Non-Functional Requirements.
*   **Preconditions**: Review copies of the Business Requirements Document, Functional Specification Document, and Requirements Traceability Matrix are available.
*   **Input Data**: Requirements identifiers `BRD-FR-001` through `BRD-FR-020` and `NF-PU-01` through `NF-ER-02`.
*   **Execution Steps**:
    1. Open the Requirements Traceability Matrix document.
    2. Audit the trace mappings against the Functional Specification sections.
    3. Verify that every requirement identifier points to a verified functional layout, design specification, or test plan section.
*   **Expected Outcome**: Every requirement is successfully mapped to at least one system verification test case without orphaned items.

### AS-MTS-STA-02: LLD Schema Configuration Check
*   **Verification Objective**: Audit the Low-Level Design database model mappings to confirm whitelisting of spelling anomalies.
*   **Preconditions**: Review copy of the Low-Level Design document is available.
*   **Input Data**: Class interface tables for Django database models.
*   **Execution Steps**:
    1. Navigate to the database schema definitions inside the Low-Level Design document.
    2. Inspect attributes of target model classes.
    3. Verify that attributes matches the misspelled keys: `Temparature` (second syllable misspelled), `Humidity ` (trailing space), and `Phosphorous` (misspelled).
*   **Expected Outcome**: Schema spelling alignments match the pre-trained machine learning model inputs exactly.

---

## 3. Unit Automation Test Cases

### AS-MTS-UNT-01: User Client AuthService Local Session Cache
*   **Verification Objective**: Verify that client-side login tokens are correctly cached and encrypted locally.
*   **Preconditions**: Emulated mobile environment running; secure Keychain/Keystore mocks active.
*   **Input Data**: JSON Web Token payload `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`.
*   **Execution Steps**:
    1. Trigger `AuthService.cacheSessionToken` class method using the input token payload.
    2. Programmatically query the emulated secure storage path.
    3. Assert the returned token string matches the source input.
    4. Assert that the stored token is unreadable via standard cleartext storage reads.
*   **Expected Outcome**: Session token is successfully encrypted, written, and verified inside secure storage, returning true upon successful write.

### AS-MTS-UNT-02: Server RandomForestClassifier crop inference
*   **Verification Objective**: Validate that crop recommendation classifications yield accurate crop outputs based on soil input vectors.
*   **Preconditions**: Crop recommendation model joblib binary is loaded into the server process memory space.
*   **Input Data**: Soil metrics dictionary mapping chemical values (Nitrogen: 90, Phosphorous: 42, Potassium: 43, Temparature: 20.8, Humidity: 82.0, pH: 6.5, Rainfall: 202.9).
*   **Execution Steps**:
    1. Instantiate the server-side classification engine class.
    2. Execute the prediction method passing the input soil metrics dictionary.
    3. Assert that the returned output crop matches the categorical label `rice`.
*   **Expected Outcome**: Inference execution outputs the correct class string mapping in under fifty milliseconds.

### AS-MTS-UNT-03: SQLite DatabaseHelper Transaction Writing
*   **Verification Objective**: Confirm that local SQLite queries insert diagnostic records and maintain local database integrity.
*   **Preconditions**: Mobile client sandbox directory is initialized; SQLite database helper instance is active.
*   **Input Data**: Diagnostic parameters object: user ID `FARMER-101`, query type `crop`, input data JSON string, result output JSON string.
*   **Execution Steps**:
    1. Call the database helper write method passing the diagnostic parameters object.
    2. Verify that the transaction returns a positive incremented primary key ID.
    3. Run a SQLite search query filtering by user ID `FARMER-101`.
*   **Expected Outcome**: Diagnostic record is successfully written to local SQLite and retrieved in under one hundred milliseconds.

---

## 4. System Integration Test Cases (SIT)

### AS-MTS-INT-01: Client-to-Server Soil Metric Data Ingestion
*   **Verification Objective**: Validate that soil metrics submitted from the mobile interface are correctly serialized, transmitted, and ingested by Django API models.
*   **Preconditions**: Mobile client and Django server instances are running; network connection is online.
*   **Input Data**: Input metrics (N: 50, P: 30, K: 40, Temparature: 25.5, Humidity: 78.2, Moisture: 15.0).
*   **Execution Steps**:
    1. Input the soil metrics into the mobile form fields.
    2. Press the recommend button to trigger the API call.
    3. Intercept the network request on the backend.
    4. Assert the received JSON payload contains the correct input metrics.
*   **Expected Outcome**: Server deserializes the input payload successfully and returns a HTTP status code two hundred response containing the predicted recommendations in under two seconds.

### AS-MTS-INT-02: Asynchronous Celery Queue Audit Trail Handoff
*   **Verification Objective**: Verify that audit logging requests are offloaded to background Celery runners without blocking the server HTTP thread.
*   **Preconditions**: Celery background worker is running; Redis queue broker is active; PostgreSQL is initialized.
*   **Input Data**: Audit log parameters (User ID: `FARMER-99`, Type: `fertilizer`, Inputs: JSON payload).
*   **Execution Steps**:
    1. Send a POST request to the backend prediction endpoint containing the audit log parameters.
    2. Monitor database records immediately after submission.
    3. Assert that a database row is inserted with sync status `Pending Sync` before the task queue finishes processing.
*   **Expected Outcome**: Backend inserts database records and responds to the client in under two seconds, routing the blockchain commit task asynchronously.

### AS-MTS-INT-03: Sepolia RPC Blockchain Write Sync
*   **Verification Objective**: Confirm that background worker classes sign transactions and commit audit data to the Sepolia Ethereum test network.
*   **Preconditions**: Celery worker is active; test wallet contains Sepolia Ethereum gas resources; Infura gateways are configured.
*   **Input Data**: Background worker task object (Audit log primary key database ID).
*   **Execution Steps**:
    1. Trigger the background blockchain sync worker task passing the audit log database ID.
    2. Intercept RPC transactions to verify wallet signature validation.
    3. Wait for block validation logs.
    4. Check the PostgreSQL database record for updates.
*   **Expected Outcome**: Database status updates to `Synchronized` and commits a valid Sepolia transaction receipt hash starting with `0x`.

### AS-MTS-INT-04: Google Gemini advisory prompt processing
*   **Verification Objective**: Validate that weather guidelines prompt constructions extract advisory responses via external large language model cognitive engines.
*   **Preconditions**: Google Gemini API connection is configured; API credentials are active.
*   **Input Data**: Weather telemetry dictionary (Temperature: 40.0, Humidity: 85.0, Rainfall: 5.0).
*   **Execution Steps**:
    1. Execute the Weather AI API endpoint using the input telemetry dictionary.
    2. Capture the prompt structure sent to the language model interface.
    3. Verify that the prompt contains agricultural context rules.
    4. Assert the response contains readable advice text blocks.
*   **Expected Outcome**: API returns formatted text agricultural advice blocks in under two seconds.

---

## 5. End-to-End System Test Cases

### AS-MTS-SYS-01: Rural Farmer crop forecasting path
*   **Verification Objective**: Verify end-to-end flow of crop forecasting from form input to results rendering.
*   **Preconditions**: Mobile device connected to staging network; user logged in as Rural Farmer.
*   **Input Data**: Credentials: user `farmer_test`, password `Password123!`; Inputs: N: 80, P: 40, K: 40, pH: 6.0, Rainfall: 150.0.
*   **Execution Steps**:
    1. Launch the mobile application.
    2. Login with credentials and navigate to the Crop Form Screen.
    3. Input metrics and submit the form.
    4. Verify that the Diagnostic Results Screen displays the predicted crop name and AI advice.
*   **Expected Outcome**: User successfully logs in, submits metrics, and views recommendation results on-screen in under two seconds.

### AS-MTS-SYS-02: Scientific Review Inspector Registry Auditing
*   **Verification Objective**: Verify that administrative inspectors search PostgreSQL audit databases and verify transactions via external links.
*   **Preconditions**: User logged in as Scientific Review Inspector; at least one synchronized audit record exists.
*   **Input Data**: Credentials: user `inspector_test`, password `AdminPassword123!`.
*   **Execution Steps**:
    1. Launch application and log in as inspector.
    2. Navigate to the Historical Audit Registry view.
    3. Input keyword search `FARMER-101` in search query field.
    4. Verify the matching record is displayed.
    5. Click the transaction hash hyperlink to open the external block explorer view.
*   **Expected Outcome**: Inspector searches audit logs and opens blockchain validation links successfully.

### AS-MTS-SYS-03: Multi-lingual Urdu/English UI Switch
*   **Verification Objective**: Validate that on-screen titles, validation error alerts, and hint text switch instantly between Urdu and English.
*   **Preconditions**: User is on the Home Dashboard.
*   **Input Data**: UI localization switch triggers.
*   **Execution Steps**:
    1. Click the Urdu language toggle button.
    2. Verify form labels and navigation headers update.
    3. Click the English language toggle button.
    4. Verify form text updates back to English.
*   **Expected Outcome**: View layouts dynamically render localization translations without layout shifts or text overlaps.

### AS-MTS-SYS-04: Security session validation
*   **Verification Objective**: Verify that user accounts with weak password credentials are blocked before creation.
*   **Preconditions**: User is on the Registration view.
*   **Input Data**: Registration username `test_user`, weak password `12345`.
*   **Execution Steps**:
    1. Input username and weak password in form fields.
    2. Click register.
    3. Assert the interface blocks submission and displays a complexity warning message.
*   **Expected Outcome**: UI alerts user of complexity requirements and blocks registration requests.

---

## 6. Operational & Installation Smoke Test Cases

### AS-MTS-OPS-01: High-Availability Offline Heuristics Timeout Interception
*   **Verification Objective**: Validate that mobile network interceptors redirect operations to the local offline rules engine within five hundred milliseconds of network timeout.
*   **Preconditions**: Mobile device connected to network emulator slot configured with a six-second latency delay.
*   **Input Data**: Input metrics (N: 50, P: 30, K: 40).
*   **Execution Steps**:
    1. Submit crop recommendations on the form.
    2. Verify that network call is intercepted at exactly five hundred milliseconds.
    3. Assert that execution redirects to local SQLite and rules engines.
*   **Expected Outcome**: Network calls intercept and fall back within five hundred milliseconds of timeout.

### AS-MTS-OPS-02: Deterministic Local Weather Fallback UI
*   **Verification Objective**: Verify that the interface displays local fallback weather advice and orange warning banners under offline states.
*   **Preconditions**: Mobile device offline mode is activated.
*   **Input Data**: Mock weather rules inputs (Temperature: 42.0, Humidity: 85.0).
*   **Execution Steps**:
    1. Navigate to the Weather Smart Screen.
    2. Verify that the system evaluates local threshold paths (High heat and humidity rules).
    3. Check for the presence of the persistent orange warning banner.
*   **Expected Outcome**: Weather advisor renders deterministic fallback suggestions with an orange warning banner.

### AS-MTS-OPS-03: Cloud Staging slot deployment check
*   **Verification Objective**: Validate the deployment candidate build on the staging cloud slot.
*   **Preconditions**: Deployment build is committed to staging environments.
*   **Input Data**: Staging API health check request.
*   **Execution Steps**:
    1. Trigger the health check API request to the staging cloud instance.
    2. Verify HTTP status response.
    3. Verify connectivity check outputs to database services.
*   **Expected Outcome**: Staging server returns a status code two hundred response indicating all internal storage integrations are online.
