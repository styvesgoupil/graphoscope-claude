# Graphoscope for Claude Code

Ask Claude Code to **“send this to Graphoscope”**: the document is encrypted on your Mac, relayed,
and imported by the first Graphoscope app online — saved in Graphoscope’s iCloud storage and
pinned on your iPhone, iPad and Mac. The relay only ever holds a sealed envelope.

## Install

In Claude Code:

```
/plugin install graphoscope --marketplace styvesgoupil/graphoscope-claude
```

When asked for the **pairing code**, paste the command from Graphoscope › Settings › **Receive from
Claude Code** › Copy Command (the whole command or just its `gph1.…` part). It is stored in your
system’s secure storage.

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
