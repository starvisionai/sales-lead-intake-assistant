# AI Sales Lead Intake Assistant

A practical AI-powered lead intake workflow built with **Google Forms**, **Make.com**, **ChatGPT**, **Google Sheets**, and **Google Chat**.

This scenario helps businesses automatically process new lead or contact form submissions by turning unstructured inquiry text into a structured lead record and internal notification.

Instead of manually reading each submission, summarizing it, logging it into a tracker, and notifying the team, this workflow handles those steps automatically.

---

## Overview

This automation captures a new form submission, sends the inquiry details to ChatGPT for structured analysis, writes the results into Google Sheets, and sends a summary notification to Google Chat.

It is intended as a simple but practical example of how AI can be embedded into a real business workflow using Make.com.

---

## What This Scenario Does

When a prospect submits a Google Form, the scenario will:

1. Capture the new response in Make.com
2. Extract and clean the submitted field values
3. Send the inquiry details to ChatGPT
4. Generate:
   - lead type
   - urgency
   - summary
   - recommended next step
5. Add the structured result to Google Sheets
6. Send a summary notification to Google Chat

The result is a repeatable intake workflow that improves speed, consistency, and visibility for incoming leads.

---

## Example Use Case

A small business or consulting firm receives inquiries through a website or internal intake form. Instead of manually reviewing each inquiry, this automation prepares the lead for action automatically.

This is useful for:

- AI consultants
- service-based businesses
- agencies
- internal operations teams
- workflow automation demos and portfolio projects

---

## Tech Stack

- **Google Forms** — Lead capture
- **Make.com** — Workflow orchestration
- **ChatGPT / OpenAI API** — Inquiry summarization and classification
- **Google Sheets** — Structured lead tracker
- **Google Chat** — Team notification

---

## Workflow Architecture

```text
Google Forms → Make.com → ChatGPT → Google Sheets → Google Chat
```

### Workflow Steps

#### 1. Google Forms
A user submits a lead or inquiry form.

#### 2. Make.com
The scenario detects the new form response and starts the workflow.

#### 3. ChatGPT
The workflow sends the submission details to ChatGPT and asks it to return structured JSON containing:

- `lead_type`
- `urgency`
- `summary`
- `next_step`

#### 4. Google Sheets
The workflow writes both the original form data and the AI-generated output into a spreadsheet for tracking and follow-up.

#### 5. Google Chat
The workflow posts a formatted summary notification into a Google Chat space.

---

## Features

- Automated lead intake processing
- AI-generated lead summary
- Lead classification
- Urgency assignment
- Recommended next step
- Structured spreadsheet logging
- Real-time team notification
- Simple architecture for demos, learning, or client solutions

---

## Sample Output

### Google Sheets

Each new submission is stored as a row containing:

- date submitted
- full name
- company
- email
- phone
- service interest
- inquiry
- timeline
- budget
- lead type
- urgency
- AI summary
- recommended next step
- status

### Google Chat

A notification is sent with a message similar to:

```text
New Lead Received

Name: Sarah Mitchell
Company: North Ridge Advisors
Service Interest: Workflow Automation
Lead Type: Sales Inquiry
Urgency: Medium

Summary:
Prospect is looking for help using AI to automate intake, internal documentation, and follow-up tasks.

Recommended Next Step:
Schedule a discovery call and share a short overview of relevant services.
```

---

## Repository Contents

This repository typically contains:

- exported Make blueprint
- this README
- optional screenshots of the workflow
- optional example form structure
- optional sample prompt used in the ChatGPT step

Example:

```text
/
├── README.md
├── blueprint.json
├── docs/
│   ├── workflow-overview.png
│   ├── sample-sheet.png
│   └── sample-chat-notification.png
```

---

## Requirements

Before importing and using this scenario, make sure you have:

- a **Make.com** account
- a **Google account** with access to:
  - Google Forms
  - Google Sheets
  - Google Chat
- an **OpenAI API key**
- a Google Chat space with either:
  - a Make Google Chat connection, or
  - an incoming webhook URL

---

## How to Use This Scenario in Make

### 1. Import the Blueprint

In Make.com:

1. Go to **Scenarios**
2. Click **Create a new scenario**
3. Choose **Import Blueprint**
4. Upload the exported blueprint JSON file from this repository

After import, Make will create the scenario structure.

### 2. Reconnect All Apps

After importing, you will need to reconnect the services used in the scenario.

Reconnect and configure:

- Google Forms
- OpenAI / ChatGPT
- Google Sheets
- Google Chat or HTTP webhook module

This is expected. Blueprint imports do not carry over your personal connections or credentials.

### 3. Configure the Google Form

Create or connect your own Google Form with the fields expected by the scenario.

#### Recommended Form Fields

- Full Name
- Company Name
- Email Address
- Phone Number
- Service Interest
- What do you need help with?
- Timeline
- Budget Range

If your form field names differ, update the mappings in Make accordingly.

### 4. Configure the Google Sheet

Create a Google Sheet for the processed lead data.

#### Recommended Sheet Columns

- Date Submitted
- Full Name
- Company
- Email
- Phone
- Service Interest
- Inquiry
- Timeline
- Budget
- Lead Type
- Urgency
- AI Summary
- Recommended Next Step
- Status

If your spreadsheet structure differs, update the Google Sheets module mappings.

### 5. Configure the OpenAI Module

Add your OpenAI API connection in Make and confirm the prompt is present.

The prompt should instruct ChatGPT to return valid JSON only with these fields:

- `lead_type`
- `urgency`
- `summary`
- `next_step`

A structured-output prompt is important so the JSON parsing step works correctly.

### 6. Configure the Google Chat Step

If using a Google Chat webhook:

- create a webhook in the target Google Chat space
- copy the webhook URL
- paste it into the HTTP module inside Make

If using the native Google Chat module instead, reconnect that module to your own Google account and target space.

### 7. Review Field Mapping Carefully

One important lesson from this build is that Google Forms responses can contain nested objects.

Make sure you map the actual answer values rather than the full response objects.

For example, use the final text answer value, not the entire JSON object returned by the Google Forms module.

This is especially important for:

- Set Variable modules
- Google Sheets row mapping
- Google Chat HTTP body content

If entire objects are mapped instead of their underlying values, the workflow may fail or write unusable data.

### 8. Run a Test Submission

Before enabling the scenario, run a test.

Recommended test steps:

1. Click **Run once** in Make
2. Submit a fresh test response through the Google Form
3. Confirm the scenario completes successfully
4. Verify:
   - the row appears correctly in Google Sheets
   - the Google Chat notification posts successfully
   - the AI fields contain clean output

### 9. Turn the Scenario On

Once testing is complete, enable the scenario so it can monitor new responses automatically.

---

## OpenAI Prompt Example

Below is an example of the prompt structure used in the ChatGPT step:

```text
You are an AI intake assistant for a consulting business.

Analyze the following contact form submission and return:
1. Lead Type
2. Urgency
3. Summary
4. Recommended Next Step

Rules:
- Lead Type must be exactly one of:
  Sales Inquiry
  Support Request
  Partnership
  General Question
- Urgency must be exactly one of:
  High
  Medium
  Low
- Summary must be no more than 2 sentences.
- Recommended Next Step must be no more than 1 sentence.
- Return valid JSON only.
- Do not include markdown.
- Use these exact keys:
  lead_type
  urgency
  summary
  next_step

Submission:
Name: {{full_name}}
Company: {{company}}
Email: {{email}}
Phone: {{phone}}
Service Interest: {{service_interest}}
Inquiry: {{inquiry}}
Timeline: {{timeline}}
Budget: {{budget}}
```

---

## Example Google Chat HTTP Body

If you are using the HTTP module with a Google Chat webhook, the payload can look like this:

```json
{
  "text": "New Lead Received\n\nName: {{full_name_clean}}\nCompany: {{company_clean}}\nService Interest: {{service_interest_clean}}\nLead Type: {{lead_type}}\nUrgency: {{urgency}}\n\nSummary:\n{{summary}}\n\nRecommended Next Step:\n{{next_step}}"
}
```

---

## Common Issues

### 1. Entire objects being inserted into Sheets or JSON

This usually happens when the Google Forms module output is mapped incorrectly.

**Fix:** Map the actual answer value, not the entire answer object.

### 2. HTTP Module JSON Errors

This usually happens when the JSON body is malformed or when mapped values are not clean strings.

**Fix:**

- validate the JSON body
- use clean variables
- avoid inserting raw response objects into the JSON payload

### 3. OpenAI Output Fails to Parse

This usually happens when the model returns extra text outside of the expected JSON format.

**Fix:** Use a stricter prompt and require valid JSON only.

### 4. Spreadsheet Columns Do Not Align

This usually happens when the sheet structure changes after the module was mapped.

**Fix:** Reopen the Google Sheets module and remap the fields.

---

## Customization Ideas

This workflow can be expanded in several ways:

- send leads into a CRM instead of Google Sheets
- auto-draft a follow-up email
- assign leads based on urgency or service type
- apply lead scoring
- route leads to different team members
- add dashboards and reporting
- trigger a Slack or email notification in addition to Google Chat

---

## Who This Build Is For

This repository is useful for:

- AI consultants building portfolio projects
- businesses looking for a lightweight lead intake automation
- Make.com users learning how to integrate AI into workflows
- anyone who wants a working example of practical business automation with AI

---

## Business Value

This automation demonstrates a practical application of AI inside business operations.

It helps reduce manual effort, improve response consistency, and create a cleaner intake process for new leads.

Instead of using AI only as a chatbot, this build shows how AI can be embedded into a workflow and used as part of an operational system.

---

## License

Add the license that fits your repo here.

Example:

```text
MIT License
```

Or:

```text
This project is provided for educational and demonstration purposes. Please review and adapt it before using it in production.
```

---

## Author

**Christopher Richard**  
Certified AI Consultant  
Star Vision Ventures