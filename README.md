# Unreal Engine Stealth Game Template

## Stealth AI and Mission Objective System – Student Guide

---

## Overview

This template provides a fully functional **stealth-game framework** built in **Unreal Engine** using **Blueprints only**. It supports both **top-down** and **third-person** perspectives and is optimised for **mobile platforms**, while remaining suitable for **PC projects**.

The template includes:

* A complete player controller with stealth mechanics
* Multiple enemy AI types implemented using **Behaviour Trees**
* Environmental threats such as **cameras** and **turrets**
* A **modular mission objective** system

You are expected to **understand, adapt, and extend** these systems rather than treat them as a black box.

---

## Player Character

**Blueprint Location:**

```
Content/Stealth/ThirdPersonBP/Blueprints/ThirdPersonCharacter
```

The player character supports the following mechanics.

---

### Core Movement and Stealth

* Walk / Jog / Run
* Crouch
* Hide in foliage
* Whistle (enemy distraction)

### Combat and Interaction

* Stealth takedowns
* Pick up and drop bodies
* Hack cameras
* Hack turrets
* Interact with mission objectives

### Utility

All player logic is implemented in `ThirdPersonCharacterBP`.

---

## Movement States

### Walk / Jog / Run

* Default state is **Jog**
* Movement speed is controlled via **Max Walk Speed**
* Jogging or running generates **noise** that enemies can detect

### Crouch

* Enemies cannot detect **footstep noise** while crouched
* Toggle with **C**

---

## Whistle

* Lures nearby enemies to the player’s location
* Useful for isolating targets
* Triggered with **T**
* Implemented in `ThirdPersonCharacterBP`

---

## Stealth Takedown

* Can be performed from **front or back** depending on enemy type
* Activated with **Q**
* Requires correct positioning and enemy state

---

## Body Interaction

* Dead enemies can be picked up and hidden
* Prevents other enemies from detecting bodies and raising alarms
* Use **E** to pick up or drop bodies

---

## Hacking Systems

### Cameras

* Detect the player and raise alarms
* Can be hacked when within the hack area
* Hacking disables detection and alarms

### Turrets

* Detect, shoot, and raise alarms
* Can be hacked from close range
* Hacking disables firing and detection

Touch/click logic resides in `ThirdPersonCharacterBP`.
System logic resides in the relevant **Actor Blueprints**.

---

## Hiding in Foliage

**Blueprint:**

```
Content/Stealth/ActorBP/StealthHide_BP
```

* Prevents enemies from seeing the player when crouched
* Collision box blocks enemy sight-line traces
* Size directly affects gameplay balance

> If the collision box is tall enough, enemies may not see the player even when standing.

---

## Enemy AI System

Enemy behaviour is driven by:

* Behaviour Trees
* Blackboards
* AI Perception (Sight + Hearing)

All Behaviour Trees are **commented in-engine** and should be explored.

---

## Shared Enemy Behaviours

Enemies can:

* Patrol
* Detect player presence
* Investigate noise, alarms, and whistles
* Chase or hunt the player
* Lose sight and return to patrol
* Raise and investigate alarms
* Detect bodies (depending on type)
* Block attacks (shielded enemies)

---

## Enemy Types

* Knife Enemy
* Rifle Enemy
* Shielded Enemy

Each type has different detection, combat, and alert behaviours.

---

## Alert System and Blackboard Keys

Enemy awareness is visualised using a **vision cone colour** and an **alert progress bar**.

| Alert Level       | Blackboard Key       | Vision Cone | Behaviour                       |
| ----------------- | -------------------- | ----------- | ------------------------------- |
| Initial detection | `CanSeeYou?`         | Yellow      | Alert bar begins filling        |
| Suspicion         | `AlertBarCanSeeYou?` | Orange      | Enemy investigates              |
| Fully alerted     | `AlertBar?`          | Red         | Enemy attacks and raises alarms |

---

## Patrol System

**Enemy Blueprint Example:**

```
EnemyCharacterRifle_BP
```

**Patrol Path Actor:**

```
PatrolPath_Actor
```

* Patrol points are assigned via an array
* Patrol point `0` is always the starting position

**Options:**

* **Path Looping:** Continuous patrol
* **Path Decrement:** Ping-pong patrol behaviour

---

## Detection and Combat Behaviour

* Sustained visual contact fills the alert bar
* Full alert triggers chase or ranged attacks
* Losing sight initiates a search pattern
* After searching three random points, enemies return to patrol

---

## Special Detection Rules

* **Front collision box:** Immediate alert on overlap
* **Shield enemy rear detection:** Detects player even when crouched
* **Shield enemies** block attacks while alert

---

## Enemy Type Differences

### Knife Enemy

* Chases and attacks in melee
* Cannot detect bodies
* Never raises alarms
* Can be killed from front or back, even when alerted

### Rifle Enemy

* Shoots while chasing
* Detects bodies
* Can raise alarms
* Can be killed from front or back
* Detects player approaching from behind while alert

### Shielded Enemy

* Child class of Rifle Enemy
* Must enable **“Is This Shielded Enemy”** in the Details panel
* Can only be killed from behind while unalerted
* Cannot be killed when alerted
* Blocks all frontal attacks

---

## Turrets

**Blueprint:**

```
Content/Stealth/ActorsBP/Turret_BP
```

* Vision cone detection
* Fires automatically on detection
* Deals **10 damage per hit** (100 total health)

### Customisation

* Fire rate adjustable in the Details panel
* Hack area and vision cone transforms editable in-level or in Blueprint

---

## Cameras

**Blueprint:**

```
Content/Stealth/ActorsBP/Camera_BP
```

* Detect player movement
* Raise alarms
* Optional rotation behaviour

### Features

* Hackable when within hack area
* Vision and hack collision boxes fully configurable
* Rotation can be enabled or disabled via a Boolean

---

## Mission Objective System

The template includes a **sequential objective system** with HUD integration.

### Objective Types

* **Non-Interactive:** Complete by reaching location
* **Interactive:** Require player input to complete

Activate with **F**.

---

## Required Blueprints

* `ObjectiveSystem_BP`
* `ObjectiveUpdate_BP`

---

## Setup Process

1. Place `ObjectiveSystem_BP` in the level
2. Define objective text (displayed on HUD)
3. Add references to `ObjectiveUpdate_BP` actors in order
4. Place one `ObjectiveUpdate_BP` per objective

Objectives will:

* Display sequentially on the HUD
* Update automatically upon completion
* Move the objective marker to the next location

---

## Expected Student Engagement

You are expected to:

* Understand the mechanics provided
* Create blockouts that utilise the mechanics
* Add additional assets to enhance the blockout
* Apply stealth level design principles
* Justify design decisions in assessment

### Artists may:

* Customise visual assets (3D, HUD, etc.)

### Programmers may:

* Extend systems meaningfully
* Read and understand Blueprint logic

### Optionally, you may also:

* Modify parameters and behaviours

---

## Maps and Project Structure

**Example map:**

```
/All/Game/Stealth/ThirdPersonBP/Maps
```

**Your assignment map:**

```
/All/Game/Maps
```

> We recommend duplicating or backing up this map for practice level design.

---

## Future Additions

Additional mechanics will be added or refined in future lessons, including:

* Player lose state
* Collectable items

