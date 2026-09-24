# Gmail Automation AI Agent

This folder contains an n8n workflow that implements an AI-powered chat agent capable of drafting and sending emails via Gmail. The workflow logic and node configurations are provided in the exported `gmail agent.json` file.

## 🧠 Workflow Architecture
The agent is built using n8n's Advanced AI (LangChain) nodes and operates through a chat interface. It leverages the following components:

* **Chat Trigger:** Initiates the workflow when a message is received through the chat interface.
* **AI Agent (Perception):** The core routing mechanism that processes user requests and decides when to use available tools.
* **Language Model (Brain):** Powered by OpenAI's `gpt-4.1-mini` model, which handles natural language understanding and instruction processing. 
* **Memory Buffer:** Maintains a conversational context window (length of 3) so the agent remembers recent interactions during the chat session.
* **Gmail Tool:** Grants the agent the ability to autonomously construct and send emails by mapping AI-generated outputs to the `To`, `Subject`, and `Message` fields.

## 🚀 How to Use

1. Ensure you have a running instance of [n8n](https://n8n.io/).
2. From your n8n workspace, create a new workflow.
3. Select **Import from File** in the top right menu, or simply copy the raw contents of `gmail agent.json` and paste them directly into the n8n canvas.
4. **Configure Credentials:** 
    * Authenticate the **OpenAI account** node with your API key.
    * Authenticate the **Gmail account** node via OAuth2 to grant sending permissions.
5. Save and activate the workflow to interact with the agent via the chat interface.
