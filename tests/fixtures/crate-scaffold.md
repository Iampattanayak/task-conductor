# Task Conductor: Crate Scaffold

## Handoff Metadata

- **Dispatch:** `direct`
- **Owning repo:** `task-conductor`
- **Allowed write scope:** task-conductor/...
- **Cross-repo edits:** none
- **Non-goals:** workflow engine logic, canopy integration, septa contracts
- **Verification contract:** cargo build, cargo test, cargo clippy
- **Completion update:** update `.handoffs/HANDOFFS.md` and archive when complete

## Problem

Task Conductor needs a Rust crate with the basic module structure, Cargo.toml, and build infrastructure before any feature work can begin. The module layout must reflect the architectural separation: parser, decomposer, workflow engine, dispatcher, monitor, retry, store.

## What exists (state)

- **task-conductor/**: Directory does not exist yet
- **Templates**: CLAUDE.md, AGENTS.md, README.md templates exist and have been filled in
- **ecosystem-versions.toml**: Shared dependency pins available
- **spore**: Shared infrastructure crate at version 0.4.9

## What needs doing (intent)

Create the task-conductor Rust crate with module stubs, Cargo.toml with ecosystem-aligned dependencies, and basic binary entry point.

### Step 1: Create Cargo.toml and module structure

**Project:** `task-conductor/`  
**Scope:** `Cargo.toml`, `src/lib.rs`, `src/main.rs`, `src/parser/mod.rs`, `src/decompose/mod.rs`, `src/workflow/mod.rs`, `src/dispatch/mod.rs`, `src/monitor/mod.rs`, `src/retry.rs`, `src/store.rs`  
**Effort:** 2-3 hours

Create `task-conductor/Cargo.toml` with:
- name = "task-conductor"
- version = "0.1.0"
- edition = "2024"
- dependencies aligned with ecosystem-versions.toml (spore, tokio, serde, serde_json, rusqlite, clap, tracing, ulid, anyhow, thiserror, chrono)

Create module files with stub types and module-level docs matching the architectural roles defined in CLAUDE.md.

#### Verification
```bash
cd task-conductor && cargo build 2>&1 | tail -5
```

### Step 2: Implement CLI subcommand skeleton

**Project:** `task-conductor/`  
**Scope:** `src/main.rs`, `src/commands/mod.rs`  
**Effort:** 1-2 hours

Implement clap-derived CLI skeleton in `src/main.rs` with stubs for:
- `task-conductor dispatch <path>` — dispatch a handoff (stub)
- `task-conductor status` — show running workflows (stub)
- `task-conductor decompose <path>` — split a large handoff (stub)
- `task-conductor cancel <workflow-id>` — cancel a workflow (stub)

#### Verification
```bash
cd task-conductor && cargo build --release 2>&1 | tail -5
./target/release/task-conductor --help 2>&1
./target/release/task-conductor dispatch --help 2>&1
```

## Completion Protocol

When verification passes, post completion status update.

## Context

First handoff in the task-conductor chain (#118a). Must complete before any feature handoffs (#118b-g) can start. Design note at docs/architecture/task-conductor-design-note.md.
