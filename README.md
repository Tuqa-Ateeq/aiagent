# AI Agent

A small command-line AI coding agent written in Python, built as part of the
[Boot.dev](https://www.boot.dev) "Build an AI Agent" course.

You give it a task in plain English, and it decides which tools to use -
listing files, reading them, writing changes, and running Python - looping
until the task is done.

## How it works

1. The user's prompt is sent to an LLM (via OpenRouter) along with a list of
   available tools.
2. The model replies with the tool it wants to call and its arguments.
3. My code runs that function and sends the result back to the model.
4. This repeats (up to 20 times) until the model gives a final answer.

All file access is restricted to a single working directory (`./calculator`),
and Python execution has a 30-second timeout.

## Tools

- `get_files_info` - list files in a directory
- `get_file_content` - read a file (truncated at 10,000 characters)
- `write_file` - create or overwrite a file
- `run_python_file` - run a Python file with optional arguments

## Usage

    uv run main.py "fix the bug: 3 + 7 * 2 shouldn't be 20" --verbose
Requires an `OPENROUTER_API_KEY` in a `.env` file.


## Disclaimer

This is a learning project, not a safe tool. It can overwrite files and run
code without asking for confirmation, so don't use it on anything important.
