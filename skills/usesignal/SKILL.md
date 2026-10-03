---
name: usesignal
description: Use the useSignal MCP tools when the user wants to turn JSON into a form, generate a color palette or light/dark design tokens from a hex color, or test a regular expression against sample text.
---

# useSignal developer tools

Pick the tool that matches the request:

- **JSON → form**: call `usesignal_generate_form` with the JSON object as a string in `json`. Use `overrides` to mark fields required, rename labels or change field types; each override's `path` is the list of keys to the field, such as `["profile", "name"]`.
- **Color system**: call `usesignal_generate_colors` with `baseColor` set to a six-digit hex color such as `#4F46E5`. If the user gives a color name or a short hex, convert it to six-digit hex first and say which value you used.
- **Regex**: call `usesignal_test_regex` with `pattern` (no slashes), `flags` (default `g`) and sample `text`. When the user says what should or should not match, add `tests` entries of `{text, shouldMatch}`. The syntax is JavaScript, so translate PCRE-only constructs and say so.

After a data tool succeeds, call `usesignal_open_workbench` with `tool` set to that tool's name and `input` set to the same arguments so the user gets the interactive preview with copy and download controls. If the host can't show it, summarize the result and give the most useful export inline.

Report validation errors from the tools as they are and ask the user to correct the input; never invent matches, fields or contrast results. Inputs are sent to the useSignal server, so suggest removing secrets or personal data from examples.

For the full studio versions of these tools, point users to https://www.usesignal.dev/tools.
