💊 AI Medication Reminder & Drug Interaction Safety System

An AI-powered medication management and safety automation workflow built with n8n. The system helps patients manage their medications by checking drug safety information through the FDA OpenFDA API and creating personalized medication reminders through a calendar integration.

The project combines AI, healthcare automation, drug safety analysis, privacy protection, and security guardrails into one workflow.

⚠️ Medical Disclaimer: This project is intended for educational and decision-support purposes. It does not replace a doctor or pharmacist. Patients should consult a qualified healthcare professional before making medication or dosage decisions.

🚀 Overview

The system provides a conversational interface where patients can enter information about their medications and medical conditions.

The AI agent analyzes the patient's medication information and uses the OpenFDA Drug Label API to retrieve official drug-label information, including warnings and safety-related information.

After the safety analysis, the system can help the patient create medication reminders based on their preferred schedule.

The workflow also includes multiple security and safety layers to protect sensitive patient information and reduce the risk of unsafe AI-generated medical responses.

✨ Key Features
💊 Drug Safety & Interaction Checking
Searches medication information using the OpenFDA Drug Label API.
Retrieves drug warnings and safety information.
Supports analysis of multiple medications provided by the patient.
Presents safety information in a simplified format.

The OpenFDA tool is configured to search the FDA drug-label database using medication names.

⏰ Medication Reminders

The AI can understand medication schedules provided in natural language, such as:

Concor 5mg, starting today at 8:00 PM, twice a day.

It converts the schedule into structured information such as:

Medication name
Dose
Start date/time
End date/time
Reminder schedule

The workflow then uses a calendar/MCP integration to create the reminder events.

🔐 Patient Data Privacy

Protecting patient information is an important part of the workflow.

The system uses two layers of Personally Identifiable Information (PII) detection:

Regular expressions for structured identifiers.
Microsoft Presidio for additional entity detection.

The workflow detects information such as:

Names
Phone numbers
Email addresses
National IDs
Medical Record Numbers
Dates
IP addresses
URLs
Account numbers




🔒 De-identification

Before the patient's information is processed by the AI, detected sensitive information is replaced with temporary tokens.

For example:

Ahmed's phone number is 01012345678

can become:

[PHONE_EG_TOKEN] 

The workflow maintains a temporary mapping that allows the information to be restored when necessary. The mapping is designed to remain within the workflow execution.

🛡️ AI Safety & Guardrails

Because this project operates in a healthcare context, several safety mechanisms are included.

Input Guardrails

The workflow checks user input for:

Jailbreak attempts
Prompt injection
Requests involving harmful substances
Toxic or lethal medication requests
Attempts to override medication safety rules




Output Validation

AI-generated responses are checked before being delivered to the patient.

The validation layer checks for issues such as:

System prompt leakage
Potentially unsafe medical recommendations
Medication dosage information without appropriate medical context
Safety-policy violations

If a response contains potentially unsafe content, the workflow can replace it with a safety message instead of sending the original response.

👨‍⚕️ Safety Guardian

A separate Safety Guardian AI agent evaluates the generated response for:

Hallucinations
Dangerous medication recommendations
Unsafe dosage recommendations
Other medical safety violations

Safe responses are passed through, while unsafe responses can be blocked.

🏗️ Workflow Architecture

The overall workflow can be summarized as:

Patient
   │
   ▼
n8n Chat Interface
   │
   ▼
PII Detection
   │
   ├── Regex Detection
   │
   └── Presidio Analysis
   │
   ▼
De-identification
   │
   ▼
Input Filtering & Guardrails
   │
   ▼
AI Clinical Agent
   │
   ├── OpenFDA Drug Search
   │       │
   │       ▼
   │   Drug Safety Information
   │
   └── Medication Reminder Agent
           │
           ▼
       Calendar Integration
   │
   ▼
Output Validation
   │
   ▼
Safety Guardian
   │
   ├── Unsafe → Block / Escalate
   │
   └── Safe → Re-identify
                    │
                    ▼
                Patient
🧠 AI Components

The workflow uses Google Gemini as the language model for several AI components, including:

Clinical medication analysis
Patient interaction
Medication reminder processing
Safety evaluation
Input guardrails




🔄 Main Workflow
1. Patient Input

The patient interacts with the system through the n8n chat interface.

2. PII Detection

The system identifies sensitive information using regex patterns and Presidio.

3. De-identification

Sensitive information is replaced with temporary tokens before AI processing.

4. Security Filtering

The input is checked for malicious or harmful requests.

5. Medication Analysis

The AI collects relevant medication information and searches OpenFDA for drug-label safety information.

6. Safety Report

The system provides the patient with a simplified explanation of relevant medication warnings and safety concerns.

7. Reminder Creation

If the patient requests a reminder, the AI converts the natural-language schedule into structured calendar parameters and creates the reminder.

8. Output Safety Validation

The generated response passes through validation and a dedicated Safety Guardian.

9. Final Response

If the response passes the safety checks, sensitive information can be restored and the final response is returned to the patient.

🧰 Technologies Used
Technology	Purpose
n8n	Workflow automation and orchestration
Google Gemini	AI-powered medical conversation and analysis
OpenFDA API	Drug-label and medication safety information
Microsoft Presidio	PII detection
Regex	Structured sensitive-data detection
MCP	Calendar/tool integration
Google Calendar	Medication reminders
Gmail	Safety incident escalation
🎯 Project Goals

The main goals of this project are to:

Improve medication adherence through automated reminders.
Provide accessible medication safety information.
Identify potential medication-related safety concerns.
Protect sensitive patient information.
Add multiple layers of AI safety validation.
Automate medication scheduling through calendar integration.
Demonstrate how AI agents and workflow automation can be combined in a healthcare-oriented application.
🔮 Future Improvements

Potential future improvements include:

More comprehensive drug–drug interaction databases.
Integration with additional clinical databases.
Medication history tracking.
Patient-specific medication profiles.
Reminder notifications through SMS or WhatsApp.
Pharmacist/physician escalation workflows.
Improved interaction severity classification.
Persistent encrypted medication records.
More advanced clinical validation.
⚠️ Disclaimer

This project is an AI-assisted medication management and safety system developed for educational and experimental purposes.

Information retrieved from OpenFDA should be interpreted carefully, and the system should not be used as a substitute for professional medical advice, diagnosis, or treatment.

Always consult a qualified physician or pharmacist before starting, stopping, or changing a medication.
