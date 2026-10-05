---
name: send
description: Send a Markdown document to Graphoscope (the user's Markdown reader app) so it lands in Graphoscope's iCloud storage, pinned on their iPhone, iPad and Mac, end-to-end encrypted. Use when the user says "send this to Graphoscope", "envoie ça vers Graphoscope", "mets ça dans Graphoscope", "push to Graphoscope", or asks to read something on their phone in Graphoscope.
---

# Send to Graphoscope

`graphoscope-send` (on the PATH while this plugin is enabled) seals a Markdown document for the
user's own devices and drops it in their Graphoscope inbox; the first Graphoscope app online
(iPhone, iPad or Mac) imports it within seconds — saved in iCloud Drive › Graphoscope and pinned
everywhere. Nothing on this machine, and nothing on the relay server, can read it back.

## Steps

1. **Pick the content.**
   - An existing Markdown file the user points to (or that the conversation is clearly about,
     e.g. "send this plan" right after writing `PLAN.md`): send that file as-is.
   - Otherwise (a summary, an answer, notes from the conversation): write the document yourself
     as clean Markdown starting with a `# Title`, into a temp file (`mktemp`), then send that
     file. Write it in the language of the conversation.
   - Markdown/text only, 2 MB max. Images are not carried: mention it if the document references
     local images.
2. **Pick the name**: the user's name if they gave one; else the H1 title; else the file name.
   Short, human, no extension.
3. **Send**:
   ```bash
   graphoscope-send send <file.md> --name "Name"
   ```
   It waits up to ~30 s for a device to import it (`--no-wait` to return at once). Stdin works:
   `graphoscope-send send - --name "Name" < file`.
4. **Confirm in one line**, in the user's language, from the output:
   - `imported by <device>` → "“Name” is pinned in Graphoscope (imported by the iPhone)."
   - `waiting` → it is safely in the inbox; it arrives the next time Graphoscope opens.

## Errors

- `not paired` → the plugin has no pairing code yet. Tell the user: in Graphoscope › Settings ›
  **Receive from Claude Code**, turn it on and **Copy Command**; then run
  `/plugin configure graphoscope@graphoscope` and paste it (the whole command is fine). The code
  is picked up at the next session start. Never invent a code.
- `refused this machine` → the pairing code was renewed or the inbox turned off: same fix with
  the new code.
- `too large` → split the document. `too many` / `inbox full` → say so; nothing was lost.
- Network error → say so; nothing was sent.
