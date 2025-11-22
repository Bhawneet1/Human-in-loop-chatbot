# Human-in-the-Loop Chatbot with LangGraph

This project demonstrates how to implement a "human-in-the-loop" (HITL) AI agent using LangGraph. It combines LLM-based reasoning (such as Groq/Llama models) with the ability to request and process human expert interventions when needed.

## Features

- **LLM Agent**: Utilizes a chat model from `langchain` (`groq:llama3-8b-8192` in this notebook).
- **Tool Integration**: Agents can select pre-configured tools, like web search via `TavilySearch`, or request human assistance via a dedicated tool.
- **Human Assistance**: When the LLM determines that human expertise is needed, the conversation is paused and can be resumed with a human-supplied response.
- **Stateful Conversation**: Uses LangGraph's state management and memory checkpointing to enable interactive, multi-step, and interruptible conversations.
- **Visual Graph**: Displays the flow of the conversation agent and tool selection as a graph (e.g., with Mermaid).

## How it Works

1. **Agent Setup**: Initialize a language model and bind it with tools. The key tools are:
   - `TavilySearch`: For live search queries.
   - `human_assistance`: Allows the agent to interrupt the conversation and request a human response to a given query.

2. **Graph Construction**: A state graph is used to manage conversation flow, tool calls, and interruptions.

3. **Execution Example**:
   - The agent receives a user message asking for expert help.
   - It chooses the `human_assistance` tool, interrupts itself, and waits for human input.
   - Once a human provides their advice, the conversation continues.

## Usage

This notebook is intended to be run in Jupyter (or similar environment) with the `AgenticLanggraph` kernel and all required dependencies installed.

### Required Packages
- `langchain`
- `langgraph`
- `langchain_tavily`
- `typing_extensions`
- `IPython.display`
- `groq` (for the underlying LLM API)
- Other standard Python libraries

### Example

```python
import os
from langchain.chat_models import init_chat_model

llm = init_chat_model("groq:llama3-8b-8192")
```

... and then follow the notebook flow to set up graph, define tools, and run the interaction.

## Notable Notebook Sections

- **Tool and Graph Definitions**: Shows how to wrap a human-in-the-loop operation into a tool node.
- **Example Run**: Simulates an agent facing a request beyond its skillset, triggering a human intervention, and then resuming assistance.
- **State Checkpointer**: Demonstrates saving the conversation workflow state for resuming after human interaction.

## Customization

- Replace or extend the tool list (`tools`) to add more agent capabilities.
- Adjust the LLM or web search engine.
- Integrate your own logic for queuing, notifying, or responding with human input.

## Visualization

If the required dependencies are installed, the notebook can render the execution graph visually using Mermaid.

---

## References

- [LangGraph Documentation](https://www.langchain.com/langgraph/)
- [LangChain](https://langchain.com/)
- [Tavily Search API](https://python.langchain.com/docs/integrations/toolkits/tavily_search/)
- [Groq API for Llama](https://groq.com/)

## License

MIT License (see repository for details)
```
