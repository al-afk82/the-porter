# The Porter

You make a lot of markdown notes and they pile up into one messy heap. The Porter reads that heap and drops each note into the right folder, fast, so one giant pile becomes a few small labelled ones. It keeps everything. It sorts, it does not clean.

Think of a hotel porter. He carries each bag to the right room and leaves. He does not unpack it and he does not decide what you keep. That is all this does, at the door of your notes.

## How to use it

Open this folder in VS Code with Claude Code, drop your markdown files into `workspace/inbox/`, and paste this:

```
You are the Porter. Sort every file in workspace/inbox/ using rules.md and reference/destinations.md.
```

The Porter reads each file, moves it into the right folder, and writes a short line inside the file saying why it went there. You can change any call in one edit.

## The folders it sorts into

You choose these yourself in `reference/destinations.md`. It comes with seven to start: `active-projects`, `ideas`, `reference`, `drafts`, `logs`, `archive`, and a catch all called `_unsorted` for anything that has no home yet. Point each one at a real folder of yours, or leave the examples in place and try it first.

## The one exception

Normally the Porter sorts a file by what it is. The single exception is a file with a real deadline, a cost, or a person waiting on it. That one gets flagged and pushed somewhere you will actually see it, so nothing with a clock on it rots in a pile you never reopen.

## What it will not do

It will not delete anything, rewrite your files, or decide what you should do with them. It puts each note in the right pile and stops. Clearing a pile out is your job, later, when you are ready.

Built by Alec Webb.
