# Stanford University Administrative Systems Business Requirements Document
## Project Name: AgroSmart (Enterprise Agricultural Intelligence Platform)
**DOCUMENT VERSION:** 1.0  
**AUTHORS:** Muhammad Omer Siddiqui (Engagement Director & Lead Architect)  

---

### AUTHORS
| Name | Role | Department |
| :--- | :--- | :--- |
| Muhammad Omer Siddiqui | Engagement Director & Lead Architect | Core Architecture & Management |
| Dr. Elena Rostova | Full-Stack Backend & Data Specialist | Backend Engineering |
| Tariq Mahmood | Frontend Mobile & QA Specialist | Mobile UI/UX & Testing |

### DOCUMENT HISTORY
| Date | Version | Document Revision Description | Document Author |
| :--- | :--- | :--- | :--- |
| 06/22/2026 | 1.0 | Initial Scope Baseline & Core Requirements Definition | Muhammad Omer Siddiqui |

### APPROVALS
| Approval Date | Approved Version | Approver Role | Approver |
| :--- | :--- | :--- | :--- |
| 06/22/2026 | 1.0 | Project Sponsor | Client Venture Team |
| 06/22/2026 | 1.0 | Lead Solution Architect | Muhammad Omer Siddiqui |

---

## Contents
1. Introduction
   1.1. Purpose of the Document
   1.2. Document Conventions, Terms, and Definitions
   1.3. Intended Audience and Reading Suggestions
   1.4. Scope
      1.4.1. Project Scope
      1.4.2. Business Requirement Document Scope
   1.5. References
2. Overall Description
   2.1. Project Overview
   2.2. Product Features
   2.3. User Classes and Characteristics
   2.4. Operating Environment
   2.5. Design and Implementation Constraints
   2.6. User Documentation
   2.7. Assumptions, Dependencies, and Risks
3. System Features
   3.1. Dual-Model Machine Learning Inference (Priority: Critical)
      3.1.1. Description
      3.1.2. Stimulus/Response Sequences
      3.1.3. Functional Requirements
         3.1.3.1. Use Cases
   3.2. High-Availability Offline Fallback Engine (Priority: Critical)
      3.2.1. Description
      3.2.2. Stimulus/Response Sequences
      3.2.3. Functional Requirements
         3.2.3.1. Use Cases
4. External Interface Requirements
   4.1. User Interface
   4.2. Hardware Interfaces
   4.3. Software Interfaces
   4.4. Communications Interfaces
   4.5. Reporting Requirements
5. Other Nonfunctional Requirements
   5.1. Performance Requirements
   5.2. Security Requirements
   5.3. Data Requirements
   5.4. Software Quality Attributes
6. Other Requirements
7. Campus Readiness and Training
*   Appendix A: Glossary
*   Appendix B: Analysis Models
*   Appendix C: Issues List
*   Appendix D: Screenshots, Mock-Ups, and Live Links
*   Appendix E: Test Scenarios

---

## 1. Introduction

### 1.1. Purpose of the Document
The purpose of this Business Requirements Document (BRD) is to establish the formal, legally binding functional and non-functional specifications contract for the **AgroSmart** platform. This document bridges business needs and software implementation prior to source code creation.

The core business need is mitigating critical regional crop yield deficits and unscientific chemical over-application. Many agricultural systems rely on subjective visual inspections or legacy habits. This guesswork leads to soil acidification, nutrient runoff, and crop failure. 

To mitigate these risks, the AgroSmart platform implements a client-server agricultural intelligence framework. This includes a cross-platform mobile client built using Flutter and a Python Django REST API backend. The platform provides data-driven soil analyses, crop recommendations, pesticide lookup, and real-time weather tips.

### 1.2. Document Conventions, Terms, and Definitions
*   **Typography:** The word **shall** denotes a binding, mandatory requirement. The word **will** indicates a future or projected system behavior. Standard font weights and headers differentiate components.
*   **Priority Inheritance:** Priorities established for system features (e.g., Critical, High, Medium, Low) are inherited by all child requirements.
*   **Literal Constraints:** All parameters derived from machine learning training datasets inherit strict character literal constraints. Typos present in training labels must be mirrored exactly in front-end forms, serialized endpoints, and database models to prevent scoring execution failures.

#### Technical Terms & Non-Standard Parameter Definitions

| Term / Parameter | Definition |
| :--- | :--- |
| **`Temparature`** | **Non-standard spelling (with 'a' in the second syllable)**. This exact string literal must be used for the soil temperature input parameter in all fertilizer recommendation payloads. |
| **`Humidity `** | **Non-standard format (containing a trailing space)**. This exact string literal with the space character must be used for the humidity input parameter in the fertilizer API payload. |
| **`Phosphorous`** | **Non-standard spelling (with 'o' before 'u')**. This exact string literal must be used for the phosphorus nutrient parameter in the fertilizer API payload. |
| **N, P, K** | Nitrogen (N), Phosphorus (P), and Potassium (K) chemical nutrient levels in the soil, measured in kilograms per hectare (kg/ha). |
| **Sepolia** | The Ethereum proof-of-stake public test network used to log cryptographic audit proofs of agricultural recommendations. |
| **Celery** | An asynchronous task queue/job queue based on distributed message passing, used to handle non-blocking blockchain writes. |
| **easy_localization** | The localization utility framework used on the mobile client to toggle translation bundles locally. |
| **Provider** | The state management package used in Flutter to manage authentication and API interaction flows. |

### 1.3. Intended Audience and Reading Suggestions
The target audience consists of the Core MVP Squad and the Shared Agency Tier, as outlined in the governance guidelines:

| Name | Designation/Job Title | Role (approve, review, create, maintain) |
| :--- | :--- | :--- |
| Muhammad Omer Siddiqui | Engagement Director & Lead Architect | Create, Maintain, Approve |
| Dr. Elena Rostova | Full-Stack Backend & Data Specialist | Create, Maintain, Review |
| Tariq Mahmood | Frontend Mobile & QA Specialist | Create, Maintain, Review |
| Marcus Vance | Scrum Master | Review |
| Alex Mercer | Backend Developer | Review, Maintain |
| Dr. Sarah Jenkins | Data Specialist | Review, Maintain |
| Kenji Sato | Blockchain Developer | Review, Create |
| Fatima Al-Sayed | DevOps Engineer | Review, Maintain |
| Client Venture Team | Project Sponsor Representative | Approve |

*   **Developers & QA Engineers:** Focus on Section 1.2 (Conventions), Section 3 (System Features), Section 4 (Interfaces), and Section 5 (NFRs).
*   **Scientific Inspectors / Auditors:** Focus on Section 2.3 (User Classes), Section 3.1 (ML Inference), and Section 6 (Sync Failures).
*   **Management & Project Sponsors:** Focus on Section 1.4 (Scope), Section 2.5 (Design Constraints), and Section 7 (Ready / Rollout).

### 1.4. Scope
The platform provides farmers with a data-driven alternative to subjective visual assessments. It targets macro crop yield inefficiencies, soil degradation, and poor resource allocation.

#### 1.4.1. Project Scope
The project scope is constrained by a fixed Capital Expenditure (CapEx) threshold of **$35,000**. This budget funds:
*   The deployment of the Django backend on Microsoft Azure Web Apps.
*   The configuration of the Azure PostgreSQL database.
*   The compilation and store deployment of the Flutter cross-platform mobile client.
*   All smart contract deployment and gas fees on the Sepolia Ethereum testnet.

#### 1.4.2. Business Requirement Document Scope
The scope of this BRD is strictly bounded to the initial Minimum Viable Product (MVP) launch of the AgroSmart system. It specifies the functional boundary lines of:
*   The user registration and session management via Firebase.
*   The crop and fertilizer prediction interfaces.
*   The localized pesticide lookup and weather tips modules.
*   The local SQLite offline caching system.
*   The backend Web3 transaction logger.

### 1.5. References
1.  **ISO 21502:2020:** Guidance on project management, scope baseline verification, and milestone execution.
2.  **Ethereum Sepolia Smart Contract Specification:** Interface and ABI guidelines for logging recommendations to the blockchain.
3.  **Google Gemini Version Two Flash API Documentation:** JSON payload formats for parsing weather parameters into structured advice.
4.  **OpenWeatherMap API Documentation:** REST endpoint schemas for coordinate-based meteorological lookups.

---

## 2. Overall Description

### 2.1. Project Overview
AgroSmart replaces traditional agricultural processes with a quantitative decision pipeline. The contrast between current operations and the proposed system is detailed below:

```text
[Current Subjective Process]
Farmer Visual Soil Inspection -> Guesswork Chemical Mix -> Manual Disease Lookup -> Sudden Weather Failures

[Proposed AgroSmart Process]
Enter NPK & pH Sensors -> RandomForest ML Classification -> Asynchronous Web3 Ledger Proof -> Offline Weather Fallbacks
```

Detailed Context Diagrams and Swim Lanes of these flows are outlined in Appendix B.

### 2.2. Product Features
The core features of the AgroSmart platform include:
1.  **Dual-Model ML Inference Engine:** Loads pre-trained Random Forest models to predict optimal crops and identify specific fertilizer deficiencies based on NPK, pH, moisture, and temperature.
2.  **Cognitive Advisory Layer:** Interfaces with Google Gemini 2.0 Flash to synthesize live local weather conditions and generate highly actionable farming instructions.
3.  **Non-Blocking Web3 Auditing:** Writes recommendation hashes to the Sepolia Ethereum testnet. This process runs in the background using Celery workers, preventing blockchain latency from blocking the mobile interface.
4.  **Multi-Language Accessibility UI:** Displays the interface in English or Urdu via a local toggle. Uses glassmorphism components and visual iconography to assist users with lower digital literacy.

### 2.3. User Classes and Characteristics
*   **Rural Farmers (Primary End Users):**
    *   *Characteristics:* Limited digital literacy, language reliance on Urdu, low cellular data budget, and operations in remote regions with unstable connectivity.
    *   *System Needs:* High-visibility layouts, instant locale toggles resolved locally on-device, and a local fallback rules engine that works without an active cellular connection.
*   **Scientific Review Inspectors & Auditors (Administrative Users):**
    *   *Characteristics:* High technical literacy, demanding transaction traceability and audit logs.
    *   *System Needs:* High-concurrency administrative query tools, secure authentication, and direct links to Sepolia blockchain explorer receipts to verify historical recommendation integrity.

### 2.4. Operating Environment
*   **Client Tier:** Cross-platform Flutter application running natively on iOS (version 15.0+) and Android (API Level 28+). Local data persistence is managed via an embedded SQLite file database.
*   **Server Tier:** Python Django REST API application hosted on Microsoft Azure Web Apps. The Django server binds to a high-availability Azure PostgreSQL instance.
*   **Web3 Infrastructure:** Public Sepolia Ethereum RPC nodes, connected via Infura Web3 providers.

### 2.5. Design and Implementation Constraints
1.  **Budget Constraint:** Total design, development, and deployment costs must not exceed the **$35,000** CapEx limit.
2.  **State Management Bounding:** The mobile client shall manage state exclusively through the `provider` package, and translations through `easy_localization`.
3.  **Asynchronous Transaction Offloading:** Direct blockchain transaction signing and mining shall be offloaded to background Celery workers. The HTTP response to the client must not wait for blockchain confirmation.
4.  **Non-Resizing Keyboard Layout:** To prevent rendering crashes on low-end devices, the mobile Scaffold's `resizeToAvoidBottomInset` property must be set to `false`. Keyboard overlap padding must be adjusted using view-insets.
5.  **Typographical Typo Alignment:** To prevent model inference failure, the front-end inputs and backend serializers must match the non-standard training labels: `Temparature` (misspelled), `Humidity ` (trailing space), and `Phosphorous` (misspelled).

### 2.6. User Documentation
*   **Visual Onboarding Guide:** Bundle of native animated assets displaying visual instruction maps for soil data testing.
*   **Localized Help Database:** SQLite-backed offline table containing explanations of Nitrogen, Phosphorus, Potassium, and pH variables in Urdu and English.

### 2.7. Assumptions, Dependencies, and Risks
*   **Assumptions:** Hardware devices retain GPS receivers and soil inputs remain within valid physical agricultural parameters.
*   **Dependencies:** Stable connection to OpenWeatherMap REST interfaces and Sepolia mining node synchronization.
*   **Risks:** Model drift over multi-year cycles. Swappable serialized `.pkl` configurations mitigate this risk.

---

## 3. System Features

The following table summarizes the requirements listed in Section 3:

| Component | Reference Number | Requirement Name | Issue # |
| :--- | :--- | :--- | :--- |
| Machine Learning | REQ-ML-001 | Soil Payload Schema Validation | #1 |
| Machine Learning | REQ-ML-002 | Non-standard Space/Typo Preservation | #2 |
| Machine Learning | REQ-ML-003 | Model Output Target Mapping | #3 |
| Offline Fallback | REQ-OF-001 | Latency Interceptor and Failover | #4 |
| Offline Fallback | REQ-OF-002 | Local Weather Threshold Calculation | #5 |
| Offline Fallback | REQ-OF-003 | Persistent Offline Visual Warning Banner | #6 |

---

### 3.1. Dual-Model Machine Learning Inference (Priority: Critical)

#### 3.1.1. Description
Ingest soil parameters and generate crop classification outputs and fertilizer recommendations from pre-trained RandomForest models loaded at startup.

#### 3.1.2. Stimulus/Response Sequences
*   **User Action:** User inputs soil metrics (N, P, K, pH, moisture) and taps "Get Recommendation".
*   **System Response:** Client compiles payload, transmits to Django, runs model file evaluations, returns recommended name, and caches metrics in SQLite.

#### 3.1.3. Functional Requirements
*   **REQ-ML-001: Soil Payload Validation**  
    The backend shall reject any POST payload mapping variables outside typical agricultural limits (e.g., pH outside range 0-14, NPK outside range 0-300).
*   **REQ-ML-002: Non-standard Parameter Mapping**  
    The fertilizer parser shall bind variables utilizing literals: `'Temparature'`, `'Humidity '` (trailing space), and `'Phosphorous'`.
*   **REQ-ML-003: Model Output Mapping**  
    The system shall decode numerical prediction indexes back to string outputs mapped to the local vocabulary.

##### Preconditions
Model `.pkl` files must be loaded into system memory.

##### Postconditions
Recommendation hash synced to the local SQLite DB.

##### Assumptions
User inputs reflect valid chemical sensor readings.

##### Risks
Serializing format mismatch causing backend 500 error outputs.

##### Exception Handling
If model processing throws exceptions, return dynamic JSON status "failed" and log error logs.

#### 3.1.3.1. Use Cases

| Field | Description |
| :--- | :--- |
| **Use Case ID** | UC-ML-001 |
| **Use Case Name** | Predictive Soil Recommendation |
| **Actors** | Rural Farmer |
| **Description** | Processes NPK values to return the recommended crop. |
| **Trigger** | Farmer submits the soil evaluation form. |
| **Preconditions** | App has authenticated state; soil guide database loaded. |
| **Postconditions** | Prediction returned; logged locally. |
| **Normal Flow** | 1. Farmer navigates to crop form.<br>2. Farmer reviews soil bounds info card.<br>3. Farmer enters NPK, temp, hum, pH, rain.<br>4. Farmer taps submit.<br>5. API runs inference and returns crop string. |
| **Alternative Flow** | *Alternative Flow A (Offline state):* API returns error; client displays dialog warning and caches metrics for sync. |
| **Exceptions** | Invalid number fields block submission; client shows inline error indicators. |
| **Includes** | Local Database Cache Sync |
| **Priority** | Critical |
| **Frequency of Use** | Weekly per farmer |
| **Business Rules** | Payload schema must match training data literals exactly. |
| **Special Requirements**| Must support instantaneous English-Urdu text swap. |
| **Assumptions** | Coordinates represent valid geographic values. |
| **Notes and Issues** | Tracks typos documented in Appendix C. |

---

### 3.2. High-Availability Offline Fallback Engine (Priority: Critical)

#### 3.2.1. Description
Executes a deterministic rules engine natively on the mobile client if backend network requests time out.

#### 3.2.2. Stimulus/Response Sequences
*   **User Action:** User initiates weather tip lookup.
*   **System Response:** Device network monitor detects a timeout exceeding 5 seconds, intercepts the process, triggers `get_fallback_advice()`, and renders the result with a persistent offline banner.

#### 3.2.3. Functional Requirements
*   **REQ-OF-001: Automated Timeout Interception**  
    The client shell shall intercept HTTP timeouts in under 500ms and swap connection streams to the local logic block.
*   **REQ-OF-002: Deterministic Rule Application**  
    The client logic shall output advice based on local thresholds:
    *   Temp > 38°C -> watering = "Yes", fertilizer = "Wait", pest = "High".
    *   Humidity > 80% -> watering = "No", fertilizer = "Wait", pest = "High".
*   **REQ-OF-003: UI Offline Banner Warning**  
    Renders a persistent, orange caution banner displaying the offline state.

##### Preconditions
Mobile location services must provide GPS coordinates.

##### Postconditions
Displays local rule-based warning metrics.

##### Assumptions
Meteorological variables can be queried locally.

##### Risks
Stale location parameters leading to outdated advice.

##### Exception Handling
If GPS values are missing, use default coordinates for Islamabad.

#### 3.2.3.1. Use Cases

| Field | Description |
| :--- | :--- |
| **Use Case ID** | UC-OF-001 |
| **Use Case Name** | Local Weather Fallback Processing |
| **Actors** | Rural Farmer |
| **Description** | Calculates weather advice locally when connectivity is lost. |
| **Trigger** | Device network request returns a timeout. |
| **Preconditions** | Location sensors are active. |
| **Postconditions** | Renders local rule outputs. |
| **Normal Flow** | 1. Farmer requests weather tips.<br>2. App timer exceeds 5 seconds.<br>3. System initiates fallback logic.<br>4. Reads current temp and humidity.<br>5. Computes and displays watering and fertilizer tips. |
| **Alternative Flow** | *Alternative Flow A (No GPS signal):* System falls back to default Islamabad coordinates. |
| **Exceptions** | If hardware sensors fail, prompt manual coordinate entry. |
| **Includes** | None |
| **Priority** | Critical |
| **Frequency of Use** | Daily |
| **Business Rules** | Fallback must run under 500ms. |
| **Special Requirements**| Displays a persistent offline status warning. |
| **Assumptions** | Offline rules reflect safe regional agricultural practices. |
| **Notes and Issues** | Rule thresholds align with regional crop requirements. |

---

## 4. External Interface Requirements

### 4.1. User Interface
*   **Immersive Login Screen:** Stacked container displaying glassmorphic card overlays on top of a looping background video file (`assets/videos/login_bg.mp4`).
*   **Keyboard Safety Padding:** The client application shall set `resizeToAvoidBottomInset` to `false` and calculate spacing manually:
    ```dart
    Padding(
      padding: EdgeInsets.only(bottom: MediaQuery.of(context).viewInsets.bottom),
      child: childContent,
    )
    ```
*   **Visual Elements:** Buttons must have a minimum tap target of 48x48 pixels. Icons accompany all form titles.

### 4.2. Hardware Interfaces
*   **GPS Receivers:** The mobile client connects to the native device GPS to retrieve latitude (`lat`) and longitude (`lon`) coordinates.
*   **Local Storage:** Reads and writes diagnostic logs to device flash storage using an SQLite database file.

### 4.3. Software Interfaces
*   **Django API Engine:** Connects via REST JSON protocols to process diagnostic models.
*   **OpenWeatherMap API:** Retrieves real-time local temperature and weather metrics.
*   **Google Gemini 2.0 Flash:** Receives weather data to generate farming tips. The parser enforces the following format:
    ```text
    💧 WATERING: (Yes/No) - (Reason)
    🌱 FERTILIZER: (Good/Wait) - (Reason)
    🐛 PEST RISK: (Low/Medium/High) - (Reason)
    ✅ TIP: (Advice)
    ```

### 4.4. Communications Interfaces
*   **Secure HTTPS:** All API traffic uses secure HTTPS connections.
*   **JSON Schema:** Enforces standard headers for all REST requests:
    ```json
    {
      "Content-Type": "application/json",
      "Accept": "application/json"
    }
    ```

### 4.5. Reporting Requirements
The backend logs all user queries to the centralized Azure PostgreSQL instance. Scientific Review Inspectors can query these records to audit recommendation accuracy, trace advice timestamps, and retrieve soil parameters.

---

## 5. Other Nonfunctional Requirements

### 5.1. Performance Requirements
*   **API Response Time:** API model inference processing must complete in under 2 seconds.
*   **Offline Transition Latency:** Switch to the local deterministic rules engine must occur within 500ms of a network timeout.
*   **SQLite Query Speed:** Database transactions on the client must execute in under 100ms.

### 5.2. Security Requirements
*   **Firebase Authentication:** Handles registration verification, enforcing strict password rules (length, case, numbers, special characters).
*   **Data Encryption:** Encrypts API tokens and cached credentials using Keychain (iOS) and Keystore (Android).

### 5.3. Data Requirements
*   **Client-Server Data Isolation:** 
    *   *SQLite DB:* Stores local history and query data on the user's device.
    *   *PostgreSQL DB:* Stores global audit records and system telemetry on the server.

### 5.4. Software Quality Attributes
*   **Robustness:** The application must remain operational without crashing during network connectivity drops or third-party service timeouts.
*   **Model Swap Compatibility:** The backend must load machine learning models dynamically from standard `.pkl` files at launch, allowing model files to be replaced without changing the core codebase.

---

## 6. Other Requirements

### 6.1. Web3 Network Latency Failover Protocol
Writing audit hashes directly to the Sepolia testnet requires transaction mining operations that can cause significant delay. To prevent blockchain network congestion from degrading mobile application performance, the system shall implement the following failover protocol:
1.  **Queue Deferral:** The API server will hand off the blockchain write task to a background task queue managed by Celery.
2.  **Immediate Client Response:** The REST API will return the recommendation output to the Flutter client without waiting for transaction mining to complete.
3.  **State Flags:** The background worker will write a `'Pending Blockchain Sync'` status flag into the database along with the transaction payload.
4.  **Transaction Execution:** The Celery worker will attempt to sign and broadcast the transaction to the Sepolia network. Once successfully mined, the database flag is updated to `'Synchronized'` and the transaction hash is saved.
5.  **Alerting & Recovery:** If transaction mining fails after three retries (due to network fees, gas errors, or node timeouts), the worker will log the failure status and trigger an automated alert to the DevOps reporting channel for manual recovery.

### 6.2. Technical Change Escalation Path
To prevent validation exceptions and schema mismatches between client forms, database columns, and ML training sets (such as the non-standard fields `'Temparature'`, `'Humidity '`, and `'Phosphorous'`), any proposed schema changes must follow this approval path:
1.  **Data Science Verification:** Dr. Sarah Jenkins verifies that changes do not impact machine learning performance.
2.  **Django Serializer Realignment:** Dr. Elena Rostova updates backend API models and validation rules.
3.  **Client-Side Parity Check:** Lead Architect Muhammad Omer Siddiqui updates Flutter input controllers.
4.  **Project Sponsor Sign-Off:** Final approval from the Project Sponsor before deploying changes to staging.

---

## 7. Campus Readiness and Training

### 7.1. Rollout Requirements
*   **Urdu/English Training Modules:** The mobile application bundles step-by-step visual training manuals in both English and Urdu.
*   **Azure Deployment Pipelines:** Fatima Al-Sayed manages CI/CD pipelines to build and deploy verified changes to the staging server.

---

## Appendices

### Appendix A: Glossary
*   **API:** Application Programming Interface.
*   **BRD:** Business Requirements Document.
*   **CapEx:** Capital Expenditure.
*   **ML:** Machine Learning.
*   **NPK:** Nitrogen, Phosphorus, Potassium.

### Appendix B: Data Flow Model

```text
+-----------------------+         Inputs Soil Data         +-----------------------+
|  Farmer Mobile Client |  ----------------------------->  |   Django REST API     |
+-----------------------+                                  +-----------------------+
     ^             |                                            |             |
     |             | Caches Queries                             |             | Runs Models
     |             v                                            v             v
+-----------------------+                                  +-----------------------+
|   Local SQLite DB     |                                  | RandomForest Classifer|
+-----------------------+                                  +-----------------------+
                                                                |
                                                                | Logs Audits (Celery)
                                                                v
                                                           +-----------------------+
                                                           |   Azure PostgreSQL    |
                                                           +-----------------------+
                                                                |
                                                                | Sync Transactions
                                                                v
                                                           +-----------------------+
                                                           |    Sepolia Network    |
                                                           +-----------------------+
```

### Appendix C: Issues List
*   **Data Ingestion Typos:** The pre-trained fertilizer prediction model was trained on dataset columns containing minor typographical errors. To ensure model compatibility, front-end inputs and database schemas must match these typos:
    *   `Temparature` (misspelled)
    *   `Humidity ` (trailing space)
    *   `Phosphorous` (misspelled)

### Appendix D: Screenshots, Mock-Ups, and Live Links
*   **Login Mock-Up:** A glassmorphism container card overlaying a looping ambient video background.
*   **Dashboard Mock-Up:** A profile header banner showing farmer stats, followed by a grid layout of service buttons.
*   **Diagnosis Mock-Up:** Clean numeric form inputs accompanied by a top guide banner listing safe ranges.

### Appendix E: Test Scenarios
1.  **Model Serialization Validation Test:** Verify that the backend API loads the crop and fertilizer `.pkl` models at startup and runs inference without raising serializing exceptions.
2.  **Network Drop Timeout Test:** Simulate network dropouts during weather requests and verify that the client triggers the local fallback engine in under 500ms.
3.  **Typo Input Preservation Test:** Verify that the `/api/fertilizer/` endpoint processes requests containing the non-standard fields (`Temparature`, `Humidity `, and `Phosphorous`) without returning validation errors.
