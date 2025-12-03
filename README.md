# 🛒 Visual Funnel Audit Agent (AI UX Researcher)

**An autonomous AI agent that visually audits eCommerce funnel pages for conversion friction using Claude 3.5 Sonnet.**

![Agent Architecture]

<img width="960" height="371" alt="funnel_audit" src="https://github.com/user-attachments/assets/cc04cd83-e2aa-4998-817c-a60bc3fdf63d" />


## 🚀 Overview

Optimizing an eCommerce funnel usually requires expensive consultants or hours of manual review. This **n8n workflow** automates the "Heuristic Analysis" phase.

It iterates through a list of specific funnel URLs (Homepage, Collections, Product Page, Cart, Checkout), captures high-resolution screenshots, and uses **Anthropic's Claude 3.5 Sonnet** to perform a visual audit. It identifies specific friction points—like poor contrast, missing trust signals, or confusing layouts—and logs actionable fixes directly to Google Sheets.

## ✨ Key Features

* **Multimodal AI Brain:** Uses **Claude 3.5 Sonnet** (via Anthropic), which currently offers state-of-the-art performance for UI/UX visual reasoning.
* **Full Funnel Coverage:** Designed to audit every stage of the customer journey, from "Landing" to "Checkout."
* **Context-Aware Analysis:** The AI prompt is tuned to act as a "Senior UX Researcher," providing concise, 50-word critiques focused on conversion blockers.
* **Automated Reporting:** Syncs every finding back to your Google Sheet for immediate review.

## 🛠️ Tech Stack

* **Orchestration:** [n8n](https://n8n.io/)
* **Vision Model:** Anthropic Claude 3.5 Sonnet
* **Screenshots:** ScreenshotAPI (or ScreenshotOne)
* **Database:** Google Sheets

## ⚙️ How It Works

1.  **Input:** Reads a list of URLs from a Google Sheet (each row represents a specific step in the funnel).
2.  **Vision:** Visits each URL and captures a full-page or viewport screenshot.
3.  **Reasoning:** Sends the image to Claude 3.5 Sonnet with a prompt to identify "Conversion Friction."
4.  **Output:** Writes the specific issue and recommendation back to the Google Sheet.

## 📋 Prerequisites & Setup

### 1. Google Sheet Structure
Create a Google Sheet with the following headers (case-sensitive if using the provided JSON):
* `URL` (The link to the page you want to audit)
* `Analysis` (Leave empty; the agent populates this)

### 2. Environment Variables / Credentials
You will need to configure the following in n8n:
* **Anthropic API:** Key for Claude 3.5 Sonnet.
* **Screenshot Service:** API Key for ScreenshotAPI (or similar).
* **Google Sheets:** OAuth2 connection.

### 3. Import
* Download the `funnel_audit.json` file from this repository.
* In n8n, select **"Import from File"** and load the workflow.
* Update the specific API keys in the **HTTP Request** node and **Analyze Image** node.

## ⚠️ Limitations

* **Empty States:** If auditing a generic `/cart` URL without an active session, the agent will audit the "Empty Cart" state (which is still valuable for checking retention paths).
* **Popups:** Strong cookie banners or full-screen popups may obscure the audit if not blocked by the screenshot service.

## 🤝 Contributing

Built by **[Shariq Iqbal](https://www.linkedin.com/in/shariqi/)**.
Check out my [Collection Page Auditor](https://github.com/shariqiqbal1/ecommerce-collection-audit-agent) for grid-specific analysis.
