# n8n AI Support Bot

A dynamic, webhook-triggered workflow in n8n that uses an AI model to answer user questions based on a custom knowledge base for a fictional product, the "SmartWatch Pro".

---

## Overview

This project is a simple but powerful AI assistant built entirely in n8n. It uses a webhook to receive questions from any application capable of making an HTTP request (like a command line or another web service). The question is then passed to an AI model that has been given a specific persona ("HubBot") and a limited set of data, ensuring it provides accurate and in-scope answers.

## Features

- **Webhook Trigger:** The workflow is triggered instantly by a `POST` request to a unique URL.
- **Dynamic AI Prompts:** The AI processes questions sent dynamically in the request body.
- **Custom Knowledge Base:** The AI's knowledge is restricted via a System Prompt, making it a reliable source for specific product information.
- **Automated Responses:** Provides instant, automated answers without manual intervention.

## Tech Stack

- **Automation Platform:** n8n.io
- **AI Model:** OpenAI (or any compatible model)
- **API Trigger:** Webhook
- **API Testing:** cURL

---

## How to Use

1.  **Import the Workflow:** Download the `ai-support-workflow.json` file from this repository and import it into your own n8n instance.
2.  **Configure the Nodes:**
    - Open the **Webhook** node and copy your new **Production URL**.
    - Open the **Message a model** node and ensure your AI provider credentials are set up. You can also customize the **System Prompt** with your own data.
3.  **Activate the Workflow:** Save and activate the workflow in your n8n instance.
4.  **Trigger the Webhook:** Use a command line tool like `curl` to send a question. Replace `YOUR_PRODUCTION_URL` with the URL from your webhook node.

    ```bash
    curl -X POST -H "Content-Type: application/json" -d '{"prompt": "What is the price?"}' YOUR_PRODUCTION_URL
    ```

---
## Examples

Here are some examples of how the AI will respond based on its defined knowledge base.

### Example 1: In-Scope Question

This is a question the AI has been trained to answer.

**Command:**
```bash
curl -X POST -H "Content-Type: application/json" -d '{"prompt": "What is the return policy?"}' YOUR_PRODUCTION_URL
```
Expected AI Response:

JSON

{
  "content": "The return policy for the SmartWatch Pro is accepted within 15 days of delivery."
}

### Example 2: Out-of-Scope Question
This is a question that is outside the AI's knowledge base.

Command:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"prompt": "Tell me a fun fact about Mars."}' YOUR_PRODUCTION_URL
```
Expected AI Response:

JSON

{
  "content": "I can only provide details about the SmartWatch Pro. For all other inquiries, our support team at help@thetechhub.example.com will be happy to assist you."
}
