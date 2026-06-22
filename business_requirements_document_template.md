# Stanford University Administrative Systems
## Business Requirements Document

**Project Name:** AgroSmart (Enterprise Agricultural Intelligence Platform)  
**Document Version:** 1.0  
**Date:** 06/22/2026  

---

### Authors
| Name | Role | Department |
| :--- | :--- | :--- |
| Muhammad Omer Siddiqui | Engagement Director & Lead Architect | Core Architecture & Management |
| Dr. Elena Rostova | Full-Stack Backend & Data Specialist | Backend Engineering |
| Tariq Mahmood | Frontend Mobile & QA Specialist | Mobile UI/UX & Testing |

### Document History
| Date | Version | Document Revision Description | Document Author |
| :--- | :--- | :--- | :--- |
| 06/22/2026 | 1.0 | Initial Scope Baseline & Core Requirements Definition | Muhammad Omer Siddiqui |

### Approvals
| Approval Date | Approved Version | Approver Role | Approver |
| :--- | :--- | :--- | :--- |
| 06/22/2026 | 1.0 | Project Sponsor | Client Venture Team |
| 06/22/2026 | 1.0 | Lead Solution Architect | Muhammad Omer Siddiqui |

---

## Contents
1. [Introduction](#1-introduction)
   1.1. [Purpose of the Document](#11-purpose-of-the-document)
   1.2. [Document Conventions, Terms, and Definitions](#12-document-conventions-terms-and-definitions)
   1.3. [Intended Audience and Reading Suggestions](#13-intended-audience-and-reading-suggestions)
   1.4. [Scope](#14-scope)
        1.4.1. [Project Scope](#141-project-scope)
        1.4.2. [Business Requirement Document Scope](#142-business-requirement-document-scope)
   1.5. [References](#15-references)
2. [Overall Description](#2-overall-description)
   2.1. [Project Overview](#21-project-overview)
   2.2. [Product Features](#22-product-features)
   2.3. [User Classes and Characteristics](#23-user-classes-and-characteristics)
   2.4. [Operating Environment](#24-operating-environment)
   2.5. [Design and Implementation Constraints](#25-design-and-implementation-constraints)
   2.6. [User Documentation](#26-user-documentation)
   2.7. [Assumptions, Dependencies, and Risks](#27-assumptions-dependencies-and-risks)
3. [System Features](#3-system-features)
   3.1. [Dual-Model Machine Learning Inference (Priority: Critical)](#31-dual-model-machine-learning-inference-priority-critical)
        3.1.1. [Description](#311-description)
        3.1.2. [Stimulus/Response Sequences](#312-stimuluscallresponse-sequences)
        3.1.3. [Functional Requirements](#313-functional-requirements)
               3.1.3.1. [Use Cases](#3131-use-cases)
   3.2. [High-Availability Offline Fallback Engine (Priority: Critical)](#32-high-availability-offline-fallback-engine-priority-critical)
        3.2.1. [Description](#321-description)
        3.2.2. [Stimulus/Response Sequences](#322-stimuluscallcallresponse-sequences)
        3.2.3. [Functional Requirements](#323-functional-requirements)
               3.2.3.1. [Use Cases](#3231-use-cases)
   3.3. [Fuzzy-Text Pesticide Knowledge Lookup (Priority: High)](#33-fuzzy-text-pesticide-knowledge-lookup-priority-high)
        3.3.1. [Description](#331-description)
        3.3.2. [Stimulus/Response Sequences](#332-stimuluscallresponse-sequences)
        3.3.3. [Functional Requirements](#333-functional-requirements)
               3.3.3.1. [Use Cases](#3331-use-cases)
   3.4. [Local SQLite Caching and History Synchronization (Priority: High)](#34-local-sqlite-caching-and-history-synchronization-priority-high)
        3.4.1. [Description](#341-description)
        3.4.2. [Stimulus/Response Sequences](#342-stimuluscallresponse-sequences)
        3.4.3. [Functional Requirements](#343-functional-requirements)
               3.4.3.1. [Use Cases](#3431-use-cases)
   3.5. [Firebase User Authentication and Session Security (Priority: Critical)](#35-firebase-user-authentication-and-session-security-priority-critical)
        3.5.1. [Description](#351-description)
        3.5.2. [Stimulus/Response Sequences](#352-stimuluscallcallresponse-sequences)
        3.5.3. [Functional Requirements](#353-functional-requirements)
               3.5.3.1. [Use Cases](#3531-use-cases)
   3.6. [Dynamic Location-Based Weather Advisory Dashboard (Priority: High)](#36-dynamic-location-based-weather-advisory-dashboard-priority-high)
        3.6.1. [Description](#361-description)
        3.6.2. [Stimulus/Response Sequences](#362-stimuluscallcallcallcallresponse-sequences)
        3.6.3. [Functional Requirements](#363-functional-requirements)
               3.6.3.1. [Use Cases](#3631-use-cases)
4. [External Interface Requirements](#4-external-interface-requirements)
   4.1. [User Interface](#41-user-interface)
   4.2. [Hardware Interfaces](#42-hardware-interfaces)
   4.3. [Software Interfaces](#43-software-interfaces)
   4.4. [Communications Interfaces](#44-communications-interfaces)
   4.5. [Reporting Requirements](#45-reporting-requirements)
5. [Other Nonfunctional Requirements](#5-other-nonfunctional-requirements)
   5.1. [Performance Requirements](#51-performance-requirements)
   5.2. [Security Requirements](#52-security-requirements)
   5.3. [Data Requirements](#53-data-requirements)
   5.4. [Software Quality Attributes](#54-software-quality-attributes)
6. [Other Requirements](#6-other-requirements)
7. [Campus Readiness and Training](#7-campus-readiness-and-training)
* [Appendix A: Glossary](#appendix-a-glossary)
* [Appendix B: Analysis Models](#appendix-b-analysis-models)
* [Appendix C: Issues List](#appendix-c-issues-list)
* [Appendix D: Screenshots, Mock-Ups, and Live Links](#appendix-d-screenshots-mock-ups-and-live-links)
* [Appendix E: Test Scenarios](#appendix-e-test-scenarios)

---

## 1. Introduction

### 1.1. Purpose of the Document
The purpose of this Business Requirements Document (BRD) is to establish a rigorous, legally and technically binding contract defining the functional, non-functional, and interface requirements for the **AgroSmart Enterprise Agricultural Intelligence Platform**. 

Regional crop yields are severely impacted by unscientific farming, erratic fertilizer application, and a lack of real-time diagnostic tools. This unscientific approach leads to soil acidification, chemical over-application, and crop failure. The AgroSmart platform aims to mitigate these risks by providing an integrated, client-server agricultural intelligence framework. This framework consists of a cross-platform Flutter mobile client and a Python Django REST API backend. It delivers localized, data-driven soil analyses, crop predictions, pesticide recommendations, and real-time weather tips.

This document translates business goals, user profiles, and architectural constraints into concrete specifications. Under the ISO 21502:2020 compliance guidelines, it serves as the definitive technical contract. It must be approved by all stakeholders prior to the commencement of source code construction or database schema initialization. All software features, APIs, and components will be verified and validated against the requirements defined herein.

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
| Pesticide Lookup | REQ-PE-001 | Fuzzy Symptom Keyword Lookup Search | #7 |
| Pesticide Lookup | REQ-PE-002 | Default Organic Neem Oil Fallback | #8 |
| Local Database | REQ-DB-001 | Automatic Database Local Logging | #9 |
| Local Database | REQ-DB-002 | Categorical Tag Query Filtering | #10 |
| Local Database | REQ-DB-003 | Historical Entry Deletion | #11 |
| User Session | REQ-AU-001 | Firebase Authentication and Password Severity | #12 |
| User Session | REQ-AU-002 | Local Session Persistence and Auto-Login | #13 |
| Weather Tips | REQ-WE-001 | Geolocator Coordinates Tracking | #14 |
| Weather Tips | REQ-WE-002 | GPS Signal Loss Islamabad Default Fallback | #15 |
| Weather Tips | REQ-WE-003 | Gemini 2.0 Flash Advisory Response Schema Parsing | #16 |

---

### 3.1. Dual-Model Machine Learning Inference (Priority: Critical)

#### 3.1.1. Description
The platform shall evaluate incoming soil chemical metrics and return crop suggestions and fertilizer mixture solutions. This feature relies on two pre-trained RandomForestClassifier models loaded at Django startup.

#### 3.1.2. Stimulus/Response Sequences
*   **User Action:** User inputs soil metrics (N, P, K, pH, moisture) and taps "Get Recommendation".
*   **System Response:** Client compiles payload, transmits to Django, runs model file evaluations, returns recommended name, and caches metrics in SQLite.

#### 3.1.3. Functional Requirements
*   **REQ-ML-001: Soil Payload Validation**  
    The backend shall reject any POST payload mapping variables outside typical agricultural limits:
    *   Nitrogen (N) must be bounded between `0.0` and `140.0`.
    *   Phosphorus (P) must be bounded between `0.0` and `145.0`.
    *   Potassium (K) must be bounded between `0.0` and `205.0`.
    *   Soil pH must be bounded between `0.0` and `14.0`.
    *   Temperature must be bounded between `0.0` and `50.0`°C.
    *   Humidity must be bounded between `0.0` and `100.0`%.
    *   Rainfall must be bounded between `0.0` and `300.0` mm.
*   **REQ-ML-002: Non-standard Parameter Mapping**  
    The fertilizer prediction endpoint (`/api/fertilizer/`) shall accept parameters using the exact strings:
    *   `Temparature` (with 'a' in the second syllable)
    *   `Humidity ` (with a trailing space character)
    *   `Phosphorous` (with 'o' before 'u')
*   **REQ-ML-003: Model Output Target Mapping**  
    The system shall decode model prediction outputs using target encoders to map numeric classifications back to their human-readable strings (e.g. crop classification classes like `rice`, `maize`, or fertilizer formulas like `Urea`, `DAP`).

##### 3.1.3.1. Use Cases

| Field | Description / Value |
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
Executes a deterministic rules engine natively on the mobile client if backend network requests time out or fail.

#### 3.2.2. Stimulus/Response Sequences
*   **User Action:** User initiates weather tip lookup.
*   **System Response:** Device network monitor detects a timeout exceeding 5 seconds, intercepts the process, triggers `get_fallback_advice()`, and renders the result with a persistent offline banner.

#### 3.2.3. Functional Requirements
*   **REQ-OF-001: Automated Timeout Interception**  
    The client shell shall intercept HTTP timeouts in under 500ms and swap connection streams to the local logic block.
*   **REQ-OF-002: Deterministic Rule Application**  
    The client logic shall output advice based on local thresholds:
    *   Temp > 38°C -> watering = "Yes - Extreme heat!", fertilizer = "Wait - Heat causes burn", pest = "High - mites", tip = "Provide shade".
    *   Humidity > 80% -> watering = "No", fertilizer = "Wait - risk of fungus", pest = "High - fungal risk", tip = "Ensure good air circulation".
    *   Rain/Thunderstorm -> watering = "No", fertilizer = "Wait", pest = "Medium", tip = "Cover sensitive crops".
*   **REQ-OF-003: UI Offline Banner Warning**  
    Renders a persistent, orange caution banner displaying the offline state.

##### 3.2.3.1. Use Cases

| Field | Description / Value |
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

### 3.3. Fuzzy-Text Pesticide Knowledge Lookup (Priority: High)

#### 3.3.1. Description
Provides localized diagnostic matches by parsing user symptom descriptions against a disease lookup table using fuzzy keyword matching.

#### 3.3.2. Stimulus/Response Sequences
*   **User Action:** User enters the target crop name (e.g. `rice`) and a symptom description (e.g. `leaves have brown spots`) and taps "Get Treatment".
*   **System Response:** System compares description against active symptom keywords, extracts matching entries, and returns dosage and application details.

#### 3.3.3. Functional Requirements
*   **REQ-PE-001: Fuzzy Keyword Parsing**  
    The system shall evaluate symptom descriptions using fuzzy matching against target disease keywords (including `blast`, `brown spot`, `stem borer`, `leaf folder`, `rust`, `mildew`, `armyworm`, `bollworm`, `whitefly`, `aphid`, `leaf miner`, `fruit borer`).
*   **REQ-PE-002: Organic Treatment Fallback Defaults**  
    If the symptom description does not match any keyword in the database, the system shall default to returning a standardized organic Neem Oil treatment regimen (dosage: `5ml per liter water`, frequency: `every 7 days`).

##### 3.3.3.1. Use Cases

| Field | Description / Value |
| :--- | :--- |
| **Use Case ID** | UC-PE-001 |
| **Use Case Name** | Fuzzy Pesticide Search |
| **Actors** | Rural Farmer |
| **Description** | Finds treatment recommendations for crop diseases. |
| **Trigger** | Farmer submits crop and symptom descriptions. |
| **Preconditions** | Selected crop matches one of the autocomplete options. |
| **Postconditions** | Returns chemical or organic treatment instructions. |
| **Normal Flow** | 1. User selects crop name (e.g., `tomato`).<br>2. User types symptoms (e.g., `leaves show white powder`).<br>3. System maps input to generic categories (e.g., tomato -> vegetable).<br>4. System matches `white powder` to `powdery mildew` keyword.<br>5. Returns target pesticide formulation and application instructions. |
| **Alternative Flow** | *Alternative Flow A (No Keyword Match):* System defaults to returning organic Neem Oil fallback instructions. |
| **Exceptions** | Empty crop name or symptoms block submission. |
| **Includes** | Local Database Cache Sync |
| **Priority** | High |
| **Frequency of Use** | As-needed during pest outbreaks |
| **Business Rules** | Vegetables (tomato, potato, brinjal, chili, onion) map to a generic "vegetable" database index. |
| **Special Requirements**| UI must support autocomplete crop selection. |
| **Assumptions** | Farmer can identify visual symptoms of the crop. |
| **Notes and Issues** | Defaults are organic to avoid chemical over-application. |

---

### 3.4. Local SQLite Caching and History Synchronization (Priority: High)

#### 3.4.1. Description
Provides offline data accessibility by automatically caching user diagnostic parameters and recommendation reports into a client-side SQLite database.

#### 3.4.2. Stimulus/Response Sequences
*   **User Action:** User views a successful recommendation result.
*   **System Response:** System automatically executes a background database write to store the query inputs and result outputs in the local cache, updating the history badge count.

#### 3.4.3. Functional Requirements
*   **REQ-DB-001: Automatic Local Database Cache**  
    The mobile client shall save all query variables and output recommendations to the local SQLite database immediately upon receipt of a successful server response.
*   **REQ-DB-002: Categorical and Keyword Filtering**  
    The History Screen shall support local keyword searching (e.g., filtering logs by crop name) and categorical filter chips (Crops, Fertilizers, Pesticides, Weather).
*   **REQ-DB-003: History Record Deletion**  
    The application shall support swipe-to-delete gestures on history cards, removing records from database storage and updating the cache list.

##### 3.4.3.1. Use Cases

| Field | Description / Value |
| :--- | :--- |
| **Use Case ID** | UC-DB-001 |
| **Use Case Name** | Historical Log Verification |
| **Actors** | Rural Farmer, Scientific Inspector |
| **Description** | Reviews past diagnostic logs cached on the mobile device. |
| **Trigger** | Taps the History icon in the dashboard. |
| **Preconditions** | SQLite file is active on device storage. |
| **Postconditions** | Lists historical advice cards. |
| **Normal Flow** | 1. User navigates to History Screen.<br>2. SQLite query loads saved records.<br>3. User applies the "Fertilizer" category chip.<br>4. List filters to display only fertilizer queries.<br>5. User taps a record to expand input/output details. |
| **Alternative Flow** | *Alternative Flow A (Log Deletion):* User swipes left on a log card; system deletes the record and updates the list. |
| **Exceptions** | Database read locks are handled gracefully. |
| **Includes** | None |
| **Priority** | High |
| **Frequency of Use** | Multiple times daily |
| **Business Rules** | Swipe-to-delete deletes data permanently from local storage. |
| **Special Requirements**| Deletion must sync dynamically with the home page badge count. |
| **Assumptions** | Local SQLite file database has read/write permissions. |
| **Notes and Issues** | Cached records persist even if the app cache is cleared. |

---

### 3.5. Firebase User Authentication and Session Security (Priority: Critical)

#### 3.5.1. Description
Secures user data and diagnostic histories by forcing user registration and session verification before enabling cloud features.

#### 3.5.2. Stimulus/Response Sequences
*   **User Action:** User inputs credentials and taps "Login".
*   **System Response:** System validates parameters, sends request to Firebase Authentication, verifies the token, caches session keys, and routes the user to the home dashboard.

#### 3.5.3. Functional Requirements
*   **REQ-AU-001: Firebase Authentication Integration**  
    The application shall handle registration and logins using the Firebase Authentication SDK. Sign-up forms must enforce strong password rules:
    *   Minimum length: 8 characters.
    *   At least one uppercase letter.
    *   At least one numeric digit.
    *   At least one special character (`!@#$%^&*`).
*   **REQ-AU-002: Persistent Session and Auto-Login Caching**  
    The system shall save authentication tokens locally. On launch, the splash screen will check token validity, bypassing the login portal for active sessions.

##### 3.5.3.1. Use Cases

| Field | Description / Value |
| :--- | :--- |
| **Use Case ID** | UC-AU-001 |
| **Use Case Name** | Farmer Account Login |
| **Actors** | Rural Farmer |
| **Description** | Logs user into the app using email and password. |
| **Trigger** | User submits the Login form. |
| **Preconditions** | Device has an active internet connection. |
| **Postconditions** | Caches session token; grants app access. |
| **Normal Flow** | 1. User inputs email and password.<br>2. System validates input formats.<br>3. Request is sent to Firebase.<br>4. Firebase validates credentials and returns a session token.<br>5. App stores session token locally and opens the Dashboard. |
| **Alternative Flow** | *Alternative Flow A (Offline Login attempt):* System blocks execution and displays a message prompting the user to connect to the internet. |
| **Exceptions** | Invalid password format displays inline errors. |
| **Includes** | None |
| **Priority** | Critical |
| **Frequency of Use** | Daily |
| **Business Rules** | Session token expiration must force a redirection to the Login Screen. |
| **Special Requirements**| Login form must use non-resizing root layouts to prevent keyboard overlap. |
| **Assumptions** | Firebase services are accessible in the region. |
| **Notes and Issues** | Password complexity limits are validated client-side. |

---

### 3.6. Dynamic Location-Based Weather Advisory Dashboard (Priority: High)

#### 3.6.1. Description
Integrates local weather coordinates with generative AI prompts to supply dynamic, weather-based farming instructions.

#### 3.6.2. Stimulus/Response Sequences
*   **User Action:** User selects "Use GPS Location" and taps "Get Weather Tips".
*   **System Response:** System reads coordinates from the GPS receiver, calls OpenWeatherMap, compiles weather values, runs Google Gemini advice generation, and displays the structured outputs.

#### 3.6.3. Functional Requirements
*   **REQ-WE-001: GPS Location Sourcing**  
    The client app shall request location permissions and query the device GPS to retrieve current latitude and longitude coordinates.
*   **REQ-WE-002: GPS Signal Loss Default Fallback**  
    If the device GPS is unavailable or permissions are denied, the system shall fallback to using default coordinates for Islamabad (`33.6844, 73.0479`) and allow manual latitude and longitude entry.
*   **REQ-WE-003: Gemini Advice Prompt and Schema Parsing**  
    The backend shall compile coordinates, query OpenWeatherMap, and structure a prompt for Google Gemini 2.0 Flash. The API response must be parsed and mapped to four specific sections: `💧 WATERING`, `🌱 FERTILIZER`, `🐛 PEST RISK`, and `✅ TIP`.

##### 3.6.3.1. Use Cases

| Field | Description / Value |
| :--- | :--- |
| **Use Case ID** | UC-WE-001 |
| **Use Case Name** | Weather AI Advisory Sourcing |
| **Actors** | Rural Farmer |
| **Description** | Generates AI farming tips using live weather data. |
| **Trigger** | Farmer taps "Get Weather Tips". |
| **Preconditions** | Selected crop field is optionally filled. |
| **Postconditions** | Renders parsed weather dashboard. |
| **Normal Flow** | 1. User selects weather diagnostic tool.<br>2. App queries GPS and returns coordinates.<br>3. Server queries OpenWeatherMap with coordinates.<br>4. Weather metrics are compiled and sent to Gemini.<br>5. Response is parsed and rendered in the dashboard. |
| **Alternative Flow** | *Alternative Flow A (Manual Entry):* Farmer manually enters coordinates or selects from quick-select city buttons. |
| **Exceptions** | If weather API limits are reached, the system triggers deterministic offline rules. |
| **Includes** | Local Database Cache Sync |
| **Priority** | High |
| **Frequency of Use** | Daily |
| **Business Rules** | Response format must strictly follow the 4-tier schema. |
| **Special Requirements**| Visual widgets must adapt dynamically based on local weather conditions. |
| **Assumptions** | Active API keys are configured on the server. |
| **Notes and Issues** | Fallbacks ensure utility even in regions with poor connectivity. |

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
    You are an agricultural expert advising a farmer in {location} growing {crop_type or 'crops'}.
    Weather: {temp}°C, {humidity}% humidity, {conditions}, wind {wind_speed} m/s.
    Give VERY SHORT advice in EXACT format:
    💧 WATERING: (Yes/No) - (4-5 words reason)
    🌱 FERTILIZER: (Good/Wait) - (4-5 words reason)
    🐛 PEST RISK: (Low/Medium/High) - (3-4 words)
    ✅ TIP: (one 5-8 word sentence)
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

## Appendix A: Glossary
*   **API:** Application Programming Interface.
*   **BRD:** Business Requirements Document.
*   **CapEx:** Capital Expenditure.
*   **ML:** Machine Learning.
*   **NPK:** Nitrogen, Phosphorus, Potassium.

## Appendix B: Analysis Models

```text
+-----------------------+         Inputs Soil Data         +-----------------------+
|  Farmer Mobile Client |  ----------------------------->  |   Django REST API     |
+-----------------------+                                  +-----------------------+
     ^             |                                            |             |
     |             | Caches Queries                             |             | Runs Models
     |             v                                            v             v
+-----------------------+                                  +-----------------------+
|   Local SQLite DB     |                                  | RandomForest Classifier|
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

## Appendix C: Issues List
*   **Data Ingestion Typos:** The pre-trained fertilizer prediction model was trained on dataset columns containing minor typographical errors. To ensure model compatibility, front-end inputs and database schemas must match these typos:
    *   `Temparature` (misspelled)
    *   `Humidity ` (trailing space)
    *   `Phosphorous` (misspelled)

## Appendix D: Screenshots, Mock-Ups, and Live Links
*   **Login Mock-Up:** A glassmorphism container card overlaying a looping ambient video background.
*   **Dashboard Mock-Up:** A profile header banner showing farmer stats, followed by a grid layout of service buttons.
*   **Diagnosis Mock-Up:** Clean numeric form inputs accompanied by a top guide banner listing safe ranges.

## Appendix E: Test Scenarios
1.  **Model Serialization Validation Test:** Verify that the backend API loads the crop and fertilizer `.pkl` models at startup and runs inference without raising serializing exceptions.
2.  **Network Drop Timeout Test:** Simulate network dropouts during weather requests and verify that the client triggers the local fallback engine in under 500ms.
3.  **Typo Input Preservation Test:** Verify that the `/api/fertilizer/` endpoint processes requests containing the non-standard fields (`Temparature`, `Humidity `, and `Phosphorous`) without returning validation errors.