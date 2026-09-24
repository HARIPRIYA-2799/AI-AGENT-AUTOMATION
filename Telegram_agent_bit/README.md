# Telegram Amazon Search Agent

This folder contains an n8n workflow for a Telegram bot that acts as a web search engine for Amazon products. The complete workflow configuration is provided in the `Telegram_Agent.json` file[cite: 2].

## 🧠 Workflow Architecture
The agent is built using n8n's Advanced AI nodes and operates through a Telegram interface[cite: 2]. It leverages the following components:

* **Telegram Trigger:** Initiates the workflow when a new message is received[cite: 2].
* **Research Agent:** Processes the user's message text and is prompted to act as a web search engine[cite: 2].
* **OpenAI Chat Model:** Acts as the brain of the agent, utilizing the `gpt-4.1-mini` model[cite: 2].
* **Simple Memory:** Maintains conversation context using the Telegram chat ID as a custom session key[cite: 2].
* **Amazon Search in SerpApi Tool:** Grants the agent the ability to search `amazon.in`, explicitly configured with a delivery zip code of `560043`[cite: 2].
* **Telegram Action:** Sends the generated text output back to the user's chat ID[cite: 2].

## 🚀 How to Use

1. From your n8n workspace, create a new workflow.
2. Import the workflow by loading the `Telegram_Agent.json` file directly into your n8n canvas[cite: 2].
3. **Configure Credentials:** 
    * Authenticate the **Telegram account** in both the trigger and the final message node[cite: 2].
    * Authenticate the **OpenAI account** node with your API key[cite: 2].
    * Authenticate the **SerpApi account** tool node[cite: 2].
4. Save and activate the workflow to start chatting with your research agent on Telegram.
