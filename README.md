# Recued for Gemini CLI

A [Gemini CLI](https://github.com/google-gemini/gemini-cli) extension that connects Gemini CLI to
your own [Recued](https://recued.com) server.

Recued is a server you run on a computer you control. It keeps your notes, tasks, mail, calendar
and the things you own, and it stands between your data and any AI: it checks every request
against what you granted, asks you before a change, and keeps a record of what was done.

The extension adds Recued as an MCP server and brings the `recued` skill, which tells Gemini how
to work with Recued's approvals. It runs no code of its own.

## What you need

- Gemini CLI (tested with 0.65.0).
- A Recued server: [install it](https://recued.com/docs/setup/install-server/) on a computer you
  control.
- A contract for Gemini CLI. In the Recued web app, open Contracts, make a contract, choose the
  tools Gemini CLI may use, and copy the key Recued shows.

## Install

```sh
gemini extensions install https://github.com/recued/gemini-recued
```

Gemini CLI asks for two settings:

- **Recued MCP address**: the address the contract's Connect tab shows. On the computer Recued
  runs on, it is `http://127.0.0.1:7717/mcp`.
- **Recued contract key**: the contract's key. Gemini CLI keeps it in your system keychain.

To change them later, run `gemini extensions config recued`.

To check, run `gemini mcp list`; it shows `recued` as connected. Then ask Gemini: "Which notes do
I have in Recued?"

## How it works

- Recued's tools appear as `mcp_recued_<tool>`, for example `mcp_recued_work.search`. The tools
  you see are the ones the contract grants; to give Gemini CLI another tool, change the contract
  in the Recued web app.
- Reading runs without asking: Recued marks its read-only tools, and Gemini CLI runs them at once.
- A change asks twice. Gemini CLI asks you first, unless you allowed that tool or server. Then
  Recued holds the change for your approval in the Recued app, from the bell at the top of the
  page. When you have answered, tell Gemini, and it can ask Recued for the result.

## Privacy

Your data stays on your Recued server. The model sees only what a tool returns, and Recued returns
only what the contract grants. The key stays in your keychain; it is not written into the
extension.

## Remove

```sh
gemini extensions uninstall recued
```

## License

MIT
