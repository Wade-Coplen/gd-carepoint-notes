# Creator Notes Structure

## High-level role

This repo is a creator workspace for the CAREpoint replacement concept. It is for research, product planning, architecture, and decision tracking.

It is not the runtime app.

## Boundaries

This repo should own:

- creator notes
- workflow research
- product requirements
- architecture documents
- decision logs
- planning backlog

This repo should not own:

- production app code for the hospital platform
- live call handling logic
- operational alert dispatch
- patient data workflows

## Recommended information model

If we keep this as a documentation-first repo, the structure can stay file-based.

Suggested folders:

- `creator-notes/`
- `Meeting Minutes/`
- `research/`
- `requirements/`
- `architecture/`
- `backlog/`

## Suggested document types

### `CreatorNote`

Freeform product or design thinking.

### `Decision`

A short record of what was decided, why, and what remains open.

### `Requirement`

A product or workflow requirement that can later move into an application repo.

### `TaskItem`

A build or research action item for the creator.

## Recommended workflow

1. Capture raw notes in `creator-notes/`
2. Move stable decisions into architecture or requirements docs
3. Track follow-up actions in backlog docs
4. Keep meeting recaps in `Meeting Minutes/`

## Future direction

When the app concept is mature enough, create a separate application repo for actual code and keep this repo focused on creator knowledge and planning history.
