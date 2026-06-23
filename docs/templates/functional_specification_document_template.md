# AgroSmart FSD Generation Master Prompt

You can copy and paste the prompt below into Google Stitch (or any advanced LLM) to generate a fully populated, production-grade Functional Specification Document (FSD) that incorporates all the technical details, field elements, validation rules, button actions, and error handling of the AgroSmart platform.

---

```text
Act as a Principal Solution Architect and Lead Business Analyst. Your task is to generate a comprehensive, production-grade Functional Specification Document (FSD) for the "AgroSmart" platform. 

You must strictly ingest and mirror the official "Stanford University Administrative Systems Functional Specification Document" structural template. Every single heading, sub-heading, table layout, and structural index from that template must be explicitly populated. 

This document must be structured strictly from a PRE-DEVELOPMENT perspective (Future/Prescriptive Tense: "The platform shall...", "The system will...") to serve as an authoritative technical contract. Fill in all sections thoroughly with full enterprise prose, complete matrices, and zero placeholders or TBDs. 

You must strictly incorporate the following technical specifications, environmental boundaries, and business rules established across our architecture workspace:

1. SYSTEM ARCHITECTURE & ENVIRONMENT:
   - Client: Cross-platform Flutter mobile client running natively on iOS (15.0+) and Android (API 28+). Persists logs locally using an SQLite file database.
   - Server Backend: Python Django REST API backend hosted on Microsoft Azure Web Apps, bound to an Azure PostgreSQL instance for system-wide auditing.
   - Machine Learning: Pre-trained RandomForestClassifier models loaded via joblib.
   - Weather API: Integration with OpenWeatherMap.
   - AI Advisory: Google Gemini 2.0 Flash API integration.
   - Web3 Audit Ledger: Auditing recommendations to the Ethereum Sepolia testnet using web3.py via Infura nodes.

2. FORM FIELDS & SCHEMAS PRESERVATION:
   - Front-end forms and backend serializers must strictly preserve non-standard spellings from the training data:
     - 'Temparature' (misspelled with 'a' in the second syllable)
     - 'Humidity ' (containing a trailing space)
     - 'Phosphorous' (misspelled with 'o' before 'u')
   - Soil Types chip values: Sandy, Loamy, Black, Red, Clayey.
   - Crop Types dropdown values: Maize, Sugarcane, Cotton, Tobacco, Paddy, Wheat, Barley.
   - Autocomplete crops values for pesticide search: rice, wheat, maize, cotton, sugarcane, etc. (Vegetables map to generic 'vegetable' category backend index).
   - Coordinates-based weather entry requires Latitude and Longitude values (falling back to Islamabad: 33.6844, 73.0479).

3. SCREEN-LEVEL LAYOUTS & MOCK-UPS TO SPECIFY:
   - Splash Screen: Linear gradient, white circuit-leaf logo icon, loader text.
   - Login & Registration: Looping background video, globe language toggle capsule (EN | Urdu), frosted glassmorphic card container with validation indicators, text input rules checklist.
   - Dashboard: Welcome avatar header, stats summary chips, 2x2 service navigation cards with high-quality icons, bottom navigation bar.
   - Crop Input: Safe range bounds sticky guides, 7 numeric fields with horizontal sliders (N, P, K, pH, temp, humidity, rain), info popups.
   - Fertilizer Input: Soil chips selection, crop dropdown selection, N, K, P, moisture, temperature, humidity text fields.
   - Pesticide Search: Active crop autocomplete field, symptom description multi-line text area, tap quick-chips, shield icon submit button.
   - Weather Advisory: GPS location vs manual coordinate toggle chips, coordinate inputs, manual city selectors, target crop text field.
   - Results Screen: Circular checkmark animation, large action header, dynamic detail accordion tables, dashed-line Sepolia ticket.
   - History logs: Categorical filter chips (All, Crops, Fertilizers, Pesticides, Weather), keyword search input, swipe-to-delete cards list.

4. SYSTEM CONFIGURATIONS & NFRS:
   - Environment Route Flag: useLocalBackend toggles client requests between localhost and production Azure hosts.
   - Performance: API response times under 2s, offline fallback activation under 500ms, SQLite queries under 100ms.
   - Security: Token encryption via Keystore/Keychain, Firebase JWT session validation.

5. ERROR REPORTING & INTEGRATION EXCEPTIONS:
   - Include an Exception Handling table mapping standard error conditions:
     - ERR-INT-101 (OpenWeatherMap timeout, default to mock Islamabad weather)
     - ERR-INT-102 (Gemini API quota exceeded, trigger local rules fallback get_fallback_advice())
     - ERR-INT-103 (Sepolia transaction gas failure, update database sync status to 'Pending Blockchain Sync' and queue Celery retries)
     - ERR-INT-104 (Typo parameter validations mismatch)

---

OUTLINE TO GENERATE:

# Stanford University Administrative Systems
## Functional Specification Document

**Project Name:** AgroSmart (Enterprise Agricultural Intelligence Platform)  
**Document Version:** 1.0  
**Date:** 06/22/2026  

### Authors
(Table with columns: Name, Role, Department. Populate with Omer Siddiqui, Dr. Elena Rostova, Tariq Mahmood)
### Document History
(Table with columns: Date, Version, Document Revision Description, Document Author. Populate with version 1.0 definition)
### Approvals
(Table with columns: Approval Date, Approved Version, Approver Role, Approver. Populate with Client Venture Team and Lead Solution Architect approvals)

## Table of Contents
(Provide complete hyperlink table of contents mapping all sections below)

## 1. Introduction
### 1.1 Purpose of the document
(Explain that FSD maps BRD functional requirements to technical specifications, field values, inputs/outputs, and validation rules)
### 1.2 Project Scope
(Summary of cap of $35k CapEx, Flutter, Django REST Azure, RandomForest, Sepolia)
### 1.3 Scope of the document
(State that this document covers specifications for the MVP launch of all 9 screen layouts)
### 1.4 Related documents
(Table linking project_charter.md, business_requirements_document.md, project_context.md)
### 1.5 Terms/Acronyms and Definitions
(Definitions table for easy_localization, Provider, resizeToAvoidBottomInset, Temparature, Humidity , Phosphorous)
### 1.6 Risks and Assumptions
(Describe GPS module dependencies and unstable remote connectivity risks)

## 2. System/ Solution Overview
### 2.1 Context Diagram/ Interface Diagram/ Data Flow Diagram, Application Screen Flow, Sitemap, Process Flow
(Incorporate text-based diagram mapping mobile client views, Django API endpoints, databases, and Sepolia testnet)
### 2.2 System Actors
(User Roles and Responsibilities table mapping Rural Farmers and Scientific Inspectors)
### 2.3 Dependencies and Change Impacts
(Detail dependencies on Firebase, OpenWeatherMap, Gemini, and Sepolia)

## 3. Functional Specifications
(Itemize the 9 screens: 3.1 Splash, 3.2 Login/Register, 3.3 Dashboard, 3.4 Crop Input, 3.5 Fertilizer Input, 3.6 Pesticide Lookup, 3.7 Weather Tips, 3.8 Results Page, 3.9 History Log. For each screen, populate all the sections below without placeholders:)

#### 3.x.1 Purpose/ Description
(Write 2-3 sentences explaining screen role and visual aesthetics)
#### 3.x.2 Use case
(A complete Use Case Table in the Stanford FSD format, defining Use Case ID, Actors, Trigger, Pre/Post-conditions, Normal Flow, and Alternative Flows/Exceptions)
#### 3.x.3 Mock-up
(A complete textual description of the user interface layout, brand colors, glassmorphic styles, and video or asset overlays)
#### 3.x.4 Functional Requirements
(Table mapping the relevant BRD-FR-xxx requirements to specific screen functions, details, and rules)
#### 3.x.5 Field level specifications
(Detail the form elements in three tables:)
- Form Elements: (Columns: Call-out, Field Label, UI Control, Mand?, Editable, Data Type, Value Set, Default Value, Data Example, Data Source. Populate with inputs details)
- Form Business Rules and Dependencies: (Columns: Field Label, Validation / Business Rules, Error Messages, Data Dependencies, Additional Info/ Notes. Specify range checks and typo details)
- Buttons, Links and Icons: (Columns: Button, Link, Icon Label, OnClick Event, Other Event, Visible, Enabled Vs Disabled, Navigate To, Validation, Dependencies)

## 4. System Configurations
(Detail setup configurations for local vs production endpoint routing, Firebase google-services files, and Celery RabbitMQ/Redis broker setups)

## 5. Other System Requirements/ Non-Functional Requirements
(Define latency limits: sub-2s inference, sub-500ms offline fallback switch, sub-100ms SQLite query times, token secure storage encryption key chains)

## 6. Reporting Requirements
(Include Azure PostgreSQL recommendation_audit_log database schema definition and reporting queries parameters)

## 7. Integration Requirements
(Define API interfaces payloads structures. Include detailed subsection:)
### 7.1 Exception Handling/ Error Reporting
(A table mapping exceptions: ERR-INT-101, ERR-INT-102, ERR-INT-103, ERR-INT-104 with Error, Cause, and Solution Strategy)

## 8. Data Migration/ Conversion Requirements
(State that this is a greenfield MVP, so data migration is N/A)

## 9. References
(ISO 21502:2020, RandomForest specifications, Sepolia Smart Contract ABI)

## 10. Open Issues
(List open issues table: ISS-001 regarding dataset typos resolved by preservation rules)

## Appendix
(Refer to BRD Appendix B)
```
