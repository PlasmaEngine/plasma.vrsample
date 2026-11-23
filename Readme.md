# VR Sample

A small room-scale playground for trying out VR in Plasma. Open this folder as a project in the editor, open
`Scenes/Playground.plScene` and use **Play in VR**, or run it in the Player with `-xr on`.

## What is in the scene

| Object | What it shows |
| --- | --- |
| **Player** | The XR rig: a `plStageSpaceComponent` (standing) and a `plXRTurnComponent` (snap turn on the right stick). |
| Player / **Head** | `plDeviceTrackingComponent` on the HMD and the main camera. |
| Player / **Left Grip**, **Right Grip** | Controller tracking at the grip pose, a `plXRHandComponent` to pick things up and a `plXRControllerModelComponent` that shows the runtime's controller model. |
| Player / **Left Aim** | Controller tracking at the aim pose and a `plXRTeleportComponent`: push the left stick forward to aim the arc, let go to teleport. |
| Player / **Right Aim** | Controller tracking at the aim pose and a `plXRPointerComponent`: a laser pointer that sends enter, exit and click events (click = trigger). Nothing in the scene reacts to them yet. |
| **Table** | Two cubes (held where you grab them) and two balls (snap into the hand). Squeeze the grip to pick one up, let go to throw it. |
| **Crate A/B/C** | A small stack to throw things at. The crates can be picked up too. |
| **Platform** | A raised block to teleport onto. |
| **Door** | A door on a hinge (`plJoltHingeConstraintComponent`, ±100°) in a frame left of the table. Push it open with an open hand. |

**Pulling things out of reach:** with an open hand, point at a grabbable object; a gold ring marks it and the controller
ticks. Squeeze the grip to lock on (the ring turns red), then flick your wrist up towards you. The object flies to you on
an arc: keep the grip squeezed to catch it.

**Hands:** SteamVR has no controller models for OpenXR, so each controller shows its fallback mesh, a small white sphere
(`Meshes/HandProxy.plMeshAsset`).

Everything else is level dressing: a checker floor, two pillars, the sky and a sun.

## Packages

| Package | Why |
| --- | --- |
| `plasma.openxr` | Talks to the headset through OpenXR. |
| `plasma.xrtoolkit` | The hand, pointer, teleport and turn components. |
| `plasma.jolt` | Physics for the grabbable objects, and the surfaces the teleport arc lands on. |

Requires Windows and Plasma Engine 0.12.2. The packages are listed in `Editor/Packages.ddl` (Jolt 1.3.2, OpenXR 1.3.2
and XR Toolkit 1.0.0) and come from the package registry: the first time the editor opens the project, it offers to
install them into `Plugins/`, which is not checked in.

## Without a headset

The XR config in the Default asset profile has XR enabled. When OpenXR cannot start (no headset or no runtime), the game
logs an error and starts without XR, in a normal window looking out from the head's default height of 1.7 m. Run with
`-xr off` to skip XR on purpose.
