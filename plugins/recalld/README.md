# recalld for Claude Code (US region)

Long-term memory for Claude Code, by [recalld](https://recalld.ai). Claude remembers your preferences, your decisions and your finished work across sessions. Connect another tool to the same recalld agent and they share one memory.

This plugin is for recalld accounts in the US region. If your account is in the EU region, install `recalld-eu` instead. The two regions are separate.

## What you get

- **Nothing to set up.** Install, sign in with your browser, done. No API key, no extra runtime.
- **Memory on every message.** Before each reply Claude receives your standing rules and the stored facts related to what you just wrote.
- **Preferences that stick.** Tell it once ("always answer briefly"). The rule is sent with every message, so it still holds at the end of a long chat.
- **Two levels.** Things that are always true about how you work, and things that belong to the current project.
- **Shared between tools.** Pick the same recalld agent in each tool to share memory. Pick a different one to keep them apart.

## Before you start

You need a recalld account in the US region. Create one at [us.recalld.ai](https://us.recalld.ai). There is a free plan.

## Install

```
/plugin install recalld --marketplace bit-robotics/recalld-plugins
```

This one line works on Claude Code 2.1.275 or later.

## Sign in

1. Start a new Claude Code session, so the plugin is loaded.
2. Run `/mcp`.
3. Pick `plugin:recalld:recalld` and follow the sign-in in your browser.
4. Choose an existing agent or create a new one.

Memory is on from your next message. To check that it works, ask "Which recalld project is memory on for?". Claude answers with the name of your folder.

## Try it

Send these one at a time:

1. `Always answer briefly. Save this as a standing rule.`
2. `Remember for this project: we release every Tuesday at 14:00.`
3. In a new session in the same folder: `When do we release?`

Claude saves the rule and the fact, then answers the last question from memory, briefly.

## How it works

On every message a hook asks recalld for two things and adds them to the conversation:

1. Your standing rules. Listing them is free.
2. Up to 5 stored facts related to your message. This is one search, billed in credits. Very short messages such as "yes" skip the search.

Claude saves memory by itself when something worth keeping happens: a decision, a finding, a finished task. It saves a standing rule only when you state a lasting instruction in your own words. In Claude's default permission mode you approve each one.

The project is named after the folder the session started in, in lowercase. It keeps that name when Claude moves into a subfolder. The same folder name in another tool or on another machine is the same project.

## What the plugin runs, sends and fetches

- It runs no program on your machine and installs nothing. It holds one hook and one skill.
- The hook runs on every message you send. It calls the `memory_context` tool on the recalld server at `https://us.recalld.ai/mcp?via=plugin` and adds the answer to the conversation.
- It sends each message you write, up to its first 1000 characters, to search your memory. The message is not saved as memory.
- It sends the path of the folder Claude is working in, and the path of the session's log file on your machine (the path only, never its content). Together they tell recalld which folder the session started in. Only that folder's name is used and stored.
- It sends what Claude chooses to save.
- It fetches nothing else and reads no credential from your machine. Sign-in happens in your browser, and Claude Code keeps the sign-in.
- The skill is a page of instructions that tells Claude when to save and when to search. Type `/recalld:memory` to read it.

The address ends in `?via=plugin` for one reason. Claude Code merges two connections that have the same address. If you also use recalld as a connector, that merge would turn this plugin's connection off, and the automatic step would stop. The extra part keeps the two apart. With both in place Claude sees the recalld tools twice, which does no harm.

## Usage and billing

Listing your rules is free. The search on each message is billed in credits, against the account that owns the agent. If the account is out of credits, the rules still arrive and Claude tells you once that memory search is off.

## If something is off

| What you see | What to do |
|---|---|
| Claude does not seem to remember anything | Run `/mcp`, pick `plugin:recalld:recalld` and sign in. Then start a new session. |
| The plugin's entry is missing in `/mcp` | The session was opened before the install. Close it and start a new one. |
| Claude says memory search is off | Your recalld account is out of credits. Standing rules still work. |
| Memory from another tool does not show up | Check that both tools are connected to the same recalld agent and the same region. |

## Remove

Uninstall the plugin from the `/plugin` menu. That stops the automatic memory. What is already stored stays in your recalld account until you delete it there.

## Links

- [Documentation](https://recalld.ai/docs/claude-code-plugin)
- [Privacy policy](https://recalld.ai/legal/privacy)
- [Terms of service](https://recalld.ai/legal/terms)
- [Security, and how to report a vulnerability](https://recalld.ai/legal/security)
- Support: [open an issue](https://github.com/bit-robotics/recalld-plugins/issues) or write to support@recalld.ai
- Licence: MIT
