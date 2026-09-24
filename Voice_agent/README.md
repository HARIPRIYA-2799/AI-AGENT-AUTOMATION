# Voice AI Agent Workflow

This repository contains the configuration for an n8n workflow file named "Voice AI Agent.json". This document provides a comprehensive, step-by-step breakdown of the agent's architecture, processing logic, and integrated capabilities.

## Workflow Overview

The "Voice AI Agent" is a multi-modal conversational assistant built in n8n. It interacts with users via Telegram, intelligently routing text and voice inputs. It utilizes OpenAI models for reasoning, transcription, and text-to-speech synthesis, alongside specialized tools for web searching, emailing, and calculations.

## Prerequisites and Required Credentials

To successfully run this workflow, the following credentials must be configured in your n8n instance:

* **Telegram API:** Required to listen for user messages and send text/audio responses.


* **OpenAI API:** Powers the core AI reasoning (`gpt-4o-mini`), Speech-to-Text (STT), and Text-to-Speech (TTS).


* **SerpAPI Account:** Enables web search capabilities.


* **Gmail OAuth2:** Enables the agent to draft and send emails.



## Step-by-Step Execution Flow

### 1. Trigger and Input Routing

* **Telegram Trigger:** The workflow initiates when a user sends a message to the connected Telegram bot. It captures the message content and the user's first name.


* **Switch Node:** A conditional router evaluates the incoming message to determine its format.


* **Voice Route:** If the payload contains a `voice.file_id`, the workflow routes to the audio processing pipeline.


* **Text Route:** If the payload contains standard `text`, it routes directly to the text processing pipeline.





### 2. Audio Processing (Speech-to-Text)

If a voice message is detected, the workflow performs the following steps:

* **Get a file:** A Telegram node downloads the voice recording using the associated `file_id`.


* **STT (Speech-to-Text):** An OpenAI node takes the downloaded audio file and transcribes it into text.


* **audio_var:** A Set node maps the transcribed output to a standard `text` variable, ensuring compatibility with the downstream AI Agent.



### 3. Text Normalization

* **Input_var:** If the user sends a standard text message, a Set node directly maps the incoming payload to the standard `text` variable. Both audio and text routes converge after their respective Set nodes.



### 4. Core AI Processing

* **AI Agent:** The central LangChain agent processes the normalized text. It utilizes the `gpt-4o-mini` model to interpret the user's intent. The agent is instructed to reply to the user using its intelligence while acknowledging the user's first name extracted from the trigger.


* **Simple Memory:** A buffer window memory node tracks conversation history. It isolates sessions using a custom key generated from the Telegram Chat ID (`telegram_{{chat_id}}`) to maintain distinct contexts for different users.


* **Integrated Tools:** The agent has access to a toolbelt governed by a strict system prompt to determine when action is required.


* **SerpAPI:** Triggered only when the user requests current data, recent news, or requires an internet search.


* **Gmail:** Triggered when the user implicitly or explicitly asks to send an email. The agent extracts the recipient, subject, and body to format a standard email payload.


* **Calculator:** Triggered for all mathematical calculations.





### 5. Output Generation and Delivery

Once the AI Agent formulates its response, the workflow branches into two simultaneous output actions:

* **Text Response (Telegram):** A standard Telegram node immediately replies to the chat ID with the agent's raw text output.


* **Audio Response Processing:**
* **Basic LLM Chain:** The raw agent output is passed to a secondary `gpt-4o-mini` model. This node is prompted to summarize the output with high accuracy, removing redundant phrases to optimize the text specifically for speech synthesis.


* **TTS (Text-to-Speech):** An OpenAI node takes the summarized text and generates an audio file.


* **Audio Delivery (Telegram1):** A final Telegram node uses the `sendAudio` operation to deliver the generated audio file back to the user's chat.
