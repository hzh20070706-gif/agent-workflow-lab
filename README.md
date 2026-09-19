# Agent Workflow Lab

A serious-looking, local-first AI workflow playground for composing prompt, transform, retrieval, tool, and evaluator nodes. It is intentionally dependency-free so the workflow engine is inspectable and can run from a static file.

## What it demonstrates

- Visual node graph with explicit inputs and outputs
- Draft, validate, run, duplicate, and reset workflows
- Deterministic local execution with step-by-step trace logs
- Prompt templates with {{input}} and {{context}} variables
- JSON import/export for workflow portability
- Version snapshots with labels and timestamps
- Run history, latency, token estimates, and status badges
- Built-in evaluation cases for relevance and format checks
- Provider adapter panel that keeps credentials out of the static client
- Keyboard-friendly controls and responsive layout

## Run

Open `index.html` in a modern browser. No build step, dependency, server, network request, API key, or account is needed.

## Architecture

The graph is represented as a JSON workflow: nodes contain a type, configuration, and position; edges connect node IDs. The local runtime topologically orders nodes and evaluates each node with a deterministic function:

- **Input** normalizes the run payload.
- **Prompt** interpolates variables and records the rendered prompt.
- **Transform** applies operations such as uppercase, summarize, or JSON shaping.
- **Retriever** selects context from the local notes panel using token overlap.
- **Tool** performs a safe built-in operation such as word counting or timestamping.
- **Evaluator** checks output length and expected phrases.
- **Output** publishes the final result.

This is a front-end reference implementation. A production deployment can replace the local adapter behind a server boundary while retaining the graph, trace, and evaluation contracts.

## Security and privacy

The static demo does not make network requests and never submits provider keys. Imported notes are rendered with text nodes. Workflow JSON is size-limited during import, and node execution is allow-listed by type.

## License

MIT © 2026 hzh20070706-gif.
