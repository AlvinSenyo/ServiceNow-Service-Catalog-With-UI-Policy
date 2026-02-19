# ServiceNow-Service-Catalog-With-UI-Policy
Implementation of a UI Policy that monitors the 'acrobat' variable.  When selected, it triggers a script to suggest 'Adobe Photoshop' under the  'Additional_software_requirements' field.

## 📝 Project Overview
This project optimizes the **MacBook Pro** catalog item using a UI Policy. [cite_start]When a user selects **Adobe Acrobat**, the system suggests **Adobe Photoshop** via a field message anchored to the additional requirements field.

---

## 🏛️ System Architecture
The solution utilizes the **ServiceNow UI Policy Engine**, providing a more maintainable, condition-based logic flow:
* [cite_start]**Trigger-Based:** Executes logic based on the `acrobat` variable state[cite: 1, 14].
* [cite_start]**Automatic Reversal:** Clears messages automatically when conditions are no longer met[cite: 17, 18].
* [cite_start]**Targeted UI:** Anchored directly to the `Additional_software_requirements` variable[cite: 16].



| Variable | Internal Name | Role |
| :--- | :--- | :--- |
| **Acrobat** | `acrobat` | [cite_start]Condition Trigger [cite: 8, 14] |
| **Additional Requirements** | `Additional_software_requirements` | [cite_start]Message Display Target [cite: 16] |

---

## 📂 File Inventory
* [cite_start][Technical Manual v2](./Technical_Manual_v2.txt) - Detailed, click-by-click build guide for manual replication.
* [cite_start][Catalog-With-UI-Policy v2](./Catalog-With-UI-Policy_v2.xml) - Update Set XML containing the UI Policy and Catalog Item[cite: 23, 24].
* [cite_start][UpdateSet_v2.PNG](./UpdateSet_v2.PNG) - Screenshot of the captured UI Policy updates[cite: 23].
* [cite_start][Output_v2.PNG](./Output_v2.PNG) - Visual verification of the info message[cite: 21].
* [UIPolicy_v2.PNG](./UIPolicy_v2.PNG) - Reference capture of the UI Policy conditions and script settings.

---

## 💡 Key Functions
* [cite_start]**Condition Engine:** Uses the built-in UI Policy condition builder instead of `onChange` triggers[cite: 8, 14].
* [cite_start]**Execute if True:** Injects the recommendation message when Acrobat is selected[cite: 14, 15].
* [cite_start]**Execute if False:** Clears the message if Acrobat is deselected, ensuring a clean UI[cite: 17, 18].

---

## 🚀 Deployment Instructions
[cite_start]This solution is packaged in a **Local Update Set**[cite: 2, 3].
1. [cite_start]**Source Instance:** Ensure state is **Complete** and export to XML[cite: 24].
2. [cite_start]**Target Instance:** **Import XML** -> **Preview** -> **Commit**[cite: 24].

---

## 🛠️ The Logic (UI Policy Script)

[cite_start]Set the UI Policy Condition to: `acrobat | is | true` (or `acrobat | is | acrobat`)[cite: 8, 14].

**Execute if True:**
```javascript
/**
 * Executes when the Acrobat condition is met.
 */
function onCondition() {
    // 1. Define the recommendation message per requirement[cite: 15].
    var msg = "Recommendation: Adobe Photoshop as well, as it may also be needed for your work.";
    
    // 2. Show the message under the specific text field[cite: 16].
    g_form.showFieldMsg('Additional_software_requirements', msg, 'info');
}

/**
 * Executes when the Acrobat condition is no longer met.
 */
function onCondition() {
    // 1. Automatically hide the recommendation if the user deselects Acrobat[cite: 17, 18].
    g_form.hideFieldMsg('Additional_software_requirements');
}
