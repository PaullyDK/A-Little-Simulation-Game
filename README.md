# WorldSim (Tick-Based Simulation CLI)

A simple tick-based simulation engine with a command-line interface (CLI).  
You can spawn entities into a world, schedule events (move/damage), advance the simulation by ticks, and save/load world state to/from JSON.

## Requirements
- Python 3.9+ recommended
- No external packages required (uses only the Python standard library)

## Project Structure (expected)

WorldSim/
cli.py
simulation.py
README.md

> If your filenames differ, adjust the commands below accordingly.

## How to Run

From the `WorldSim/` directory:

bash
python3 cli.py

You should see the CLI prompt:

=== Simulation CLI ===
Commands:
 spawn TYPE x y [health]
 move ENTITY_ID dx dy
 damage ENTITY_ID amount
 tick N
 save filename
 load filename
 print
 quit
------------------------
>

Commands

spawn TYPE x y [health]

Creates a new entity in the world at position (x, y).
	•	TYPE is a string (example: orc, player, npc)
	•	health is optional (defaults to 100)

Example:

> spawn orc 2 5 120

move ENTITY_ID dx dy

Schedules a move event for an entity on the current tick.
	•	dx and dy are directional steps (positive/negative/0)
	•	The movement handler moves the entity by 1 unit max per axis per event
	•	dx > 0 moves right by 1
	•	dx < 0 moves left by 1
	•	dy > 0 moves up by 1
	•	dy < 0 moves down by 1

Example:

> move 1 1 0

damage ENTITY_ID amount

Schedules a damage event for an entity on the current tick.

If health drops to 0 or below, the entity is removed.

Example:

> damage 1 25

tick N

Advances the simulation by N ticks.

Each tick:
	•	processes events scheduled for that tick
	•	prints world state
	•	increments the tick counter

Example:

> tick 5

print

Prints the current world state (all entities and their positions/health).

Example:

> print

save filename

Saves the current world state to a JSON file.

Example:

> save world.json

load filename

Loads world state from a JSON file created by save.

Example:

> load world.json

quit

Exits the CLI.

Example:

> quit



Notes / Gotchas
	•	move and damage schedule events at the current world tick (world.tick).
	•	If you try to move/damage an entity ID that no longer exists, the event will be ignored.
	•	Save files are standard JSON and can be inspected manually.
EOF