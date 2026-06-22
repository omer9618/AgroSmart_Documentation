# AgroSmart BRD Generation Master Prompt

You can copy and paste the prompt below into Google Stitch (or any advanced LLM) to generate a fully populated, production-grade Business Requirements Document (BRD) that incorporates all the technical constraints and all 20 functional requirements of the AgroSmart workspace.

---

```text
Act as a Principal Solution Architect and Lead Business Analyst. Your task is to generate a comprehensive, production-grade Business Requirements Document (BRD) for the "AgroSmart" platform. 

You must strictly ingest and mirror the official "Stanford University Administrative Systems Business Requirements Document" structural template. Every single heading, sub-heading, table layout, and structural index from that template must be explicitly populated. 

This document must be structured strictly from a PRE-DEVELOPMENT perspective (Future/Prescriptive Tense: "The platform shall...", "The system will...") to serve as an authoritative technical contract. Fill in all sections thoroughly with full enterprise prose, complete matrices, and zero placeholders or TBDs. 

You must strictly incorporate the following technical specifications, environmental boundaries, and business rules established across our architecture workspace:

1. SYSTEM ARCHITECTURE & ENVIRONMENT:
   - Client: Cross-platform Flutter mobile client running natively on iOS (15.0+) and Android (API 28+). Persists logs locally using an SQLite file database.
   - Server Backend: Python Django REST API backend hosted on Microsoft Azure Web Apps, bound to an Azure PostgreSQL instance for system-wide auditing.
   - Machine Learning: Pre-trained RandomForestClassifier models loaded via joblib.
   - Weather API: Integration with OpenWeatherMap.
   - AI Advisory: Google Gemini 2.0 Flash API integration.
   - Web3 Audit Ledger: Auditing recommendations to the Ethereum Sepolia testnet using web3.py via Infura nodes.

2. MACHINE LEARNING & INPUT SPELLING CONSTRAINTS:
   - Crop Prediction Model (crop_model.pkl): Ingests Nitrogen (N: 0-140), Phosphorus (P: 0-145), Potassium (K: 0-205), Soil pH (0-14), Temperature (0-50°C), Humidity (0-100%), and Rainfall (0-300mm). Output decoded crop classes (e.g. rice, maize, wheat).
   - Fertilizer Prediction Model (fertilizer_model_final.pkl): Ingests Nitrogen, Potassium, Phosphorous, Temperature, Humidity, Moisture, Soil Type, and Crop Type.
   - CRITICAL SCHEMA Preservation: Front-end forms and backend serializers must strictly preserve non-standard spellings from the training data:
     - 'Temparature' (misspelled with 'a' in the second syllable)
     - 'Humidity ' (containing a trailing space)
     - 'Phosphorous' (misspelled with 'o' before 'u')
     - Soil Types: Sandy, Loamy, Black, Red, Clayey.
     - Crop Types: Maize, Sugarcane, Cotton, Tobacco, Paddy, Wheat, Barley.

3. COGNITIVE AI & WEATHER ADVISORY:
   - Gemini 2.0 Flash prompt mapping must parse and enforce a rigid 4-tier output schema:
     💧 WATERING: (Yes/No) - (4-5 words reason)
     🌱 FERTILIZER: (Good/Wait) - (4-5 words reason)
     🐛 PEST RISK: (Low/Medium/High) - (3-4 words)
     ✅ TIP: (one 5-8 word sentence)
   - High-Availability Offline Fallback: If network requests to OpenWeatherMap or Gemini exceed 5 seconds, client-side interceptors must trigger get_fallback_advice() within 500ms using deterministic local rules:
     - Rain/Thunderstorm: watering = "No", fertilizer = "Wait", pest = "Medium", tip = "Cover sensitive crops".
     - Temp > 38°C: watering = "Yes", fertilizer = "Wait", pest = "High - mites", tip = "Provide shade".
     - Humidity > 80%: watering = "No", fertilizer = "Wait", pest = "High - fungal risk", tip = "Ensure good air circulation".

4. WEB3 AUDITING & FAILOVER PROTOCOL:
   - Async Web3 Ledger Sync: To bypass transaction mining delays, Django REST API offloads Sepolia transactions to Celery background tasks.
   - Status Registration: Worker writes 'Pending Sync' state to PostgreSQL.
   - Sync Success: Mined transaction hash and Sepolia explorer link are cached in the PostgreSQL database.
   - Failure: If gas fails or nodes timeout after 3 retries, log failure state and trigger an email/Slack alert to DevOps (Fatima Al-Sayed). The mobile UI remains non-blocked and outputs advice immediately.

5. LOCAL DATABASE & OFFLINE EXPERIENCE:
   - SQLite cache: Saves query inputs, outputs, timestamps, and transaction hashes locally on the mobile client. Supports search queries, Recent records filtering, and delete operations.
   - UI safety: Scaffold resizeToAvoidBottomInset: false. Spacing adjusted manually via MediaQuery.of(context).viewInsets.bottom.
   - Localization: Local easy_localization English ('en') and Urdu ('ur') translation dictionaries loaded on device memory.

6. TECHNICAL CHANGE PATH:
   - Changes impacting parameters/schemas require approval: Data Science Verification (Sarah Jenkins) -> Serializer Update (Elena Rostova) -> Client Controller Update (Omer Siddiqui) -> Sponsor authorization.

---

OUTLINE TO GENERATE:

# Stanford University Administrative Systems
## Business Requirements Document

**Project Name:** AgroSmart (Enterprise Agricultural Intelligence Platform)  
**Document Version:** 1.0  
**Date:** 06/22/2026  

### Authors
(Table with columns: Name, Role, Department. Populate with Omer Siddiqui, Dr. Elena Rostova, Tariq Mahmood)
### Document History
(Table with columns: Date, Version, Document Revision Description, Document Author. Populate with version 1.0 definition)
### Approvals
(Table with columns: Approval Date, Approved Version, Approver Role, Approver. Populate with Client Venture Team and Lead Solution Architect approvals)

## Contents
(Provide complete hyperlink table of contents mapping all sections below)

## 1. Introduction
### 1.1. Purpose of the Document
(Full enterprise prose on food security, unscientific farming mitigation, and why this BRD is the binding contract prior to source code construction)
### 1.2. Document Conventions, Terms, and Definitions
(Typographical conventions. Detail the non-standard fields: 'Temparature', 'Humidity ', and 'Phosphorous' and their preservation rules)
### 1.3. Intended Audience and Reading Suggestions
(Audience table mapping Omer, Elena, Tariq, Marcus Vance, Alex Mercer, Sarah Jenkins, Kenji Sato, Fatima Al-Sayed, and Sponsor. Suggested reading path)
### 1.4. Scope
#### 1.4.1. Project Scope
(Detail boundaries of $35k CapEx budget)
#### 1.4.2. Business Requirement Document Scope
(Boundaries of the initial MVP launch)
### 1.5. References
(ISO 21502:2020, Sepolia smart contracts, Gemini API, OpenWeatherMap API)

## 2. Overall Description
### 2.1. Project Overview
(Legacy subjective workflow vs proposed ML-cognitive flow. Textual details of the diagrams in Appendix B)
### 2.2. Product Features
(Summary of ML inference, weather advisories, Web3 sync, and multi-language UI)
### 2.3. User Classes and Characteristics
(Detailed profiles of Rural Farmers and Scientific Review Inspectors)
### 2.4. Operating Environment
(Flutter client, SQLite, Django server, Azure Web Apps, Azure PostgreSQL, Sepolia RPC nodes)
### 2.5. Design and Implementation Constraints
(Budget, Provider state package, easy_localization, Celery async, non-resizing root layouts, spelling typos)
### 2.6. User Documentation
(Visual guides, Urdu/English help database)
### 2.7. Assumptions, Dependencies, and Risks
(External APIs, Sepolia network, model drift, API quotas)

## 3. System Features
(Provide a summary table mapping all 20 requirements below to reference numbers, component names, and priorities)

Itemize the following features, each with: Description (3.x.1), Stimulus/Response Sequences (3.x.2), Functional Requirements list (3.x.3) mapping specific BRD-FR requirements, and a detailed Use Case Table (3.x.3.1) matching the Stanford format:

3.1. Dual-Model Machine Learning Inference (Priority: Critical)
- BRD-FR-003: Dual-Model ML Ingestion (N, P, K, pH, temp, humidity, rainfall)
- BRD-FR-011: Soil Diagnostic Guidance Overlay (NP/K bounds tooltips)
- BRD-FR-019: Global Staging and Production Endpoint Routing (useLocalBackend flag)
- Use Case: UC-ML-001 (Predictive Soil Recommendation)

3.2. High-Availability Offline Fallback Engine (Priority: Critical)
- BRD-FR-004: High-Availability Offline Fallback (get_fallback_advice thresholds)
- BRD-FR-018: Network State Alerting (persistent orange warning banner)
- Use Case: UC-OF-001 (Local Weather Fallback Processing)

3.3. Fuzzy-Text Pesticide Knowledge Lookup (Priority: High)
- BRD-FR-007: Fuzzy-Text Pesticide Lookup (fuzzy symptomatology parsing & Neem Oil fallback)
- Use Case: UC-PE-001 (Pest Disease Diagnosis)

3.4. Local SQLite Caching and History Synchronization (Priority: High)
- BRD-FR-008: Local Database Cache Synchronization (automatic SQLite storage)
- BRD-FR-012: Advisory Query Detail Expansion (tap to expand detail views)
- BRD-FR-015: Historical Log Searching (keyword search query-string filtering)
- BRD-FR-016: Historical Log Categorical Filtering (categorical filter chips)
- Use Case: UC-DB-001 (Historical Log Verification)

3.5. Firebase User Authentication and Session Security (Priority: Critical)
- BRD-FR-009: User Account Registration (email/password validation parameters)
- BRD-FR-010: Session Authentication & Persistent Login (token caching and auto-login)
- BRD-FR-017: Session Termination & Account Sign-out (sign-out state flushing)
- BRD-FR-001: Native Multi-Language Toggling (easy_localization en/ur locale toggling)
- BRD-FR-002: Low-Spec UI Layout Safety (resizeToAvoidBottomInset: false, manual padding)
- Use Case: UC-AU-001 (Farmer Account Login)

3.6. Dynamic Location-Based Weather Advisory Dashboard (Priority: High)
- BRD-FR-006: Cognitive Advisory Formatting (Gemini 2.0 Flash 4-tier output prompt parsing)
- BRD-FR-013: Geographic Coordinates Sourcing (GPS reading and fallback coordinates)
- BRD-FR-014: Unified Weather Advisory Dashboard (combined weather and advisory cards)
- BRD-FR-005: Non-Blocking Web3 Auditing (Sepolia blockchain async auditing via Celery)
- BRD-FR-020: Ledger Verification Link Generation (Etherscan link on transaction card)
- Use Case: UC-WE-001 (Weather AI Advisory Sourcing)

## 4. External Interface Requirements
### 4.1. User Interface
(Frosted glass login cards, video loop underlay, keyboard viewInsets, tap targets, Urdu layout direction)
### 4.2. Hardware Interfaces
(GPS receivers, client flash storage)
### 4.3. Software Interfaces
(Django, OpenWeatherMap, Gemini, Sepolia Infura RPC)
### 4.4. Communications Interfaces
(HTTPS, JSON content headers)
### 4.5. Reporting Requirements
(Azure PostgreSQL audit logging, Etherscan transaction hashes)

## 5. Other Nonfunctional Requirements
### 5.1. Performance Requirements
(Sub-500ms offline failover activation, sub-2s inference)
### 5.2. Security Requirements
(Firebase Authentication, secure storage encryption key chains)
### 5.3. Data Requirements
(Data isolation dividing local SQLite from cloud PostgreSQL)
### 5.4. Software Quality Attributes
(Robustness, swappable RandomForest models)

## 6. Other Requirements
(Detailed Web3 Network Latency Failover Protocol, Celery workers, error logging, and the Technical Change Escalation Path)

## 7. Campus Readiness and Training
(Urdu/English onboarding visual guides, automated CI/CD staging release pipelines)

## Appendix A: Glossary
## Appendix B: Analysis Models
(Data Flow Diagram in text format, showing Mobile client, SQLite, Django REST, models, Gemini, Celery, PostgreSQL, Sepolia)
## Appendix C: Issues List
(Data Ingestion Typographical list: Temparature, Humidity , Phosphorous)
## Appendix D: Screenshots, Mock-Ups, and Live Links
## Appendix E: Test Scenarios
(Unit and integration tests for ML model loading, offline failovers, and non-standard query structures)
```