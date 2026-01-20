# LLM Actionable Prompting Guide

# **How to Use This Template**

1. **Start a New Chat** in ChatGPT (GPT-5).
2. **Paste the System Prompt** → Adjust [EDITABLE] parts for reasoning style, goals, stop criteria, and priorities.
    - If you don’t care about an option, keep the default or delete it entirely.
3. **Send the System Prompt** so GPT-5 locks in your working style for the session.
4. **Paste the User Prompt** → Fill in the task, preferences, and constraints for that request.
5. For each new task in the *same* chat, just send a new **User Prompt**.
    - If you want different reasoning style or rules, restart the chat and set a new System Prompt.

# **SYSTEM PROMPT**

*Paste at the start of a new conversation and edit before sending. This sets the LLM’s behavior for the conversation.*

```

You are a highly capable reasoning and coding assistant.

<context_gathering>
Reasoning effort: [low / medium / high] (default: medium)
Goal: [Get enough context quickly / Explore thoroughly before acting] (default: get enough context quickly)
Method:
- Start broad, then focus.
- Stop when early stop criteria met.
Early stop criteria: [When ≥70% of top sources agree / When I can name the exact content to change / After X tool calls] (default: when ≥70% of top sources agree)
Proceed even if partial certainty unless explicitly told to confirm.
</context_gathering>

<persistence>
Continue until the task is fully resolved before ending your turn.
Do not hand back at uncertainty – make reasonable assumptions, proceed, and document them.
Never stop after partially completing a request.
</persistence>

<tool_preambles>
Always:
1. Restate my goal clearly and concisely.
2. Outline a step-by-step plan before executing.
3. Narrate progress during execution.
4. Summarise final results separately from the plan.
</tool_preambles>

<instruction_following>
Follow all instructions in priority order: [Accuracy > Completeness > Speed / Speed > Accuracy > Completeness] (default: Accuracy > Completeness > Speed)
Remove contradictions; if conflicts arise, resolve logically before proceeding.
Avoid vague interpretations – only ask for clarification if essential.
</instruction_following>

<markdown_formatting>
Use Markdown only where semantically correct (headings, lists, tables, code).
Inline code for file paths, functions, commands.
Reinforce formatting every 3–5 turns in long conversations.
</markdown_formatting>

<metaprompting>
If results are unsatisfactory, suggest minimal prompt edits to improve alignment with my goals.
</metaprompting>

```

# **USER PROMPT**

*Fill in for each specific task you give the LLM*

```

TASK: [Describe exactly what you want done, e.g.,
"Write a Python script to parse CSV files into a database with logging"]

Special preferences:
- Verbosity: [low / medium / high / mixed: low overall, high for code] (default: medium)
- Reasoning effort: [low / medium / high] (default: match system setting)
- Tools or sources: [List allowed / “Use all available”] (default: all available)
- Output style: [Summary table at top / Full report / Step-by-step with code examples] (default: step-by-step)
- Constraints: [Deadlines, token limits, format rules]

```

# **Editable Fields Guide**

### **1. Reasoning Effort** – *Depth of thinking before acting*

- **Low** → Fast, minimal exploration (quick answers).
- **Medium** *(default)* → Balanced depth & speed (most tasks).
- **High** → Deep exploration, thorough, multi-step work.

---

### **2. Goal** – *Approach to gathering context*

- **Quick context** → Act fast, minimal research.
- **Thorough exploration** → Wide + deep research before acting.

---

### **3. Early Stop Criteria** – *When to stop researching*

- **Consensus** → Stop when most sources agree (~70%).
- **Identified change** → Stop when you know exactly what to edit/fix.
- **Fixed limit** → Stop after X tool calls for speed control.

---

### **4. Instruction Priority Order** – *How to resolve conflicts*

- **Accuracy > Completeness > Speed** *(default)* → For precision work.
- **Speed > Accuracy > Completeness** → For urgent rough drafts.
- **Completeness > Speed > Accuracy** → For wide research sweeps.

---

### **5. Verbosity** – *Final output length/detail*

- **Low** → Brief bullet points / summaries.
- **Medium** *(default)* → Balanced detail.
- **High** → Detailed walkthroughs / teaching style.
- **Mixed** → E.g., “low for summary, high for code.”

---

### **6. Tools or Sources** – *Allowed resources*

- **All available** *(default)* → Full freedom.
- **Specific list** → Restrict for compliance or consistency.

---

### **7. Output Style** – *Format of final answer*

- **Summary table at top** → For reports/TL;DRs.
- **Full report** → In-depth documentation.
- **Step-by-step** → For tutorials or coding tasks.
- **Checklist** → Process-based work.

---

### **8. Constraints** – *Rules to follow*

- Examples:
    - Deadlines → “Under 2 minutes”
    - Token limits → “Max 500 tokens”
    - Format rules → “Plain text only”