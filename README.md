# useSignal for Claude

![useSignal](./assets/icon.svg)

useSignal brings three focused developer tools from [usesignal.dev](https://www.usesignal.dev/) into Claude, with an interactive workbench for previewing and exporting results. No sign-in or API key is required.

## Tools

| Tool | What it does |
| --- | --- |
| `usesignal_generate_form` | Turns a JSON object into an editable form: nested fields, labels, required flags, and HTML, React JSX, JSON Schema and config exports. |
| `usesignal_generate_colors` | Builds a brand shade scale and light/dark semantic tokens from a six-digit hex color, with measured text contrast and CSS, JSON and Tailwind exports. |
| `usesignal_test_regex` | Runs a JavaScript regular expression against sample text and expected cases, showing matches and capture groups. |
| `usesignal_open_workbench` | Opens an interactive preview of a form, color system or regex result where the host supports MCP Apps. |

All tools are read-only and stateless.

## Install

**Claude Code**

```bash
claude plugin marketplace add sanket-naik/usesignal-claude-plugin
claude plugin install usesignal@usesignal
```

**claude.ai and Claude Desktop** — add it from the Claude directory, or go to Settings → Connectors → Add custom connector and enter `https://www.usesignal.dev/mcp`.

## Try it

- "Use useSignal to turn {\"name\":\"Ada\",\"email\":\"ada@example.com\",\"subscribe\":false} into a form with name and email required."
- "Generate a light and dark color system from #7C3AED with useSignal."
- "Test INV-(?<id>\\d{4}) against INV-2048 and OLD-1234 with useSignal."

## What this plugin sends and where

This plugin contains no local code. It only registers one remote MCP server, `https://www.usesignal.dev/mcp`, hosted by useSignal on Vercel. When Claude calls a tool, the tool arguments (the JSON, color or regex and sample text you provide) are sent to that server, processed in memory and returned. The server does not store inputs, keep accounts, send telemetry or call other APIs. Hosting-provider request logs are outside the plugin's control, so avoid sending secrets or personal data.

Limits: form JSON up to 50 KB, 100 fields and depth 8; regex patterns up to 1,000 characters, sample text up to 20,000 characters, and a 500 ms runtime limit.

- Support: https://www.usesignal.dev/plugin-support.html
- Privacy: https://www.usesignal.dev/plugin-privacy.html
- Terms: https://www.usesignal.dev/plugin-terms.html

## License

MIT
