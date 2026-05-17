# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running

Open `index.html` directly in a browser — no build step, no server required.

## Architecture

Single-file app (`index.html`): all HTML, CSS, and JS are inline with no external dependencies.

**State (JS globals):**
- `current` — the number currently shown in the display
- `previous` — the left-hand operand saved when an operator is pressed
- `operator` — the pending binary operator (`+`, `-`, `*`, `/`, `**`)
- `shouldReset` — flag that causes the next digit to replace `current` rather than append to it
- `mode` — `'deg'` or `'rad'`, controls trig function conversions

**Key functions:**
- `applyFn(fn)` — applies a unary function (sin, cos, log, sqrt, etc.) to `current` in-place
- `setOperator(op)` — saves `current` → `previous`, sets `operator`, arms `shouldReset`
- `calculate(chain?)` — evaluates `previous op current`, writes result back to `current`; `chain=true` keeps operator pipeline alive for chained operations
- `fmt(n)` — rounds to 12 significant figures via `toPrecision(12)` then drops trailing zeros

**Display:** `#result` shows `current`; `#expression` shows the running expression string built manually by each operation.

Keyboard input is handled by a single `keydown` listener at the bottom of the script.
