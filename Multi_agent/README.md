# Telegram Multi-Agent Workflow

This directory contains the `multi agent.json` file, which defines an n8n workflow that operates as a Telegram-based multi-agent assistant[cite: 3]. The agent processes incoming Telegram messages and uses a language model to determine which connected tool to execute based on the user's request[cite: 3].

## 🧠 Workflow Architecture
The workflow is built using n8n's advanced LangChain nodes to handle reasoning and tool execution[cite: 3]. 
* **Telegram Trigger:** Initiates the process whenever a new message is received in the chat[cite: 3].
* **Multi Agent Tool:** The central routing node configured with a system prompt to assign specific roles to its tools, allowing a maximum of 6 iterations per request[cite: 3].
* **OpenAI Chat Model:** Acts as the reasoning engine for the agent, utilizing the `gpt-4.1-mini` model[cite: 3].
* **Simple Memory:** Maintains context across the conversation by using the Telegram chat ID as a unique session key[cite: 3].
* **Telegram Message Node:** Delivers the agent's final text output back to the user in the same Telegram chat[cite: 3].

## 🛠️ Integrated Tools & Capabilities
The agent is equipped with several tools to perform various tasks automatically:
* **Gmail:** Allows the agent to construct and send emails dynamically by generating the "To", "Subject", and "Message" fields[cite: 3].
* **Amazon Search (SerpApi):** Allows the agent to perform search operations on `amazon.in`[cite: 3].
* **Google Calendar:** Configured specifically to create calendar events based on the IST time zone for the account `haripriyadesai27@gmail.com`[cite: 3].
* **Google Docs:** Enables the agent to create new documents in a default folder with dynamically generated titles[cite: 3]. *(Note: The agent's internal system instructions mention "google sheets" for appending data, but the actual tool connected in the workflow is Google Docs for creating documents[cite: 3]).*

## 🚀 Setup Instructions
To deploy this workflow in your own n8n environment:
1. Import the `multi agent.json` file directly into your n8n workspace[cite: 3].
2. Ensure you have the following credentials configured and authenticated[cite: 3]:
    * **Telegram account** (required for both the trigger and the final message node)[cite: 3].
    * **OpenAI account**[cite: 3].
    * **Gmail account** (via OAuth2)[cite: 3].
    * **Google Calendar account** (via OAuth2)[cite: 3].
    * **Google Docs account** (via OAuth2)[cite: 3].
    * **SerpApi account**[cite: 3].
3. Activate the workflow and interact with your bot on Telegram.
