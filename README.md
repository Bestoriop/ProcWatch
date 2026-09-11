# ProcWatch

**Version 1.1 (modified)**
World of Warcraft 1.12.1 Addon — Proc rate tracker.

ProcWatch helps determine the proc rate of an effect (weapon enchant, spell,
buff, etc.) by counting hits landed and occurrences of the tracked event in
combat chat.

## Installation

1. Copy the `ProcWatch` folder into `Interface/AddOns/`.
2. Restart the game or type `/reload`.

## Getting Started

Set up a key binding in-game (Key Bindings menu > ProcWatch) to toggle the
window, or use the following commands:

| Command | Effect |
|---|---|
| `/procwatch` | Shows the window |
| `/procwatch show` | Shows the window (same as no argument) |
| `/procwatch hide` | Hides the window, monitoring continues in the background |
| `/procwatch exit` | Completely stops monitoring and resets everything |
| `/procwatch (text)` | Defines the event to watch for (same as clicking "Event") |

The event text can be partial (e.g. `Your Fiery Weapon`) or a full line.
Matching is case-insensitive.

## Interface

- **Title / status icon**: shows the current state (green = active,
  yellow = paused, grey = idle, red = stopped).
- **Event**: the text currently being watched. Click it to change it
  (this restarts monitoring and resets totals).
- **Last**: stats for the fight in progress, updated **in real time**
  (refreshed every 1 second).
- **Total**: cumulative history already committed **plus** the current
  fight, also updated in real time.
- **Reset** (under each column):
  - Last column: removes the last completed fight from the totals
    (useful for anomalies: disarmed, wrong weapon equipped, etc.)
  - Total column: resets the entire history.

### Displayed statistics

| Row | Meaning |
|---|---|
| Hits | Number of hits landed |
| Procs | Number of times the tracked event occurred |
| Time | Fight duration (mm:ss or h:mm:ss) |
| Procs/Hits | Proc rate, as a percentage (`Procs / Hits × 100`, rounded to one decimal) |
| Procs/Min | Number of procs per minute |


## Options

Accessible via the gear button below the statistics:

- **Ignore one-hit fights**: excludes one-hit fights from the totals.
- **Watch all combat**: starts the timer as soon as you enter combat rather
  than on the first hit landed.
- **Notify on procs**: shows an on-screen alert (error frame) each time a
  proc is detected.
- **Show tooltips**: toggles help tooltips on/off.

The pin-shaped button (next to the pause button) locks the window in place:
once pinned, it can no longer be moved or dismissed with Escape.

## Technical Notes

- Proc tracking works by detecting a substring within `CHAT_MSG_SPELL*` and
  `CHAT_MSG_COMBAT*` chat events.
- Hit tracking uses `CHAT_MSG_COMBAT_SELF_HITS`.
- All data (totals, options, position) is saved between sessions via
  `SavedVariables.lua`.

## Authors

Gello, Hyjal — original version.

## Changelog

**1.1**
- Stats are now updated in real time during combat (instead of
  a static display only refreshed at the end of a fight).
- The pause button can now be used in combat (it is very useful for dummy fights)
- Renamed "Hits/Proc" to "Procs/Hits", now shown as a percentage rounded
  to one decimal instead of a truncated ratio.
- Fixed a bug where ending combat while paused would break the addon (the
  chat hook was never released, stats were never committed).
- Fixed a bug where procs kept being counted while paused even though hits
  were correctly suspended.

**1.0**
- Initial release.
