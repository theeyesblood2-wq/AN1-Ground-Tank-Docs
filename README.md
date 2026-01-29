# AN1 Ground Tank (UE 5.7) — Quick Start

**AN1** is a plug-and-play ground tank framework for Unreal Engine 5.7.  
No DefaultEngine.ini edits required — import the plugin, assign assets, wire inputs, hit Play.

- **Engine:** UE 5.7
- **Example Content:** BP_Tank (add your own mesh/FX/audio)
- **Support:** jbkm66777@gmail.com

> This plugin is content-free. You must provide your own tank meshes/materials/VFX/SFX.

---

## Install
1. Copy the plugin into: `YourProject/Plugins/AN1_Ground_Tank/`
2. Enable it in **Edit → Plugins**
3. Restart the editor

---

## Quick Start (5–10 minutes)
1. Create a **Blueprint** project (Games → Blank is fine).
2. Enable the plugin and restart.
3. Drag **BP_Tank** into the level.
4. Assign required assets (minimum):
   - Tank skeletal mesh / collision root setup (per example BP)
   - Weapon assets (optional, can be empty for movement-only test)
5. Wire inputs (see next section).
6. Press **Play**.

---

## Input Setup (Legacy Input)

Project Settings → **Input**

> If you use **Enhanced Input**, create equivalent Actions/Axes and call the same Blueprint functions shown below.

### Axis Mappings
- `MoveForward` (W +1, S -1)
- `Turn` (D +1, A -1)
- `LookUp` (Mouse Y)
- `LookRight` (Mouse X)
- `CameraZoomAxis` (Mouse Wheel Axis) — TPP/FPP/Gunner zoom
- `MonitorZoomin_Out` (Mouse Wheel Axis or custom axis) — Turret monitor zoom (hold-style)

### Action Mappings
- `Brake` (Space)
- `Aim` (Right Mouse) — hold
- `FireMG` (Left Mouse) — hold
- `FireTurret` (Left Ctrl) — press
- `DeploySmoke` (G) — press
- `ToggleCamera` (C) — press (TPP ↔ Gunner)
- `CameraReset` (R or Middle Mouse) — press
- `DriverFPP_Toggle` (V) — press (TPP ↔ Driver FPP)
- `DriverFPP_TurretAim_Toggle` (B) — press
- `MonitorResetZoom` (R) — press

Optional (monitor zoom as buttons instead of axis):
- `MonitorZoom_In` (MouseWheelUp or key)
- `MonitorZoom_Out` (MouseWheelDown or key)

---

## Blueprint wiring (BP_Tank)

### Movement
- `InputAxis MoveForward` → `MoveForward(Value)` *(Target: self / AN1 Tank Base)*
- `InputAxis Turn` → `MoveRight(Value)` *(Target: self / AN1 Tank Base)*
- `Brake` pressed → `SetBrake(InBrake=1.0)` *(Target: PhysicsMovement / AN1 Physics Tank Movement Component)*
- `Brake` released → `SetBrake(InBrake=0.0)` *(Target: PhysicsMovement)*

### Look
- `InputAxis LookUp` → `LookUp(AxisValue)` *(Target: self / AN1 Tank Base)*
- `InputAxis LookRight` → `LookRight(AxisValue)` *(Target: self / AN1 Tank Base)*

### Camera zoom + reset (TPP/FPP/Gunner)
- `InputAxis CameraZoomAxis` → `CameraZoomAxis(AxisValue)` *(Target: self / AN1 Tank Base)*
- `CameraReset` pressed → `CameraReset()` *(Target: self / AN1 Tank Base)*

### Toggle camera (TPP ↔ Gunner)
- `ToggleCamera` pressed → `ToggleCamera()` *(Target: self / AN1 Tank Base)*

### Driver FPP toggles
> These functions work only when the relevant TPP/Driver FPP camera mode is active.
- `DriverFPP_Toggle` pressed → `ToggleDriverFPP()` *(Target: self / AN1 Tank Base)*
- `DriverFPP_TurretAim_Toggle` pressed → `ToggleDriverFPPTurretAim()` *(Target: self / AN1 Tank Base)*

### Aim / Weapons / Smoke
- `Aim` pressed → `AN1 SetTPPAimHeld(true)` *(Target: self / AN1 Tank Skeletal)*
- `Aim` released → `AN1 SetTPPAimHeld(false)` *(Target: self / AN1 Tank Skeletal)*
- `FireMG` pressed → `StartFireMG()` *(Target: TankWeapons / AN1 Tank Weapon Component)*
- `FireMG` released → `StopFireMG()` *(Target: TankWeapons)*
- `FireTurret` pressed → `FireTurretOnce()` *(Target: TankWeapons)*
- `DeploySmoke` pressed → `DeploySmoke()` *(Target: TankWeapons)*

### Turret Monitor zoom
Hold-style (axis):
- `MonitorResetZoom` pressed → `MonitorResetZoom()` *(Target: self / AN1 Tank Base)*
- `InputAxis MonitorZoomin_Out` → `MonitorZoomAxis(AxisValue)` *(Target: self / AN1 Tank Base)*

Optional (button-style):
- `MonitorZoom_In` pressed → `MonitorZoomIn()` *(Target: self / AN1 Tank Base)*
- `MonitorZoom_Out` pressed → `MonitorZoomOut()` *(Target: self / AN1 Tank Base)*

---

## Recommended Physics Settings (especially for multiplayer)
Project Settings:
- Engine → Physics → Framerate: **Tick Physics Async** *(recommended)*
- Engine → Physics → Replication: **Enable Physics Prediction**
- Engine → Physics → Replication: **Enable Physics History Capture**

AN1 works without these, but prediction/history capture improves resimulation stability for networked physics.

---

## Customization

### Animation
Create your own AnimBP and set Parent Class to `AN1TankAnimInstance`.  
Use exposed variables (Pitch/Roll, throttle response, turret yaw/cannon pitch, running gear arrays) to drive your bone transforms.

### Projectiles / FX
Create `BP_Shell`, `BP_Tracer`, `BP_Smoke` derived from AN1 base classes.  
Assign these Blueprint classes in the Tank’s Weapon Component.

---

## Troubleshooting

### Tank doesn’t move
- Confirm BP_Tank is possessed (Auto Possess Player = Player 0 for quick tests).
- Confirm your axis mappings are created and events fire in BP.
- Confirm Brake isn’t stuck at 1.0.

### Aim / turret not moving
- Confirm Aim is enabled in BP settings and you’re holding the Aim input (if configured).
- Confirm you’re testing as the owning client (some HUD/aim visuals are owner-only).

### Multiplayer looks jittery
- Enable Tick Physics Async + Physics Prediction + Physics History Capture.
- Test Listen Server + 1 Client first.

---
## More Documentation
- [Inputs / Keybinds (Blueprint wiring screenshots)](INPUTS.md)
- [Settings Reference (screenshots)](SETTINGS_REFERENCE.md)

---
## Support
Email: **jbkm66777@gmail.com**
