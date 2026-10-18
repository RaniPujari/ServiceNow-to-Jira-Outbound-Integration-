# 🔄 ServiceNow & Jira Outbound Integration

## 📌 Project Overview

This project implements a robust **outbound integration between ServiceNow and Jira**, designed to automatically synchronize ServiceNow incidents with Jira issues using native platform tools.

The solution leverages **Flow Designer**, **Workflow Studio**, and **Integration Hub** to orchestrate secure REST API calls, transforming incident data into structured JSON payloads while ensuring duplicate prevention through strict `correlation_id` tracking.

---

## 🎯 Project Objectives

* Automate the creation of Jira issues directly from ServiceNow incident workflows.
* Ensure seamless data mapping for key fields (Summary, Description, Priority, and Project Keys).
* Implement reliable deduplication logic to prevent duplicate issue creation.
* Provide clear monitoring and error-handling capabilities using ServiceNow system logs and HTTP status codes.

---

## 🏗️ Architecture Overview

```text
[ServiceNow Incident Created/Updated] 
              │
              ▼
[Workflow Studio / Flow Designer] ──► [Decision Table / Coalesce Check]
                                              │
                                              ▼
                                    [Outbound REST Step]
                                              │
                                              ▼
                                     [Jira REST API Endpoint]
                                              │
                                              ▼
[ServiceNow Incident updated with Jira Key] ◄─┘
```

---

## 📂 Included Components

* **Flow Designer / Workflow Studio:** Orchestrates trigger conditions and execution steps.
* **Outbound REST Message & Action:** Securely connects to the Jira REST API endpoint using Integration Hub.
* **Deduplication Logic:** Employs `correlation_id` checks to map Jira issue keys back to ServiceNow records.
* **Payload Builder:** Transforms ServiceNow field data into the required Jira JSON structure.

---

## 🛠️ Configuration & Setup Guide

1. **Jira Prerequisites:** Ensure your target Jira project has an active project key (e.g., `IT`) and generate an Atlassian API Token.
2. **ServiceNow Credentials:** Set up Basic Authentication credentials under `System Security > Credentials` and link them to a Connection Alias.
3. **REST Message Setup:** Configure your endpoint and HTTP methods under `System Web Services > Outbound > REST Message`.
4. **Flow Automation:** Build the integration flow in Flow Designer to check the `correlation_id`, dispatch the REST step, and update the incident record with the returned Jira issue key.