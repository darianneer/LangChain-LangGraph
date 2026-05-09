# LLM-Powered Customer Support Email Triage

This notebook demonstrates a system for automating customer support email triage using a Language Model (LLM) and LangGraph. The system classifies incoming emails, searches a knowledge base for relevant articles, makes a decision on how to handle the email (auto-reply or escalate), drafts a response, and schedules follow-ups.

## Project Overview

The goal of this project is to streamline customer support operations by intelligently routing and responding to emails. It leverages an LLM (Gemini 2.5 Flash) for classification and response drafting, a TF-IDF based knowledge base search, and a state-based graph (LangGraph) to orchestrate the workflow.

## Setup and Installation

1.  **Install Dependencies**: The first cell in the notebook installs the necessary Python libraries.
    ```python
    !pip install langchain langchain-google-genai langgraph scikit-learn --quiet
    ```

2.  **Google API Key**: This project requires a Google API Key for accessing the Gemini LLM. Store your API key in Google Colab's secrets manager under the name `GEMINI_API_KEY`. The notebook will automatically load this key.
    ```python
    from google.colab import userdata
    os.environ["GOOGLE_API_KEY"] = userdata.get('GEMINI_API_KEY')
    ```

3.  **LLM Initialization**: The `ChatGoogleGenerativeAI` model is initialized with the `gemini-2.5-flash` model.
    ```python
    MODEL = 'gemini-2.5-flash'
    llm = ChatGoogleGenerativeAI(model=MODEL)
    ```

## Core Components

### 1. Email Classification (`EmailClassification`, `classify_chain`)

An LLM is used to classify incoming emails based on `urgency` (Low, Medium, High) and `topic` (Account, Billing, Bug, Feature Request, Technical Issue). A `Pydantic` model defines the structured output for the classification, ensuring consistency.

### 2. Knowledge Base (`KNOWLEDGE_BASE`, `search_knowledge_base`)

A predefined knowledge base contains articles with IDs, topics, titles, and content. A TF-IDF vectorizer is used to convert the knowledge base content and incoming email queries into numerical representations. Cosine similarity then helps find the most relevant articles for a given email.

### 3. Decision Logic (`decide_escalation`, `schedule_followup`)

Based on the email classification and the relevance of knowledge base articles, the system decides on an action: `auto-reply` or `escalate`. It also schedules appropriate follow-up times and reasons.

### 4. LangGraph Workflow (`SupportAgentState`, `workflow`)

LangGraph is used to define and manage the multi-step support agent workflow. The `SupportAgentState` defines the data structure passed between nodes. The workflow consists of the following nodes:

*   **`classify_node`**: Classifies the email using the LLM.
*   **`search_kb_node`**: Searches the knowledge base for relevant articles.
*   **`escalation_node`**: Determines whether to auto-reply or escalate.
*   **`draft_node`**: Drafts a response using the LLM, considering the decision and KB context.
*   **`followup_node`**: Schedules follow-up actions.

### 5. Email Processing and Display (`process_email`, `display_result`)

The `process_email` function orchestrates the entire workflow for a given email using the compiled LangGraph agent. The `display_result` function then pretty-prints the output, including classification, decision, drafted response, and follow-up details.

## Usage Example

The notebook includes a `SAMPLE_EMAILS` list. The `results` loop processes each sample email through the LangGraph workflow, printing the detailed output for each email. A final summary table provides an overview of the processing results.

This system provides a robust and extensible framework for intelligent customer support automation.
