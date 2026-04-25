# TaskGenie:Personal Assistant Agent

This project demonstrates an agentic AI notebook with function calling and tool execution using Gemini through LiteLLM.

## Project Description

Personal Assistant Agent is a notebook-based AI assistant that combines natural language understanding with tool execution. Instead of only replying with text, it can decide when to call structured functions (for reminders, tasks, notes, scheduling, and text analysis), validate arguments, run the tool, and return reliable results. The project is designed as a practical learning and implementation template for building agentic systems with function calling.

## Problem It Solves

General chatbots often fail when users need actionable outcomes, such as storing a reminder, organizing tasks, or scheduling events, because they are not connected to explicit tools and validation logic. This project solves that gap by:

- Turning user intent into structured tool calls
- Validating required parameters before execution
- Handling tool and API errors in a controlled way
- Maintaining conversation memory for multi-step requests
- Providing a reusable architecture for dependable task-oriented assistants

## What This Notebook Includes

- Native function calling with JSON Schema tool definitions
- A reusable agent loop with memory, validation, and execution logging
- Error handling for missing tool calls and invalid arguments
- Rate-limit resilience through exponential backoff
- End-to-end test scenarios for reminders, tasks, notes, events, and text analysis

## Project Structure

- `Agent.ipynb`: Main notebook with setup, tools, schemas, and test flows.

## Tool Catalog

The notebook registers five tools:

1. `create_reminder(reminder_text, priority)`
2. `add_task(task, category)`
3. `take_note(note_content, tags)`
4. `schedule_event(event_name, date, time)`
5. `analyze_text(text, language, detailed)`

Each tool has a JSON Schema with required fields so the model can generate structured calls safely.

## Secure Setup

1. Create your local environment file from the example:

```bash
cp ../.env.example ../.env
```

2. Add your key to `../.env`:

```env
GOOGLE_API_KEY=your_real_google_api_key
```

3. Open and run `Agent.ipynb` from top to bottom.

## Dependencies

Install required packages in the notebook or with pip:

```bash
pip install litellm python-dotenv
```

## How To Run

Run cells from top to bottom in `Agent.ipynb`.

Recommended order:

1. Install dependencies
2. Import modules and load environment variables
3. Define tool functions
4. Register tool schemas
5. Define extraction and validation helpers
6. Run the agent loop with provided test cases

## Architecture Summary

For each user message, the agent performs this cycle:

1. Add user input to conversation memory
2. Request model output with available tool schemas
3. Extract tool call and arguments from model response
4. Validate arguments against schema requirements
5. Execute the matching Python function
6. Append result to memory and conversation log

This structure keeps behavior traceable and easy to debug.

## Example Usage

Example inputs supported by the notebook:

- "Remind me to submit my assignment with high priority"
- "Add a task in work category: finish weekly report"
- "Schedule dentist appointment on 2026-05-01 at 10:30"
- "Analyze this text in detailed mode"

## Troubleshooting

- Missing API key error:
	- Ensure `../.env` exists and includes `GOOGLE_API_KEY=...`
- Import error for dotenv or litellm:
	- Re-run the install cell or run `pip install litellm python-dotenv`
- Rate-limit errors:
	- Increase delay in `run_agent(user_messages, delay_between_calls=...)`
- No tool call found:
	- Retry with a more explicit instruction (for example, "create a reminder for...")

## Security Checklist Before Pushing

- Keep real keys only in `.env`
- Do not commit `.env`
- Ensure notebook outputs are cleared
- Verify no hardcoded secrets exist in notebook source

## Notes

- Never commit `.env` to GitHub.
- `.gitignore` in the workspace root already excludes `.env` and local artifacts.
