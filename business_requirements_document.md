# AgroSmart: Business Requirements Document (BRD)
**Compliance Framework:** ISO 21502:2020 (Requirements Engineering and Scope Baseline Guidelines)  
**Contract Baseline:** Pre-Development Technical Specification  

---

### 1.0 Project Overview & Business Objectives
The proposed AgroSmart platform is an integrated client-server agricultural intelligence solution designed to deliver predictive crop recommendations, optimized soil chemical advice, and localized farming tips to users in remote regions. The core business objectives of the system are:
1.  **Resource Deficit Mitigation:** To reduce the operational expenses and diagnostic errors of regional farming portfolios by replacing intuitive soil management with machine learning analysis of NPK attributes.
2.  **Verifiable Diagnostics:** To provide high-accuracy field recommendations accessible on low-specification mobile devices under volatile environmental conditions.
3.  **Institutional Liability Protection:** To log all generated advice transactions to an immutable public blockchain ledger, protecting advising institutions from legal disputes and facilitating verification audits.

To maximize capital efficiency, the platform will be implemented under a fixed Capital Expenditure (CapEx) threshold of $35,000. Development resource governance will follow a three-tier model: a full-time core agile squad (comprising Muhammad Omer Siddiqui, Dr. Elena Rostova, and Tariq Mahmood) supported by a subsidized shared agency resource tier (including specialists in data serialization, blockchain programming, and DevOps pipelines) whose hours are scaled across parallel portfolios.

---

### 2.0 User Profiles & Demographic Constraints
The system will satisfy the operational requirements of two distinct user classes:
*   **Rural Farmers:**
    *   *Demographic Profile:* Characterized by limited digital literacy, high sensitivity to cellular data costs, and primary reliance on regional languages.
    *   *System Requirement:* The mobile client interface must support high-visibility graphics, simple navigation patterns, and instant English/Urdu translation matrix toggling. It must execute deterministic fallback rules natively on the device hardware when offline to bypass network connectivity constraints.
*   **Scientific Review Inspectors & Auditors:**
    *   *Demographic Profile:* Domain experts requiring data integrity checks, regulatory audits, and access to historical logs.
    *   *System Requirement:* The central backend must provide access to complete query histories and diagnostic logs via index-optimized search parameters.

These profiles establish the requirement for a cross-platform mobile client (Flutter-based) and a web-based administrative audit interface.

---

### 3.0 Functional Requirements Matrix

| Unique ID | Requirement Description | Target User Group | Priority |
| :--- | :--- | :--- | :--- |
| **BRD-FR-001** | **Native Multi-Language Toggling:** The system shall support instant toggling between English and Urdu language string matrices resolved natively on the device hardware via tokenized dictionary files. | Rural Farmers | High |
| **BRD-FR-002** | **Low-Spec UI Safety:** Screen layouts must isolate keyboard input fields, configuring the root container to prevent viewport resizing and utilizing manual view-inset offsets to eliminate form collapses on small screens. | Rural Farmers | High |
| **BRD-FR-003** | **Dual-Model ML Ingestion:** The planned API backend shall process diagnostic queries using two distinct pre-trained machine learning classification models to recommend optimal crop types and fertilizer mixtures. | Rural Farmers | High |
| **BRD-FR-004** | **High-Availability Offline Fallback:** If cloud APIs timeout or local network connectivity is lost, the client shall execute a local threshold rules engine to parse weather variables (precipitation, heat above 38°C, humidity above 80%) natively. | Rural Farmers | High |
| **BRD-FR-005** | **Non-Blocking Web3 Auditing:** The system shall log recommendation parameters to the Ethereum Sepolia network using background asynchronous tasks, keeping mobile threads responsive and preventing mining delays from blocking the user interface. | Scientific Inspectors | Medium |
| **BRD-FR-006** | **Cognitive Advisory Generation:** The backend API shall format weather parameters and crop context, filter external LLM responses, and enforce a rigid, hardcoded four-tier text output format (WATERING, FERTILIZER, PEST RISK, TIP). | Rural Farmers | Medium |
| **BRD-FR-007** | **Fuzzy-Text Pesticide Lookup:** The system shall host a lookup database that maps crop names and disease symptoms using fuzzy text keyword validation to retrieve matching treatments, defaulting to an organic Neem Oil protocol. | Rural Farmers | Medium |

---

### 4.0 Non-Functional Requirements (NFRs)

| NFR Category | Technical & Operational Specifications |
| :--- | :--- |
| **Availability & Performance** | The mobile client shall transition to the local fallback rules engine in less than 500 milliseconds during connection dropouts. The machine learning serialization models must load at backend startup, maintaining prediction response times under 2 seconds. |
| **Data Isolation & Concurrency** | The platform shall maintain absolute separation between database layers: local user histories and offline query caches will run natively on a client-side SQLite file database, while the global audit registry will run on a high-availability Azure PostgreSQL backend to support concurrent inspector administrative queries. |
| **Data Ingestion Integrity** | To prevent execution crashes during model queries, the backend serializers and the mobile form entry fields must strictly mirror the typographical parameters of the training datasets: `'Temparature'` (with 'a' in the second syllable), `'Humidity '` (with trailing space), and `'Phosphorous'` (with 'o' before 'u'). |
| **Security & Local Session Caching** | The client application shall validate passwords using strong registration parameters (length, uppercase, numbers, and symbols) and cache active session keys securely on local hardware to prevent unauthorized offline access. |

---

### 5.0 System Failover & Conflict Governance Protocols
The proposed platform will enforce strict governance protocols to handle system exceptions and configuration modifications:
1.  **Web3 Network Latency Failover:** If transaction mining loops on the Ethereum Sepolia network fail or time out, the background worker queue shall:
    *   Write a `'Pending Blockchain Sync'` status flag into the central PostgreSQL transaction registry.
    *   Bypass blocking UI loops, allowing the Django API to immediately return recommendations to the mobile user.
    *   Route the transaction failure log to DevOps reporting channels for automated sync retries.
2.  **Technical Change Escalation Path:** To prevent model execution failures, any changes to database columns, API data payloads, or core parameter spelling conventions—specifically `'Temparature'`, `'Humidity '`, and `'Phosphorous'`—shall require a formal change request. The modification escalation path requires:
    *   Validation analysis by the Data Specialist (Dr. Elena Rostova) verifying model input compatibility.
    *   Architectural impact review by the Lead Architect (Muhammad Omer Siddiqui) checking REST API and client-side view integrations.
    *   Written authorization and formal sign-off from the Project Sponsor prior to production deployment.
