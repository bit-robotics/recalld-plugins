# recalld plugins

Long-term memory for coding agents, by [recalld](https://recalld.ai).

Your agent remembers your preferences, your decisions and your finished work across sessions. Connect two tools to the same recalld agent and they share one memory.

## What you get

- **Nothing to set up.** Install, sign in with your browser, done. No API key, no extra runtime.
- **Memory on every message.** Before each reply the agent receives your standing rules and the stored facts related to what you just wrote.
- **Preferences that stick.** Tell it once ("always answer briefly"). The rule is sent with every message, so it still holds at the end of a long chat.
- **Two levels.** Things that are always true about how you work, and things that belong to the current project.
- **Shared between tools.** Pick the same recalld agent in each tool to share memory. Pick a different one to keep them apart.

## Install in Claude Code

Pick the region where your recalld account lives. The two regions are separate.

| Region | Plugin |
|---|---|
| US | `recalld` |
| EU | `recalld-eu` |

```
/plugin marketplace add bit-robotics/recalld-plugins
/plugin install recalld@recalld
```

For the EU region install `recalld-eu@recalld` instead.

Then sign in:

1. Run `/mcp`.
2. Pick recalld and follow the sign-in in your browser.
3. Choose an existing agent or create a new one.

Memory is on from your next message.

## How it works

On every message a hook asks recalld for two things and adds them to the conversation:

1. Your standing rules. Listing them is free.
2. Up to 5 stored facts related to your message, limited to the current project. This is one search, billed in credits. Very short messages such as "yes" skip the search.

The agent saves memory by itself when something worth keeping happens: a decision, a finding, a finished task. It saves a standing rule only when you state a lasting instruction in your own words. In Claude's default permission mode you approve each one.

The project is named after the folder the session started in, in lowercase. It keeps that name when the agent moves into a subfolder. The same folder name in another tool or on another machine is the same project.

Type `/recalld:memory` to see the instructions the agent follows.

## What is sent to recalld

- Each message you write, up to its first 1000 characters, to search your memory. It is not saved as memory.
- The path of the folder Claude is working in, and the path of the session's log file on your machine (the path only, never its content). Together they tell recalld which folder the session started in. Only that folder's name is used and stored.
- What the agent chooses to save.

How recalld handles your data is described in the [privacy policy](https://recalld.ai/legal/privacy).

## If something is off

| What you see | What to do |
|---|---|
| The agent does not seem to remember anything | Run `/mcp`, pick recalld and sign in. |
| The agent says memory search is off | Your recalld account is out of credits. Standing rules still work. |
| Memory from another tool does not show up | Check that both tools are connected to the same recalld agent and the same region. |

## Other tools

Codex and GitHub Copilot versions are planned. Any tool that speaks MCP can already connect to `https://us.recalld.ai/mcp` or `https://eu.recalld.ai/mcp` without the automatic part.

## Working on this repo

```
claude plugin validate . --strict
claude plugin validate ./plugins/recalld --strict
claude plugin validate ./plugins/recalld-eu --strict
```

The two plugin folders differ only in name, region address and the server name inside `hooks/hooks.json`. Their `skills` folders must stay identical; CI checks that.

To try a plugin from a local checkout:

```
claude plugin marketplace add ./
claude plugin install recalld@recalld
```

## Licence

[MIT](LICENSE)
