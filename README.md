# AI-Powered GitHub Commit Monitor

An automated IT monitoring pipeline built to capture repository updates, parse technical commit logs using AI, and instantly broadcast human-readable summaries to team communication channels. 

This project eliminates the need for manual repository checks, improving visibility and keeping project stakeholders seamlessly updated in real time.

## 🚀 How It Works

This background automation relies on a four-step data pipeline:

1. **The Trigger (GitHub):** A webhook listens to the `decodelabs-task1` repository. Every time code is pushed to the main branch, a raw JSON payload containing the commit data is generated.
2. **The Processor (n8n):** The webhook payload is caught by a self-hosted or cloud n8n workflow, which extracts key metadata (modified files, branch, author, commit message).
3. **The Brain (Google Gemini):** An AI Agent processes the technical metadata and generates a concise, plain-English summary of the update.
4. **The Delivery (Discord / Telegram):** The final summary is instantly dispatched to a dedicated team chat channel via webhook.

## 🛠️ Technology Stack

* **n8n:** Workflow automation and data routing.
* **Google Gemini AI:** Large Language Model used for natural language summarization.
* **GitHub Webhooks:** Real-time event streaming.
* **Discord API:** End-point notification delivery.

## ⚙️ Setup & Installation

To deploy this monitoring system in your own n8n environment, follow these steps:

1. **Import the Workflow:**
   * Open your n8n workspace.
   * Click **Add Workflow** -> **Import from File** (or copy-paste the JSON workflow data if provided).
2. **Configure the GitHub Trigger:**
   * Authenticate your GitHub account within n8n.
   * Select your target repository and set the trigger event to `push`.
3. **Connect Google Gemini:**
   * Generate an API key from Google AI Studio.
   * Add the Gemini Chat Model node and input your API key. 
   * Ensure the node is configured to read the `$json.body` expressions from the GitHub trigger.
4. **Set Up the Discord Webhook:**
   * In your Discord server, navigate to Channel Settings -> Integrations -> Webhooks.
   * Create a new webhook and copy the URL.
   * Paste the URL into the n8n Discord node and set the content field to pull the AI's output (`{{ $json.output }}`).
5. **Activate:** Toggle the workflow to **Active**.

## 💡 IT & Operational Use Case

Monitoring infrastructure and codebase integrity is a critical IT function. This automation demonstrates the ability to integrate disparate APIs, manage JSON data structures, and leverage AI to reduce manual operational overhead. It ensures that any changes to critical files (like system configurations or documentation) are immediately visible to the team without requiring developers to constantly monitor Git logs.
