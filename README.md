# Somfy / TaHoma (Overkiz) – Cover Position Restore Blueprint

## Purpose
This Home Assistant automation blueprint is designed for **Somfy / TaHoma devices using the Overkiz integration**.

Its purpose is to **store the last known cover position** and **restore it after a Home Assistant restart**, ensuring that position sliders in the UI always reflect the real physical position of the cover.

This is especially useful because many Somfy devices **do not report their position on startup**, causing sliders to reset to `0%`.

---

## Description
The blueprint performs two tasks:

1. **Position Tracking**
   - Listens for state changes of selected `cover` entities
   - Reads the `current_position` attribute
   - Stores the value in a corresponding `input_number` helper

2. **Restart Synchronization**
   - Triggers on Home Assistant startup
   - Waits for a configurable delay
   - Restores each cover to its last stored position using `cover.set_cover_position`

Each cover is handled **individually** (no group logic).

---

## Supported Devices
- Somfy blinds, shutters, awnings and valances
- TaHoma / Connexoon hubs
- Home Assistant Overkiz integration
- Devices that support `current_position`

---

## Requirements
- Home Assistant
- Overkiz integration configured
- One `input_number` helper **per cover**
- Covers must support `current_position`

---

## How It Works
- The blueprint maps covers to helpers by **list order**
- The first cover uses the first helper, the second cover the second helper, etc.
- Correct order is required for proper operation

---

## Setup Overview
1. Create one `input_number` helper per cover (min: 0, max: 100)
2. Import the blueprint using the GitHub RAW URL
3. Create an automation from the blueprint
4. Select covers and helpers in the same order
5. Set a restart delay (recommended: 10–20 seconds)

---

## Notes
- This blueprint does **not** create helpers automatically
- This blueprint does **not** create UI cards
- Blueprint updates do not modify existing automations

---

## License
MIT License
