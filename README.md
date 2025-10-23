# ⚓ Zizoo QA Eng. Challenge - Case Study 

### **Project Goal**

To conduct a strategic and improvised Exploratory Test on the search page (`https://www.zizoo.com/en/search`), focusing on identifying defects with **high business impact, critical usability, and data integrity**, moving beyond basic functionality checks.

---

### 🚀 Test Strategy (Exploratory Test Charters)

This table consolidates the strategic missions and the high-value tactical test steps used to expose CRITICAL and MAJOR defects.

| Scenario | Primary Focus Area | Tactical Test Strategy (What was executed) |
| :---: | :--- | :--- | 
| **C1** | **Critical Logic (Price/Date)** | 1. **Data Boundary Test:** Searches crossing the end of the year (365+ days) and selecting a `check-out` date before `check-in`. 2. **Cross-Currency Pricing:** Applying min/max price filter and changing the currency to verify immediate and correct recalculation. |
| **C2** | **Stress and Global Control** | 1. **Max Stress (URL Contamination):** Activating **ALL available filters** (types, brands, equipment) to deliberately trigger the HTTP 413/414 error. 2. **Critical Reset Action:** Testing the **'Reset All Filters'** button to ensure 100% cleanup of the UI and URL. 3. **'Sort By' Integrity:** Changing the sort order (e.g., `price_high` vs `price_low`) and verifying that the first and last results are mathematically correct. | 
| **C3** | **State Coherence and Usability** | 1. **Location Clear (Key Functionality):** Attempting to clear the main search location field to force a null state and remove the `location` parameter from the URL. 2. **Context Persistence:** Navigating to a boat detail page (PDP) and returning via the browser's 'Back Button' to validate that the filter state and **scroll position** are maintained. |
| **C4** | **Responsiveness & Security** | 1. **Resolution Tests:** Validation of full functionality across **Mobile (375px)** and **Tablet (768px)**. 2. **Accessibility:** Complete **keyboard navigation** (`Tab` and `Enter`) to ensure all interactive elements are focusable and actionable. 3. **Ethical Injection:** Insertion of test strings (e.g., `test' OR 1=1 --`) in search fields to verify input sanitization (XSS/SQLi protection). |
---

### ⚠️ Identified Defects Backlog

The following 5 high-value defects were identified and prioritized based on their actual impact on the user experience and business metrics:

| # | Defect Title | Severity | Priority | Category |
| :---: | :--- | :---: | :---: | :--- |
| **1** | **Functional Failure/State Corruption: 'Reset Filters' fails, resulting in an infinite loading spinner (UI Lock).** | **CRITICAL** | HIGH | State Management |
| **2** | **CRITICAL E2E FAILURE: URL Length Contamination blocks Email Subscription/Community Access (HTTP 413 Side Effect).** | **CRITICAL** | HIGH | Stability/Engagement Funnel |
| **3** | **Search: HTTP 413 Error when applying excessive filters (URL too long).** | **CRITICAL** | HIGH | Functionality/Backend |
| **4** | **Functional/UX Barrier: Location Search Field cannot be manually cleared/reset after initial input.** | MAJOR | HIGH | Usability (UX) 
| **5** | **Localization/UX: Inconsistency in legal disclosure terminology ('Impressum' link leads to 'Imprint' page title).** | MINOR | MEDIUM | Localization |

---

### 📸 Visual Evidence of Key Defects (Screenshots)

Below is the visual evidence supporting the most critical findings listed in the Defect Backlog (#1 to #5).

#### **Defect 1: Functional Failure/State Corruption: 'Reset Filters' fails (CRITICAL)**
*The screenshot shows the unresponsive UI state with the infinite loading spinner visible.*

<img width="1917" height="1021" alt="image" src="https://github.com/user-attachments/assets/b2581d2e-163d-40e3-9b0d-cc94f26d419f" />

#### **Defect 2: CRITICAL E2E FAILURE: URL Length Contamination blocks Email Subscription (CRITICAL)**
*Evidence of the page state after the critical error, showing the inability to engage with other modules.*

<img width="1937" height="1097" alt="Screen Shot 10-22-25 at 12 32 PM 003" src="https://github.com/user-attachments/assets/b6148eab-c3ad-46d9-aaeb-bdb2bcecb33b" />

#### **Defect 3: Search: HTTP 413 Error when applying excessive filters (CRITICAL)**
*The images capture the complex URL exceeding the server limit (413 Payload Too Large or 414 Request-URI Too Long).*

<img width="1937" height="1097" alt="Screen Shot 10-22-25 at 12 20 PM 001" src="https://github.com/user-attachments/assets/adfe14c0-d943-4ddd-aba2-2a76955d9c76" />
<img width="1937" height="1097" alt="Screen Shot 10-22-25 at 12 20 PM 002" src="https://github.com/user-attachments/assets/0f84f9af-3ee1-457d-beb5-6a9694ac30b8" />

#### **Defect 4: Functional/UX Barrier: Location Search Field cannot be manually cleared (MAJOR)**
*The evidence shows the Location input field refusing to enter a clear/empty state.*

<img width="1937" height="1097" alt="Screen Shot 10-22-25 at 12 36 PM" src="https://github.com/user-attachments/assets/fc65ef73-b6ea-4783-aa97-f43d09d51161" />

#### **Defect 5: State Desynchronization: Filters UI not cleared/reset (MAJOR)**
*The images demonstrate the visual persistence of old filters in the UI that are not reflected in the URL parameters.*

<img width="1937" height="1097" alt="image" src="https://github.com/user-attachments/assets/fd366921-9f7f-4c60-9671-d023b9e3b186" />
<img width="1937" height="1097" alt="image" src="https://github.com/user-attachments/assets/db55e185-95a5-44f6-b8ac-a6dc08d505f6" />

### 🛠️ Deliverables and Tools

* **Test Plan (Detailed Charters):** ScenariosBDD.docx
* **Bug Intake Form (Detailed Reproduction Steps):** Bugs.docx
* **Evidences:** https://drive.google.com/drive/folders/1GcLesEUAiQFLGUXTmqIjrqawb7jiEjf2?usp=sharing
* **Tools Used:** Google Chrome with DevTools
* **Actual Solution Time Spent:** 2h
