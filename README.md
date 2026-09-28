# AdmitCrew – Agentic Team for Admissions

AdmitCrew is an agentic AI system designed for **Nowshera Study Abroad Consultants** to automate common student-admissions tasks while keeping staff in control.

The system is built using **n8n, AI agents, Groq models, and Google Sheets**.

## Project Purpose

The project helps a study-abroad office:

- Respond to student inquiries
- Collect and save student information
- Prevent duplicate leads
- Answer university questions only from approved university data
- Check uploaded test documents
- Escalate unsupported university questions to staff
- Prepare follow-up reminders for inactive students
- Require staff approval before reminder messages are marked as sent
- Maintain records that staff can review

## AI Workflows

### 1. Student Chat Agent

The Student Chat Agent communicates with prospective students and collects:

- Full name
- Phone number
- Preferred study country
- Academic marks
- IELTS score
- Study budget

It checks existing phone numbers before creating a new lead to prevent duplicates.

For university-specific questions, the agent uses the approved Universities sheet and does not invent fees, deadlines, marks, IELTS requirements, or document requirements.

Unsupported university questions are escalated for staff review.

### 2. Document Checker

The Document Checker accepts fake test documents and extracts document information.

It can check:

- Passport
- Transcript
- IELTS result

The workflow records the document checking result in Google Sheets, including whether the document is OK or has a problem such as an expired passport or name mismatch.

**Important:** Only fake test documents are used in this project. No real student documents are included in this repository.

### 3. Reminder Agent

The Reminder Agent handles follow-up reminders for inactive students.

A reminder is first added to the approval queue with a `Pending` status.

Staff must manually approve the reminder before it can proceed.

The workflow also checks previously sent messages to prevent duplicate sending.

## Database

Google Sheets is used as the project database.

The system uses the following sheets:

- Universities
- Leads
- Chats
- Documents
- Approval_Queue
- Sent_Messages
- Escalations

The university dataset contains at least 15 example programs from multiple countries.

## Test Cases

The project was tested using seven scenarios:

1. New student details are saved without creating duplicate leads.
2. University fees, deadlines, and requirements are returned from the approved university list.
3. Unknown university questions are escalated to staff and unrelated questions are declined.
4. Prompt-injection requests such as asking the agent to claim acceptance are refused.
5. An expired fake passport is identified as a problem.
6. Student reminders require staff approval before being processed as sent.
7. Staff can review leads, chats, document results, approvals, sent messages, and escalations.

## Technology Stack

- n8n
- Google Sheets
- Groq AI models
- AI Agents
- Workflow Automation

## Repository Files

The repository contains the three exported n8n workflows:

- `Student Chat Agent (1).json`
- `AdmitCrew - Document Checker (1).json`
- `AdmitCrew - Reminder Agent (1).json`

## Setup

1. Import the JSON workflow files into n8n.
2. Configure your own Groq credentials.
3. Configure your own Google Sheets OAuth credentials.
4. Create the required Google Sheets tabs and data structure.
5. Reconnect the Google Sheets nodes to your own database.
6. Test the workflows using fake student data and fake documents.

## Security

API keys and authentication secrets should never be committed to GitHub.

Use your own credentials inside n8n and keep secrets private.

Do not use real passports, transcripts, IELTS results, or other sensitive student documents when testing this demo.

## Project Status

The AdmitCrew prototype demonstrates an agentic admissions workflow with student intake, university information retrieval, document checking, escalation, staff approval, and follow-up management.
