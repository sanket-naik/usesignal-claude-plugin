# useSignal for Claude

![useSignal](./assets/icon.svg)

useSignal brings the developer tools from [usesignal.dev](https://www.usesignal.dev/) into Claude. Each tool gives exact results for jobs that are easy to get subtly wrong by hand, such as hashes, cron schedules across time zones, scannable QR codes and large JSON diffs. An interactive workbench lets you preview, edit and export what each tool produces. No sign-in or API key is required.

## Tools

| Tool | What it does |
| --- | --- |
| `usesignal_generate_qr` | Builds a scannable QR code for a link, text, Wi-Fi network, contact card, email, SMS, phone number, WhatsApp chat or UPI payment. Returns an SVG file and a PNG preview. |
| `usesignal_diff_json` | Compares two JSON documents and lists every added, removed and changed value with its path. Numbers compare exactly. |
| `usesignal_format_json` | Validates, pretty-prints or minifies JSON, reports the exact line and column of errors, and repairs common mistakes such as trailing commas and single quotes. |
| `usesignal_encode_decode` | Base64 and URL encoding and decoding, MD5/SHA-1/SHA-256/SHA-512 hashes, and JWT decoding with readable expiry dates. JWT signatures are not verified. |
| `usesignal_explain_cron` | Explains a cron expression in plain English and lists its next run times in any time zone, including across daylight saving changes. |
| `usesignal_convert_timestamp` | Converts Unix seconds, Unix milliseconds or ISO dates into ISO, UTC, epoch and local time in any time zone. |
| `usesignal_placeholder_image` | Creates a placeholder image URL served by usesignal.dev, with HTML, Markdown and CSS snippets. |
| `usesignal_flowchart` | Turns code, arrow steps or Mermaid-style arrows into a flowchart, as Mermaid source and an SVG diagram. |
| `usesignal_generate_form` | Turns a JSON object into an editable form with HTML, React JSX, JSON Schema and config exports. |
| `usesignal_generate_colors` | Builds a brand shade scale and light/dark semantic tokens from a hex color, with measured text contrast and CSS, JSON and Tailwind exports. |
| `usesignal_test_regex` | Runs a JavaScript regular expression against sample text and expected cases, showing matches and capture groups. |
| `usesignal_open_workbench` | Opens an interactive preview of any result above where the host supports MCP Apps. |

All tools are read-only and stateless. Every result includes a link to the matching full tool on usesignal.dev.

## Install

**Claude Code**

```bash
claude plugin marketplace add sanket-naik/usesignal-claude-plugin
claude plugin install usesignal@usesignal
```

**claude.ai and Claude Desktop**: add it from the Claude directory, or go to Settings → Connectors → Add custom connector and enter `https://www.usesignal.dev/mcp`.

## Try it

- "Make a Wi-Fi QR code for network Studio Guest, password welcome2026."
- "What changed between these two API responses?" (paste both JSON documents)
- "When does `30 8 * * 1-5` run next in Asia/Kolkata?"
- "SHA-256 of hello world."
- "Decode this JWT and tell me when it expires."
- "Give me a 1200×630 placeholder image for an Open Graph mockup."
- "Turn these steps into a flowchart: Start -> Validate -> Save -> End."

## What this plugin sends and where

This plugin contains no local code. It registers one remote MCP server, `https://www.usesignal.dev/mcp`, hosted by useSignal on Vercel. When Claude calls a tool, the tool arguments are sent to that server, processed in memory and returned. Arguments can include JSON documents, text to encode or hash, JWTs, QR code content such as Wi-Fi passwords, cron expressions and code for flowcharts. The server does not store inputs, keep accounts, send telemetry or call other APIs. Hosting-provider request logs are outside the plugin's control, so prefer test tokens and test passwords and avoid personal data.

Placeholder image URLs point at usesignal.dev, so anyone who views a page that uses one loads that image from useSignal's server.

Limits: form JSON up to 50 KB; JSON format and diff up to 200,000 characters per document; encoding and hashing up to 100,000 characters; regex patterns up to 1,000 characters with a 500 ms runtime limit; flowcharts up to 100 nodes.

- Support: https://www.usesignal.dev/plugin-support.html
- Privacy: https://www.usesignal.dev/plugin-privacy.html
- Terms: https://www.usesignal.dev/plugin-terms.html

## License

MIT
