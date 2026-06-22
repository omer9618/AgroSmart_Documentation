# Stanford University — Administrative Systems
## Functional Specification Document

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
| 06/22/2026 | 1.0 | Initial Functional Specification Baseline | Muhammad Omer Siddiqui |

### Approvals
| Approval Date | Approved Version | Approver Role | Approver |
| :--- | :--- | :--- | :--- |
| 06/22/2026 | 1.0 | Project Sponsor | Client Venture Team |
| 06/22/2026 | 1.0 | Lead Solution Architect | Muhammad Omer Siddiqui |

---

## Table of Contents
1. [Introduction](#1-introduction)
   - 1.1 [Purpose of the document](#11-purpose-of-the-document)
   - 1.2 [Project Scope](#12-project-scope)
   - 1.3 [Scope of the document](#13-scope-of-the-document)
   - 1.4 [Related documents](#14-related-documents)
   - 1.5 [Terms/Acronyms and Definitions](#15-termsacronyms-and-definitions)
   - 1.6 [Risks and Assumptions](#16-risks-and-assumptions)
2. [System/ Solution Overview](#2-system-solution-overview)
   - 2.1 [Context Diagram/ Interface Diagram/ Data Flow Diagram, Application Screen Flow, Sitemap, Process Flow](#21-context-diagram-interface-diagram-data-flow-diagram-application-screen-flow-sitemap-process-flow)
   - 2.2 [System Actors](#22-system-actors)
   - 2.3 [Dependencies and Change Impacts](#23-dependencies-and-change-impacts)
3. [Functional Specifications](#3-functional-specifications)
   - 3.1 [Splash Screen](#31-splash-screen)
   - 3.2 [Login & Registration Screen](#32-login--registration-screen)
   - 3.3 [Home Dashboard Screen](#33-home-dashboard-screen)
   - 3.4 [Crop Recommendation Form Screen](#34-crop-recommendation-form-screen)
   - 3.5 [Fertilizer Recommendation Form Screen](#35-fertilizer-recommendation-form-screen)
   - 3.6 [Pesticide Lookup Form Screen](#36-pesticide-lookup-form-screen)
   - 3.7 [Weather & AI Advisory Screen](#37-weather--ai-advisory-screen)
   - 3.8 [Result & Diagnostic Report Screen](#38-result--diagnostic-report-screen)
   - 3.9 [Historical Logs & Audit Registry Screen](#39-historical-logs--audit-registry-screen)
4. [System Configurations](#4-system-configurations)
5. [Other System Requirements/ Non-Functional Requirements](#5-other-system-requirements-non-functional-requirements)
6. [Reporting Requirements](#6-reporting-requirements)
7. [Integration Requirements](#7-integration-requirements)
   - 7.1 [Exception Handling/ Error Reporting](#71-exception-handling-error-reporting)
8. [Data Migration/ Conversion Requirements](#8-data-migration-conversion-requirements)
9. [References](#9-references)
10. [Open Issues](#10-open-issues)
11. [Appendix](#appendix)

---

## 1. Introduction

This Functional Specification Document (FSD) translates the high-level business goals and constraints defined in the AgroSmart Business Requirements Document (BRD) into technical specifications. It defines the screen-level structures, data elements, operational parameters, and exception handling paths for the frontend mobile client and Django backend.

### 1.1 Purpose of the document
The Functional Specification Document is a document that provides detailed information on how the system solution will function and the requested behavior. This document is created based on the high-level requirements identified in the Business Requirements Document and provides traceability on the functional specifications back to the business requirements. 

This document defines the functional behavior of the cross-platform Flutter application and the Django REST API. It serves as the primary reference contract for frontend development, backend database schemas, and quality assurance testing.

### 1.2 Project Scope
The project scope is constrained by a fixed Capital Expenditure (CapEx) threshold of **$35,000**. The AgroSmart system delivers:
*   A cross-platform Flutter mobile client running natively on iOS and Android.
*   A Python Django REST API backend hosted on Microsoft Azure Web Apps and connected to an Azure PostgreSQL instance.
*   Random Forest machine learning prediction models for crops and fertilizer mix advice.
*   A cognitive weather advisory layer using Google Gemini 2.0 Flash and OpenWeatherMap APIs.
*   A Web3 auditing ledger that records diagnostic advice hashes asynchronously to the Sepolia Ethereum testnet.

### 1.3 Scope of the document
This document specifies the functional details for the Minimum Viable Product (MVP) release of the AgroSmart system, detailing all 9 screen interfaces, their validation parameters, use cases, configurations, and exception strategies.

### 1.4 Related documents
| Component | Name (with link to the document) | Description |
| :--- | :--- | :--- |
| Project Charter | [project_charter.md](file:///c:/Users/Admin/.gemini/antigravity-ide/scratch/agrosmart/project_charter.md) | Standardized project management baseline and constraints under ISO 21502:2020. |
| Business Requirements | [business_requirements_document.md](file:///c:/Users/Admin/.gemini/antigravity-ide/scratch/agrosmart/business_requirements_document.md) | Business requirements, user groups, and the 20 core functional requirements. |
| Technical Context | [project_context.md](file:///c:/Users/Admin/.gemini/antigravity-ide/scratch/agrosmart/project_context.md) | Technical constraints, dataset spelling conventions, and API structures. |

### 1.5 Terms/Acronyms and Definitions
*   **easy_localization:** Flutter library used to manage English ('en') and Urdu ('ur') locale bundles natively on the mobile client.
*   **Provider:** Flutter state management architecture that handles data flows and loader signals.
*   **resizeToAvoidBottomInset:** Flutter Scaffold property configured to `false` on forms to prevent viewport collapses when virtual keyboards pop up.
*   **Temparature:** Typographical parameter typo (with 'a' in the second syllable) used in the fertilizer machine learning model training dataset.
*   **Humidity :** Typographical parameter typo (with a trailing space) used in the fertilizer API validation serializers.
*   **Phosphorous:** Typographical parameter typo (with 'o' before 'u') used in soil phosphorus fertilizer recommendation queries.

### 1.6 Risks and Assumptions
*   **Assumption:** The target hardware devices run native iOS (15.0+) or Android (API 28+) operating systems and contain functioning GPS location modules.
*   **Risk:** Volatile network signals in remote agricultural fields can prevent real-time server evaluations. This is mitigated by the client-side deterministic fallback engine.

---

## 2. System/ Solution Overview
The AgroSmart platform implements a client-server structure designed to process agricultural inputs and output scientific suggestions. It utilizes localized SQLite databases for offline logging and Celery background workers for non-blocking Ethereum audits.

### 2.1 Context Diagram/ Interface Diagram/ Data Flow Diagram, Application Screen Flow, Sitemap, Process Flow
```text
 +------------------------------------------------------------------------------------------+
 |                                  FLUTTER MOBILE CLIENT                                   |
 |                                                                                          |
 |  [Splash Screen] -> [Login / SignUp] -> [Dashboard]                                      |
 |                                            |                                             |
 |       +------------------------------------+-----------------------------------+          |
 |       |                    |                    |                             |          |
 |  [Crop Form]       [Fertilizer Form]    [Pesticide Form]             [Weather Screen]    |
 |       |                    |                    |                             |          |
 |       +------------------------------------+-----------------------------------+          |
 |                                            |                                             |
 |                                     [Results Card]                                       |
 |                                            |                                             |
 |                                     [History List]                                       |
 +--------------------------------------------|---------------------------------------------+
                                              | HTTPS (JSON API)
                                              v
 +------------------------------------------------------------------------------------------+
 |                                  DJANGO REST API BACKEND                                 |
 |                                                                                          |
 |  Azure Web App Backend <---> joblib RandomForest (Crop & Fertilizer Inference)           |
 |         ^                  |                                                             |
 |         |                  |---> JSON Fuzzy Match (Pesticide Database)                   |
 |         v                  |                                                             |
 |   Azure PostgreSQL         |---> API Proxy (OpenWeatherMap + Gemini 2.0 Flash)           |
 |                            |                                                             |
 |                            |---> Background Tasks (Celery Queue)                         |
 |                                            |                                             |
 |                                            v (Web3 Infura)                               |
 |                                    [Sepolia Testnet]                                     |
 +------------------------------------------------------------------------------------------+
```

### 2.2 System Actors
#### 2.2.1 User Roles and Responsibilities / Authority Requirements
| User/Role | Example | Frequency of Use | Security/Access, Features Used | Additional Notes |
| :--- | :--- | :--- | :--- | :--- |
| Rural Farmer | Local Grower | Frequent (Daily/Weekly) | Standard app authentication. Accesses all prediction, weather, pesticide lookup, and local history screens. | Requires English/Urdu toggles. |
| Scientific Inspector | Government Auditor | Occasional (Monthly) | Read-only access to transaction history, search parameters, and Etherscan transaction validation hyperlinks. | High technical literacy. |

### 2.3 Dependencies and Change Impacts
#### 2.3.1 System Dependencies
*   **Firebase Authentication Service:** Validates user identity and maintains tokenized session persistence.
*   **OpenWeatherMap API:** Supplies coordinate-based meteorological parameters.
*   **Google Gemini 2.0 Flash:** Processes weather metrics and returns structured advice blocks.
*   **Ethereum Sepolia RPC Nodes:** Confirms audited recommendation receipts.

#### 2.3.2 Change Impacts
*   **Model Upgrades:** Modifying Random Forest models requires validating and aligning front-end input fields and backend serializers to preserve original spelling configurations.

---

## 3. Functional Specifications

The following table summarizes the mapping of the 20 functional requirements (`BRD-FR-001` to `BRD-FR-020`) to the specific FSD screen subsections:

| FSD Section | Screen Name | Mapped Functional Requirements | Priority |
| :--- | :--- | :--- | :--- |
| Section 3.1 | Splash Screen | BRD-FR-010 (Persistent Login) | Critical |
| Section 3.2 | Login & Registration | BRD-FR-001 (Localization), BRD-FR-002 (UI Safety), BRD-FR-009 (Registration) | Critical |
| Section 3.3 | Home Dashboard | BRD-FR-008 (Cache Synchronization), BRD-FR-018 (Offline Alerting), BRD-FR-019 (Endpoint Routing) | High |
| Section 3.4 | Crop Form | BRD-FR-003 (ML Ingestion), BRD-FR-011 (Diagnostic Overlay) | High |
| Section 3.5 | Fertilizer Form | BRD-FR-003 (ML Typo Ingestion) | Critical |
| Section 3.6 | Pesticide Search | BRD-FR-007 (Fuzzy Lookup) | High |
| Section 3.7 | Weather Advisory | BRD-FR-006 (AI Formatting), BRD-FR-013 (GPS Coordinates), BRD-FR-004 (Offline Fallback) | High |
| Section 3.8 | Results Card | BRD-FR-014 (Weather Dashboard), BRD-FR-020 (Verification Link) | High |
| Section 3.9 | History Logs | BRD-FR-012 (Advisory Expansion), BRD-FR-015 (Log Search), BRD-FR-016 (Log Filtering), BRD-FR-017 (Sign-out), BRD-FR-005 (Web3 Auditing) | High |

---

### 3.1 Splash Screen
#### 3.1.1 Purpose/ Description
Displays the brand identity on launch, triggers background state initializations, and checks local authentication tokens.

#### 3.1.2 Use case
| UC-1 | Splash Initial Check |
| :--- | :--- |
| **Primary Actor(s)** | Rural Farmer, Scientific Inspector |
| **Stakeholders and Interest** | Core developers (speed of launch verification) |
| **Trigger** | User opens the mobile application. |
| **Pre-conditions** | App assets are initialized on-device. |
| **Post-conditions** | Navigates the user to the Dashboard (if session token is cached) or the Login Screen. |
| **Main Success Scenario** | 1. User launches the application.<br>2. App displays background gradient and circular emblem logo.<br>3. System reads local token from secure storage.<br>4. Token is valid; system routes user directly to Home Dashboard within 2 seconds. |
| **Extensions** | *Session Token Missing or Expired*:<br>1. Secure storage query returns null.<br>2. System navigates to Login Screen. |
| **Priority** | Critical |
| **Special Requirements** | Must load easy_localization language dictionaries into memory before navigation. |
| **Open Questions** | None |

#### 3.1.3 Mock-up
A full-screen linear gradient running from deep forest green (`#1B5E20`) at the top-left to mint green (`#A5D6A7`) at the bottom-right. The circular white outline logo of a leaf-circuit hybrid floats in the center. An animated linear loading bar pulses at the bottom with text "Checking authentication...".

#### 3.1.4 Functional Requirements
*   **BRD-FR-010: Session Authentication & Persistent Login**  
    The system shall query secure client storage (Keychain/Keystore) on splash launch to check if a valid Firebase session token exists. If valid, the system shall bypass the login screen and load the user dashboard immediately.

#### 3.1.5 Field level specifications
*This screen contains no user input form fields.*

##### Buttons, Links and Icons:
*This screen contains no interactive buttons or links. Loading flows transition automatically.*

---

### 3.2 Login & Registration Screen
#### 3.2.1 Purpose/ Description
Provides a secure login and registration form, supported by client-side format checks and a floating multi-language locale switch toggle.

#### 3.2.2 Use case
| UC-2 | Farmer Account Registration & Access |
| :--- | :--- |
| **Primary Actor(s)** | Rural Farmer, Scientific Inspector |
| **Stakeholders and Interest** | Project Sponsor (data tracking and security) |
| **Trigger** | User navigates to the Login/Registration card. |
| **Pre-conditions** | Active internet connection must be established. |
| **Post-conditions** | Registers a new account or validates credentials, caching the token. |
| **Main Success Scenario** | 1. User inputs email, password, and full name.<br>2. User taps "Register".<br>3. Firebase validates input parameters.<br>4. Registration succeeds; system caches session token and logs user into Dashboard. |
| **Extensions** | *Registration Offline Flow*:<br>1. User tries to submit form while offline.<br>2. System blocks submit and alerts "Internet connection required". |
| **Priority** | Critical |
| **Special Requirements** | Enforce non-resizing layout to prevent virtual keyboard rendering crashes. |
| **Open Questions** | None |

#### 3.2.3 Mock-up
A dark transparent overlay on top of a looping local video background (`assets/videos/login_bg.mp4`). A floating language switch capsule is pinned to the top-right showing "🇬🇧 EN | 🇵🇰 اردو". A centered frosted glassmorphic card container contains input fields with white borders for Email, Password, and Full Name, followed by a solid emerald action button.

#### 3.2.4 Functional Requirements
*   **BRD-FR-001: Native Multi-Language Toggling**  
    The language switcher toggle shall instantly swap all form text, hints, error tags, and titles between English and Urdu using local dictionary bundles.
*   **BRD-FR-002: Low-Spec UI Layout Safety**  
    The root Scaffold shall configure `resizeToAvoidBottomInset: false`. All input fields are padded using:
    `Padding(padding: EdgeInsets.only(bottom: MediaQuery.of(context).viewInsets.bottom))`
*   **BRD-FR-009: User Account Registration**  
    The registration validator shall block form submission unless:
    *   Email conforms to standard syntax checks (`^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`).
    *   Password has a minimum length of 8 characters, with 1 uppercase letter, 1 digit, and 1 special symbol.

#### 3.2.5 Field level specifications
##### Form Elements:
| Call-out | Field Label | UI Control | Mand? | Editable | Data Type | Value Set | Default Value | Data Example | Data Source |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Email Input | Email Address | text field | Yes | Yes | String | None | N/A | user@farm.com | User entry |
| Pass Input | Password | text field | Yes | Yes | String | None | N/A | SecureP@ss123 | User entry |
| Name Input | Full Name | text field | No | Yes | String | None | N/A | Muhammad Omer | User entry |

##### Form Business Rules and Dependencies:
| Field Label | Validation / Business Rules | Error Messages | Data Dependencies | Additional Info/ Notes |
| :--- | :--- | :--- | :--- | :--- |
| Email Address | Must be non-empty and match standard email syntax. | "Please enter a valid email address." | None | Validation runs on form submit. |
| Password | Minimum 8 characters, containing uppercase, digit, and symbol. | "Password must contain 8+ characters, an uppercase letter, a number, and a special character." | None | Eye icon toggles text obscuring. |

##### Buttons, Links and Icons:
| Button, Link, Icon Label | OnClick Event | Visible | Enabled Vs Disabled | Navigate To | Validation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| EN / اردو | Toggles localization context. | Yes | Always Enabled | Re-draws Current | None |
| Submit Button | Authenticates credentials. | Yes | Enabled if fields are filled | Dashboard | Calls input validation checks. |
| Toggle Card Link | Swaps view between Login and Sign-Up. | Yes | Always Enabled | Re-draws Card | None |

---

### 3.3 Home Screen / Main Dashboard
#### 3.3.1 Purpose/ Description
Acts as the central operational hub, showing stats, active connection indicators, and buttons routing to individual tools.

#### 3.3.2 Use case
| UC-3 | Navigation Hub and Stats Review |
| :--- | :--- |
| **Primary Actor(s)** | Rural Farmer, Scientific Inspector |
| **Stakeholders and Interest** | Project Sponsor (reviewing query metrics) |
| **Trigger** | User enters the application home view. |
| **Pre-conditions** | Valid authenticated session. |
| **Post-conditions** | Renders dynamic cards showing local history counts and online state. |
| **Main Success Scenario** | 1. Dashboard loads stats cards.<br>2. App checks local SQLite database files to count log records.<br>3. Displays active counts and network state status badge.<br>4. Farmer taps a service card (e.g., "Crop Recommendation") to navigate to that feature. |
| **Extensions** | None |
| **Priority** | High |
| **Special Requirements** | The history icon in the header displays a red notification badge showing the current total count of cached diagnostics. |
| **Open Questions** | None |

#### 3.3.3 Mock-up
Top App Bar in emerald green containing the title "AgroSmart Dashboard", local language switcher, and a History icon with a red badge. Below is a welcome card displaying the farmer's name. A horizontal row displays stats: "Saved Diagnostics" and "System Mode". Below is a 2x2 grid of cards: "Crop Recommendation", "Fertilizer Advisory", "Pesticide Diagnosis", and "Weather Smart Tips", each with a thumbnail and card titles.

#### 3.3.4 Functional Requirements
*   **BRD-FR-008: Local Database Cache Synchronization**  
    The Home Screen shall query the SQLite database helper class on launch to populate the active log count badge.
*   **BRD-FR-018: Network State Alerting**  
    The application shall monitor network status. If offline, the top header must display a persistent orange warning banner indicating that recommendations are restricted to local fallback advice.
*   **BRD-FR-019: Global Staging and Production Endpoint Routing**  
    The application configures base URLs dynamically using the `useLocalBackend` toggle flag. If active, API transactions route to `http://127.0.0.1:8000/api`. If inactive, requests route to the production Azure endpoint.

#### 3.3.5 Field level specifications
*This screen contains no input fields.*

##### Buttons, Links and Icons:
| Button, Link, Icon Label | OnClick Event | Visible | Enabled Vs Disabled | Navigate To | Validation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Crop Recommendation | Launches soil inputs. | Yes | Always Enabled | Crop Input Screen | None |
| Fertilizer Advisory | Launches fertilizer inputs. | Yes | Always Enabled | Fertilizer Input Screen | None |
| Pesticide Diagnosis | Launches pest symptomatology form. | Yes | Always Enabled | Pesticide Search Screen | None |
| Weather Smart Tips | Launches location advisory page. | Yes | Always Enabled | Weather Advisory Screen | None |
| History Icon (Badge) | Opens history logs list. | Yes | Always Enabled | Historical Logs Screen | None |

---

### 3.4 Crop Recommendation Form Screen
#### 3.4.1 Purpose/ Description
Ingests N, P, K, pH, temperature, humidity, and rainfall attributes to evaluate the optimal crop.

#### 3.4.2 Use case
Refer to [Section 3.1.3.1 (UC-ML-001)](#3131-use-cases) for the detailed soil recommendation use case.

#### 3.4.3 Mock-up
Green App Bar "Soil Crop Diagnosis". Pinned at the top is a light-mint banner showing the safe agronomic bounds. The body contains 7 numeric input fields for N, P, K, pH, Temperature, Humidity, and Rainfall. In addition, the pH, Temperature, and Humidity fields feature horizontal adjustment sliders. A solid green floating bottom button is labeled "Get Crop Recommendation".

#### 3.4.4 Functional Requirements
*   **BRD-FR-003: Dual-Model ML Ingestion**  
    The client app shall package inputs and dispatch a POST request to `/api/crop/`. Form validation must block inputs outside typical bounds before dispatch:
    *   Nitrogen (N): `0` to `140`
    *   Phosphorus (P): `0` to `145`
    *   Potassium (K): `0` to `205`
    *   Soil pH: `0` to `14`
    *   Temperature: `0` to `50`°C
    *   Humidity: `0` to `100`%
    *   Rainfall: `0` to `300`mm
*   **BRD-FR-011: Soil Diagnostic Guidance Overlay**  
    Tapping the info icon next to each input label shall render a popup overlay card describing the specific soil nutrient's role.

#### 3.4.5 Field level specifications
##### Form Elements:
| Call-out | Field Label | UI Control | Mand? | Editable | Data Type | Value Set | Default Value | Data Example | Data Source |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Input N | Nitrogen (N) | numeric textbox | Yes | Yes | Float | 0.0 - 140.0 | N/A | 90.0 | User entry |
| Input P | Phosphorus (P) | numeric textbox | Yes | Yes | Float | 0.0 - 145.0 | N/A | 42.0 | User entry |
| Input K | Potassium (K) | numeric textbox | Yes | Yes | Float | 0.0 - 205.0 | N/A | 43.0 | User entry |
| Input pH | Soil pH | textbox / slider | Yes | Yes | Float | 0.0 - 14.0 | 6.5 | 6.5 | User entry |
| Input Temp | Temperature (°C) | textbox / slider | Yes | Yes | Float | 0.0 - 50.0 | 25.0 | 20.6 | User entry |
| Input Hum | Humidity (%) | textbox / slider | Yes | Yes | Float | 0.0 - 100.0 | 50.0 | 82.0 | User entry |
| Input Rain | Rainfall (mm) | numeric textbox | Yes | Yes | Float | 0.0 - 300.0 | N/A | 200.2 | User entry |

##### Form Business Rules and Dependencies:
| Field Label | Validation / Business Rules | Error Messages | Data Dependencies | Additional Info/ Notes |
| :--- | :--- | :--- | :--- | :--- |
| Nitrogen (N) | Must be a valid float between 0 and 140. | "Nitrogen must be between 0 and 140 kg/ha" | None | Validated on submit. |
| Soil pH | Must be a valid float between 0 and 14. | "pH must be between 0 and 14" | None | Sliders scale in increments of 0.1. |

##### Buttons, Links and Icons:
| Button, Link, Icon Label | OnClick Event | Visible | Enabled Vs Disabled | Navigate To | Validation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Info Icon | Displays modal guidance bounds dialog. | Yes | Always Enabled | Overlay modal | None |
| Submit Button | Dispatches soil metrics payload to backend. | Yes | Enabled if fields are valid | Result Screen | Triggers validations. |

---

### 3.5 Fertilizer Recommendation Form Screen
#### 3.5.1 Purpose/ Description
Ingests Nitrogen, Potassium, Phosphorous, Temperature, Humidity, Moisture, Soil Type, and Crop Type parameters to suggest fertilizer combinations. Enforces strict typo preservation.

#### 3.5.2 Use case
| UC-4 | Fertilizer Advisory Sourcing |
| :--- | :--- |
| **Primary Actor(s)** | Rural Farmer |
| **Stakeholders and Interest** | Data Specialist (Sarah Jenkins) (ensuring typo alignment) |
| **Trigger** | User submits the fertilizer form. |
| **Pre-conditions** | Active authenticated session. |
| **Post-conditions** | Returns the recommended fertilizer and caches to SQLite history. |
| **Main Success Scenario** | 1. Farmer selects Soil Type (e.g. "Sandy") and Crop Type (e.g. "Maize").<br>2. Farmer inputs moisture, N, K, P, temperature, and humidity.<br>3. Taps submit.<br>4. System dispatches fields using exact typo payload schemas.<br>5. Django runs model and returns result. |
| **Extensions** | None |
| **Priority** | Critical |
| **Special Requirements** | Parameter strings must match typos: `'Temparature'`, `'Humidity '`, and `'Phosphorous'` to fit RandomForest dataset keys. |
| **Open Questions** | None |

#### 3.5.3 Mock-up
A vertical scrollable form containing: a horizontal list of scrollable soil chips (Sandy, Loamy, Black, Red, Clayey); a dropdown menu of crops; and numeric text boxes for Moisture, Nitrogen, Potassium, Phosphorous, Temparature, and Humidity. A prominent bottom action button is labeled "Get Fertilizer Mixture".

#### 3.5.4 Functional Requirements
*   **BRD-FR-003: Dual-Model ML Ingestion**  
    The frontend form values and backend REST validators shall package the inputs using the exact typographical keys:
    - `"Temparature"` (spelled with 'a' in the second syllable)
    - `"Humidity "` (containing a trailing space character)
    - `"Phosphorous"` (spelled with 'o' before 'u')

#### 3.5.5 Field level specifications
##### Form Elements:
| Call-out | Field Label | UI Control | Mand? | Editable | Data Type | Value Set | Default Value | Data Example | Data Source |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Soil Chips | Soil Type | card chips list | Yes | Yes | String | Sandy, Loamy, Black, Red, Clayey | Sandy | Sandy | User selection |
| Crop Dropdown | Crop Type | dropdown | Yes | Yes | String | Maize, Sugarcane, Cotton, Tobacco, Paddy, Wheat, Barley | Maize | Maize | User selection |
| Input Moisture | Moisture | numeric textbox | Yes | Yes | Float | 0.0 - 100.0 | N/A | 38.0 | User entry |
| Input N | Nitrogen | numeric textbox | Yes | Yes | Float | 0.0 - 140.0 | N/A | 37.0 | User entry |
| Input K | Potassium | numeric textbox | Yes | Yes | Float | 0.0 - 205.0 | N/A | 0.0 | User entry |
| Input P | Phosphorous | numeric textbox | Yes | Yes | Float | 0.0 - 145.0 | N/A | 0.0 | User entry |
| Input Temp | Temparature | numeric textbox | Yes | Yes | Float | 0.0 - 50.0 | N/A | 26.0 | User entry |
| Input Hum | Humidity | numeric textbox | Yes | Yes | Float | 0.0 - 100.0 | N/A | 52.0 | User entry |

##### Form Business Rules and Dependencies:
| Field Label | Validation / Business Rules | Error Messages | Data Dependencies | Additional Info/ Notes |
| :--- | :--- | :--- | :--- | :--- |
| Soil Type | Must choose exactly one chip from the set. | "Please select a Soil Type." | None | Tapping chip highlights it in green. |
| Crop Type | Must choose exactly one option from dropdown. | "Please select a Crop Type." | None | Uses localized icon tags. |

##### Buttons, Links and Icons:
| Button, Link, Icon Label | OnClick Event | Visible | Enabled Vs Disabled | Navigate To | Validation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Submit Button | Dispatches fertilizer payload to backend API. | Yes | Enabled if fields are valid | Result Screen | Triggers validations. |

---

### 3.6 Pesticide Lookup Form Screen
#### 3.6.1 Purpose/ Description
Maps crop names and symptom descriptions against a disease database using fuzzy keyword matches.

#### 3.6.2 Use case
Refer to [Section 3.3.3.1 (UC-PE-001)](#3331-use-cases) for the detailed fuzzy pesticide search use case.

#### 3.6.3 Mock-up
App Bar "Pest & Disease Diagnosis". Pinned top is a "Pest Symptom Quick Guide" summary block. In the body, a Select Crop autocomplete text field is followed by a multi-line Describe Symptoms text area. Below this are horizontal scrollable chips for quick-symptom populating. A wide action button at the bottom features a shield icon and the text "Get Treatment Recommendation".

#### 3.6.4 Functional Requirements
*   **BRD-FR-007: Fuzzy-Text Pesticide Lookup**  
    The backend shall process requests sent to `/api/pesticide/` using fuzzy keyword matching against symptom keys (including `blast`, `brown spot`, `stem borer`, `leaf folder`, `rust`, `mildew`, `armyworm`, `bollworm`, `whitefly`, `aphid`, `leaf miner`, `fruit borer`).
    *   If no keyword matches, the system shall split the query and fallback to the organic Neem Oil default protocol.
    *   Vegetables (`tomato`, `potato`, `brinjal`, `chili`, `onion`, `garlic`) must map to a generic `"vegetable"` database category tag.

#### 3.6.5 Field level specifications
##### Form Elements:
| Call-out | Field Label | UI Control | Mand? | Editable | Data Type | Value Set | Default Value | Data Example | Data Source |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Crop Input | Select Crop | autocomplete textbox | Yes | Yes | String | rice, wheat, maize, cotton, sugarcane, etc. | N/A | rice | User entry |
| Symptom Input | Describe Symptoms | text area | Yes | Yes | String | None | N/A | leaves have brown spots | User entry |

##### Form Business Rules and Dependencies:
| Field Label | Validation / Business Rules | Error Messages | Data Dependencies | Additional Info/ Notes |
| :--- | :--- | :--- | :--- | :--- |
| Select Crop | Text must not be empty. Autocomplete suggests matches. | "Please specify a crop." | None | Syncs with pesticide database labels. |
| Describe Symptoms | Must have at least 3 characters. | "Please describe symptoms in more detail." | None | Tapping quick chips fills this field. |

##### Buttons, Links and Icons:
| Button, Link, Icon Label | OnClick Event | Visible | Enabled Vs Disabled | Navigate To | Validation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Symptom Chips | Appends chip text to Describe Symptoms field. | Yes | Always Enabled | Re-draws field | None |
| Submit Button | Dispatches inputs payload to backend. | Yes | Enabled if fields are valid | Result Screen | Calls form validation. |

---

### 3.7 Weather & AI Advisory Screen
#### 3.7.1 Purpose/ Description
Retrieves GPS location coordinates, triggers local weather lookups, and generates structured AI farming recommendations.

#### 3.7.2 Use case
Refer to [Section 3.6.3.1 (UC-WE-001)](#3631-use-cases) for the detailed weather advisory use case.

#### 3.7.3 Mock-up
Top location chip toggle bar: "Use GPS Location" vs "Enter Coordinates Manually". The GPS panel shows a satellite dish indicator and latitude/longitude boxes. The manual panel features manual textboxes for Latitude and Longitude and quick-select buttons for local cities. A crop dropdown menu is followed by a full-width action button: "Get Weather Farming Tips".

#### 3.7.4 Functional Requirements
*   **BRD-FR-006: Cognitive Advisory Formatting**  
    The backend shall enforce a rigid prompt structure returning exactly four headings: `💧 WATERING`, `🌱 FERTILIZER`, `🐛 PEST RISK`, and `✅ TIP`.
*   **BRD-FR-013: Geographic Coordinates Sourcing**  
    The application shall query device GPS sensors to obtain coordinates. If sensors fail or permissions are denied, it shall default to Islamabad coordinates (`33.6844, 73.0479`) and allow manual adjustments.
*   **BRD-FR-004: High-Availability Offline Fallback**  
    If network connectivity is lost or the API request times out (exceeding 5 seconds), client-side interceptors shall trigger `get_fallback_advice()` within 500ms using deterministic local rules based on current temperature, humidity, and conditions:
    *   Rain/Thunderstorm -> watering = "No", fertilizer = "Wait", pest = "Medium", tip = "Cover sensitive crops".
    *   Temp > 38°C -> watering = "Yes", fertilizer = "Wait", pest = "High", tip = "Provide shade".
    *   Humidity > 80% -> watering = "No", fertilizer = "Wait", pest = "High - fungal", tip = "Ensure air circulation".

#### 3.7.5 Field level specifications
##### Form Elements:
| Call-out | Field Label | UI Control | Mand? | Editable | Data Type | Value Set | Default Value | Data Example | Data Source |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Toggle Bar | Location Mode | toggle tab bar | Yes | Yes | String | GPS, Manual | GPS | GPS | User selection |
| Lat Input | Latitude | text field | Yes | Yes | Float | -90.0 to 90.0 | 33.6844 | 33.6844 | GPS/User entry |
| Lon Input | Longitude | text field | Yes | Yes | Float | -180.0 to 180.0| 73.0479 | 73.0479 | GPS/User entry |
| Crop Input | Target Crop | dropdown | No | Yes | String | wheat, rice, maize, cotton, sugarcane, etc. | N/A | wheat | User selection |

##### Form Business Rules and Dependencies:
| Field Label | Validation / Business Rules | Error Messages | Data Dependencies | Additional Info/ Notes |
| :--- | :--- | :--- | :--- | :--- |
| Latitude | Must be a valid float between -90 and 90. | "Latitude must be between -90 and 90." | Enabled in Manual mode only | Automatically populated in GPS mode. |
| Longitude | Must be a valid float between -180 and 180. | "Longitude must be between -180 and 180." | Enabled in Manual mode only | Automatically populated in GPS mode. |

##### Buttons, Links and Icons:
| Button, Link, Icon Label | OnClick Event | Visible | Enabled Vs Disabled | Navigate To | Validation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| City Quick-Select | Populates Latitude and Longitude with pre-set coordinates. | Yes (Manual mode only) | Always Enabled | Re-draws fields | None |
| Submit Button | Dispatches coordinates and crop to backend API. | Yes | Enabled if fields are valid | Result Screen | Validates floats bounds. |

---

### 3.8 Result & Diagnostic Report Screen
#### 3.8.1 Purpose/ Description
Presents the evaluation report for crop, fertilizer, pesticide, or weather advice, complete with input tables, AI text blocks, and Ethereum validation receipts.

#### 3.8.2 Use case
| UC-5 | Validation Audit Verification |
| :--- | :--- |
| **Primary Actor(s)** | Rural Farmer, Scientific Inspector |
| **Stakeholders and Interest** | Lead Architect (Omer Siddiqui) (audit consistency) |
| **Trigger** | Result data is returned to the UI. |
| **Pre-conditions** | Diagnostic query succeeds. |
| **Post-conditions** | Renders results and caches verification hashes. |
| **Main Success Scenario** | 1. Screen loads returned advice details.<br>2. Displays structured accordion values.<br>3. Reads blockchain hash receipt block.<br>4. User clicks "Verify on Sepolia Etherscan" to view transaction details. |
| **Extensions** | *Blockchain Transaction Pending Sync*:<br>1. Celery task is processing mining.<br>2. Ticket renders "Pending Sync" status in blue. |
| **Priority** | High |
| **Special Requirements** | Renders dynamic backgrounds based on weather conditions (warm gradient for clear sky, blue/grey for rain). |
| **Open Questions** | None |

#### 3.8.3 Mock-up
App Bar with a back arrow and history link. The body contains an elevated gradient card showing a white circular checkmark and the recommended action in large typography. Below is an input/output details comparison table. Pinned to the bottom is a dashed-line "Security Audit Receipt" ticket displaying the transaction hash, Sepolia status flag, and a "Verify on Sepolia Etherscan" link.

#### 3.8.4 Functional Requirements
*   **BRD-FR-014: Unified Weather Advisory Dashboard**  
    The Result Screen shall combine localized weather readings (temperature, humidity, wind conditions) with structured, parsed conversational advisory recommendations in a single scrollable panel.
*   **BRD-FR-020: Ledger Verification Link Generation**  
    The receipt ticket shall read the transaction hash returned from Django. If synchronized, it must enable a clickable hyperlink redirecting the user to `https://sepolia.etherscan.io/tx/{hash}`.

#### 3.8.5 Field level specifications
*This screen contains no input fields.*

##### Buttons, Links and Icons:
| Button, Link, Icon Label | OnClick Event | Visible | Enabled Vs Disabled | Navigate To | Validation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Etherscan Link | Launches external web browser containing transaction hash. | Yes (if hash exists) | Enabled if status is 'Synchronized' | External Browser | None |
| Save Record Button | Forces manual SQLite cache database lock and write. | Yes | Enabled if record isn't auto-saved | Dashboard | None |
| Try Another Query | Clears active screen states and resets forms. | Yes | Always Enabled | Dashboard | None |

---

### 3.9 Historical Logs & Audit Registry Screen
#### 3.9.1 Purpose/ Description
Provides a searchable, filterable list of all local query logs cached in the SQLite database, with swipe-to-delete gestures.

#### 3.9.2 Use case
Refer to [Section 3.4.3.1 (UC-DB-001)](#3431-use-cases) for the detailed historical log verification use case.

#### 3.9.3 Mock-up
App Bar with a "Clear All" trash bin icon. Below is a sticky row of filter chips: "All Records", "🌾 Crops", "🧪 Fertilizers", "🐛 Pesticides", and "🌤️ Weather Tips". Below is a scrollable list of history cards showing custom colored avatars, query summary titles, and timestamps. Sliding a card left reveals a red background with a delete icon.

#### 3.9.4 Functional Requirements
*   **BRD-FR-008: Local Database Cache Synchronization**  
    The view list shall load records from the local SQLite cache, automatically updating the homepage log count badge on deletion events.
*   **BRD-FR-012: Advisory Query Detail Expansion**  
    Tapping a historical diagnostic log card shall trigger a details drawer expanding raw inputs and exact output advice cached locally on SQLite.
*   **BRD-FR-015: Historical Log Searching**  
    The search bar shall support keyword queries, filtering history cards based on crop, fertilizer, or location strings.
*   **BRD-FR-016: Historical Log Categorical Filtering**  
    Tapping category chips must restrict list items to only those corresponding to the selected type (Crops, Fertilizers, Pesticides, Weather).
*   **BRD-FR-017: Session Termination & Account Sign-out**  
    A settings sign-out trigger shall terminate active Firebase sessions, clear cached authentication tokens, flush the local memory state, and redirect users to the Login Screen.
*   **BRD-FR-005: Non-Blocking Web3 Auditing**  
    Audit history records shall expose sync status tags showing whether the recommendation transaction is 'Synchronized' or 'Pending Blockchain Sync' on the Sepolia Ethereum testnet.

#### 3.9.5 Field level specifications
##### Form Elements:
| Call-out | Field Label | UI Control | Mand? | Editable | Data Type | Value Set | Default Value | Data Example | Data Source |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Search Input | Search Logs | search textbox | No | Yes | String | None | N/A | Urea | User entry |
| Category Row | Category | filter chips | No | Yes | String | Crops, Fertilizers, Pesticides, Weather | All Records | Crops | User selection |

##### Form Business Rules and Dependencies:
| Field Label | Validation / Business Rules | Error Messages | Data Dependencies | Additional Info/ Notes |
| :--- | :--- | :--- | :--- | :--- |
| Search Logs | Filters list dynamically as the user types. | "No matching records found." | SQLite DB connection | Empty string restores full list. |

##### Buttons, Links and Icons:
| Button, Link, Icon Label | OnClick Event | Visible | Enabled Vs Disabled | Navigate To | Validation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Trash Icon | Clears the entire SQLite database cache history. | Yes | Enabled if list is not empty | Re-draws view | Prompts confirmation. |
| Log Card | Opens details expansion drawer showing details. | Yes | Always Enabled | Expansion Drawer | None |

---

## 4. System Configurations

This section outlines the setup configurations required to compile the mobile client and initialize the Django backend:

1.  **Environment Routing Flags:**  
    *   `useLocalBackend` (Boolean): Maps client endpoints to `http://127.0.0.1:8000/api` (if true) or production Azure host (`https://agrosmart-app-service-bcg4hadja2e0ddhe.southeastasia-01.azurewebsites.net/api`) (if false).
2.  **Firebase Client Setup:**  
    *   Android: Requires staging `google-services.json` copied to `/android/app/`.
    *   iOS: Requires staging `GoogleService-Info.plist` copied to `/ios/Runner/`.
3.  **Celery Queue Configurations:**  
    *   Broker URL: Central Azure Redis instance or RabbitMQ config.
    *   Result Backend: Configured to save state logs to Azure PostgreSQL database.

---

## 5. Other System Requirements/ Non-Functional Requirements

*   **API Response Times:** Model inferences shall compile and output recommendation results in under 2 seconds.
*   **Offline Transition Latency:** Connection dropouts must trigger the local fallback engine in under 500ms.
*   **SQLite Transaction Speed:** Reads and writes to local database files must complete in under 100ms.
*   **Security Protocol:** Secure storage utilities must encrypt Firebase JWT tokens using Keychain (iOS) and Keystore (Android) platforms.

---

## 6. Reporting Requirements

The Django backend records recommendation events to the Azure PostgreSQL database for audit tracking.

### Audit Transaction Schema (PostgreSQL):
```sql
CREATE TABLE recommendation_audit_log (
    id SERIAL PRIMARY KEY,
    user_id VARCHAR(128) NOT NULL,
    query_type VARCHAR(64) NOT NULL,
    input_payload JSONB NOT NULL,
    output_result JSONB NOT NULL,
    blockchain_tx_hash VARCHAR(66),
    sync_status VARCHAR(32) DEFAULT 'Pending Sync',
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
*   **Reporting Access:** Scientific Review Inspectors can extract summaries of these logs filtered by `timestamp` ranges or `query_type` using administrative SQL tools.

---

## 7. Integration Requirements

The system integrates with three external software APIs:
1.  **OpenWeatherMap API:** Connects via REST using:
    `GET https://api.openweathermap.org/data/2.5/weather?lat={lat}&lon={lon}&appid={key}&units=metric`
2.  **Google Gemini 2.0 Flash:** Integrates using the standard SDK:
    *   Model: `models/gemini-2.0-flash`
    *   Enforces schema prompt parsing rules.
3.  **Ethereum Sepolia testnet:** Uses Infura endpoints and web3.py to broadcast signed transactions to the contract ABI, calling the `logRecommendation(string type, string recommendation, string inputData)` function.

### 7.1 Exception Handling/ Error Reporting
The following table outlines the integration error exception handling strategies:

| Exception/ Error ID | Error | Cause | Solution Strategy |
| :--- | :--- | :--- | :--- |
| **ERR-INT-101** | OpenWeatherMap Timeout | Network loss or API rate limits reached. | Backend falls back to mock Islamabad parameters and logs warning. |
| **ERR-INT-102** | Gemini API Quota Exceeded | Free API tier query limits hit. | Interceptor redirects calculation to deterministic `get_fallback_advice()`. |
| **ERR-INT-103** | Web3 Node Latency / Gas failure | Sepolia block validation delay or insufficient gas fees. | Celery worker updates PostgreSQL status flag to `'Pending Blockchain Sync'` and retires task up to 3 times before logging alert to Fatima Al-Sayed. |
| **ERR-INT-104** | Typo Parameter Validation Crash | Serializer checks mismatch dataset spelling attributes. | Data serializer enforces strict schema matches for `'Temparature'`, `'Humidity '`, and `'Phosphorous'` keys. |

---

## 8. Data Migration/ Conversion Requirements

### 8.1 Data Conversion Strategy
As AgroSmart is a greenfield MVP, no legacy historical data migration is required.
### 8.2 Data Conversion Preparation
N/A
### 8.3 Data Conversion Specifications
N/A

---

## 9. References
1.  **ISO 21502:2020:** Guidelines for project management and scope verification.
2.  **Scikit-Learn Random Forest Classifier Specification:** Requirements for serialization compatibility.
3.  **Ethereum Smart Contract ABI Standards:** Integration interfaces.

---

## 10. Open Issues
| Issue ID | Issue | Raised By | Raised On | Solution/ Decision | Resolved By | Resolved On | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **ISS-001** | Fertilizer dataset typos | Tariq Mahmood | 06/22/2026 | Typographical column names verified as locked. Forms and API serializers must preserve original typos to prevent model evaluation failures. | Elena Rostova | 06/22/2026 | Closed |

---

## Appendix
*Refer to `business_requirements_document.md` Appendix B for Context diagrams, DFD mapping, and visual workflows.*
