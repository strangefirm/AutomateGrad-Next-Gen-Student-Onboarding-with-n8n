# AI-Powered Student Welcome Email Automation (n8n Workflow)

An automated, intelligent workflow built in **n8n** that streamlines student onboarding. It reads enrollment data from Google Sheets, uses an LLM to generate personalized welcome emails, cleans and normalizes the output via custom JavaScript, and dispatches them directly through Gmail.

---

## 🚀 Project Architecture & Workflow Steps

1. **Schedule Trigger**: Initiates the automation on a recurring schedule.
2. **Google Sheets ("Get row(s) in sheet")**: Fetches student records (Name, Email, Course, DOJ, Place, Paid status).
3. **If Node**: Filters records (e.g., processes only paid or newly registered students matching specific criteria).
4. **Message a Model (LLM Node)**: Crafts a customized, engaging welcome message using student parameters and strict JSON constraints.
5. **Code in JavaScript Node**: 
   - Loops through all batch items (`$input.all()`).
   - Strips markdown code blocks and conversational text from the AI output.
   - Parses the JSON response safely.
   - **Admin Fallback Guard:** Intercepts blank, missing, or placeholder email addresses and automatically routes them to `admin@example.com`.
   - Transforms data into a standardized mail composition format (`to`, `subject`, `body`).
6. **Send a Message (Gmail Node)**: Automatically dispatches the personalized emails to recipients.

---

## 🛠️ Key Technical Features
* **Resilient Parsing:** Handles markdown wrappers (` ```json `) and conversational AI intros automatically.
* **Batch Multi-Item Processing:** Iterates over multiple records simultaneously without cutting off at the first item.
* **Fail-Safe Admin Routing:** Ensures zero workflow crashes due to missing recipient fields.