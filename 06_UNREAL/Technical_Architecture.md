# Unreal Engine Technical Architecture

## Target

A modular Unreal Engine 5 project named **Syntopolis** supporting a navigable island and a data-driven simulation of 100 residents.

## Recommended approach

- Unreal Engine 5 current stable production release
- C++ foundation with Blueprint-facing components
- World Partition for terrain and future scale
- Enhanced Input for first-person controls
- UMG for the society dashboard
- Data Assets / Data Tables for residents, buildings and system parameters
- Mass Entity considered for scalable resident representation
- SaveGame for prototype persistence
- source control excluding generated Unreal files

## High-level modules

### SyntopolisCore

Shared types, identifiers, simulation clock, event bus and save contracts.

### SyntopolisWorld

Island zones, points of interest, environmental state and world-to-simulation bindings.

### SyntopolisSociety

Residents, households, roles, competencies, relationships and routines.

### SyntopolisSystems

Water, energy, food, housing, work and education models.

### SyntopolisPresentation

First-person pawn, interaction, resident visualization, world feedback and UI.

## Simulation principle

The authoritative social model should not depend on every resident being represented by a full Actor. Data simulation continues for all 100 residents; visible pawns are spawned or promoted near the player.

## Suggested runtime layers

1. **Data layer** — persistent resident and system state.
2. **Simulation layer** — time steps, decisions, production, consumption and events.
3. **World layer** — buildings, devices, zones and spatial queries.
4. **Presentation layer** — characters, animation, effects, audio and dashboard.

## Initial project structure

```text
Syntopolis/
├── Config/
├── Content/
│   ├── Core/
│   ├── World/
│   ├── Settlement/
│   ├── Characters/
│   ├── Systems/
│   ├── UI/
│   └── Audio/
├── Source/
│   ├── Syntopolis/
│   ├── SyntopolisCore/
│   ├── SyntopolisSociety/
│   └── SyntopolisSystems/
└── Syntopolis.uproject
```

## First vertical slice

- one terrain block representing the full island;
- one small settlement cluster;
- first-person pawn;
- five representative residents rendered in world;
- all 100 residents simulated in data;
- water and energy as the first connected resource systems;
- dashboard with live indicators;
- accelerated day/night cycle;
- one shortage scenario with visible consequences.

## Performance target

Prototype target: stable 60 fps on the development machine at a chosen quality preset, while the data simulation for 100 residents runs independently of render distance.

## Repository hygiene

Do not commit generated directories:

- `Binaries/`
- `DerivedDataCache/`
- `Intermediate/`
- `Saved/`
- IDE caches and generated project files

Large binary assets will require Git LFS once the Unreal project is added.
