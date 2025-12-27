# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**모자 디펜스: 택티컬 (Hat Defense: Tactical)** - A single-file browser-based tower defense/clicker game where players defend against falling hat monsters by tapping/clicking them.

## Development

This is a single `index.html` file with no build process. To run:
- Open `index.html` directly in a browser, or
- Use any local server (e.g., `npx serve`, VS Code Live Server)

## Architecture

**Single-file structure** containing:
- **CSS**: Tailwind CDN + custom styles (Korean font "Jua", game UI, modals)
- **HTML**: Canvas element + UI overlay layers (HUD, item bar, menus, shop modal)
- **JavaScript**: All game logic inline (~650 lines)

### Core Game Components

**State Management** (`state` object):
- Persistent data (coins, upgrades, inventory) saved to `localStorage` with `ht_` prefix
- Session data (current score, spawned monsters, pets) reset each game

**Game Classes**:
- `HatMonster`: Enemy entities with HP, movement, freeze/slow states, hit feedback
- `Godzilla`: Deployable pet with auto-attack and slow aura
- `Particle`/`FloatingText`: Visual effects

**Input Modes** (`state.actionMode`):
- `WEAPON`: Default tap attack (basic or shotgun if purchased)
- `LASER`: Horizontal line attack consumable
- `NET`: Area freeze consumable
- `PLACING_GODZILLA`: Pet deployment mode

**Game Loop** (`animate` function):
- 60fps via `requestAnimationFrame`
- Monster spawning with progressive difficulty
- Win/lose conditions based on monster count and screen boundary

### Key Functions
- `handleInput()`: Routes taps based on current action mode
- `checkKill()`: Handles monster death, rewards, bonus system
- `updateUI()`: Syncs game state to all UI elements
- `saveData()`/`loadData()`: localStorage persistence

## Localization

Game text is in Korean. UI elements use Korean labels.
