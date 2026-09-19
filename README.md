# AirPrompter for Gemini CLI

Run your saved AirPrompter prompts and workflows from Gemini CLI.

## Install

```bash
gemini extensions install https://github.com/airprompter/airprompter-gemini-extension
```

Start Gemini CLI and ask it to list your workflows. It detects that
AirPrompter needs authorization and opens your browser to sign in; the
token is stored by Gemini CLI, not by this extension.

## Without the extension

The extension is a convenience. One command connects the same server:

```bash
gemini mcp add --transport http airprompter https://mcp.airprompter.com/mcp
```

The extension adds the routing context file on top of that, so Gemini
reaches for AirPrompter when you mention a saved prompt or workflow
instead of answering from scratch.

## What this extension contains

- `gemini-extension.json` -- names the AirPrompter MCP server.
- `GEMINI.md` -- routing rules, loaded into every session.
- `references/` -- loaded on demand, not at startup.

No credential, client id, or customer identifier is packaged here.
Gemini CLI discovers OAuth from the server and stores its own tokens.
Run `/mcp auth airprompter` to connect or reconnect.

## Publishing

The gallery has no review queue. Push this directory to the root of a
public GitHub repository and add the `gemini-cli-extension` topic to it;
the gallery crawler picks it up daily once the manifest validates.
