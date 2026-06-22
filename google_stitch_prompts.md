# AgroSmart Google Stitch UI/UX Prompts

This document provides a set of highly structured, professional Google Stitch prompts for each screen in the **AgroSmart** mobile application. These prompts are designed using the **"Zoom-Out-Zoom-In"** framework to help Google Stitch (or similar tools like v0.dev) generate premium, visually stunning, and highly functional agricultural interfaces.

---

## 🎨 Global Design System & Brand Identity
To ensure consistency across all generated screens, Google Stitch prompts should inherit the following visual guidelines:
*   **Color Palette:** Sleep Forest Green (`#1B5E20`), Leaf Emerald (`#2E7D32`), Mint Green (`#A5D6A7`), Warm Sand (`#F5F5DC`), and Golden Sand (`#FFD54F`) for accents.
*   **Visual Style:** Glassmorphism overlay panels (frost transparency, border highlight, shadow depth), curved container corners (`border-radius: 20px`), clean micro-shadows, and high contrast text.
*   **Typography:** Modern typography using *Montserrat* or *Outfit* for headings, and *Inter* or *Roboto* for high-legibility body content.
*   **Demographic Focus:** High visual clarity (prominent visual icons, large tap targets, intuitive layout) to support rural farmers with varying digital literacy.

---

### 1. Splash Screen
**Inspiration:** *Headspace & Duolingo* (calming, playful, sleek transition loaders)

```text
Create a splash screen for a modern agricultural mobile app called "AgroSmart". The design should feel premium, sleek, and immediately welcoming. 

- BACKGROUND: Use a beautiful, smooth gradient starting from deep forest green (#1B5E20) at the top-left, blending into a vibrant leaf emerald green (#2E7D32) and soft mint (#A5D6A7) at the bottom-right. Incorporate a subtle, semi-transparent organic vector pattern of leaf veins or soil topology lines in the background.
- LOGO: Centered on the screen. A glowing, floating circular emblem with a minimalist white outline of a plant leaf merging with a futuristic digital circuit/sensor icon.
- TITLE: Below the logo, display the title "AgroSmart" in bold, elegant typography (Montserrat font) in bright white, with wide letter spacing (2px) and a soft drop shadow.
- SUBTITLE: Below the title, show "Intelligent Crop Advisory System" in a glassmorphic capsule overlay with white-70% text.
- LOADING STATUS: Near the bottom, a clean, thin horizontal loading progress bar (100% border-radius, pure white) indicating "Checking authentication..." with a pulsing 3-dot micro-animation.
- FOOTER: Pinned at the very bottom, "Version 1.0.0 | Spring 2026" in tiny, low-opacity white text.
```

---

### 2. Login & Registration Screen
**Inspiration:** *Spotify & Airbnb* (immersive backgrounds, glassmorphic card forms, fluid toggles)

```text
Design a hybrid Login and Sign-Up screen for the "AgroSmart" app. The design must handle a looping background video of green wheat fields swaying under a sunny sky.

- STRUCTURE: Enable a dark, semi-transparent overlay gradient (gradient from black-40% at the top to black-80% at the bottom) over the background to keep the forms legible. 
- LANGUAGE TOGGLE: In the top-right corner, place a small floating button using a glassmorphic capsule design (border-radius: 30) featuring a globe icon and showing "🇬🇧 EN | 🇵🇰 اردو" to switch languages instantly.
- FORM CONTAINER: A large, centered glassmorphic card (frosted background, white border with 30% opacity, rounded corners 30px) that hovers elegantly.
- CONTENT INSIDE CARD:
  - An agricultural icon (green leaf/sprout) in a circular overlay.
  - A clean title: "Welcome to AgroSmart" (or "Create Account" depending on mode).
  - INPUT FIELDS: Transparent inputs with white outlines (1.5px thickness). Border turns solid white on focus, and soft red on validation error. Prefix icons (person, email, lock) are white-90%.
  - PASSWORD FIELD: Includes a toggle icon (eye/eye-off) to show/hide the password. When in Sign-Up mode, show a micro-checklist of strong password rules (e.g., "8+ characters", "1 uppercase", "1 number", "1 special char") that light up in mint green when met.
  - BUTTON: A prominent, solid green button (#2E7D32) with a bold white text "Login" / "Register".
  - TOGGLE LINK: At the bottom, a text button "Don't have an account? Sign Up" to transition screens.
- MOBILE FRIENDLY: Do not resize the background video when the virtual keyboard opens.
```

---

### 3. Home Screen / Main Dashboard
**Inspiration:** *Apple Health & Robinhood* (visual grids, card summary widgets, personalized headers)

```text
Design a gorgeous, high-performance dashboard screen for the "AgroSmart" app tailored to farmers.

- HEADER SYSTEM:
  - Top app bar with a gradient background (deep green to light emerald). Includes the app title, a floating language switcher capsule, and a History icon showing a small red badge containing the count of saved diagnostics.
  - Below, a welcome banner with a profile avatar: "Welcome back," and the farmer's name in bold white.
- HERO BANNER:
  - A swipeable visual carousel or card depicting "Smart Farming: AI-Powered Agricultural Insights". Background uses a premium organic photo of a healthy crop field with a glassmorphic dark-green overlay text box.
- STATS WIDGETS:
  - A horizontal row displaying two statistics cards: "Recent Queries (5)" with a clock icon, and "Offline Mode (Sync Ready)" in soft blue showing that data is stored locally.
- QUICK ACTIONS / MENU CARDS:
  - Create a 2x2 grid or a vertical list of large cards for the core services:
    1. "Crop Recommendation": Input soil metrics to discover the best crops. Icon: green leaf. BG image: wheat fields.
    2. "Fertilizer Advisory": Calculate soil nutrients. Icon: test tube. BG image: modern soil testing.
    3. "Pesticide Diagnosis": Scan/describe crop symptoms. Icon: ladybug. BG image: leaf diagnosis.
    4. "Weather Smart Tips": Real-time AI advisory. Icon: sun and rain. BG image: misty hills.
  - Each service card must feature a high-quality relevant image, a semi-transparent dark overlay, a clean white header, a short subtext description, and a round arrow-forward icon in the corner.
- NAVIGATION: Pinned bottom navigation bar with icons for Home, History, and Settings.
```

---

### 4. Crop Input (Soil Data Diagnosis) Screen
**Inspiration:** *Yara FarmCare & Clean Tech Dashboards* (interactive slider inputs, guidance overlays)

```text
Create a form screen for "Crop Recommendation" soil variable input in the "AgroSmart" app. 

- APP BAR: Clean green background, back arrow, title "Soil Crop Diagnosis", and language switcher toggle.
- SOIL DATA GUIDE (INFO CARD):
  - A sticky banner at the top in soft mint green (#E8F5E9) with a green border and info icon. It lists the typical, safe agronomic boundaries: "N: 0-140, P: 0-145, K: 0-205, pH: 0-14, Temp: 0-50°C, Humidity: 0-100%, Rainfall: 0-300mm".
- INPUT FORM:
  - 7 input fields for: Nitrogen (N), Phosphorus (P), Potassium (K), Soil pH, Temperature (°C), Humidity (%), and Rainfall (mm).
  - INPUT WIDGETS: Each input field features a clear labeled title, numeric keypad trigger, prefix icon (e.g. droplet, thermometer, science beaker), and a small info bubble button. Tapping the bubble triggers a floating tooltip explaining the role of that nutrient.
- OPTIMIZED INTERACTION: Instead of raw textboxes, the key values (like pH or Temperature) can also be tweaked using horizontal range sliders, with colored zones indicating "low", "optimal", and "high" ranges.
- SUBMIT ACTION: A sticky, floating bottom button "Get Crop Recommendation" that lights up in solid emerald when the form is valid, showing a spinning green wheel when executing API inference.
```

---

### 5. Fertilizer Input Screen
**Inspiration:** *John Deere Operations Center* (hybrid select grids, agricultural parameter inputs)

```text
Design the "Fertilizer Advisory" input screen for the "AgroSmart" app.

- APP BAR: Green app bar with a back arrow, screen title "Fertilizer Predictor", and English/Urdu switcher.
- NUTRIENT ADVISORY PANEL:
  - An expandable info box at the top labeled "Fertilizer Soil Guide" with a detailed card summarizing typical values for Temperature, Humidity, Moisture, N, P, and K.
- DROPDOWN SELECTORS:
  - "Soil Type": A horizontal scrollable list of visual card chips with icons representing Sandy, Loamy, Black, Red, and Clayey soils. Tapping a chip highlights it in emerald green with a checkmark.
  - "Crop Type": A dropdown or grid selector of primary crops (Maize, Sugarcane, Cotton, Tobacco, Paddy, Wheat, Barley) with miniature crop icons.
- NUMERIC PARAMETERS:
  - Vertical list of text fields with rounded borders (10px) and clean icons for:
    - Temperature (°C)
    - Humidity (%)
    - Moisture (%)
    - Nitrogen (N)
    - Potassium (K)
    - Phosphorous (P)
- CALL TO ACTION: A full-width, heavy-set green button at the bottom: "Get Fertilizer Mixture". When processing, the button changes to a progress spinner with text "Calculating optimal mix...".
```

---

### 6. Pesticide Symptom Lookup Screen
**Inspiration:** *Plantix & Apple Visual Search* (fuzzy-search autocomplete, tap-symptom cards)

```text
Design a "Pesticide Diagnosis & Symptom Lookup" interface for the "AgroSmart" app.

- HEADER: App bar with back button, screen title "Pest & Disease Diagnosis", and Urdu translation trigger.
- SYSTEM DIAGNOSIS GUIDE: A card at the top displaying "Pest Symptom Quick Guide" with visual indicators of common plant issues (e.g., "Brown spots on leaves", "White powdery mildew", "Insect bites").
- FORM INPUTS:
  - "Select Crop": An autocomplete text field with suggestions (rice, wheat, maize, cotton, sugarcane, etc.) that filters list options as the farmer types. Includes a leaf icon.
  - "Describe Symptoms": A spacious text field (at least 3-4 lines tall) with a bug icon, placeholder text "Describe the problem (e.g., leaves have brown spots with gray centers)".
- QUICK CHIPS SECTION:
  - Below the symptom box, display a series of horizontal tap-chips for common symptoms so farmers don't have to type long descriptions: "Brown Spots 🌾", "Leaf Holes 🐛", "White Powder ❄️", "Tiny Bugs 🐜", "Fruit Holes 🍎". Tapping a chip automatically populates the text field.
- BUTTON: A wide, high-contrast action button "Get Treatment Recommendation" styled with a safety-first shield icon.
```

---

### 7. Weather & AI Advisory Screen
**Inspiration:** *Yahoo Weather & Carrot Weather* (dynamic weather cards, conversational AI panels)

```text
Design a "Weather-Based Farming Tips" screen that displays real-time weather metrics and localized agricultural advice.

- LOCATION SELECTOR:
  - Toggle chip bar at the top: "Use GPS Location" vs "Enter Coordinates Manually".
  - GPS CARD: When active, shows a card with a blinking satellite dish indicator and coordinates "📍 Islamabad (33.6844, 73.0479)". Features a large "Refresh GPS Location" button.
  - MANUAL CARD: Features two adjacent text fields for Latitude and Longitude. Below the inputs, display a row of quick-select capsule buttons for cities: "Islamabad", "Lahore", "Karachi", "Multan".
- CROP FIELD: An optional text input field labeled "Target Crop (Optional)" to tailor the weather advice.
- CTA: A prominent button at the bottom "Get Weather Farming Tips".
- LAYOUT STYLE: Rich, modern styling with glassmorphism overlays and background gradients that change according to the local weather condition (sunny = warm amber gradient, rainy = misty blue gradient).
```

---

### 8. Result & Diagnostic Report Screen
**Inspiration:** *Duolingo (Celebration screens) & High-End Medical Labs* (success circles, structured tables, blockchain validation receipts)

```text
Create a multi-purpose "Diagnostic Result Screen" for the "AgroSmart" app. It displays the outcome of crop, fertilizer, pesticide, or weather advice.

- TOP ACTION BAR: Green app bar with a back button, the title of the analysis, and a history shortcut button.
- HERO RESULT CARD:
  - A elevated card with a dark-green gradient background (#1B5E20 to #2E7D32).
  - Inside, a large white circular tick checkmark animation.
  - Large bold white heading: "RECOMMENDED ACTION"
  - Main result text in giant typography (28px) with a glowing shadow (e.g., "Recommended Crop: Rice", "Use Fertilizer: Urea", "Apply: Neem Oil").
- ANALYSIS DETAILS ACCORDION:
  - A white card displaying specific details under an info header:
    - If Crop/Fertilizer: Shows a comparison table of "Inputs Provided" (Nitrogen, Phosphorus, pH, etc.) vs the system's target range.
    - If Pesticide: Shows a red-shaded box summarizing "Pesticide Name", "Dosage (e.g., 5ml per liter)", "Application Method (Foliar spray)", and "Frequency (Every 7 days)".
    - If Weather: Shows weather parameters (temp, humidity, wind) and a green-shaded custom text card containing the AI advisory sections: 💧 WATERING, 🌱 FERTILIZER, 🐛 PEST RISK, and ✅ TODAY'S TIP.
- BLOCKCHAIN VERIFICATION TICKET:
  - A specialized glassmorphism ticket at the bottom with a dashed-line divider. Displays "Security Audit Receipt: Sepolia Ethereum Network". Includes transaction status "Synchronized" in mint green, the Ethereum logo, and a direct hyperlink "Verify on Sepolia Etherscan".
- BOTTOM BUTTONS:
  - Two adjacent buttons: "Try Another Query" (grey, outline style) and "Save Record" (solid green, with checkmark).
```

---

### 9. Historical Logs / Audit Registry Screen
**Inspiration:** *Revolut & Google Keep* (swipe-to-delete tiles, categorical filter chips, log drawers)

```text
Design the "Historical Diagnostics Registry" screen for the "AgroSmart" app.

- HEADER: App bar with a back button, title "Diagnostic History", and a "Clear All" garbage-can button.
- FILTER CHIPS: A sticky, horizontal scrolling row of category chips at the top:
  - "All Records", "🌾 Crops", "🧪 Fertilizers", "🐛 Pesticides", "🌤️ Weather Tips". Selecting a chip highlights it in green.
- LIST LAYOUT:
  - A scrollable list of card items.
  - Each item is a card showing:
    - Left: A colored circular avatar with a custom icon depending on type (Crop = green grass icon, Fertilizer = orange test-tube, Pesticide = red bug, Weather = blue sun).
    - Center: Main recommendation title (e.g., "Urea", "Wheat Recommendation") in bold text, with the date/time (e.g., "2 hours ago", "Jun 23, 2026") in grey.
    - Right: A chevron icon inside a light-grey circle.
- SWIPE ACTION: Sliding a log tile to the left reveals a red background with a trash bin icon, indicating swipe-to-delete.
- LOG DETAILS MODAL (EXPANSION DRAWER):
  - Tapping a log tile opens a modal dialog or slide-up bottom drawer.
  - The drawer displays:
    - The type tag (e.g., Fertilizer) in a colored chip.
    - An inputs card displaying the raw numbers submitted by the farmer in a gray code-box.
    - A outputs card displaying the advice returned by the system.
    - A copy button and a delete button at the bottom of the drawer.
```
