# System Integration Test Plan
## AgroSmart Enterprise Agricultural Intelligence Platform

**Document Identifier:** AS-SITP-V1.0  
**Version:** 1.0  
**Date of Issue:** June 23, 2026  
**Issuing Organization:** Quality Assurance Division  
**Metadata:** 06/23/2026 8:00:00 PM | Page 1 of 15  

---

## Table of Contents
- [1. Introduction](#1-introduction)
  - [1.1 Test Objectives](#11-test-objectives)
  - [1.2 Scope of Testing](#12-scope-of-testing)
  - [1.3 System Overview](#13-system-overview)
  - [1.4 Definitions/Acronyms](#14-definitionsacronyms)
    - [1.4.1 Definitions](#141-definitions)
    - [1.4.2 Acronyms](#142-acronyms)
  - [1.5 References](#15-references)
- [2. Approach](#2-approach)
  - [2.1 Assumptions/Constraints](#21-assumptionsconstraints)
    - [2.1.1 Assumptions](#211-assumptions)
    - [2.1.2 Constraints](#212-constraints)
  - [2.2 Coverage](#22-coverage)
    - [2.2.1 Software Components](#221-software-components)
    - [2.2.2 Requirements](#222-requirements)
    - [2.2.3 Business Processes](#223-business-processes)
  - [2.3 Test Tools](#23-test-tools)
  - [2.4 Test Type (Regression, Conversion, etc.)](#24-test-type-regression-conversion-etc.)
  - [2.5 Test Data](#25-test-data)
- [3. Plan](#3-plan)
  - [3.1 Test Team](#31-test-team)
  - [3.2 Team Reviews](#32-team-reviews)
  - [3.3 Major Tasks and Deliverables](#33-major-tasks-and-deliverables)
  - [3.4 Environmental Needs](#34-environmental-needs)
    - [3.4.1 Test Environment](#341-test-environment)
    - [3.4.2 Test Lab](#342-test-lab)
  - [3.5 Training](#35-training)
- [4. Features to be Tested](#4-features-to-be-tested)
  - [4.1 Build 1](#41-build-1)
    - [4.1.1 User Authentication](#411-user-authentication)
    - [4.1.2 SQLite Cache Initialization](#412-sqlite-cache-initialization)
    - [4.1.3 Soil Metric Forms](#413-soil-metric-forms)
    - [4.1.4 Interface Usability](#414-interface-usability)
    - [4.1.5 Local Cache Response Performance](#415-local-cache-response-performance)
  - [4.2 Build 2](#42-build-2)
    - [4.2.1 Random Forest Crop Recommendations](#421-random-forest-crop-recommendations)
    - [4.2.2 Google Gemini Advisory Tips](#422-google-gemini-advisory-tips)
    - [4.2.3 Django API General Ledger & Audit Interfaces](#423-django-api-general-ledger--audit-interfaces)
    - [4.2.4 Form Validation & Viewport Heuristics](#424-form-validation--viewport-heuristics)
    - [4.2.5 Classification Inference Performance](#425-classification-inference-performance)
  - [4.3 Build 3](#43-build-3)
    - [4.3.1 Asynchronous Blockchain Syncing](#431-asynchronous-blockchain-syncing)
    - [4.3.2 Slack Exception Alerts](#432-slack-exception-alerts)
    - [4.3.3 Mobile Audit History Logs](#433-mobile-audit-history-logs)
    - [4.3.4 Network Interception Performance](#434-network-interception-performance)
    - [4.3.5 Local Fallback Recovery](#435-local-fallback-recovery)
- [5. Features Not to be Tested](#5-features-not-to-be-tested)
  - [5.1 System Administration Functions](#51-system-administration-functions)
- [6. Testing Procedures](#6-testing-procedures)
  - [6.1 Test Execution](#61-test-execution)
    - [6.1.1 Test Cases](#611-test-cases)
    - [6.1.2 Order of Testing](#612-order-of-testing)
  - [6.2 Pass/Fail Criteria](#62-passfail-criteria)
  - [6.3 Suspension Criteria and Resumption Requirements](#63-suspension-criteria-and-resumption-requirements)
    - [6.3.1 Normal Criteria](#631-normal-criteria)
    - [6.3.2 Abnormal Criteria](#632-abnormal-criteria)
  - [6.4 Defect Management](#64-defect-management)
- [7. Risks and Contingencies](#7-risks-and-contingencies)
- [8. Appendix](#8-appendix)
  - [8.1 Appendix A: Work Breakdown Structure](#81-appendix-a-work-breakdown-structure)

---

## 1. Introduction

### 1.1 Test Objectives
The system integration test of the AgroSmart platform shall validate from both the requirements perspective and business perspective that:
*   All localized farming operation business processes are fully supported under variable connectivity.
*   All soil chemical data ingestion and input validation flows operate correctly.
*   The pre-trained Random Forest prediction engines output precise crop and fertilizer recommendations.
*   The asynchronous blockchain logging sync pipeline offloads transaction signing to background queues.
*   The SQLite client-side caching engine updates diagnostics history in under one hundred milliseconds.
*   The system is easy to use for rural farmers, supporting Urdu/English localization.
*   All data schemas handle the required typographical constraints (`Temparature`, `Humidity `, and `Phosphorous`) without throwing execution anomalies.
*   Security controls are in place, caching user session keys securely via mobile Keychain/Keystore environments.
*   The system fallback mechanisms activate within five hundred milliseconds of network timeout to execute local heuristics.
*   All integration interfaces with external APIs (OpenWeatherMap, Google Gemini, and Sepolia RPC) function according to the design criteria.
*   Slack alerting integrations dispatch crash notices to the DevOps channel upon third-party gateway failures.

The objective of system integration testing is to validate the system operation as a cohesive whole. At the conclusion of testing, the project architect and test team will have a high level of confidence that the platform will work according to user requirements and will meet core agricultural business needs.

### 1.2 Scope of Testing
*   **Inclusions:** The system integration test will cover the Flutter Mobile Client, the Django REST API Backend, the Celery worker task runner, the Redis message queue, the sandboxed SQLite cache database, and the Azure PostgreSQL audit database. Testing will validate the interfaces between these systems and external gateways, including Google Gemini, OpenWeatherMap, and Sepolia Ethereum RPC nodes.
*   **Exclusions:** Testing will not include platform-level cloud resource provisioning (Azure App Service scale-out controls), physical network router hardware validation, or public Sepolia testnet validator node consensus logic.

### 1.3 System Overview
The AgroSmart platform is an enterprise agricultural intelligence system that accepts personnel credentials and soil metrics from regional farming inputs, processes crop and fertilizer predictions, and generates secure audit trails. The mobile application links to local database systems for offline caching and connects to Django REST API endpoints when online. The backend schedules transaction logs to Celery queues to commit event hashes to the Sepolia Ethereum test network, and requests diagnostic advice from Google Gemini cognitive engines.

#### System Interface Flow Diagram

```
         ┌─────────────────────────┐
         │  Flutter Mobile Client  │◄────────┐
         └───────┬─────────▲───────┘         │
                 │         │                 │
                 ▼         │                 │
         ┌─────────────────────────┐         │
         │ SQLite Local Cache DB   │         │
         └───────┬─────────────────┘         │
                 │                           │
                 ▼                           ▼
 ┌─────────────────────────┐       ┌─────────────────────────┐
 │ Django REST API Backend │◄─────►│ Azure PostgreSQL Audit  │
 └───────────┬─────────┬───┘       └─────────────┬───────────┘
             │         │                         │
             ▼         ▼                         ▼
 ┌───────────┐ ┌───────────┐             ┌───────────┐
 │ OpenWeather│ │ Celery/   │             │ Google    │
 │ & Sepolia  │ │ Redis     │             │ Gemini AI │
 └───────────┘ └───────────┘             └───────────┘
```

### 1.4 Definitions/Acronyms

#### 1.4.1 Definitions
*   **Build:** A functionally independent piece of software that supports a well-defined logical subset of a system. A build can be tested independently and then integrated with other builds.
*   **Critical Processing Unit:** A program, module, or class that is critical to the correct functioning of the system. A critical processing unit carries with it a high impact of failure.
*   **Model Office:** A validation of the implementation, operation, and training of the system in a simulated environment using real-world scenarios.
*   **Prototype:** A working model of the software demonstrating look and feel, but not supporting all processing features and database integrations.
*   **Regression Testing:** Testing to ensure that unchanged parts of the software function correctly after a code change or bug fix.
*   **Requirement:** A feature or behavior the system must display, based on user, business, or technical needs.
*   **Static Test:** A verification performed without executing code on a computer (e.g., inspecting design diagrams).
*   **System Integration Testing:** A testing level validating both internal and external interfaces, ensuring the system works as a cohesive whole according to requirements.
*   **Test Tool:** Any software framework or utility that assists in test execution.
*   **Unit Testing:** A testing level where the smallest modules or classes of a system are separately verified.
*   **Unit-to-Unit Testing:** A testing level that validates interface compatibility between groups of related units.

#### 1.4.2 Acronyms
*   **NPK:** Nitrogen, Phosphorus, Potassium soil nutrients.
*   **RPC:** Remote Procedure Call.
*   **JWT:** JSON Web Token.
*   **ML:** Machine Learning.
*   **ADR:** Architecture Decision Record.
*   **BRD:** Business Requirements Document.
*   **FSD:** Functional Specification Document.
*   **NFR:** Non-Functional Requirements.

### 1.5 References
*   *Requirements Specification Document for the AgroSmart System*
*   *Functional Specification Document for the AgroSmart System*
*   *Non-Functional Requirements Document for the AgroSmart System*
*   *High-Level Design Document for the AgroSmart System*
*   *Low-Level Design Document for the AgroSmart System*
*   *Architecture Decision Record 001 for the AgroSmart System*

---

## 2. Approach

### 2.1 Assumptions/Constraints

#### 2.1.1 Assumptions
*   The first build of the AgroSmart system will be ready for system integration testing on July 1, 2026.
*   Each build will pass unit and unit-to-unit verification suites before transfer to the integration test environment.

#### 2.1.2 Constraints
*   The six-week testing window limits the depth of long-duration transaction testing on the Sepolia network, which may experience testnet network latency.

### 2.2 Coverage
Test coverage will be tracked using:
*   A completed matrix mapping testable requirements to test cases.
*   A completed matrix mapping agricultural business processes to integration test cases.

#### 2.2.1 Software Components
All software classes and modules within the mobile client, the API serializer models, the prediction engines, the queue handlers, and the database connectors will be tested.

#### 2.2.2 Requirements
All requirements detailed in the Requirements Specification Document and Functional Specification Document will be tested.

#### 2.2.3 Business Processes
The system integration testing will validate five critical business processes:
*   **Soil Metric Data Ingestion**: Capturing geographical coordinates and importing soil NPK inputs from the UI.
*   **Random Forest Crop & Fertilizer Inferences**: Processing inputs through pre-trained classification models to return recommendations.
*   **Weather AI Advisory Content Generation**: Retrieving location data, calling weather endpoints, and generating guidelines via large language models.
*   **Asynchronous Blockchain Auditing**: Dispatching transaction payloads to background Celery tasks, signing with server keys, and posting audit records to Sepolia.
*   **Automated Slack Exception Alerting**: Monitoring connection drops and broadcasting logs to the DevOps communication channel.

### 2.3 Test Tools
*   *Automated UI Execution Tool*: Used to simulate user interactions on mobile simulator screens.
*   *Backend Test Framework*: Used to execute Django component and API integration scripts.
*   *Queue Task Simulator*: Used to monitor Celery job states and Redis message routing.
*   *Defect Tracker Portal*: Used to log and assign software anomalies.

### 2.4 Test Type (Regression, Conversion, etc.)
*   **Functional testing**, by executing test cases against soil forms and classification pipelines.
*   **Compliance testing**, by verifying that forms and databases process misspelled schema columns (`Temparature`, `Humidity `, `Phosphorous`).
*   **Security testing**, by checking Keychain/Keystore token encryption.
*   **Controls testing**, by auditing PostgreSQL audit database sync states and block transaction receipt hashes.
*   **Regression testing**, to confirm that bug resolutions do not impact machine learning performance.
*   **Recovery testing**, to ensure the offline rules engine triggers within five hundred milliseconds of network timeout.

### 2.5 Test Data
Test data will be stored on the staging server and local client sandbox caches:
*   **UserProfile Table**: Configured credentials representing standard farmers and review inspectors.
*   **SoilMetricPayload File**: Test matrices mapping varied chemical profiles to expected crop and fertilizer outcomes.
*   **CropModelWeights Binary**: Serialized classifier weights and categorical labels loaded at server startup.
*   **WeatherRules Data**: Configured local threshold rules (temperature and humidity bounds) to test fallback advisory generation.

---

## 3. Plan

### 3.1 Test Team

| Name | Title | Level of Involvement | Responsibilities |
| :--- | :--- | :--- | :--- |
| **Joe Johnson** | Team Leader - Independent Test Team | $40 \text{ hrs/wk}$ | Lead testing activities, plan schedules, and generate status reports. |
| **Mary Anderson** | Assistant Team Leader - Independent Test Team | $40 \text{ hrs/wk}$ | Design and execute test cases, create test data datasets, and write summary reports. |
| **Pete Wilson** | End user - Agricultural Specialist | $25 \text{ hrs/wk}$ | Design and execute validation tests for model predictions and advising content. |
| **Tom Jones** | End user - Quality Auditor | $40 \text{ hrs/wk}$ | Design and execute tests to check database audit logs and blockchain receipts. |
| **Jane Peterson** | End user - UI Tester | $30 \text{ hrs/wk}$ | Design and execute tests for screen layouts, forms, and localization switches. |
| **Doug Thompson** | Independent Tester | $40 \text{ hrs/wk}$ | Design and execute tests verifying client-side caching and SQLite database operations. |
| **Dot Wong** | Independent Tester | $40 \text{ hrs/wk}$ | Design and execute tests for background queue workers and API serializers. |
| **Renee Roberts** | Independent Tester | $40 \text{ hrs/wk}$ | Design tests for external interfaces, weather integrations, and error alerts. |
| **Gary Moore** | Core Developer | $40 \text{ hrs/wk}$ | Provide technical assistance and resolve anomalies. |

### 3.2 Team Reviews
The test team and quality representatives will conduct four reviews:
*   **Test Plan Review**: Verifying scope and test tools.
*   **Test Case Review**: Checking coverage of the five critical business processes.
*   **Test Progress Review**: Tracking defect density and schedule health.
*   **Post-Test Review**: Assessing release readiness and documenting lessons learned.

### 3.3 Major Tasks and Deliverables

| Task | Start | Stop | Deliverable(s) |
| :--- | :--- | :--- | :--- |
| System integration test case design | 5/1/2026 | 6/1/2026 | System integration test cases |
| Build system integration test environment | 5/15/2026 | 6/15/2026 | Test environment and mock API gateways |
| Build system integration test data | 6/2/2026 | 6/15/2026 | Soil input matrices and user credentials |
| Train test team | 6/15/2026 | 6/17/2026 | Trained validation engineers |
| Build 1 delivered for integration testing | — | 6/29/2026 | Build 1 package (Core Client and Storage) |
| Build 1 test execution | 7/1/2026 | 7/15/2026 | Build 1 integration test log |
| Build 1 test summary report due | — | 7/17/2026 | Build 1 test summary report |
| Build 2 test execution | 7/18/2026 | 7/26/2026 | Build 2 integration test log |
| Build 2 test summary report due | — | 7/28/2026 | Build 2 test summary report |
| Build 3 test execution | 8/1/2026 | 8/15/2026 | Build 3 integration test log |
| Build 3 test summary report due | — | 8/17/2026 | Build 3 test summary report |
| System migration to model office environment | 8/20/2026 | 8/22/2026 | Deployed staging candidate |

### 3.4 Environmental Needs

#### 3.4.1 Test Environment
*   **Hardware**:
    *   Staging Server in the QA cloud network environment.
    *   One networked document printer.
    *   Two Asus workstations: Intel Core i5-4460S, 8GB DDR3 RAM, 24X Super-Multi DVD/RW drive.
    *   Two Dell Inspiron 3000 workstations: Intel Pentium G3240 dual-core 3.1 GHz 3MB cache, 4GB RAM, 1TB hard drive.
    *   Two iMac workstations: 1.4GHz dual-core Intel Core i5, 8GB onboard memory, 500GB hard drive.
*   **Network**:
    *   LAN - Synoptic 810 10Base-T Ethernet Concentrator.
    *   Category 5 cables to meet 10Base-T specifications.
*   **Software**:
    *   AgroSmart application builds.
    *   Python runtime environments and Django components.
    *   Flutter client execution environments.
    *   PostgreSQL relational databases and SQLite engines.

#### 3.4.2 Test Lab
The test team requires full-time access to:
*   One large whiteboard with markers and erasers.
*   Organizational folders, notebooks, and storage containers.

> **NOTE:** These items are in addition to the hardware and software detailed in Section 3.4.1.

### 3.5 Training
Test team members will undergo testing technique training. The training will span three days at the corporate training facility from June 15 to June 17, 2026.

---

## 4. Features to be Tested

### 4.1 Build 1

#### 4.1.1 User Authentication
*   Verify user registration constraints and database writes.
*   Validate JWT secure login token storage.
*   Test Keychain/Keystore access control.
*   Verify session timeouts and logout routines.

#### 4.1.2 SQLite Cache Initialization
*   Verify local database creation in target directories.
*   Test diagnostics history table initialization.
*   Validate SQLite query responses.
*   Check database locks during concurrent reads.

#### 4.1.3 Soil Metric Forms
*   Verify coordinate input captures from hardware mock files.
*   Test integer range validation on input sliders.
*   Validate misspelled fields (`Temparature`, `Humidity `, `Phosphorous`) mapping.
*   Test form submit event intercepts.

#### 4.1.4 Interface Usability
*   Verify Urdu and English localization switches.
*   Validate viewport constraints and card scaling.
*   Test keyboard view-insets manual calculations.

#### 4.1.5 Local Cache Response Performance
*   Verify SQLite write speeds execute in under one hundred milliseconds.
*   Validate memory load during history listing sweeps.

### 4.2 Build 2

#### 4.2.1 Random Forest Crop Recommendations
*   Verify loading of pre-trained crop binary classifiers.
*   Test prediction output ranges against mock soil data.
*   Validate label encoder conversions.
*   Test inference exception recovery.

#### 4.2.2 Google Gemini Advisory Tips
*   Verify prompt construction structures.
*   Validate generated advice parsing algorithms.
*   Test output localization translation formatting.
*   Test token consumption quota checks.

#### 4.2.3 Django API General Ledger & Audit Interfaces
*   Verify PostgreSQL table inserts.
*   Validate serialization schemas.
*   Test REST API endpoints response structures.
*   Verify audit search filtering parameters.

#### 4.2.4 Form Validation & Viewport Heuristics
*   Test dynamic range checks on model inputs.
*   Validate decimal parsing routines.
*   Verify error message text formats.

#### 4.2.5 Classification Inference Performance
*   Verify crop recommendation executions return JSON payloads in under two seconds.
*   Test CPU usage spikes during inference batches.

### 4.3 Build 3

#### 4.3.1 Asynchronous Blockchain Syncing
*   Verify dispatching of tasks to Celery queues.
*   Test transaction signing via server wallet keys.
*   Validate transaction broadcast protocols to Sepolia RPC nodes.
*   Verify PostgreSQL update updates with receipt hashes.

#### 4.3.2 Slack Exception Alerts
*   Verify monitoring of Sepolia RPC connection failures.
*   Validate retry loop threshold limits.
*   Test webhook execution logic.
*   Verify Slack alert formats.

#### 4.3.3 Mobile Audit History Logs
*   Verify data synchronization between SQLite and PostgreSQL.
*   Validate swipe-to-delete history events.
*   Test historical filter sorting.
*   Verify blockchain explorer hyperlink generation.

#### 4.3.4 Network Interception Performance
*   Verify that offline checks intercept network calls in under five hundred milliseconds.
*   Validate memory stability during continuous offline transitions.

#### 4.3.5 Local Fallback Recovery
*   Test offline heuristics decision paths.
*   Verify orange warning banner rendering.
*   Validate mock weather parameters fallback data.
*   Test database recovery after browser or app crashes.

---

## 5. Features Not to be Tested

### 5.1 System Administration Functions
*   Management of Azure database connection string storage.
*   Deployment updates on production servers.
*   Wallet key rotation operations on server hosts.

---

## 6. Testing Procedures

### 6.1 Test Execution

#### 6.1.1 Test Cases
Testers will execute pre-defined integration test cases. If observed results equal expected results, the case passes. If observed results differ, the case fails, and the engineer logs an anomaly.

#### 6.1.2 Order of Testing
Testing will follow the build delivery sequence:

##### Build 1
1.  User Authentication
2.  SQLite Cache Initialization
3.  Soil Metric Forms
4.  Interface Usability
5.  Local Cache Response Performance

##### Build 2
1.  Random Forest Crop Recommendations
2.  Google Gemini Advisory Tips
3.  Django API General Ledger & Audit Interfaces
4.  Form Validation & Viewport Heuristics
5.  Classification Inference Performance

##### Build 3
1.  Asynchronous Blockchain Syncing
2.  Slack Exception Alerts
3.  Mobile Audit History Logs
4.  Network Interception Performance
5.  Local Fallback Recovery

### 6.2 Pass/Fail Criteria
To pass the system integration test, the following criteria must be met:
*   Soil metric forms and API gateways parse inputs correctly.
*   Pre-trained crop/fertilizer predictions match validation thresholds.
*   Weather advisory calls return structured cognitive summaries.
*   Celery workers sign and commit logs to Sepolia testnet.
*   The interface translates Urdu/English assets dynamically.
*   Offline fallback triggers within five hundred milliseconds of network timeouts.
*   Local diagnostic history caches and searches run in under one hundred milliseconds.
*   Audit history logs provide valid blockchain transaction verification links.

### 6.3 Suspension Criteria and Resumption Requirements

#### 6.3.1 Normal Criteria
*   Daily testing will suspend at 5:00 p.m. Testers will mark executed cases and run backups of SQLite cache tables.
*   Upon executing all integration cases, testing suspends, and the QA lead compiles the System Integration Test Summary Report.

#### 6.3.2 Abnormal Criteria
*   If the defect backlog increases continuously over a two-week period, testing will suspend. Developers will resolve open anomalies before testing resumes.
*   If a critical processing unit (e.g., Random Forest prediction class) fails validation, testing suspends. Once fixed, all dependent integrations will run again to verify stability.

### 6.4 Defect Management
The test team will track defects in the QA portal. Anomalies will follow the severity classifications defined below:
*   **1 - Critical (Blocker)**: Severe crashes, database corruption, or Celery queue failures preventing testing progress. Testing will not advance to the next build.
*   **2 - High**: Features return invalid data (e.g., wrong crop recommendations or incorrect NPK range evaluations).
*   **3 - Medium**: Validation check failures, such as UI forms rejecting misspelled database column names (`Temparature`, `Humidity `, `Phosphorous`).
*   **4 - Low**: Aesthetic discrepancies (e.g., card alignments or localization typos).
*   **5 - Info**: Ambiguity in requirements requiring structural review.

---

## 7. Risks and Contingencies
*   **Random Forest Classifier Accuracy**: *Risk level moderate.* Inaccurate prediction classifications can affect user recommendations. Staging models will be benchmarked against datasets before integration.
*   **API Network Latency**: *Risk level high.* Timeouts on OpenWeatherMap or Google Gemini could freeze threads. Integration tests will verify that response interceptors trigger the offline heuristics rules engine in under five hundred milliseconds.
*   **Sepolia Gas Validation**: *Risk level moderate.* Volatile Sepolia testnet transaction processing speeds could stall Celery queues. Workers will be tested to verify retry logic and Slack alert triggers.

---

## 8. Appendix

### 8.1 Appendix A: Work Breakdown Structure
*   **SIT-Task-01**: Design integration test cases (QA Team).
*   **SIT-Task-02**: Provision staging databases and mock external APIs (DevOps).
*   **SIT-Task-03**: Compile and import soil input datasets (Data Specialist).
*   **SIT-Task-04**: Execute Build 1, 2, and 3 validation sweeps (Test Team).
*   **SIT-Task-05**: Review anomalies and compile final summary reports (QA Lead).
