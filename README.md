# Graphoscope for Claude Code

[Graphoscope](https://graphoscope.app) is a Markdown viewer and editor for Mac, iPhone and iPad.
This plugin lets Claude Code send a Markdown document **to your own devices** — the ones where
*you* installed Graphoscope, signed in with *your* Apple ID.

Ask Claude Code to **“send this to Graphoscope”** (a plan, a summary, notes, any `.md` file), and
a moment later the document is pinned in Graphoscope on your iPhone, iPad and Mac, ready to read
or edit.

**It only ever reaches you.** Pairing ties this plugin to the private inbox your Graphoscope app
created: no account, nobody else’s devices, no sharing. The document is encrypted on the computer
running Claude Code with a key that exists only in your iCloud Keychain, so only your own
Graphoscope apps can open it.

How it travels:

1. Claude Code encrypts the document and drops it in your inbox on the Graphoscope relay server.
   The relay only ever holds a sealed envelope it cannot read, and deletes it once delivered.
2. Whichever of **your** devices running Graphoscope is online first picks it up and saves it in
   Graphoscope’s folder in **your** iCloud Drive.
3. iCloud syncs it, pinned, to your other devices.

## Install

In Claude Code:

```
/plugin install graphoscope --marketplace styvesgoupil/graphoscope-claude
```

When asked for the **pairing code**, copy it from Graphoscope › Settings › **Receive from Claude
Code** (turn it on first, on any of your devices). It is stored in your system’s secure storage.
Each Graphoscope user has their own code; it only sends to that user’s devices.

From a shell instead:

```bash
claude plugin marketplace add styvesgoupil/graphoscope-claude
claude plugin install graphoscope@graphoscope --config pairing_code='gph1.…'
```

Then start a new session and say “send this to Graphoscope”.

## What’s inside

- `skills/send` — when and how Claude sends a document
- `bin/graphoscope-send` — the command-line tool (universal, signed with Developer ID and notarized):
  it seals the document with HPKE (P-256, AES-256-GCM) for your devices only and drops it
- `hooks/hooks.json` — at session start, pairs the tool with the code you entered (silent, and
  a no-op once paired)

Works with any agent or script too: `graphoscope-send send notes.md`.

Graphoscope: <https://graphoscope.app> · Privacy: <https://graphoscope.app/privacy/>
