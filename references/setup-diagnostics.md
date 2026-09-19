# Setup Diagnostics

Use this reference when AirPrompter tools are missing, or when the user asks
to diagnose, repair, reconnect, or reinstall AirPrompter in Gemini CLI.

## Readiness Layers

Treat the extension, MCP server registration, OAuth session, and current
Gemini CLI session as separate states. An installed extension does not by
itself prove that OAuth completed or that the current session has refreshed
its tool inventory.

1. Run `gemini extensions list` in the shell and confirm the AirPrompter
   extension is enabled.
2. Run `gemini mcp list` in the shell and confirm the bundled server
   `airprompter` points at `https://mcp.airprompter.com/mcp`.
3. In Gemini CLI, run `/mcp auth airprompter` to start or
   refresh the browser authorization flow.
4. Restart Gemini CLI after installing or updating the extension so the
   session reloads its extension context and MCP tool inventory.
5. Run `diagnose_connection` before executing a saved workflow. Tool
   discovery alone does not prove the authenticated account is ready.

## Customer Installation

Install the extension from its public GitHub repository:

```bash
gemini extensions install https://github.com/airprompter/airprompter-gemini-extension
```

Gemini CLI discovers AirPrompter OAuth from the remote MCP server. Do not
ask customers to paste a token, add a client id, edit OAuth settings, or
register a second server.

## Manual MCP Fallback

If the user explicitly wants the MCP connection without extension routing
context, register the same Streamable HTTP endpoint:

```bash
gemini mcp add --transport http airprompter https://mcp.airprompter.com/mcp
```

Then start Gemini CLI and run `/mcp auth airprompter`.
Never print or request the token stored by Gemini CLI.

## Maintainer Local Validation

Run `gemini extensions link <generated-extension-path>`, restart Gemini CLI,
and verify the extension and MCP server with the commands above. Remove the
link after validation if it should not remain installed.
