# AP Control Tower: Cognitive Guardrails

An enterprise-grade, cloud-native Intelligent Accounts Payable (AP) pipeline that bridges low-code automation with advanced semantic intelligence to eliminate silent automation failures in corporate finance.

## 🚀 Overview

Traditional AP automation is notoriously brittle, breaking or failing silently the moment a vendor alters an invoice layout or when data matches ambiguously. This project introduces an **Intelligent Human-in-the-Loop architecture** that utilizes Generative AI as a cognitive firewall. 

By integrating **Gemini 2.5 Flash** with **UiPath Studio Web**, the pipeline contextually evaluates unstructured invoice data against internal master purchase order (PO) records, dynamically calculates a behavioral fraud risk score, and handles exceptions gracefully via **UiPath Action Center**.

---

## 🛠️ Tech Stack & Architecture

* **Orchestration Platform:** UiPath Studio Web & UiPath Cloud Orchestrator
* **Cognitive AI Engine:** Gemini 2.5 Flash (via Google Vertex AI Connection)
* **Human-in-the-Loop Interface:** UiPath Action Center
* **Database Layer:** Google Sheets (Simulating an ERP/Master PO Database)
* **Expression Scripting:** VB.NET (for advanced data payload sanitation)

### Pipeline Architecture Workflow
1. **Document Ingestion:** The robot automatically intercepts and downloads an incoming invoice PDF.
2. **Semantic Analysis:** Gemini 2.5 Flash acts as the logical core, cross-referencing unstructured line items with backend PO records without relying on rigid templates.
3. **Conditional Routing:**
   * **MATCH:** If data aligns perfectly, the bot seamlessly logs a success token and proceeds to automated ERP data entry.
   * **MISMATCH / ANOMALY:** If layout discrepancies or high-risk variances are detected, the bot routes the data payload to a supervisor.
4. **Asynchronous Closed-Loop:** A validation task is generated side-by-side inside the UiPath Action Center. A human supervisor clicks submit, instantly firing a cloud webhook that unpauses the robot to finish the transaction securely.

---

## 🧠 Engineered Prompt Logic (Phase 2 Cognitive Shield)

The core intelligence layer utilizes a sophisticated semantic prompt layout within the `Generate Text Completion using Gemini` activity block to extract advanced behavioral patterns.

```text
[Extracted_Invoice_Data] [Database_PO_Records] 

In addition to your MATCH/MISMATCH evaluation, analyze the invoice for behavioral anomalies. 
Provide the output in this strict string format: 

FRAUD RISK SCORE: [Calculate a score from 0-100 based on changes in routing, sequence, or total spikes] 
REASONING TIMELINE: [Write a 1-sentence plain-English explanation of the discrepancy or data stability history for a supervisor to read.]
