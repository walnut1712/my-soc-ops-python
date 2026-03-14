---
applyTo: "**"
description: Workspace conventions, development practices, and architectural patterns for the Soc Ops project.
---

# Soc Ops Workspace Instructions

## ✅ Mandatory Development Checklist

Before committing, run these in order:

```bash
uv run ruff check . --fix && uv run ruff format .  # Lint & format
uv run pytest                                       # Test
```

---

## Quick Start

**Stack:** FastAPI + Jinja2 + HTMX, Python 3.13+, uv  
**Server:** `uv run uvicorn app.main:app --reload --port 8000`  
**Structure:** `/app/` (backend), `/app/templates/` (frontend), `/tests/`

---

## Architecture

### Core Modules
- **main.py** — FastAPI routes, session management
- **game_logic.py** — Pure functions (board gen, toggle square, win detection)
- **game_service.py** — GameSession (in-memory state)
- **models.py** — Pydantic models (frozen/immutable)
- **data.py** — QUESTIONS, FREE_SPACE

### Templates (/app/templates/components/)
- `game_screen.html` — Active board
- `bingo_board.html` — 5×5 grid
- `bingo_modal.html` — Win screen

---

## Key Patterns

### 1. Immutable State (Pydantic)
All models frozen. Create new instances with `.model_copy(update={...})`:
```python
new_square = square.model_copy(update={"is_marked": True})
```

### 2. Pure Functions
Game logic returns new lists, never mutates inputs:
```python
def toggle_square(board: list[BingoSquareData], square_id: int) -> list[BingoSquareData]:
    return [sq.model_copy(update={"is_marked": not sq.is_marked}) if sq.id == square_id else sq for sq in board]
```

### 3. Session-Based State
Player state keyed by session_id cookie (no database):
```python
session = get_session(request.session.get("session_id", uuid.uuid4().hex))
```

### 4. HTMX for Interactivity
Fragment-based updates on backend:
```html
<button hx-post="/toggle/3" hx-target="#board" hx-swap="outerHTML">Mark</button>
```

---

## Python Conventions

**Ruff rules:** E, F, I, N, W (88 char line length, target py313)  
**Type hints:** Required  
**Naming:** functions=snake_case, Classes=PascalCase, CONSTANTS=UPPER_CASE  
**Docstrings:** One-liner minimum  
**Imports:** stdlib → third-party → local

---

## Frontend

### Jinja2 Context
```python
templates.TemplateResponse(request, "home.html", {"session": session, "GameState": GameState})
```

### HTMX Attributes
- `hx-post/get` — HTTP method
- `hx-target` — CSS selector to swap
- `hx-swap` — outerHTML, innerHTML, beforeend, etc.

### CSS
Use utility classes from `app.css` (flex, p-4, mb-6, bg-accent, etc.). See `css-utilities.instructions.md`.

---

## Common Tasks

| Task | Command |
|------|---------|
| Run dev server | `uv run uvicorn app.main:app --reload` |
| Run tests | `uv run pytest` |
| Lint/format | `uv run ruff check . --fix && uv run ruff format .` |
| Add route | Create endpoint in main.py + template in components/ |
| Add question | Edit QUESTIONS list in app/data.py |
| Debug | Add `import pdb; pdb.set_trace()` or print() |

---

## Constraints

- **No database** — In-memory per session, lost on restart
- **No Simple Browser** — Test in real browser (HTMX needs HTTP)
- **5×5 board only** — 25 squares, center (index 12) is free space
- **Immutability** — Never mutate models/lists in-place

---

## Resources

- **Live:** https://madebygps.github.io/vscode-github-copilot-agent-lab/
- **Workshop:** /workshop/ (5-part lab guides)
- **Tests:** /tests/ (25 tests, examples)
