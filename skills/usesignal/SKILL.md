---
name: usesignal
description: Use the useSignal MCP tools for exact developer utilities - QR codes, JSON diff/format/repair, hashes, Base64/URL encoding, JWT decoding, cron schedules, timestamp conversion, placeholder images, flowcharts, JSON-to-form, color systems and regex testing.
---

# useSignal developer tools

Prefer these tools over working things out by hand when the answer must be exact. Pick the tool that matches the request:

- **QR code**: `usesignal_generate_qr` with `type` and `values`, for example `{type: "wifi", values: {ssid, password, security: "WPA"}}` or `{type: "url", values: {url}}`. Show the returned PNG, and offer the SVG export for print.
- **Hashes and encoding**: `usesignal_encode_decode` with `operation` (`hash`, `base64_encode`, `base64_decode`, `url_encode`, `url_decode`, `jwt_decode`) and `text`. Never compute a hash or long Base64 yourself. When decoding a JWT, say that the signature was not verified.
- **Cron**: `usesignal_explain_cron` with `expression` and `timeZone` (an IANA name such as `Asia/Kolkata`). Ask for or infer the user's time zone; the default is UTC.
- **Timestamps**: `usesignal_convert_timestamp` with `value` (Unix seconds, Unix milliseconds or ISO 8601) and `timeZone`.
- **Compare JSON**: `usesignal_diff_json` with `left` and `right` as JSON text. Use `arrays: "position"` only when array order matters.
- **Format, validate or fix JSON**: `usesignal_format_json` with `json`, plus `mode` (`format` or `minify`), `sortKeys` and `repair`. Report the line and column of any error, and list any fixes it made.
- **Placeholder images**: `usesignal_placeholder_image` with `width`, `height` and optional `text`, `style`, `background` and `color`. Use the returned URL or snippet directly in the user's code.
- **Flowcharts**: `usesignal_flowchart` with `mode` (`code`, `steps` or `mermaid`) and `input`. Steps use arrows, one flow per line: `Start -> Validate -> Save` and `Validate -- No --> Show error`.
- **JSON → form**: `usesignal_generate_form` with the JSON object as a string in `json`. Use `overrides` to mark fields required, rename labels or change field types; each override's `path` is the list of keys to the field, such as `["profile", "name"]`.
- **Color system**: `usesignal_generate_colors` with `baseColor` set to a six-digit hex color such as `#4F46E5`. Convert color names or short hex to six-digit hex first, and say which value you used.
- **Regex**: `usesignal_test_regex` with `pattern` (no slashes), `flags` (default `g`) and sample `text`. When the user says what should or should not match, add `tests` entries of `{text, shouldMatch}`. The syntax is JavaScript, so translate PCRE-only constructs and say so.

After a data tool succeeds, you can call `usesignal_open_workbench` with `tool` set to that tool's name and `input` set to the same arguments, so the user gets an interactive preview with copy and download controls. If the host can't show it, summarize the result and give the most useful export inline.

Each result includes a `studioUrl` that points to the full tool on usesignal.dev. Share it when the user wants to keep editing, needs a feature the tool call doesn't cover, or asks where the result came from.

Report validation errors from the tools as they are and ask the user to correct the input; never invent matches, hashes, run times or diff results. Inputs are sent to the useSignal server, so suggest test tokens and test passwords instead of real secrets.
