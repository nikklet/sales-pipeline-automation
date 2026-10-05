# Sales Pipeline Automation

An n8n workflow that pulls leads from three channels into one pipeline and alerts the sales team in Slack.

> **Note:** Built for client work. Code, screenshots, and client details are confidential. This page describes the approach only.

## The Problem
Leads came in through Tally forms, Google Forms, and email. Each source used different field names and formats, so someone had to copy details into the CRM by hand, check for duplicates, and tell the team. Leads sat unanswered, and records were inconsistent.

## How It Works
1. **Capture:** Triggers for Tally (webhook), Google Forms (response sheet), and incoming email.
2. **Normalize:** All sources are mapped to one standard lead format (name, email, company, message, source).
3. **Extract:** For emails, an LLM pulls the contact details and the request out of the unstructured body.
4. **Deduplicate:** The workflow checks HubSpot and the Google Sheet for an existing contact before creating one.
5. **Store:** New contacts go to HubSpot and a Google Sheets log. Existing ones are updated.
6. **Notify:** A Slack message gives the sales team the lead's details, source, and a short summary of the request.

## Problems Solved
- **Workflow breakdowns from overloaded nodes.** The first version crammed too much logic into a few complex nodes, and they kept failing. I diagnosed where the breakdowns were happening and split those stages into separate sub-workflows. Each one now handles a single job, so failures are easier to trace and fix, and one stage failing no longer takes down the whole pipeline.
- **Three formats, one pipeline.** A normalization step means everything downstream only handles one structure.
- **Duplicate records.** A lookup before every create step keeps the CRM clean.
- **Messy email leads.** Structured LLM extraction turns free text into usable fields.
- **Silent failures.** An error workflow sends a Slack alert if an API call fails, so no lead is lost quietly.

## Tools
n8n · Tally · Google Forms · Gmail · HubSpot API · Google Sheets · Slack API · Claude

## Outcome
Less manual data entry and follow-up work, and new leads reach the sales team right away.

## Contact
onwukwetc@gmail.com · [LinkedIn](https://www.linkedin.com/in/tochukwu-onwukwe-9931651b5)
