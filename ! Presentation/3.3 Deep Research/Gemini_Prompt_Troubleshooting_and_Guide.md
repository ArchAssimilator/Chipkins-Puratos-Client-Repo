# Gemini Deep Research Prompt: Troubleshooting & Analysis

## Why the Prompt Failed

You experienced a refusal ("I cannot do that" or similar) when using the previous prompt. After analyzing Gemini's current safety and operational parameters (as of early 2026), here are the specific reasons why the prompt likely failed:

### 1. "System Instruction" Conflict
The previous prompt started with **"Role: You are a Senior Strategic Research Analyst..."** and **"Task: Execute a Deep Research operation..."**.
*   **The Issue:** When you paste this into the standard Gemini chat window, you are issuing a "User Message". Gemini's internal system instructions already define its role (as a helpful assistant). Attempting to rigidly "re-program" its persona with "You are X" and "You must Y" can sometimes trigger **Safety Filters** designed to prevent "Prompt Injection" or "Jailbreaking" (attempts to override the model's safety protocols).
*   **The Fix:** We will remove the rigid "Role" definition and simply ask it to help with the task.

### 2. "Execute" Command vs. Feature Trigger
The phrase **"Execute a Deep Research operation"** sounds like a command to run a specific code function.
*   **The Issue:** While "Deep Research" is a feature, the model often activates it based on the *nature* of the request (e.g., "Find me details about X"), not a direct command to "execute the operation." Commanding the model to control its own internal tools can sometimes be flagged as an unauthorized system command.
*   **The Fix:** We will phrase the request as a natural language question: "Please conduct deep research on..."

### 3. Recursive Formatting (The Code Block Trap)
The prompt asked the model to: *"Generate the report inside a markdown code block following this exact template:"* and then provided a template inside a code block.
*   **The Issue:** Models sometimes get confused by **nested code blocks**. If the prompt contains a code block (```) and asks for the output to *be* a code block, the model might fail to parse where the prompt ends and the output begins, or it might refuse to generate a massive block of code (the report) due to output token limits for a single block.
*   **The Fix:** We will ask for the report in **Standard Markdown** (not inside a code block), which is how Gemini naturally formats text anyway. This is much more reliable.

### 4. Negative Constraints
The prompt contained phrases like **"No Hallucinations"** and **"You must strictly follow"**.
*   **The Issue:** While intended to ensure quality, aggressive negative constraints can paradoxically make the model more likely to refuse the task if it calculates it cannot meet your strict standard of "zero" error.
*   **The Fix:** We successfully use positive framing: "Use only credible sources" instead of "No hallucinations".

---

## The Solution

I have rewritten the prompt in **`260201 DR Prompt for Gemini.md`** to be "Gemini-Native".

### Key Changes:
1.  **Removed the "Persona"**: It now speaks directly to the AI as a collaborator.
2.  **Natural Language Trigger**: "Please conduct a comprehensive deep research deep dive..."
3.  **Simplified Output**: Removed the requirement to put the report inside a code block. It will just render the report normally, which you can still copy-paste easily.
4.  **Positive Instructions**: Focused on what to do, not what to avoid.

Please try the updated prompt.
