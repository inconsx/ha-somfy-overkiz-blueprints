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

## Helper Configuration (Required)

This blueprint **requires one `input_number` helper per cover** to store the last known position.

Helpers can be created:
- via **Home Assistant UI** *(recommended)*  
- or via **YAML configuration**

### YAML Example (helpers.yaml)
Below is an **anonymized example** showing how helpers should be defined.

```yaml
cover_pos_livingroom_left:
  min: 0
  max: 100
  step: 1

cover_pos_livingroom_right:
  min: 0
  max: 100
  step: 1

cover_pos_bedroom:
  min: 0
  max: 100
  step: 1

## Include the helpers.yaml code in your configuration.yaml (Required)
input_number: !include helpers.yaml

