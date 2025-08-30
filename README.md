# TaskForge AI - A Browser-Based Multi-Tool Reasoning Agent

[cite_start]TaskForge AI is a minimal yet powerful proof-of-concept for an LLM-powered agent that operates entirely within the browser[cite: 3]. [cite_start]It is designed to intelligently accomplish user goals by dynamically selecting and executing multiple tools in a continuous reasoning loop[cite: 10, 19].

[cite_start]This project is built to be simple, hackable, and easily extendable, demonstrating the core logic of a modern AI agent[cite: 32].

---

## Core Features

* [cite_start]**Browser-Based**: Runs entirely in the browser using HTML and vanilla JavaScript—no backend required[cite: 6].
* [cite_start]**Multi-Tool Reasoning**: Dynamically uses a set of external tools like web search and code execution to solve problems[cite: 9].
* [cite_start]**Reasoning Loop**: The agent loops, calling tools and integrating their results, until the user's task is fully accomplished[cite: 10].
* [cite_start]**OpenAI-Style Tool Interface**: Utilizes the standard and widely-adopted tool-calling API format for seamless LLM integration[cite: 30, 49].
* [cite_start]**Simple & Hackable Code**: The implementation is intentionally kept minimal to encourage experimentation and extension[cite: 32].
* [cite_start]**Graceful UI**: Features a clean user interface with a model/provider picker and clear error notifications using `bootstrap-alert`[cite: 29, 31].

---

## Architecture: The Agent Loop

[cite_start]The agent's core logic is a JavaScript implementation of the reasoning loop concept[cite: 12]. [cite_start]The agent starts with user input and repeatedly calls an LLM, which can either respond directly to the user or request that one or more tools be executed[cite: 15, 17, 19].

[cite_start]**Conceptual Logic (from the specification)[cite: 12]:**
```python
def loop (llm):
  msg = [user_input()] # App begins by taking user input
  while True:
    output, tool_calls = llm(msg, tools) # and sends the conversation tools to the LLM
    print("Agent: ", output) # Always stream LLM output, if any
    if tool_calls: # Continue executing tool calls until LLM decides it needs no more
      msg += [handle_tool_call(tc) for tc in tool_calls] #Allow multiple tool calls (may be parallel)
    else:
      msg.append(user_input()) # Add the user input message and continue