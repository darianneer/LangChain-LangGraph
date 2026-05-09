# Travel Chatbot

This notebook implements a simple travel chatbot using the `langchain-google-genai` library. The chatbot is designed to answer travel-related questions and manages conversation history by periodically summarizing it to conserve context.

## Features

- **Travel-specific responses**: The chatbot is configured to only answer questions related to travel (flights, hotels, destinations, trips, itineraries, visas, packing, and travel tips).
- **Conversation summarization**: To manage the context window, the chat history is summarized every 5 turns.
- **Interactive chat interface**: A command-line interface allows users to interact with the chatbot, quit, or reset the conversation.

## Setup

### 1. Install Dependencies

Run the first cell in the notebook to install the necessary library:

```python
!pip install langchain-google-genai
```

### 2. Google API Key

You need a Google API key for the `langchain-google-genai` library to function. 

- Create a key in [Google AI Studio](https://aistudio.google.com/app/apikey).
- Add the key to Colab's secrets manager. Click the "🔑" icon in the left panel, and add your API key with the name `GEMINI_API_KEY`.

### 3. Run the Notebook Cells

Execute all the code cells sequentially. This will:

- Import necessary libraries.
- Configure the `GOOGLE_API_KEY` from Colab's secrets.
- Initialize two `ChatGoogleGenerativeAI` models: one for the main chat (streaming enabled) and one for summarization (streaming disabled).
- Define the system prompt for the travel agent and create prompt templates for both the main chat and summarization.
- Set up helper functions for managing and summarizing chat history.
- Start the interactive chat loop.

## Usage

After running all cells, an interactive prompt will appear:

```
Travel Chatbot — type 'quit' or 'exit' to stop, 'reset' to clear history.

You: 
```

- Type your travel-related questions into the prompt.
- The chatbot will stream its response.
- To clear the conversation history, type `reset`.
- To end the chat, type `quit` or `exit`.

## Code Structure

- Installs `langchain-google-genai`.
- Imports necessary libraries.
- Sets up the `GOOGLE_API_KEY` and initializes the LLM models.
- Defines the system prompt and prompt templates.
- Contains functions for managing and summarizing chat history.
- Implements the `chat` and `reset_chat` functions.
- The main loop for interacting with the chatbot.
