# Low-Level Design Report: Coupl

**Project Short-Name:** Coupl  
**Course Code:** CS491/2 — Senior Design Project  
**Institution:** Bilkent University, Department of Computer Engineering  
**Date:** February 28, 2022  

**Authors:** Cankat Anday Kadim, Rüzgar Ayan, Ege Türker, Emre Derman, Kamil Kaan Erkan  
**Supervisor:** Cevdet Aykanat  
**Jury Members:** Erhan Dolak, Tağmaç Topal  

---

## Table of Contents
1. [Introduction](#1-introduction)
   - 1.1 [Object Design Trade-offs](#11-object-design-trade-offs)
     - 1.1.1 [Efficiency vs Concurrency](#111-efficiency-vs-concurrency)
     - 1.1.2 [Feasibility vs Extensibility](#112-feasibility-vs-extensibility)
     - 1.1.3 [Scalability vs Efficiency](#113-scalability-vs-efficiency)
   - 1.2 [Interface Documentation Guidelines](#12-interface-documentation-guidelines)
   - 1.3 [Engineering Standards](#13-engineering-standards)
   - 1.4 [Definitions, Acronyms, and Abbreviations](#14-definitions-acronyms-and-abbreviations)
2. [Packages](#2-packages)
   - 2.1 [Client Side](#21-client-side)
     - 2.1.1 [User](#211-user)
     - 2.1.2 [Event Organizer](#212-event-organizer)
   - 2.2 [Server Side](#22-server-side)
3. [Class Interfaces](#3-class-interfaces)
   - 3.1 [Client Side](#31-client-side)
     - 3.1.1 [User](#311-user-1)
     - 3.1.2 [Event Organizer](#312-event-organizer-1)
   - 3.2 [Server Side](#32-server-side-1)
4. [References](#references)

---

## 1. Introduction
Coupl is a mobile application that creates a safe environment for users to meet with new people in-person within a matter of minutes. Event organizers make their events available via the application, and users join events by scanning QR codes provided at these event locations. Potential events include musical concerts, parties, art exhibitions, and more. 

Coupl matches users at the same event based on preferences from the current participant pool, their event history, and prior matches within the application. As a service, Coupl aims to be an innovative alternative to traditional dating and meeting networks. By matching active participants in real-time who possess similar profiles, Coupl facilitates connections rooted in shared interests. Compared to online swipe-based dating apps that rely purely on text chat, this application delivers a dynamic experience focused on immediate in-person meetings.

### 1.1. Object Design Trade-offs
This section examines the architectural object design trade-offs across efficiency, concurrency, feasibility, extensibility, scalability, and usability.

#### 1.1.1. Efficiency vs Concurrency
Coupl’s core operations rely on efficiency and concurrency. When architectural conflicts arise, the requirement for concurrency trumps pure execution efficiency. Concurrency configurations must be engineered for long-term stability without introducing race conditions or system bugs. High execution efficiency is of minimal value if the underlying system cannot sustain stable concurrent session states.

#### 1.1.2. Feasibility vs Extensibility
Initial software versions typically operate as functional proofs-of-concept subject to multiple iterative releases. Because the capacity and data volume expand with each phase to improve user experience, application extensibility is treated as a critical requirement. While system practicality is important, prioritizing extensible structures over static feasibility ensures a sustainable platform over a long operational lifespan.

#### 1.1.3. Scalability vs Efficiency
System scalability is a major objective for the Coupl platform. While reaching a broad consumer base is vital, providing a reliable, responsive, and predictable experience takes precedence. Consequently, where conflicts emerge, localized efficiency is favored to optimize immediate application usability over raw, unconstrained scale.

#### 1.1.4. Admin vs User Usability Focus
* **Admin Perspective:** The administrative front-end requires dense functional capability to manage customer orders, data overrides, and system rules. Because this environment is strictly utilized for structural data modification, the layout focuses on maximum utility over simple learnability.
* **User Perspective:** The consumer client interface focuses primarily on account creation, real-time matching loops, and smooth communication with backend servers. Consequently, instead of wide functional complexity, a highly intuitive, lean, and frictionless user interface is preferred.

### 1.2. Interface Documentation Guidelines
To ensure consistency across this document, class names are singular and declared in `PascalCase`. Variables and method signatures follow standard `camelCase` conventions (e.g., `variableName`, `methodName()`). 

Class interfaces use the following structural documentation layout:

| Element | Specification | Description |
| :--- | :--- | :--- |
| **Class:** | `ClassName` | General class description and core functional context. |
| **Attributes:** | `attributeName: type` | Attribute description and type constraints. |
| **Methods:** | `methodSignature(params): returnType` | Method responsibility, parameters, and return targets. |

### 1.3. Engineering Standards
Unified Modeling Language (UML) guidelines are followed strictly across all class definitions, structural package diagrams, operational scenarios, use case maps, and subsystem compositions. Formal IEEE engineering standards govern project design lifecycle phases.

### 1.4. Definitions, Acronyms, and Abbreviations
* **API:** Application Programming Interface
* **REST:** Representational State Transfer (Architectural web services standard)
* **UI:** User Interface
* **HTTP:** Hypertext Transfer Protocol
* **QR Code:** Quick Response Code

---

## 2. Packages

### 2.1. Client Side

#### 2.1.1. User Client Package
The user client controls consumer interactions and contains the following view controllers and components:
* **UIController:** Handles global screen navigation, routing stacks, and active state transitions.
* **LoginScreen:** Provides an authentication entry portal for existing users.
* **SignupScreen:** Collects personal parameters, preferences, and attributes to establish new consumer records.
* **UpcomingEventsScreen:** Features interactive lists, keyword searching, and categorical filters for future events.
* **HomeScreen:** Launches native camera streams to scan destination QR codes and handle event entry.
* **ProfileScreen:** Manages personal biographies, attributes, matching filters, and multi-media photo arrays.
* **MessagesScreen:** Orchestrates direct text messaging streams, chat record histories, and match chat termination logic.
* **MatchingScreen:** Displays active matching pools, processing choices, skips, and profile score likeness overlays.
* **FoundMatchScreen:** Renders successful matchmaking alerts, physical meeting location targets, and choices to accept or reject matches.
* **EventHomeScreen:** Houses real-time participant hub stats, active match tracking, and post-event rating tools.

#### 2.1.2. Event Organizer Client Package
The event organizer package handles partner interactions and contains:
* **UIController:** Controls layout navigation across administrative view states.
* **LoginScreen:** Authenticates authorized management accounts via phone configurations.
* **OrganizedEventsScreen:** Tracks ongoing, historical, and future scheduled events alongside analytics reporting.
* **EventCreationScreen:** Collects metadata, time structures, location bounds, and partition limits for new event staging.
* **EventLocationsScreen:** Configures physical venue landmarks and spatial map partitions for post-match meetings.

### 2.2. Server Side
The backend architecture is structured around focused server-side microservices:
* **CoupleMatchingManager:** Executes matching calculations on active participant pools utilizing preference matrices and historical match scores.
* **NotificationManager:** Triggers alerts for event timelines, successful matching confirmations, and core profile state modifications.
* **UserManager:** Governs sessions, account lifecycles, permissions, and synchronization tasks between active profiles and storage databases.
* **DatabaseManager:** Handles CRUD cycles, multi-user request execution, REST connection endpoints, and connection management to internal data storage networks.
* **EventManager:** Processes structural event execution, QR code token generation, and real-time user checkout/check-in requests.
* **MessagingManager:** Preserves peer-to-peer message integrity, handling message ingestion, deletion, and historical payload delivery.

---

## 3. Class Interfaces

### 3.1. Client Side

#### 3.1.1. User Client Class Specifications

##### ProfileScreen
* **Description:** Manages the user's editable profile data and photo configurations.
* **Attributes:**
  - `name: String` — User's given first name.
  - `surname: String` — User's family name.
  - `birthDate: Date` — User's birthdate.
  - `phoneNumber: String` — Unique phone number identifier.
  - `gender: String` — Self-identified gender.
  - `preferredGender: String` — Target preference matching filter.
  - `photos: Image[]` — Active multi-media asset portfolio.
  - `hobbies: String[]` — Catalog of personal interest tags.
* **Methods:**
  - `changeInformation(newUserInformation: User): boolean` — Modifies editable fields on a user's record.
  - `addPhoto(newPhoto: Image): boolean` — Appends a fresh picture to the user's asset stack.
  - `deletePhoto(deletePhotoIndex: int): boolean` — Purges an asset from the portfolio by array index.

##### SignupScreen
* **Description:** Entry form capturing account creation variables.
* **Attributes:**
  - `name: String`, `surname: String`, `birthDate: Date`, `phoneNumber: String`, `password: String`, `gender: String`, `preferredGender: String`
* **Methods:**
  - `signup(name: String, surname: String, birthDate: Date, phoneNumber: String, password: String, gender: String, preferredGender: String): boolean` — Validates information and registers a new account with the server.
  - `showErrors(): JSX.Element` — Visualizes form validation errors to the end-user.

##### LoginScreen
* **Description:** User entry credentials dashboard.
* **Attributes:**
  - `phoneNumber: String`, `password: String`
* **Methods:**
  - `login(phoneNumber: String, password: String): void` — Submits credential payloads. Routes successful sessions to `HomeScreen`.

##### HomeScreen
* **Description:** Entry point handling QR event ingestion.
* **Methods:**
  - `openQRScanner(): int` — Interacts with camera hardware to process visual QR matrix assets.
  - `joinEvent(eventID: int, phoneNumber: String): boolean` — Submits the scanned token to register the client inside the active event participant pool.

##### UpcomingEventsScreen
* **Description:** Discoverable events directory.
* **Attributes:**
  - `events: Event[]` — Cached array of upcoming destination records.
* **Methods:**
  - `filterEvents(date: Date?, location: Location?, eventType: EventType?, tag: Tag): Event[]` — Narrows events matching specified conditions.
  - `openEventDetails(eventID: int): Event` — Navigates to target event informational panes.
  - `searchByName(name: String): EventInfo[]` — Searches the database via plain-text keywords.

##### EventHomeScreen
* **Description:** In-event operational hub.
* **Attributes:**
  - `eventInfo: Event`, `likedUsers: int`, `match: User`
* **Methods:**
  - `leaveEvent(eventID: int): void` — Retracts the active user from matching consideration.
  - `startMatching(): User[]` — Requests an ordered list of viable candidates from the matching server.
  - `seeCurrentMatch(userID: int): void` — Opens operational views for an active pair.
  - `rateEvent(eventID: int, rating: int, comment: String): void` — Logs client-side event review metadata.

##### MessagesScreen
* **Description:** Active chat routing controller.
* **Attributes:**
  - `chatRecords: ChatRecord[]` — Persistent text history list.
* **Methods:**
  - `openChatBox(userID: int): ChatRecord` — Spawns direct private messaging windows.
  - `sendMessage(userID: int, message: String): void` — Dispatches message payloads.
  - `terminateChat(userID: int): void` — Concludes active session and isolates message streams.
  - `startChatWithMatch(userID: int): ChatRecord` — Initializes matching chat connection parameters.

##### MatchingScreen
* **Description:** Interactive evaluation view.
* **Attributes:**
  - `abbreviatedName: String` (e.g., "Rüzgar Ayan" → "Rüzgar A."), `age: int`, `photos: Image[]`, `hobbies: String[]`, `commonEventTypes: EventType[]`, `matchingScore: int`
* **Methods:**
  - `like(userID: int): boolean` — Expresses programmatic interest. If reciprocal, immediately transitions the client to `FoundMatchScreen`.
  - `skip(userID: int): void` — Declines candidate and fetches the next queue record.

##### FoundMatchScreen
* **Description:** Successful matchmaking outcome overlay.
* **Attributes:** Same profile metadata as `MatchingScreen` with addition of: `meetingLocation: Location`
* **Methods:**
  - `chooseMeetingLocation(location: Location): void` — Identifies a coordinate destination inside the designated venue partition.
  - `acceptMatch(): void` — Finalizes meeting intent and routes to `EventHomeScreen`.
  - `removeMatch(): void` — Cancels connection and returns the user to the active `MatchingScreen` loop.

##### UIController
* **Description:** Orchestrates navigation actions.
* **Attributes:** `currentScreen: String`, `loginInformation: User`
* **Methods:**
  - `changeCurrentScreen(screenName: String, loginInformation: User): JSX.Element` — Re-renders root screen windows matching target strings.

---

#### 3.1.2. Event Organizer Class Specifications

##### OrganizedEventsScreen
* **Attributes:** `organizedEvents: Event[]`
* **Methods:**
  - `cancelEvent(eventID: int): void` — Marks an item as cancelled and fires cancellation updates to registered attendees.
  - `updateEventDetails(eventID: int, updatedEvent: Event): void` — Re-writes description metadata records.
  - `viewEventDetails(eventID: int): Event` — Queries deep configuration maps.
  - `viewEventStatistics(eventID: int): EventStatistics` — Collects aggregate metrics like match totals and attendance curves.
  - `promoteEvent(eventID: int): void` — Bumps event visibility to the top of the consumer discoverability feed.

##### EventCreationScreen
* **Attributes:** `eventName: String`, `startTime: Date`, `endTime: Date`, `eventPlace: Location`, `chosenPartition: Partition`, `tag: Tag[]`, `eventPhoto: String`
* **Methods:**
  - `submitForConfirmation(eventName: String, startDate: Date, endDate: Date, eventPlace: Location, chosenPartition: Partition, tag: Tag[], eventPhoto: String): void` — Registers a newly scheduled event entry.

##### EventLocationsScreen
* **Attributes:** `eventLocations: Location[]`
* **Methods:**
  - `addNewEventLocation(location: Location): void` — Creates a valid architectural destination record.
  - `addEventLocationPartition(partition: Partition): void` — Implements geographical venue sub-divisions for programmatic meeting assignment.
  - `viewEventsAtLocation(location: Location): Event[]` — Lists past and upcoming event calendars for a designated location.

---

### 3.2. Server Side Model Interfaces (Django Architecture)

#### User
* **Description:** Core model inheriting from Django’s default authentication base structure.
* **Attributes:** `username: String`, `email: String`, `password: String`

#### Profile
* **Description:** Represents extended consumer profile variables bound via a structural `OneToOneField` link to the standard `User` model.
* **Attributes:** `name: String`, `surname: String`, `phone_number: String`, `date_of_birth: Date`, `description: String`, `gender: String`, `preference: String`, `profile_picture: String`
* **Methods:**
  - `updateProfile(**profile_data): bool` — Mutates profile field models cleanly.
  - `updateProfilePicture(picture_link: string): bool` — Overwrites file storage reference pointers.
  - `changePassword(oldPassword: string, newPassword: string): bool` — Validates credentials and writes fresh password hashes.

#### Event
* **Description:** Core entity governing event states.
* **Attributes:** `event_name: String`, `event_description: String`, `event_tags: Tag[]`, `event_start_time: Date`, `event_finish_time: Date`, `event_creator: User`, `event_location: Location`, `event_attendees: User[]`
* **Methods:**
  - `updateEventDetails(**details): bool` — Overwrites primary event properties.
  - `updateTags(**tags): bool` — Alters categorization tags.

#### Organizer
* **Description:** Multi-tenant profile layer extending base users for professional roles.
* **Attributes:** `user: User` (Inheritance model wrapper), `organizer_phone: String`, `organizer_contact: String`, `organizer_rating: double`
* **Methods:**
  - `updateRating(rating: int): double` — Re-computes dynamic organizer scores using rolling calculations.
  - `updateOrganizerPhone(phone_number: String): Organizer` — Edits primary callback phone values.
  - `updateOrganizerContact(contact: String): Organizer` — Edits additional notification or support channels.

#### Comment
* **Description:** Houses user reviews for past event interactions.
* **Attributes:** `commenter: User`, `event: Event`, `rating: int`, `comment_text: String`

#### Match
* **Description:** Tracks successful pairing outcomes inside an active event partition.
* **Attributes:** `user1: User`, `user2: User`, `event: Event`

#### Location
* **Description:** Stores geography records.
* **Attributes:** `name: String`, `description: String`, `address: String`
* **Methods:**
  - `updateName(location_name: String): Location`
  - `updateDescription(location_description: String): Location`
  - `updateLocation(location_address: String): Location`

#### Ticket
* **Description:** Governance entity managing user reporting and platform safety parameters.
* **Attributes:** `reporter: User`, `reported: User`, `description: String`

#### Tag
* **Description:** Simple label categorization entity.
* **Attributes:** `tag_name: String`, `tag_description: String`

---

## 4. References
* [1] Bruegge, B. & Dutoit, A. H. (2004). *Object-Oriented Software Engineering, Using UML, Patterns, and Java, 2nd Edition*. Prentice-Hall. ISBN: 0-13-047110-0.
