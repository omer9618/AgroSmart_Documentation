# AgroSmart Google Stitch UI/UX Prompts (Modern Minimalist Edition)

This document provides a set of highly structured, professional Google Stitch prompts for each screen in the **AgroSmart** mobile application. These prompts have been fully redesigned from scratch to follow a premium **Modern Minimalist** design aesthetic, emphasizing clean layouts, generous whitespace, strict typographic hierarchy, and single-accent focal points.

---

## 🎨 Global Design System & Brand Identity
To ensure absolute visual cohesion across all generated screens, Google Stitch prompts inherit the following minimalist guidelines:
*   **Color Palette:** Monochromatic bases. Pure White (`#FFFFFF`) and warm off-white (`#F9F9FB`) for clean backgrounds. Slate grey (`#71717A`) for borders and description text. Dark graphite (`#18181B`) for primary headings. Use a single vibrant organic emerald green (`#10B981`) *very sparingly* as the sole accent color for active navigation states, success indicators, and primary call-to-actions.
*   **Visual Style:** Completely flat layout. Zero gradients, zero glassmorphic transparency, and zero heavy multi-colored cards. Container borders are thin and clean (`1px` solid, `#E4E4E7` or `#E5E7EB`). Flat card structures have zero elevation or a faint, subtle layout shadow. Corners must be tight and sharp with a maximum border-radius of `8px` to `12px`.
*   **Typography:** Modern, structural sans-serif (*Inter* or *SF Pro*). Strict size hierarchy: large, bold, black headings for primary context, and small, high-density metadata fields in muted gray.
*   **Whitespace:** Generous spacing (`24px` to `32px` block padding) between content blocks to create a highly legible, premium editorial feel.
*   **Demographic Focus:** High readability, clean high-contrast elements, and highly legible text fields to assist rural farmers with differing digital literacy without using cluttered layouts.

---

### 1. Splash Screen
**Inspiration:** *Linear & Apple* (monochromatic, high-contrast, pure minimalism, crisp lines)

```text
Create a splash screen for a modern agricultural mobile app called "AgroSmart". The design must follow a strict modern minimalist aesthetic.

- BACKGROUND: Solid, clean off-white (#F9F9FB) with zero gradients, patterns, or image overlays.
- LOGO: Centered on the screen. A thin, single-line-art vector emblem of a plant seedling emerging from a sharp vertical grid line, drawn in graphite gray (#18181B). No gradients, glow, or 3D effects.
- TITLE: Located below the logo, display the title "AgroSmart" in clean, bold, high-contrast black typography (using the Inter font). Keep the letters sharp with normal letter-spacing, without shadow or glow effects.
- SUBTITLE: Below the title, show "Intelligent Crop Advisory" in muted slate gray (#71717A) with regular font weight and small typography.
- LOADING STATUS: Near the bottom, a single, ultra-thin horizontal line (2px height, #E4E4E7 background) acting as a loading bar, with the left portion filled with a solid, vibrant emerald green (#10B981) indicating progress. Above it, show "Connecting..." in small, muted gray text.
- FOOTER: Pinned to the very bottom, "v1.0.0" in tiny, low-opacity monospace text.
```

---

### 2. Login & Registration Screen
**Inspiration:** *Vercel & Stripe* (flat layouts, thin borders, inline active states)

```text
Design a hybrid Login and Sign-Up screen for the "AgroSmart" app following a modern minimalist design. Do not use video backgrounds, background images, or glassmorphic transparency.

- STRUCTURE: The entire screen uses a flat, neutral light gray background (#F4F4F5).
- LANGUAGE TOGGLE: In the top-right corner, place a small, flat text button with a thin border (1px solid #E4E4E7, border-radius: 6px) showing "EN | UR" to switch languages.
- FORM CONTAINER: A flat white card container centered on the screen with a thin border (1px solid #E4E4E7) and tight corners (border-radius: 8px). No shadow or background gradient.
- CONTENT INSIDE CARD:
  - Header: A bold title "Welcome to AgroSmart" (or "Create Account" depending on mode) in dark graphite (#18181B) with a small, flat leaf icon next to it.
  - INPUT FIELDS: Flat text inputs with a thin light-gray border (1px solid #E4E4E7, border-radius: 8px). On focus, the border turns sharp dark-gray (#18181B). If validation fails, the border turns thin red. Placeholders are in light gray (#A1A1AA). Prefix icons (person, email, lock) are drawn in thin dark gray outline style.
  - PASSWORD FIELD: Includes a simple text-based button "Show" / "Hide" inside the right edge of the input. When in Sign-Up mode, show a small, clean list of validation checks below the input, colored green (#10B981) when valid, and muted gray when invalid.
  - PRIMARY ACTION: A solid emerald green button (#10B981) with bold white text, sharp corners (border-radius: 8px), and zero gradient. Text: "Login" or "Register".
  - TOGGLE LINK: At the bottom, a flat text button "Don't have an account? Sign Up" in slate gray.
```

---

### 3. Home Screen / Main Dashboard
**Inspiration:** *Linear Dashboard & Airbnb* (editorial whitespace, high contrast, clean list grids)

```text
Design a clean, modern minimalist dashboard screen for the "AgroSmart" app tailored to farmers. 

- APP BAR: Pinned white header with a thin bottom border (1px solid #E4E4E7). Features the app title "AgroSmart" in clean black text, a flat language switch button ("EN/UR"), and a simple outline History icon on the right with a small, flat green dot if there are new diagnostics.
- HEADER WELCOME: Below the app bar, a clean greeting block with generous vertical padding: "Good morning," followed by the farmer's name in bold black text. No avatars or colored backgrounds.
- HERO STATS ROW: A flat row of key dashboard statistics separated by thin vertical gray lines:
  - "Recent Queries" showing "5 saved"
  - "Offline Mode" showing "Ready (Local Sync)"
- SERVICE TILES: A vertical stack or 2x2 grid of flat, white cards with thin borders (1px solid #E4E4E7, border-radius: 8px). No background images or gradients. Each card features:
  - A small, clean outline-style green icon in the corner.
  - A short bold title (e.g., "Crop Recommendation", "Fertilizer Advisory", "Pesticide Diagnosis", "Weather Smart Tips").
  - A single-line description in muted gray text (#71717A).
  - A tiny flat arrow pointing right.
- BOTTOM NAVIGATION: Pinned bottom bar with a white background and a thin top border (1px solid #E4E4E7). Contains simple outline icons for Home, History, and Settings. The active tab is highlighted in emerald green (#10B981) with a thin green horizontal line above the active icon.
```

---

### 4. Crop Input (Soil Data Diagnosis) Screen
**Inspiration:** *Tailwind UI Forms & Apple Health* (dense but clean inputs, flat inline warnings)

```text
Create a minimalist form screen for "Crop Recommendation" soil variable input in the "AgroSmart" app.

- APP BAR: Solid white background with a thin bottom border (1px solid #E4E4E7), back arrow, screen title "Crop Soil Input" in black, and flat language toggle.
- SOIL GUIDE BANNER: A flat, light green-tinted info card at the top (#F0FDF4 background, 1px solid border #DCFCE7, border-radius: 8px). It lists the typical, safe agronomic boundaries: "N: 0-140, P: 0-145, K: 0-205, pH: 0-14, Temp: 0-50°C, Humidity: 0-100%, Rainfall: 0-300mm" in clean green text (#15803D).
- INPUT FIELDS: A clean vertical list of 7 input fields: Nitrogen (N), Phosphorus (P), Potassium (K), Soil pH, Temperature (°C), Humidity (%), and Rainfall (mm).
  - Each input field has a bold title label, a thin border (1px solid #E4E4E7, border-radius: 8px), and a small unit indicator text (e.g. "ppm", "pH", "°C", "%", "mm") on the right.
  - A small question mark icon next to each label triggers a simple flat inline tip box explaining the role of that nutrient. No sliders, overlays, or gradients.
- SUBMIT ACTION: A flat, solid green button (#10B981) at the bottom: "Get Crop Recommendation". Shows a minimal spinning line indicator when loading.
```

---

### 5. Fertilizer Input Screen
**Inspiration:** *Figma UI & Stripe Dashboard* (segmented text controls, nested select inputs)

```text
Design the "Fertilizer Advisory" input screen for the "AgroSmart" app using modern minimalist style.

- APP BAR: Solid white background with a thin bottom border (1px solid #E4E4E7), back arrow, title "Fertilizer Input", and language selector.
- PARAMETER GUIDE: A simple, thin-bordered white box containing bulleted typical values for soil parameters (Temp: 0-50°C, Humidity: 0-100%, Moisture: 0-100%, N, P, K).
- SOIL TYPE SELECTOR: A row of flat, text-only chips (Sandy, Loamy, Black, Red, Clayey) with off-white backgrounds (#F4F4F5) and thin borders. Tapping a chip changes its border to solid dark-gray (#18181B) and text to black. No images or icons.
- CROP SELECTOR: A simple dropdown field with a thin border containing maize, sugarcane, cotton, tobacco, paddy, wheat, and barley.
- NUMERIC INPUTS: Simple stacked input fields with a thin border (1px solid #E4E4E7) and light-gray placeholders for Temperature (°C), Humidity (%), Moisture (%), Nitrogen (N), Potassium (K), and Phosphorus (P).
- SUBMIT ACTION: A full-width, flat, solid green button (#10B981) at the bottom labeled "Get Fertilizer Advisory".
```

---

### 6. Pesticide Symptom Lookup Screen
**Inspiration:** *Linear Search & Apple Spotlight* (inline chips, auto-filtering lists)

```text
Design a "Pesticide Diagnosis & Symptom Lookup" interface for the "AgroSmart" app following modern minimalist guidelines.

- APP BAR: Clean white background, thin bottom border, back button, title "Pest & Disease Diagnosis".
- SYSTEM DIAGNOSIS GUIDE: A flat, light-gray box with a thin border listing common crop symptoms in bullet points (e.g. brown spots, mildew, insect damage).
- FORM INPUTS:
  - "Select Crop": A clean text field with a dropdown menu displaying matching suggestions as the user types.
  - "Describe Symptoms": A spacious text field (3-4 lines) with a thin border (1px solid #E4E4E7, border-radius: 8px) and placeholder text "Describe the crop symptoms...".
- QUICK SYMPTOM CHIPS: Below the text field, a series of small, flat text chips: "Brown Spots", "Leaf Holes", "White Powder", "Tiny Bugs", "Fruit Holes". Tapping a chip inserts the text.
- SUBMIT ACTION: A flat, solid green button (#10B981) at the bottom labeled "Get Treatment Recommendation".
```

---

### 7. Weather & AI Advisory Screen
**Inspiration:** *Simple Weather & Yahoo Finance* (clean layout, text coordinates inputs)

```text
Design a "Weather-Based Farming Tips" screen that displays real-time weather metrics and localized agricultural advice using a modern minimalist style. Do not use color gradients based on weather conditions.

- HEADER LOCATION SELECTOR:
  - A clean segmented control (tab switcher) at the top: "GPS Location" and "Enter Coordinates".
  - GPS PANELS: Displays coordinates "Islamabad (33.6844, 73.0479)" inside a flat card with a thin border, featuring a small "Refresh" text button.
  - MANUAL PANELS: Two clean, side-by-side text input fields for Latitude and Longitude. Below them, a row of text link shortcuts for cities: "Islamabad", "Lahore", "Karachi", "Multan".
- CROP TYPE FIELD: A clean text field labeled "Target Crop (Optional)".
- SUBMIT ACTION: A flat, solid green button (#10B981) at the bottom: "Get Weather Farming Tips".
- LAYOUT: Solid off-white background. All weather metrics are displayed in high-contrast text and thin vector boxes.
```

---

### 8. Result & Diagnostic Report Screen
**Inspiration:** *Linear Issue Detail & Medical Lab Reports* (structural hierarchy, high density tabular outputs)

```text
Create a multi-purpose "Diagnostic Result Screen" for the "AgroSmart" app following a modern minimalist design. 

- APP BAR: Clean white background, back button, title of the analysis.
- HERO RESULT CARD:
  - A flat white card with a thick green left border (4px solid #10B981) and thin gray borders on the other three sides.
  - Small, uppercase label at the top: "RECOMMENDED ACTION" in slate gray (#71717A).
  - Main result text in large, bold black typography (32px, e.g., "Crop: Rice", "Use: Urea", "Apply: Neem Oil").
- ANALYSIS DETAILS TABLE:
  - A clean data table with thin horizontal divider lines:
    - If Crop/Fertilizer: Columns for "Nutrient", "Your Input", and "Optimal Range".
    - If Pesticide: Clean text blocks for "Pesticide Name", "Dosage", "Application Method", and "Frequency".
    - If Weather: Simple bulleted AI recommendations organized under headings: "Watering", "Fertilizer", "Pest Risk", and "Today's Tip".
- BLOCKCHAIN VERIFICATION:
  - A flat light-gray box (#F4F4F5) at the bottom with a dashed border. Displays "Security Audit Receipt: Sepolia Ethereum Network". Includes a monospace transaction hash and a link button "Verify on Etherscan".
- BOTTOM BUTTONS:
  - A row of two flat buttons: "Try Another Query" (white background, thin border, dark text) and "Save Record" (solid green background, white text).
```

---

### 9. Historical Logs / Audit Registry Screen
**Inspiration:** *Github Commits List & Revolut* (clean list layout, flat tags, minimal action sheets)

```text
Design the "Historical Diagnostics Registry" screen for the "AgroSmart" app using a modern minimalist style.

- APP BAR: Pinned white header with a thin bottom border (1px solid #E4E4E7), back button, title "Diagnostic History", and a "Clear All" text button.
- CATEGORICAL FILTER CHIPS: A horizontal scrolling row of simple text chips: "All", "Crops", "Fertilizers", "Pesticides", "Weather". Selected chips use a solid black background and white text. Unselected chips use an off-white background with a thin gray border.
- HISTORICAL LIST:
  - A stack of list items separated by thin horizontal divider lines (1px solid #E4E4E7).
  - Each item displays:
    - A simple label tag indicating the type (e.g. "[Crop]" or "[Fertilizer]").
    - A bold title (e.g., "Wheat Recommendation") and a small, muted gray timestamp (e.g., "2 hours ago").
    - A tiny arrow icon on the far right.
- SWIPE ACTION: Swiping a tile to the left reveals a flat red bar containing the word "Delete".
- DETAIL DRAWER / MODAL:
  - Tapping a log item opens a clean modal sheet from the bottom.
  - Shows two sections: "Submitted Inputs" and "System Output" in high-contrast text on flat light-gray backgrounds.
  - Features two outline buttons: "Copy Output" and "Delete".
```
