# Stanford University — Administrative Systems
## Requirements Traceability Matrix (RTM)

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
| 06/22/2026 | 1.0 | Initial Requirements Traceability Matrix Baseline | Muhammad Omer Siddiqui |

### Approvals
| Approval Date | Approved Version | Approver Role | Approver |
| :--- | :--- | :--- | :--- |
| 06/22/2026 | 1.0 | Project Sponsor | Client Venture Team |
| 06/22/2026 | 1.0 | Lead Solution Architect | Muhammad Omer Siddiqui |

---

## 1. Introduction
This Requirements Traceability Matrix (RTM) traces the connections between high-level business justifications, functional requirements specified in the Functional Specification Document (FSD), non-functional requirements specified in the Non-Functional Requirements (NFR) document, and validation test cases. 

This matrix serves as the authoritative verification loop to ensure that all requirements are fully specified, designed, implemented, and tested under standard quality controls.

---

## 2. Requirements Traceability Matrix

| ID | Ass. ID | Requirements Description | Business Need, Justification | Project Objective | Requested By | Department | WBS Element | Specification | Design | Test Cases |
|---|---|---|---|---|---|---|---|---|---|---|
| **1** | **BRD-FR-003** | Dual-Model ML Ingestion | Scientific prediction replaces subjective visual crop/fertilizer checks, optimizing yield. | Deliver crop/fertilizer models predictions within budget boundaries. | Scientific Review Team | Data & ML | 1.1 (ML Integration) | Finished | Finished | TC-ML-01, TC-ML-02 |
| **1** | **BRD-FR-011** | Soil Guidance Overlay | Help farmers understand bounds, preventing out-of-range numeric input errors. | Maximize usability and reduce input error rates in field environments. | Rural Farmers | Frontend Mobile | 1.2 (Soil Guidance UI) | Finished | Finished | TC-UI-03 |
| **1** | **BRD-FR-019** | Global Endpoints Routing | Dynamic toggle mapping for local staging vs Azure production endpoints testing. | Enable rapid endpoint switching during staging, QA, and production. | Lead Architect | DevOps | 1.3 (Config Routing) | Finished | Finished | TC-DV-01 |
| **2** | **BRD-FR-004** | HA Offline Fallback Engine | Local threshold calculations run offline during network drops to ensure uptime. | Mitigate remote signals drops and prevent connection failures. | Rural Farmers | Frontend Mobile | 2.1 (Offline Fallback) | Finished | Finished | TC-OF-01 |
| **2** | **BRD-FR-018** | Network State Alerting | Persistent orange warning banner displays when device shifts offline. | Inform users clearly that calculations are using local fallback rules. | Rural Farmers | Frontend Mobile | 2.2 (Offline Banner UI) | Finished | Finished | TC-UI-04 |
| **3** | **BRD-FR-007** | Fuzzy-Text Pesticide Lookup | Fuzzy symptom keywords check and default organic Neem Oil treatment. | Provide symptom lookup without requiring strict string inputs. | Rural Farmers | Backend Engineering | 3.1 (Pesticide Database) | Finished | Finished | TC-PE-01, TC-PE-02 |
| **4** | **BRD-FR-008** | SQLite Database Cache Sync | Automatically save prediction history to client SQLite database file. | Enable offline record views and reduce recurring network bandwidth costs. | Rural Farmers | Frontend Mobile | 4.1 (SQLite Persistence) | Finished | Finished | TC-DB-01 |
| **4** | **BRD-FR-012** | Advisory Query Expansion | Tap historical log cards in history to inspect full query parameters. | Render clear details of past inputs and advice results. | Rural Farmers | Frontend Mobile | 4.2 (Logs Details Drawer) | Finished | Finished | TC-UI-05 |
| **4** | **BRD-FR-015** | Historical Logs Searching | Keyword search filters to look up history records by crop or location. | Provide fast logs search capabilities natively. | Rural Farmers | Frontend Mobile | 4.3 (History Search UI) | Finished | Finished | TC-DB-02 |
| **4** | **BRD-FR-016** | Logs Categorical Filtering | Filter chips separating records by Crop, Fertilizer, Pesticide, or Weather. | Simplify user log analysis. | Rural Farmers | Frontend Mobile | 4.4 (Filter Chip Widget) | Finished | Finished | TC-DB-03 |
| **5** | **BRD-FR-009** | User Account Registration | Password complexity checking (8+ chars, uppercase, digit, symbol) signups. | Restrict platform access and protect user profile logs records. | Project Sponsor | Frontend Mobile | 5.1 (Auth Form UI) | Finished | Finished | TC-AU-01 |
| **5** | **BRD-FR-010** | Persistent Session Auto-Login| Caches active Firebase session tokens locally to automate logins on restart. | Bypass recurrent logins, supporting active offline workflows. | Rural Farmers | Frontend Mobile | 5.2 (Token Cache Store) | Finished | Finished | TC-AU-02 |
| **5** | **BRD-FR-017** | Session Account Sign-out | Sign-out button closes session, flushes security tokens, and clears state. | Protect farmer data profiles on shared hardware devices. | Project Sponsor | Frontend Mobile | 5.3 (Settings Screen UI) | Finished | Finished | TC-AU-03 |
| **5** | **BRD-FR-001** | Multi-Language Toggle | Language switch capsule translates views between English and Urdu. | Remove literacy barriers and make application accessible. | Rural Farmers | Frontend Mobile | 5.4 (Locale Toggle) | Finished | Finished | TC-UI-01 |
| **5** | **BRD-FR-002** | Keyboard Safety Layout | Root Scaffold setting `resizeToAvoidBottomInset: false` to protect forms layout. | Prevent Android/iOS soft keyboards from breaking visual inputs. | Tariq Mahmood | Frontend Mobile | 5.5 (Padding ViewInsets) | Finished | Finished | TC-UI-02 |
| **6** | **BRD-FR-006** | Cognitive Advisory Formatting| Enforce structured Google Gemini 4-tier output advice block structure. | Render formatted advice blocks that map inputs to distinct widget cards. | Rural Farmers | Backend Engineering | 6.1 (LLM Parser SDK) | Finished | Finished | TC-AI-01 |
| **6** | **BRD-FR-013** | Coordinate Sourcing Fallback |GPS coords sourcing falling back manually to Islamabad coordinates. | Identify user location context to lookup local weather metrics. | Rural Farmers | Frontend Mobile | 6.2 (Geolocator GPS) | Finished | Finished | TC-WE-01 |
| **6** | **BRD-FR-014** | Unified Advisory Dashboard | Combined weather readings widget with structured advice cards panel. | Present agricultural data and advice in a single panel. | Rural Farmers | Frontend Mobile | 6.3 (Dashboard UI) | Finished | Finished | TC-UI-06 |
| **6** | **BRD-FR-005** | Non-Blocking Web3 Auditing | Sepolia transaction writing offloaded to background Celery workers. | Prevent Ethereum mining delays from blocking mobile UI threads. | Scientific Inspectors | Backend Engineering | 6.4 (Celery Web3 Queue) | Finished | Finished | TC-BC-01 |
| **6** | **BRD-FR-020** | Ledger Verification Link | Capture transaction hash and render Etherscan verification hyperlinks. | Secure verification paths for inspectors and auditors. | Scientific Inspectors | Frontend Mobile | 6.5 (Verification link) | Finished | Finished | TC-BC-02 |
| **7** | **NF-PU-01** | Response Times Normal Load | API model inference responds under 2s; SQLite writes under 100ms. | Ensure fast application usability, avoiding user wait times. | Rural Farmers | Core Engineering | 7.1 (System Performance) | Finished | Finished | TC-PF-01 |
| **7** | **NF-PU-02** | Response Times Peak Load | Switch client-side connections to local fallback rules in under 500ms. | Ensure continuous advisory availability during connection dropouts. | Rural Farmers | Frontend Mobile | 7.2 (Network Timer) | Finished | Finished | TC-PF-02 |
| **7** | **NF-PB-01** | Celery Sync Latency | Celery task signing completes within 30s of REST queue handoff. | Maintain immediate API responsiveness for client devices. | Scientific Inspectors | Backend Engineering | 7.3 (Celery Broker Setup)| Finished | Finished | TC-PF-03 |
| **7** | **NF-SA-01** | Sepolia Auditing Security | Log signed transaction proofs to Ethereum Sepolia ledger. | Guarantee immutable records and liability audit protection. | Scientific Inspectors | Core Engineering | 7.4 (Smart Contract ABI) | Finished | Finished | TC-SEC-01 |
| **7** | **NF-SS-01** | Keychain / Keystore Security | Encrypt cached authentication tokens locally using Keychain and Keystore. | Secure local authentication assets from unauthorized reading. | Project Sponsor | Frontend Mobile | 7.5 (Secure Storage API) | Finished | Finished | TC-SEC-02 |
| **7** | **NF-CC-01** | Flutter Native Compatibility | Native execution on Android (API 28+) and iOS (15.0+). | Guarantee compatibility across target user mobile devices. | Lead Architect | Frontend Mobile | 7.6 (Flutter Native SDK) | Finished | Finished | TC-COMP-01 |
| **7** | **NF-LC-01** | SQLite Database Caching | Maintain local relational caching tables sandbox offline. | Deliver history access and deletes when disconnected. | Rural Farmers | Frontend Mobile | 7.7 (SQLite Engine Setup)| Finished | Finished | TC-COMP-02 |
| **7** | **NF-ER-01** | Exception Logs Alerting | Log ERR-INT-101/104 exceptions to Postgres, alerting DevOps via Slack. | Capture integration failovers immediately to allow dev mitigation. | Lead Architect | DevOps | 7.8 (PostgreSQL Logger) | Finished | Finished | TC-MAINT-01 |
| **7** | **NF-ER-02** | Schema Typo Verification | Data Specialist checks serializer typos before backend modifications. | Prevent typographical column mismatches from crashes during scoring. | Sarah Jenkins | Data Engineering | 7.9 (Serializer Schemas) | Finished | Finished | TC-MAINT-02 |

---

## 3. Related Documents
*   **AgroSmart Business Requirements Document (BRD) Version 1.0:** [business_requirements_document.md](file:///c:/Users/Admin/.gemini/antigravity-ide/scratch/agrosmart/business_requirements_document.md)
*   **AgroSmart Functional Specification Document (FSD) Version 1.0:** [functional_specification_document.md](file:///c:/Users/Admin/.gemini/antigravity-ide/scratch/agrosmart/functional_specification_document.md)
*   **AgroSmart Non-Functional Requirements (NFR) Document Version 1.0:** [non_functional_requirements.md](file:///c:/Users/Admin/.gemini/antigravity-ide/scratch/agrosmart/non_functional_requirements.md)
