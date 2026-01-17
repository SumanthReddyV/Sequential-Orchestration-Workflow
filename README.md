# Sequential-Orchestration-Workflow

## Project Goal
To streamline customer feedback processing by chaining multiple AI agents into a single, automated workflow.

## What I Built
I designed and implemented a sequential orchestration pipeline using the Microsoft Agent Framework SDK. My goal was to take raw, often messy customer feedback and turn it into structured, actionable data without manual intervention.

To achieve this, I built an "assembly line" of three specialized AI agents that work in a strict order:

1. **The Summarizer**: This agent ingests the raw text and strips away the noise, condensing the feedback into a single, neutral sentence.
2. **The Classifier**: Once the text is summarized, this agent analyzes the core message and tags it as Positive, Negative, or a Feature Request.
3. **The Action Agent**: Based on the classification, this agent suggests the immediate next step—for example, logging a feature request into the product backlog.

## How I Implemented It
I developed this solution in Python, leveraging the `SequentialBuilder` class to strictly enforce the order of operations.

### My Tech Stack & Architecture
- **Language**: Python
- **SDK**: Microsoft Agent Framework (`azure-ai-agents`, `azure-ai-projects`)
- **Orchestration Pattern**: Sequential (Linear)

### The Code Logic
I used the `SequentialBuilder` to define the participants in the exact order I needed them to run. This ensures that the Classifier never sees the raw text, only the clean summary, and the Action agent always acts on categorized data.

```python
# Here is how I constructed the workflow
workflow = SequentialBuilder().participants([
    summarizer,   # Step 1: Clean the data
    classifier,   # Step 2: Tag the data
    action        # Step 3: Decide what to do
]).build()
```

To make the application responsive, I implemented streaming logic using `workflow.run_stream(...)`. This allows me to capture and display the output from each agent as it happens, rather than waiting for the entire process to finish.

## Project Structure
I organized the project to be modular and easy to configure. Here is the file structure I used:

```
ai-agents/
└── Labfiles/
    └── 05-agent-orchestration/
        └── Python/
            ├── .env             # Where I store my Azure OpenAI endpoints and keys
            └── agents.py        # The main logic containing my agent definitions and workflow builder
```

## How to Run My Code
If you want to test this pipeline yourself, you can follow the steps I used during development:

1. **Clone the Repository**: Use the standard AI Agents repository. Navigate to the specific folder for this module:

    ```bash
    cd ai-agents/Labfiles/05-agent-orchestration/Python
    ```

2. **Launch the Application**: Simply run the main script. I've set it up to process a sample feedback string automatically.

    ```bash
    python agents.py
    ```

### Outcome
You will see the raw feedback enter the pipeline and be transformed step-by-step into a final, actionable recommendation.
