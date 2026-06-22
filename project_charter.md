# AgroSmart: Enterprise Project Charter
**Compliance Framework:** ISO 21502:2020 (Project, Programme, and Portfolio Management Guidelines)  
**Contract Baseline:** Pre-Development Initial Agreement  

---

### 1. Project Information
*   **Project name:** AgroSmart (Enterprise Agricultural Intelligence Platform)
*   **Project description:**  
    The proposed AgroSmart platform is a client-server agricultural intelligence system designed to deliver predictive crop recommendations, optimized fertilizer management, and real-time farming tips via a cross-platform mobile application. The target client-side application shall be built using the Flutter framework, utilizing Dart as the core runtime language to provide a uniform user experience on both Android and iOS devices. The planned client application will utilize the 'provider' package for application state control and the 'easy_localization' library to handle dynamic English and Urdu language string matrices.
    
    The mobile architecture shall mandate a configuration-driven environment routing strategy. The engineering team will implement an environment toggle flag that programmatically maps client API requests between a local staging endpoint (http://127.0.0.1:8000/api) and a centralized production environment hosted on Microsoft Azure Web Apps. The central server will process prediction queries using two custom-trained RandomForestClassifier machine learning models loaded at server startup using standard Python serialization utilities to perform low-latency predictive analysis.

---

### 2. Business Case
The proposed AgroSmart system will mitigate agricultural inefficiencies by offering localized prediction parameters directly in the field. To maintain 100% operational availability in remote areas lacking network connectivity, the platform will mitigate rural connectivity drops by engineering a client-side deterministic fallback engine. This engine will process local weather-threshold exceptions (such as precipitation, extreme heat above 38°C, and high humidity above 80%) natively on the hardware when cloud servers time out, ensuring continuous advisory uptime.
    
In accordance with ISO 21502 guidelines, the platform will implement a transparent risk and data-traceability governance structure. All issued recommendations (crop suggestions, fertilizer application formulas, and weather tips) will be recorded permanently to the Ethereum Sepolia testnet blockchain. By publishing receipt hashes to a decentralized blockchain ledger, the project sponsor and adviser group will secure absolute liability protection. This immutable trace will prevent retrospective tampering, providing verifiable evidence of agronomic advice that can be utilized to settle disputes, satisfy crop insurance criteria, and secure institutional micro-financing.

---

### 3. Project Deliverables
List the key planned deliverables of the project to be produced during the development lifecycle:
*   **Deliverable 1 (Cross-Platform Mobile UI Framework):**  
    A compiled, cross-platform mobile client built using Flutter to ensure native execution on Android and iOS devices. The planned layout features a highly responsive home dashboard screen linking to modular input screens. The onboarding login portal will utilize a custom glassmorphism overlay positioned on top of a looping local background video asset. To mathematically eliminate layout collapses when mobile virtual keyboards are engaged, the root Scaffold configuration shall enforce 'resizeToAvoidBottomInset: false' and apply custom-calculated view-inset padding dynamically using screen metrics.
*   **Deliverable 2 (Central User Authentication Service):**  
    A client-side security interface integrated with Firebase Authentication to handle secure logins, user registrations, and password recoveries. The system shall employ robust local validation algorithms for text entry fields, including strong password evaluation rules (requiring uppercase characters, numeric digits, and special characters) and email syntax checkers, redirecting authenticated users to the home dashboard.
*   **Deliverable 3 (Local Relational Database & History Tracker):**  
    A local SQLite database database engine managed via custom helper utilities to handle local persistence. The database will define tables structured to save recommendations, storing user identification keys, query types, inputs, results, and timestamp strings. The database helper will implement indexing to accelerate query fetches, support search operations across saved records, count queries, and enable full user-bound deletion controls.
*   **Deliverable 4 (Machine Learning Django API Backend):**  
    A central REST API backend hosted on Django REST Framework loading pre-trained RandomForestClassifier serialization models via Python utilities. To guarantee data ingestion compatibility and prevent key-mapping runtime exceptions, the backend data models and the frontend form input controllers must strictly mirror the typographical parameters of the training datasets, specifically:
    *   'Temparature' (utilizing the typographical 'a' in the second syllable)
    *   'Humidity ' (containing a mandatory trailing space within the parameter string)
    *   'Moisture'
    *   'Soil Type' (restricted to the categorical classes: Sandy, Loamy, Black, Red, Clayey)
    *   'Crop Type' (restricted to the categorical classes: Maize, Sugarcane, Cotton, Tobacco, Paddy, Wheat, Barley)
    *   'Nitrogen'
    *   'Potassium'
    *   'Phosphorous' (spelled with an 'o' before 'u')
*   **Deliverable 5 (AI & Weather Cognitive Advisory Layers):**  
    A backend cognitive integration pipeline connecting to external diagnostic systems:
    *   *Weather Client:* A REST connection to OpenWeatherMap querying latitude ('lat') and longitude ('lon') parameters to extract live temperature, humidity, pressure, and conditions.
    *   *AI Generation Client:* A connection to Google Gemini Version Two Flash passing real-time weather and crop types to generate advice in the following exact format:
        *   💧 WATERING: (Yes/No) - (4-5 words reason)
        *   🌱 FERTILIZER: (Good/Wait) - (4-5 words reason)
        *   🐛 PEST RISK: (Low/Medium/High) - (3-4 words)
        *   ✅ TIP: (one 5-8 word sentence)
    *   *Pesticide Database:* A rule-based lookup database mapping crop names and disease symptoms using fuzzy text search matches for keywords (including blast, brown spot, stem borer, leaf folder, rust, mildew, armyworm, bollworm, whitefly, aphid, leaf miner, fruit borer), mapping specific crop families to generic 'vegetable' treatment logic, and defaulting to a Neem Oil protocol if no direct match is found.
*   **Deliverable 6 (Auditable Blockchain Smart Contract Ledger):**  
    A Web3 RPC gateway integrated into the Django backend to connect with the Sepolia Ethereum testnet. The system will sign and broadcast transaction receipts via the logRecommendation smart contract function, tracking recommendation parameters and raw query JSON inputs. Query functions (such as reading logs by index or checking total counts) will be exposed to the client, while all transactions are wrapped in a non-blocking asynchronous architecture to prevent blockchain mining latency from delaying REST API HTTP responses.

---

### 4. Project Benefits
Describe the expected benefits of the project:
*   **Benefit 1:** Maximized crop yields and minimized fertilizer waste via precise, data-driven soil attribute processing (Nitrogen, Phosphorus, Potassium, pH).
*   **Benefit 2:** Absolute institutional risk mitigation and liability protection through an unalterable, tamper-proof digital ledger tracking all issued advisory data.
*   **Benefit 3:** Rapid adoption within rural demographics due to native multi-language support and high-availability offline capability.

---

### 5. Project Risks & Proactive Mitigations
| Risk Identifier | Risk Description | Engineering Mitigation Strategy |
| :--- | :--- | :--- |
| **Risk 1** | Typographical Alignment between Datasets and Serializers causing key-mapping runtime crashes during parameter processing. | Enforce strict backend serializer schema validation that maps incoming payloads exactly to model properties, matching dataset spellings. |
| **Risk 2** | Volatile rural network signals causing API connection drops in remote regions and preventing database synchronization. | Implement a client-side deterministic fallback engine in the mobile application that executes offline threshold algorithms using local data. |
| **Risk 3** | Third-party API rate limitations or quota exhaustion on live LLM endpoints resulting in advice failure. | Design an automated server-side exception routine to downgrade queries to local rules without UI disruption. |
| **Risk 4** | Ethereum block validation delays causing REST API execution timeouts on the transaction thread. | Route smart contract write operations to background asynchronous workers to keep API response times immediate. |
| **Risk 5** | Authentication Session Expirations and Sync Desynchronization due to sudden network loss in field operations. | Implement secure client-side storage to cache authentication state, combined with local request queue buffers that defer synchronization. |
| **Risk 6** | Local Relational Database Schema Upgrades causing tables conflict or data loss when modifying existing structures. | Enforce strict migration procedures in the local database initializer class, running transaction-safe commands to verify schema updates. |
| **Risk 7** | Long-Term Predictive Model Drift and performance decay due to shifting local climate and soil factors. | Build a modular server framework to support zero-downtime classification model swaps, requiring automated evaluation before staging. |
| **Risk 8** | Generative AI Output Formatting Deviations breaking backend parsers when third-party parameters shift. | Deploy strict regular expression and JSON structure verification layers to intercept and format AI output strings. |

---

### 6. Project Budget
| Core Development Scope | Fiscal Allocation | Resource Responsibility |
| :--- | :--- | :--- |
| Backend Engineering & Data Pipelines | $15,000 | Dr. Elena Rostova |
| Frontend Mobile Development | $12,000 | Tariq Mahmood |
| Cloud Infrastructure & DevOps | $8,000 | Muhammad Omer Siddiqui / Tariq Mahmood |

---

### 7. Project Milestones
| Milestone Identifier | Target Date | Acceptance Criteria |
| :--- | :--- | :--- |
| Milestone 1 - Requirements Architecture & Discovery Sign-off | 07/15/2026 | Requirements architecture will be verified as signed-off, UI design mockups frozen, database schemas finalized, and staging environments configured. |
| Milestone 2 - Core Backend REST API & Predictive Model Implementation Complete | 09/15/2026 | Central backend framework will be verified as active, REST API endpoints deployed, classification model serialization completed, and local endpoint testing validated. |
| Milestone 3 - Frontend UI Integration, Smart Contract Deployment, & Final QA Sign-off | 11/15/2026 | Smart contracts will be deployed to the Sepolia testnet, Flutter views successfully integrated with the REST backend, localization matrices verified, and all automated quality assurance scripts passed. |

---

### 8. Project Team Members
| Role | Name | Enterprise Contact Channels | Scope of Ownership |
| :--- | :--- | :--- | :--- |
| Project Manager & Lead Solution Architect | Muhammad Omer Siddiqui | omer@softwarehouse.com | Project Governance, Milestone Verification, Client Liaison. |
| Full-Stack Backend & Data Engineer | Dr. Elena Rostova | engineering@softwarehouse.com | REST API Construction, Data Serialization, Web3 Integration. |
| Frontend Mobile & QA Specialist | Tariq Mahmood | qa@softwarehouse.com | Flutter UI Development, State Binding, Translation Quality Verification. |

---

### 9. Project Stakeholders
| Target Stakeholder Group | Project Role | Operational Expectations & Requirements |
| :--- | :--- | :--- |
| Project Sponsor | Client Venture Team | Non-technical agricultural business entrepreneur. Expects a fully functional, market-ready MVP delivered within the fixed budget parameters to secure early-stage venture funding. |
| Agricultural Advisory Board | Scientific Review Team | Technical agronomy advisors. Require complete data transparency, accurate model prediction values, and a tamper-proof auditing framework to validate recommendation safety. |

---

### 10. Project Approval
By signing below, the Project Sponsor and the Project Manager formally authorize this Project Charter, establishing the project baseline, timeline constraints, budget allocations, and ISO 21502 compliance boundaries.

*   Project Sponsor Signature: _______________________ Date: 06/22/2026  
*   Project Manager Signature: _______________________ Date: 06/22/2026  
