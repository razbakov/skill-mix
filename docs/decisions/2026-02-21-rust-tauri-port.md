---
title: "Rust + Tauri port: built, abandoned, recovered"
date: 2026-02-21
status: superseded (the app remains Electron)
---

# Rust + Tauri port

There was once a complete Rust + Tauri port of this app. It was built in a single
session on 2026-02-21, never pushed, and later lost when its working directory was
deleted. It has since been recovered from a session transcript and now lives at
[razbakov/skill-mix-rust](https://github.com/razbakov/skill-mix-rust).

This note exists because nothing in this repository recorded that the port ever
happened. Searching for "Rust" or "Tauri" across every branch, tag and commit here
returns nothing.

## Timeline

| When (UTC) | What |
|---|---|
| 2026-02-20 00:33 | Desktop UI options considered: SwiftUI, Tauri, Electron. |
| 2026-02-20 | Electron chosen and built. First commit `7353fac`. |
| 2026-02-21 13:30 | Branch `codex/evaluate-rust-rewrite-options` pushed. One commit, `85b1b35` ("cleanup"), touching only a demo `.tape` file. No evaluation artifact. |
| 2026-02-21 18:17:39 | `4962dc2` tagged `v0.1.0`. |
| 2026-02-21 18:18:53 | Rust + Tauri port begins, 74 seconds after the tag. Frontend copied wholesale from `src/electron-v2/src/` at `v0.1.0`; backend rewritten in Rust. |
| 2026-02-23 onward | Electron work continues to v0.7.1. The port is never mentioned again. |

## Why it was attempted

The only motivation on record is the prompt that started the build:

> instead of typescript use Rust and Tauri. And app should be easy to start for
> users (be in Applications folder on mac, so probably installable via dmg) it
> should work crossplatform: windows, mac, linux

The driver was **distribution**, not performance or language preference: a
double-clickable installed app plus genuine cross-platform packaging. The port's
`tauri.conf.json` reflects that, targeting `dmg`, `app`, `msi`, `nsis`, `deb`,
`appimage` and `rpm`.

Note that this reversed a decision made the previous day, when Tauri was one of
three candidates and Electron was picked.

## Why it was abandoned

Unknown. No transcript, commit, issue or note records that decision anywhere. The
port simply stops after 2026-02-21 and Electron continues.

The likeliest home for the missing analysis is the Codex Cloud task that produced
the `codex/evaluate-rust-rewrite-options` branch name, which ran roughly five hours
before the build. Because the branch holds no document, that evaluation was
delivered as chat and lives in Codex Cloud rather than on disk or in this repo.

## What the port contained

15 Rust modules, about 5,400 lines, covering the same surface as the TypeScript
backend at `v0.1.0`: `scanner`, `actions`, `config`, `importing`, `exporting`,
`recommendations`, `snapshot`, `skill_review`, `commands`, `models`, `util`,
`constants`. The Vue frontend was reused unchanged apart from swapping the Electron
IPC bridge for Tauri commands.

It compiles. Recovery notes, per-file provenance and known gaps (the `Cargo.lock`
was lost, which raises the floor to Rust 1.88) are in `RECOVERY.md` in that
repository.

## Status

Superseded. This project stays on Electron. The port is preserved for reference
and in case desktop packaging is revisited.
