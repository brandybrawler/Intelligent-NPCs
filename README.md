# Intelligent NPCs Plugin for Unreal Engine 5

[![INPC Logo](docs/INPC_Logo.png)](docs/INPC_Logo.png)

Bring your Unreal Engine 5 worlds to life with dynamic and believable Non-Player Characters (NPCs) using the **Intelligent NPCs** plugin. Forget complex AI setups and dive into a simple yet powerful system for creating characters with realistic behaviors, needs, and routines, all within the visual scripting environment of Blueprints.

## Table of Contents

*   [Overview](#overview)
*   [Key Features](#key-features)
*   [Getting Started](#getting-started)
    *   [Prerequisites](#prerequisites)
    *   [Setting up Activities](#setting-up-activities)
    *   [Setting up NPCs](#setting-up-npcs)
    *   [Navigation](#navigation)
*   [Activity Types Explained](#activity-types-explained)
*   [Troubleshooting](#troubleshooting)
*   [Support](#support)
*   [Video Demos](#video-demos)
*   [License](#license)

## Overview

This plugin offers a drag-and-drop solution for populating your games with engaging NPCs. Leveraging the power and efficiency of State Trees (instead of traditional Behavior Trees), you can define complex behaviors without sacrificing performance. The entire plugin is built in Blueprints, ensuring ease of understanding, customization, and extension.

## Key Features

*   Drag-and-Drop Simplicity: Integrate NPCs seamlessly into your environment. Simply drag your character blueprints into the level and assign them activities.
*   State Tree Powered AI: An optimized state tree system provides a robust and flexible framework for defining complex NPC behaviors with excellent performance.
*   Blueprint-Based Flexibility: Fully customizable and extensible using the visual scripting power of Blueprints.
*   Variety of Activities: NPCs can roam around, get hungry, eat, perform random actions (sitting, sleeping, etc.), and even hold jobs with dedicated workstations.
*   Optimized Performance: High-performance AI that won't bog down your game.
*   No C++ Required: Perfect for designers and artists who want to create compelling NPC behavior.
*   Create Immersive Worlds: Breathe life into your game environments.

## Getting Started

### Prerequisites

Before using the Intelligent NPCs plugin, ensure the following plugins are enabled in your Unreal Engine project:

![Plugins](docs/INPC_Plugins.png)

1.  **StateTree:** This is essential for the plugin's core functionality.
2.  **GameplayStateTree:** This plugin complements the StateTree plugin.

**To enable these plugins:**

1.  Go to **Edit -> Plugins** in the Unreal Engine Editor.
2.  Search for "StateTree" and "GameplayStateTree."
3.  Check the "Enabled" box for each plugin.
4.  Restart the Unreal Engine editor.

### Setting up Activities

Activities define what your NPCs can do in the world. These are created using the `BP_BaseActivityActor`.

1.  **Drag and Drop:** Drag the `BP_BaseActivityActor` from the Content Browser into your level.

2.  **Configure Activity Type:** In the Details panel of the placed actor, set the `Activity Type`. The available activity types are:

    *   **Sandbox:** Allows the NPC to randomly interact with the activity actor. This is the default.
    *   **Roaming:** Makes the NPC randomly walk around the map.
    *   **Talking:** Allows the NPC to randomly talk to other nearby NPCs.
    *   **Food:** Designates the actor as a food source. NPCs will go to the nearest unoccupied food source when hungry.
    *   **Work:** Marks the actor as a workstation for a specific NPC with a job.

    ![Activity Type Enum](docs/INPC_ActiviyTypeEnums.png)

3.  **Activity Time:** Set the `Activity Time` value. This determines how long the NPC will spend performing the activity.

4.  **Activity Montage:** Set the `Activity Montage` to the animation montage the NPC should play while performing the activity.

5.  **Food Source (Food Activity Type Only):** If the `Activity Type` is set to `Food`, check the `Food?` variable in the Details panel. This is *crucial* for the AI to recognize the actor as a food source.

    ![Activity Actor Details Panel](docs/INPC_ActivityActorDetails.png)

### Setting up NPCs

1.  **Drag and Drop:** Drag the `BP_BaseAiCharacter` actor into your level.

2.  **Configure NPC Behavior:** In the Details panel of the placed actor, configure the following:

    *   **Activity Type:** Set the initial `Activity Type` for the NPC. This determines the NPC's default behavior (roaming, talking, sandbox interactions). This setting can be overridden by hunger or job requirements.

    *   **Has A Job:** Check this box if the NPC should have a job.

    *   **Workstation (If Has A Job is True):** If `Has A Job` is checked, you *must* select a `Workstation` actor. Use the eyedropper tool to select an activity actor in the level that has its `Activity Type` set to `Work`.

    > **Important:** Each NPC that has a job *must* have a unique workstation. Do not assign multiple NPCs to the same workstation.

    ![NPC Details Panel](docs/INPC_npcDetails.png)

### Navigation

The AI characters require a NavMesh to move around the level.

1.  **Add Nav Mesh Bounds Volume:** Drag a `Nav Mesh Bounds Volume` into your level.
2.  **Resize and Place:** Resize the volume to encompass the area where you want the NPCs to be able to move.
3.  **Rebuild Navigation:**

    *   Press the 'P' key to visualize the navmesh.
    *   Then, press the "Build" button in the main toolbar to generate the navigation mesh. The walkable areas will be highlighted in green.

4.  **Restart Level:** Restart the level for the navigation mesh to build.

## Activity Types Explained

The `Activity Type` enum dictates the primary behavior of the NPC. Here's a breakdown:

*   **Sandbox:** The NPC will randomly interact with `BP_BaseActivityActor` instances in the level that are also set to `Sandbox`. This is the default activity type.
*   **Roaming:** The NPC will wander randomly around the level within the bounds of the NavMesh.
*   **Talking:** The NPC will attempt to engage in conversation with other nearby NPCs.
*   **Food:** (Used in conjunction with the `Food?` flag on Activity Actors) When the NPC's hunger level is high enough, it will seek out the nearest unoccupied `BP_BaseActivityActor` that has its `Activity Type` set to `Food` and the `Food?` flag checked.
*   **Work:** (Used in conjunction with the `Has A Job` and `Workstation` variables on the NPC) The NPC will exclusively interact with its assigned `Workstation` actor, unless it gets hungry, in which case it will seek out a `Food` activity.

## Troubleshooting

*   **NPCs not moving:**

    *   Ensure you have a `Nav Mesh Bounds Volume` in the level.
    *   Verify that the navigation mesh has been built.
    *   Confirm that the NPC is within the bounds of the NavMesh.
*   **NPCs not interacting with activities:** Double-check that the `Activity Type` on both the NPC and the `BP_BaseActivityActor` are set correctly. For food, make sure the `Food?` flag is checked.
*   **NPCs stuck at workstations:** Confirm that only one NPC is assigned to a given `Work` activity actor.

## Support

For support or questions, please contact [Your Support Email/Forum Link Here].

## Video Demos

*   **Initial Setup:** [https://youtu.be/-mnQs1wSNp4](https://youtu.be/-mnQs1wSNp4)
*   **Workplace Setup:** [https://youtu.be/INQquO3Y9Nc](https://youtu.be/INQquO3Y9Nc)

## License

[Your License Information Here]
