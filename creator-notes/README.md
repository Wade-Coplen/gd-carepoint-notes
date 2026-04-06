# Creator Notes Workspace

This folder is for creator-only notes about the CAREpoint replacement concept.

It is not an in-product feature. It is a planning space for the person designing and building the app.

## Purpose

Use this workspace to keep:

- product thinking
- workflow observations
- architecture decisions
- admin model ideas
- backlog items
- open questions

## Repo role

This repository should function as a separate creator repo for the app concept and supporting notes.

The actual application repo can come later as a separate codebase when the product direction is ready.

## Recommended categories

- Creator Notes
- Workflow Research
- Product Gaps
- Architecture Decisions
- Admin Model
- Backlog

## Suggested first objects if later turned into software

If this creator workspace eventually becomes a lightweight internal tool, useful object types would be:

### `CreatorNote`

- `id`
- `title`
- `body`
- `author`
- `createdAt`
- `updatedAt`
- `status`
- `tags`

### `Decision`

- `id`
- `title`
- `summary`
- `status`
- `owner`
- `createdAt`

### `TaskItem`

- `id`
- `title`
- `status`
- `owner`
- `dueDate`

## Why this separation matters

Creator notes should stay separate from app runtime features. Keeping this repo creator-focused prevents product planning from getting confused with the user-facing application design.
