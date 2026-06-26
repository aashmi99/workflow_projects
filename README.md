# AI Automation Workflows

Production-ready automation pipelines built with n8n, LLM APIs (OpenAI, Claude), and Python. These workflows demonstrate end-to-end AI engineering — from ingesting unstructured data to extracting structured outputs and routing them to downstream systems.

---

## Workflows

### 1. Jira LLM User Extraction
**`jira_llm_user_extraction.json`**

Automates extraction of structured user data from unstructured Jira ticket descriptions using GPT-4o-mini.

**Flow:** Jira API → clean & normalize text → GPT-4o-mini → parse JSON output → append to Google Sheets

**What it does:**
- Connects to Jira via REST API and pulls all tickets from a target project
- Cleans raw ticket descriptions (strips HTML, normalizes whitespace)
- Sends each description to GPT-4o-mini with a structured extraction prompt
- Parses the LLM output and extracts: `firstName`, `lastName`, `email`, `location`
- Writes clean structured rows to Google Sheets automatically

**Tech:** n8n · Jira REST API · OpenAI GPT-4o-mini · Google Sheets · JavaScript

---

### 2. Employee Onboarding Automation
**`employee_onboarding_automation.json`**

Triggers on new rows added to a Google Sheet and automatically sends personalized onboarding emails via Gmail.

**Flow:** Google Sheets Trigger → field mapping → loop over items → send Gmail

**What it does:**
- Watches a Google Sheet for new employee records (name, email, role, start date)
- Loops over each new row and maps fields for downstream use
- Sends a personalized onboarding email to each new hire via Gmail
- Handles batch processing via loop node for multiple new hires at once

**Tech:** n8n · Google Sheets API · Gmail API · JavaScript

---

### 3. Document Summarization Pipeline
**`document_summarization_pipeline.json`**

Automatically analyzes text documents and writes AI-generated summaries, key points, and categories back to a Google Sheet.

**Flow:** Google Sheets Trigger → GPT-4o-mini → parse output → update row in sheet

**What it does:**
- Watches for new rows added to a Google Sheet with a `pending` status
- Sends the document text to GPT-4o-mini with a structured analysis prompt
- Parses the LLM response and extracts: `summary`, `key_points`, `category`
- Updates the original row in Google Sheets with the extracted data
- Marks processed rows as `completed` to prevent reprocessing

**Tech:** n8n · OpenAI GPT-4o-mini · Google Sheets API · JavaScript

---

## Stack

| Tool | Purpose |
|---|---|
| n8n | Workflow orchestration |
| OpenAI GPT-4o-mini | LLM inference and structured extraction |
| Jira REST API | Issue ingestion |
| Google Sheets API | Data input/output layer |
| Gmail API | Automated email delivery |
| JavaScript | Data transformation and parsing |

---

## How to Use

1. Install n8n locally: `npx n8n` or via [n8n.io](https://n8n.io)
2. Import any workflow: open n8n → new workflow → three dots menu → Import from file
3. Reconnect credentials (Jira, OpenAI, Google) with your own API keys
4. Update project keys, sheet names, and email addresses to match your environment
5. Execute workflow

---

## Background

These workflows were built to demonstrate production-style LLM pipeline architecture — the same patterns used in enterprise AI automation: structured prompt design, JSON output parsing, error handling, and multi-system data routing.

Related professional experience: built and deployed LLM-assisted automation workflows at Beyondsoft Consulting that processed 400+ monthly Jira requests and reduced manual intervention by 65%, achieving 94% structural reliability on LLM-driven outputs.
