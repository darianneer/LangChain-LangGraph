# README: Prompt Quality Scoring Agent
Prompt Quality Scoring Agent Using LangChain

This Agent demonstrates a prompt quality evaluation system built using `langchain-google-genai` and the Gemini API. It allows users to assess the quality of a given prompt based on several criteria and provides suggestions for improvement.

## How It Works

The system uses a `ChatGoogleGenerativeAI` model (specifically `gemini-2.5-flash`) with a predefined system prompt that acts as a "prompt expert engineer." This expert evaluates user-provided prompts against the following criteria, scoring each from 0-10:

1.  **Clarity**: Is the prompt easy to understand and does it have a clear goal?
2.  **Specificity/Details**: Does it provide sufficient details and requirements?
3.  **Context**: Is background information, audience, or use case mentioned?
4.  **Output Format & Constraints**: Are expected output format, tone, or length specified?
5.  **Persona Defined**: Does the prompt assign a specific role to the AI?

The notebook then computes a **Final Score** (average of all five criteria), **Scores of each quality criterion** (Clarity, Specificity/Details, Context, Output Format & Constraints and Persona Defined) and provides a **Short Explanation** along with **2-3 suggestions to improve the prompt**.

## Setup and Usage

1.  **Install Dependencies**: Installs the necessary `langchain-google-genai` library.
2.  **Google API Key**: You need to set your Gemini API key in Colab secrets. 
    *   Click the "🔑" icon in the left sidebar.
    *   Add a new secret named `GEMINI_API_KEY`.
    *   Paste your API key as the value. 
    *   Ensure "Notebook access" is enabled for this secret.

    This retrieves this key and initializes the `ChatGoogleGenerativeAI` model.
3.  **Define the Evaluation Prompt**: Define the `prompt_template` that structures the evaluation process for the AI.
4.  **Evaluate Your Prompt**: 
    *   Modify the `inputPrompt` variable within `prompt_template.format_prompt()` to the prompt you want to evaluate.
    *   Run this to format the prompt for the LLM.
5.  **Get the Evaluation**: Invoke the LLM with your prompt and display the evaluation results, including scores, explanation, and improvement suggestions.

## Example Evaluation Output

- Final Score: 4.8/10
- Scores of each quality criterion:
    - Clarity: 8/10
    - Specificity/Details: 2/10
    - Context: 1/10
    - Output Format & Constraints: 3/10
    - Persona Defined: 10/10

- Short Explanation: The prompt successfully defines a clear persona and outlines general goals for code analysis and improvement. However, it critically lacks specificity regarding the actual code to be analyzed, its context, and concrete definitions for terms like "perfect," "scalable," or "works everywhere." The output constraints are also quite vague.

- 2-3 suggestions to improve the prompt:
    1.  Provide the actual code: This is the most crucial missing element. Without the code, the prompt is unactionable.
    2.  Add context about the code: Specify the programming language, framework, purpose of the code, current known issues, and target environment/audience.
    3.  Define "perfect," "scalable," and "everywhere" more concretely: Provide specific metrics, performance targets, or target platforms/environments. Clarify what "not too long" means for explanations (e.g., max X paragraphs, focus on key changes).

