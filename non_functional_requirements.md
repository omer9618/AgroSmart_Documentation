# California Department of Technology — Consulting & Planning Division
## Non-Functional Requirements Document

**Project Name:** AgroSmart (Enterprise Agricultural Intelligence Platform)  
**Document Version:** 1.0  
**Date:** 06/22/2026  
**Origin:** Department of Technology, Consulting and Planning Division  

---

## Table of Contents
1. [Introduction](#1-introduction)
2. [Overview](#2-overview)
3. [Referenced Documents](#3-referenced-documents)
4. [Non-Functional Requirements](#4-non-functional-requirements)
   - 4.1 [Performance](#41-performance)
     - 4.1.1 [User Responsiveness](#411-user-responsiveness)
       - 4.1.1.1 [Normal User Load](#4111-normal-user-load)
       - 4.1.1.2 [End-of-Month Load (Peak Harvest/Sowing Load)](#4112-end-of-month-load-peak-harvestsowing-load)
     - 4.1.2 [Batch Processing](#412-batch-processing)
       - 4.1.2.1 [Background Ledger Auditing](#4121-background-ledger-auditing)
   - 4.2 [Security](#42-security)
     - 4.2.1 [Auditing](#421-auditing)
       - 4.2.1.1 [Recommendation Ledger Auditing](#4211-recommendation-ledger-auditing)
     - 4.2.2 [Session & Session Data Security](#422-session--session-data-security)
   - 4.3 [Compatibility](#43-compatibility)
     - 4.3.1 [Cross-Platform Native Compatibility](#431-cross-platform-native-compatibility)
     - 4.3.2 [Local Cache Compatibility](#432-local-cache-compatibility)
   - 4.4 [Maintainability](#44-maintainability)
     - 4.4.1 [Error Reporting](#441-error-reporting)
       - 4.4.1.1 [Application & Integration Errors](#4411-application--integration-errors)
       - 4.4.1.2 [Database Logging & Auditing Errors](#4412-database-logging--auditing-errors)
5. [Appendix A. Considerations](#appendix-a-considerations)

---

## 1. Introduction
Non-functional requirements identify the constraints upon the system and software by:
1.  Identifying environmental conditions for the system,
2.  The qualities the system must possess, and
3.  All other constraints applicable for the development and implementation of the system.

Non-functional requirements do not describe what the system and software will do in terms of the system or software’s functionality or behavior, nor do they identify deliverables or other transitional needs.

This document specifies the non-functional requirements for the system that have been elicited from the **AgroSmart** Project stakeholders. These non-functional requirements were then analyzed, elaborated, and formatted into a standard requirements structure, and then re-reviewed and validated by the stakeholders to ensure the defined requirements are correct, consistent, and necessary. The details of the process used are defined and described in the Requirements Definition Plan.

---

## 2. Overview
Each non-functional requirement specified in this document consists of five sections: **Scenario**, **Requirement**, **Constraints**, **Verification Method**, and **Notes**. For each non-functional requirement, all five sections must exist and each section must be consistent with the other sections as well as consistent across all non-functional requirements.

*   **Scenario**: "Sets the stage" or defines the context for the requirement. It identifies what is occurring within the system and external to the system, such as by actors within a Use Case context. This section is where the environmental conditions for the system are documented, including what the system is being exposed to, specific to each non-functional requirement.
*   **Requirement**: The actual non-functional requirement that will be measured when the scenario begins (e.g., the system shall have a response time of 1 second). This section is where the qualities that the system must possess are defined.
*   **Constraints**: Identifies all constraints upon the Scenario, Requirement, or Verification Method. A Constraint may be considered a limitation, a boundary, or other factor that must be considered when creating a solution that meets the identified Requirement. This section documents all constraints applicable for the development and implementation of the system.
*   **Verification Method**: Identifies the approach to how the requirement will be verified. It must identify a sound and reasonable method or approach that can be used to verify the requirement and the identified method must be consistent with and actually verify the specified requirement. If a Verification Method cannot be identified, this is a significant indicator that the requirement is poor and requires a different or alternate approach.
*   **Notes**: Available to document any additional information necessary to communicate the state’s needs for the specific requirement for further elaboration and understanding.

To establish consistency and to aid in communications, the following table matrix structure is used to document each requirement:

| ID# | Unique | "Name of the requirement" |
| :--- | :--- | :--- |
| **Scenario:** | Who or what initiates the scenario | The event that initiates the scenario \| The system or environmental conditions (e.g., normal operations, shutting down) \| Which part of system, or whole, is involved \| How is the system being stressed |
| **Requirement:** | What noticeable event happens as a result of the scenario | |
| **Constraints:** | Limitations, boundaries, other conditions that must be considered | |
| **Verification Method:** | Describe how the Requirement can be tested and verified | |
| **Notes:** | Additional information to help communicate the needs | |

---

## 3. Referenced Documents
The following documents were referenced and used in creating this deliverable; they also provide definitions and descriptions of non-functional requirements that are used in this document:
*   ISO/IEC/IEEE 24765:2010(E) Systems and software engineering – Vocabulary
*   IEEE “Guide to the Software Engineering Body of Knowledge® (SWEBOK®) Version 3.0”, January 17, 2014
*   IIBA “A Guide to the Business Analysis Body of Knowledge® (BABOK® Guide) Version 2.0”, March 31, 2009
*   SEI Technical Report CMU/SEI-95-TR-021, “Quality Attributes”, December 1995
*   “Understanding Quality Attributes in Software Architecture, 3rd Edition”, Len Bass, Paul Clements, Rick Kazman, Sep 25, 2012
*   **AgroSmart Business Requirements Document (BRD) Version 1.0**, June 22, 2026.
*   **AgroSmart Functional Specification Document (FSD) Version 1.0**, June 22, 2026.

## 4. Non-Functional Requirements

### 4.0. Requirements Traceability Matrix
The following matrix maps each Non-Functional Requirement (NFR) specified in this document back to the corresponding sections, constraints, and protocols defined in the AgroSmart Business Requirements Document (BRD):

| NFR ID | Requirement Name | Category | Primary BRD Mapping Section | Description |
| :--- | :--- | :--- | :--- | :--- |
| **NF-PU-01** | User Responsiveness (Normal Load) | Performance | BRD Section 5.1 (Performance) | API inference under 2s, SQLite under 100ms. |
| **NF-PU-02** | User Responsiveness (Peak Load) | Performance | BRD Section 5.1 (Performance) | Offline trigger under 500ms on 5s timeout. |
| **NF-PB-01** | Background Ledger Auditing | Performance | BRD Section 6.1 (Web3 Failover) | Celery background confirmation under 30s. |
| **NF-SA-01** | Recommendation Ledger Auditing | Security | BRD Section 5.3 (Data Isolation) & 6.1 | Sepolia auditing proof logs mapping. |
| **NF-SS-01** | Session Security & Encryption | Security | BRD Section 5.2 (Security) & 2.5 | Firebase credentials secure storage caching. |
| **NF-CC-01** | Cross-Platform Client | Compatibility | BRD Section 2.4 (Operating Environment) | iOS 15.0+ / Android API 28+ execution. |
| **NF-LC-01** | Local Cache Compatibility | Compatibility | BRD Section 5.3 (Data Isolation) & 5.1 | SQLite offline filtering and history query times. |
| **NF-ER-01** | Multi-Tier Application Errors | Maintainability | BRD Section 6.1 (Alerting & Recovery) | Interception log error codes (ERR-INT-101/104). |
| **NF-ER-02** | Ingestion Schema Typo Realignment | Maintainability | BRD Section 2.5 & 6.2 (Change Path) | Typo parameters alignment validations. |

---

### 4.1. Performance

#### 4.1.1. User Responsiveness

##### 4.1.1.1 Normal User Load
| ID# | NF-PU-01 | Normal User Load Responsiveness |
| :--- | :--- | :--- |
| **Scenario:** | • During normal farming operations (non-peak seasons), users query crop or fertilizer predictions from the mobile client interface.<br>• The system is in normal operating mode (active network connection, API online, and no background resource locks).<br>• The system receives requests at an average rate of 20 queries per minute across the entire user base. |
| **Requirement:** | • The backend API response time for model inference evaluations (crop recommendations and fertilizer mixture predictions) shall be less than 2.0 seconds for 95% of requests.<br>• The local SQLite caching queries on the mobile device shall execute in under 100 milliseconds. |
| **Constraints:** | Network delays beyond the system boundaries (local ISP, carrier network latency, or cellular signal dropouts) shall be excluded from the 2.0-second backend measurement. The 2.0-second time applies from when the HTTP payload enters the Azure Web App API boundary until the JSON response departs that boundary. |
| **Verification Method:** | This requirement can be verified by:<br>1. Deploying automated integration tests using a load simulation tool (e.g., Apache JMeter) to send 20 requests per minute to the Azure Web Apps staging environment.<br>2. Inspecting backend application access logs on Azure PostgreSQL and measuring the `response_time` metrics.<br>3. Running client-side profiling scripts in the Flutter simulator to verify local SQLite transaction latencies are under 100ms. |
| **Notes:** | Normal user operations expect a stable server environment where pre-trained RandomForest classification models (`crop_model.pkl` and `fertilizer_model_final.pkl`) are pre-loaded in memory at Django server startup to minimize computation lag. |

##### 4.1.1.2 End-of-Month Load (Peak Harvest/Sowing Load)
| ID# | NF-PU-02 | Peak Harvest/Sowing Season Load Responsiveness |
| :--- | :--- | :--- |
| **Scenario:** | • During peak agricultural harvest or sowing periods, farmers query crop predictions, fertilizer recommendations, and weather-based AI tips concurrently in remote areas.<br>• The system is stressed under peak demand, receiving up to 100 queries per minute.<br>• Network latency increases, or connectivity drops entirely on the client side, causing backend connection dropouts or timeouts exceeding 5.0 seconds. |
| **Requirement:** | • Under peak load, backend API inference response times shall not exceed 3.0 seconds.<br>• If a network timeout or connection dropout occurs, the client application's local fallback engine shall intercept the connection stream within 500 milliseconds and trigger `get_fallback_advice()` using local deterministic rule thresholds. |
| **Constraints:** | The 500ms offline intercept requirement is constrained by the device's native network state listener and local execution loop processing overhead. |
| **Verification Method:** | This requirement can be verified by:<br>1. Using LoadRunner to inject a simulated spike of 100 concurrent requests at the API boundary, measuring response times.<br>2. Artificially introducing packet dropouts on a test mobile client (using network throttling profiles in Xcode or Android Studio) during a weather tips query.<br>3. Verifying that the UI triggers the persistent offline warning banner and renders deterministic advice (based on temp, humidity, conditions) within 500ms. |
| **Notes:** | The offline fallback engine bypasses Gemini and OpenWeatherMap APIs during outages, ensuring that rural farmers retain continuous access to critical advice in regions with poor connectivity. |

#### 4.1.2. Batch Processing

##### 4.1.2.1 Background Ledger Auditing
| ID# | NF-PB-01 | Asynchronous Web3 Ledger Synchronization |
| :--- | :--- | :--- |
| **Scenario:** | • A prediction or weather tip transaction is successfully executed by a user.<br>• The Django REST API hands off the transaction hash logging task to the background Celery worker queue.<br>• The system is running in normal operation mode, processing incoming audit entries. |
| **Requirement:** | • Celery background workers shall sign and broadcast the recommendation receipt hash to the Sepolia Ethereum testnet within 30 seconds of queue receipt. |
| **Constraints:** | Synchronization latency is dependent on public Ethereum Sepolia network congestion, mining block confirmation times, and Infura node RPC provider response times. |
| **Verification Method:** | This requirement can be verified by:<br>1. Executing a batch of 50 diagnostic queries on the client.<br>2. Querying the Azure PostgreSQL audit database table (`recommendation_audit_log`) to calculate the difference between the timestamp of query completion and the timestamp when the `sync_status` transitions to `'Synchronized'`. |
| **Notes:** | By offloading the transaction signing to Celery background tasks, the REST API returns the recommendation immediately to the client, preventing blockchain mining delays from blocking the user interface. |

---

### 4.2. Security

#### 4.2.1. Auditing

##### 4.2.1.1 Recommendation Ledger Auditing
| ID# | NF-SA-01 | Audit Ledger Integrity and Accountability |
| :--- | :--- | :--- |
| **Scenario:** | • A user receives crop suggestions, fertilizer recommendations, or weather tips from the AgroSmart system.<br>• An auditor or administrative review inspector queries the transaction logs to audit advice safety or verify transaction history.<br>• The system is in normal operation or review auditing mode. |
| **Requirement:** | • The system shall automatically log every recommendation transaction, recording user ID, query type, input parameters, and output recommendation details to the database.<br>• The transaction receipt hash must be cryptographically written to the Sepolia testnet blockchain contract, and the database status updated to reflect sync state. |
| **Constraints:** | Recommendation receipt records on the blockchain ledger are immutable and cannot be deleted or modified. The database audit records in PostgreSQL shall not be editable or deletable by standard users. |
| **Verification Method:** | This requirement can be verified by:<br>1. Triggering crop queries and checking the database table to ensure the `user_id`, `input_payload`, and `output_result` JSON structures are successfully populated.<br>2. Verifying that a mined transaction hash is recorded for each audit entry, and clicking the generated Etherscan link redirects to the Sepolia blockchain explorer. |
| **Notes:** | Standard users do not have permissions to modify audit records. The blockchain logs serve as verifiable proof of advice, providing liability protection for advising agricultural agencies. |

#### 4.2.2. Session & Session Data Security
| ID# | NF-SS-01 | User Authentication and Session Data Encryption |
| :--- | :--- | :--- |
| **Scenario:** | • A user registers an account, logs in, or restarts the mobile application in the field.<br>• The system is running on local device hardware, checking or storing credential tokens. |
| **Requirement:** | • Registration inputs shall enforce strict client-side validation, blocking submissions that do not meet password complexity (min 8 characters, 1 uppercase, 1 digit, 1 special character).<br>• Authentication tokens and user credentials shall be encrypted locally on the device using Keychain (iOS) and Keystore (Android) secure storage. |
| **Constraints:** | Secure storage access is subject to native device operating system security permissions. In addition, the root Scaffold must enforce `resizeToAvoidBottomInset: false` to ensure forms do not collapse on login screens. |
| **Verification Method:** | This requirement can be verified by:<br>1. Attempting to register an account with weak passwords, verifying that submission is blocked.<br>2. Inspecting device storage logs in the debugger to ensure no plain-text JWT tokens or password parameters are written to standard cache files. |
| **Notes:** | Persistent session tokens allow farmers to access cached data and local history without requiring internet logins on application restart. |

---

### 4.3. Compatibility

#### 4.3.1. Cross-Platform Native Compatibility
| ID# | NF-CC-01 | Cross-Platform Client Execution |
| :--- | :--- | :--- |
| **Scenario:** | • Farmers download and launch the client application on low-specification personal mobile devices.<br>• The system runs under standard operating systems and hardware contexts. |
| **Requirement:** | • The mobile application shall execute natively and consistently across iOS (version 15.0 and later) and Android (API Level 28 and later) devices.<br>• UI forms, sliders, and buttons must render without visual breaks, supporting Urdu and English localizations. |
| **Constraints:** | Layout dimensions must adapt dynamically to prevent bottom-inset keyboard overlap, utilizing MediaQuery padding configurations. |
| **Verification Method:** | This requirement can be verified by:<br>1. Deploying the compiled Flutter client to virtual device suites on Firebase Test Lab, testing layout compatibility on 15+ different iOS and Android device screens.<br>2. Verifying that the language toggle instantly translates all views natively using the easy_localization dictionary bundles. |
| **Notes:** | Consistently rendered, large tap targets (minimum 48x48 pixels) and Urdu localization are critical to accommodate users with lower digital literacy. |

#### 4.3.2. Local Cache Compatibility
| ID# | NF-LC-01 | Offline SQLite Local Database Engine |
| :--- | :--- | :--- |
| **Scenario:** | • The mobile client writes diagnostic log histories or queries saved entries locally without cellular connection.<br>• The device runs on internal flash storage. |
| **Requirement:** | • The local caching engine shall be compatible with SQLite relational file structures natively supported by iOS and Android.<br>• The history screen shall support keyword filters, category chips (Crops, Fertilizers, Pesticides, Weather), and swipe-to-delete gestures in under 100ms. |
| **Constraints:** | The database file is subject to local device storage limits and must be sandboxed within the application directory. |
| **Verification Method:** | This requirement can be verified by:<br>1. Storing 100 mock diagnostic entries in the local database.<br>2. Triggering search query filters on the History screen and measuring the list redraw latency under the debugger.<br>3. Performing swipe-to-delete gestures and ensuring records are purged from the database file immediately. |
| **Notes:** | Relational SQLite indexes prevent log fetch latencies from degrading the user experience as the query history grows. |

---

### 4.4. Maintainability

#### 4.4.1. Error Reporting

##### 4.4.1.1 Application & Integration Errors
| ID# | NF-ER-01 | Multi-Tier Application Exception Reporting |
| :--- | :--- | :--- |
| **Scenario:** | • Third-party API failures, network timeouts, or schema errors occur during backend evaluations (e.g. OpenWeatherMap endpoint timeout or Google Gemini API quota limits).<br>• The server backend executes error interception routines. |
| **Requirement:** | • All third-party integration exceptions shall be logged to the Azure PostgreSQL audit database under distinct error identifiers (`ERR-INT-101` to `ERR-INT-104`).<br>• Any critical integration failure (e.g., node synchronization drops or gas limits exceeded on Sepolia after 3 Celery retries) shall trigger an automated Slack or email notification to DevOps (Fatima Al-Sayed). |
| **Constraints:** | Error payloads must not log decrypted API keys, database credentials, or user passwords to protect system security. |
| **Verification Method:** | This requirement can be verified by:<br>1. Simulating integration failures (e.g., withdrawing API keys or blocking connection to Sepolia RPC nodes).<br>2. Verifying that the backend intercepts the failure, logs the correct `ERR-INT` code to the PostgreSQL log, and dispatches a Slack alert to the DevOps channel. |
| **Notes:** | Automated alerting prevents silent failures in background blockchain syncing operations, allowing the operations team to adjust gas fees or node providers promptly. |

##### 4.4.1.2 Database Logging & Auditing Errors
| ID# | NF-ER-02 | Ingestion Schema Typo Realignment |
| :--- | :--- | :--- |
| **Scenario:** | • Shift in ML training models requires renaming schema validation properties.<br>• Solution architects or developers initiate schema modifications to the database or serializer. |
| **Requirement:** | • To prevent serializer execution crashes, any changes to database schemas or input validation rules must strictly follow the change path: Data Specialist (Jenkins) verification -> Backend Serializer Realignment (Rostova) -> Client Controller Update (Siddiqui) -> Project Sponsor sign-off.<br>• Form inputs and API serializers must preserve original typos: `'Temparature'` (misspelled), `'Humidity '` (trailing space), and `'Phosphorous'` (misspelled) unless this validation alignment path is completed. |
| **Constraints:** | Changing conventions requires synchronized deployments of both backend API and compiled client binaries. |
| **Verification Method:** | This requirement can be verified by:<br>1. Checking that the validation error logs capture any schema mismatch exceptions during prediction runs.<br>2. Verifying that the Technical Change Path signatures are updated in the project repository before staging changes. |
| **Notes:** | The strict change path guards against accidental mismatch overrides that would break pre-trained model scoring runs. |

---

## Appendix A. Considerations

| CONSIDERATIONS FOR COTS, MOTS, and CUSTOM IMPLEMENTATION |
| :--- |
| **COTS**<br>For COTS products, many of the non-functional requirements may not apply as they are already built into the COTS application and there is little that can be changed. However, external to the application, there are still a number of non-functional requirements that are applicable, which are those involving the environment where the COTS application is hosted. Therefore, non-functional requirements such as performance, availability, some security, and others are applicable and should be specified. |
| **MOTS**<br>For MOTS, all parts of the application that are not modified, the non-functional requirements are limited, as in COTS. Also, specifying non-functional requirements related to items such as maintainability of code, security of the application, etc., the effect of these non-functional requirements is limited as they would only apply to the modified parts of the application. Therefore, MOTS should follow the approach of COTS when specifying non-functional requirements unless the project determines that there is value in adding non-functional requirements that only apply to part of the software application. |
| **CUSTOM**<br>For custom developments, all non-functional requirements apply and should be specified consistent with the needs of the stakeholders and the project. The AgroSmart platform is a custom implementation, meaning all NFRs detailed in Section 4 are fully applicable and must be tested and verified accordingly. |
