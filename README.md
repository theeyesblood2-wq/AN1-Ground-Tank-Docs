# AN1 Ground Tank (UE 5.7) — Quick Start

**AN1** is a plug-and-play ground tank framework for Unreal Engine 5.7.
No DefaultEngine.ini edits required — import the plugin, assign assets, wire inputs, hit Play.

- Engine: **UE 5.7**
- Example Content: **BP_Tank** (add your own mesh/FX/audio)

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

### Axis Mappings
- `MoveForward` (W +1, S -1)
- `Turn` (D +1, A -1)

### Action Mappings
- `Brake` (Space)
- `Aim` (Right Mouse)
- `FireMG` (Left Mouse)
- `FireTurret` (Left Ctrl) *(or any key you want)*
- `DeploySmoke` (G)
- `ToggleDriverFPP` (V)
- `ToggleDriverFPPTurretAim` (B)
- `MonitorResetZoom` (R)
- `MonitorZoomIn` (MouseWheelUp)
- `MonitorZoomOut` (MouseWheelDown)

### Blueprint wiring (BP_Tank)
- `InputAxis MoveForward` → `MoveForward(Value)`
- `InputAxis Turn` → `MoveRight(Value)`
- `Brake` pressed/released → `SetBrake(1.0 / 0.0)`
- `Aim` pressed/released → `AN1 SetTPPAimHeld(true/false)`
- `FireMG` pressed/released → `StartFireMG / StopFireMG`
- `FireTurret` pressed → `FireTurretOnce`
- `DeploySmoke` pressed → `DeploySmoke`
- `MonitorResetZoom` → `MonitorResetZoom`
- `MonitorZoom*` → `MonitorZoomIn / MonitorZoomOut` (or axis if you use one)
- `ToggleDriverFPP` → `ToggleDriverFPP`
- `ToggleDriverFPPTurretAim` → `ToggleDriverFPPTurretAim`

---

## Recommended Physics Settings (especially for multiplayer)
Project Settings:
- Engine → Physics → Framerate: **Tick Physics Async** (recommended)
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
**Tank doesn’t move**
- Confirm BP_Tank is possessed (Auto Possess Player = Player 0 for quick tests).
- Confirm your axis mappings are created and events fire in BP.
- Confirm Brake isn’t stuck at 1.0.

**Aim / turret not moving**
- Confirm Aim is enabled in BP settings and you’re holding the Aim input (if configured).
- Confirm you’re testing as the owning client (some HUD/aim visuals are owner-only).

**Multiplayer looks jittery**
- Enable Tick Physics Async + Physics Prediction + Physics History Capture.
- Test Listen Server + 1 Client first.

---

## Support
Email: jbkm66777@gmail.com

