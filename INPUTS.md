# AN1 Inputs & Blueprint Wiring (Legacy Input)

Project Settings → **Input**

> If you use **Enhanced Input**, create equivalent Actions/Axes and call the same Blueprint functions shown here.

---

## Movement + Brake

**Axis Mappings**
- `MoveForward` (W +1, S -1)
- `Turn` (D +1, A -1)

**Action Mappings**
- `Brake` (Space)

**BP Wiring (BP_Tank)**
![](Images/INPUTS/Screenshot%202026-01-29%20002611.png)

---

## Look Up / Right

**Axis Mappings**
- `LookUp` (Mouse Y)
- `LookRight` (Mouse X)

**BP Wiring (BP_Tank)**
![](Images/INPUTS/Screenshot%202026-01-29%20003044.png)

---

## TPP/FPP/Gunner Zoom + Reset

**Axis Mappings**
- `CameraZoomAxis` (Mouse Wheel Axis)

**Action Mappings**
- `CameraReset`

**BP Wiring (BP_Tank)**
![](Images/INPUTS/Screenshot%202026-01-29%20002623.png)

---

## Toggle Camera (TPP ↔ Gunner)

**Action Mappings**
- `ToggleCamera`

**BP Wiring (BP_Tank)**
![](Images/INPUTS/Screenshot%202026-01-29%20002629.png)

---

## Driver FPP Toggles

**Action Mappings**
- `DriverFPP_Toggle`
- `DriverFPP_TurretAim_Toggle`

> Works only when the relevant TPP/Driver FPP camera mode is active.

**BP Wiring (BP_Tank)**
![](Images/INPUTS/Screenshot%202026-01-29%20002634.png)

---

## Aim / FireMG / FireTurret / Smoke

**Action Mappings**
- `Aim` (hold)
- `FireMG` (hold)
- `FireTurret` (press)
- `DeploySmoke` (press)

**BP Wiring (BP_Tank)**
![](Images/INPUTS/Screenshot%202026-01-29%20002647.png)

---

## Turret Monitor Zoom (Hold-style)

**Axis Mappings**
- `MonitorZoomin_Out`

**Action Mappings**
- `MonitorResetZoom`

**BP Wiring (BP_Tank)**
![](Images/INPUTS/Screenshot%202026-01-29%20002653.png)

---

## Turret Monitor Zoom (Button-style, optional)

**Action Mappings**
- `MonitorZoom_In`
- `MonitorZoom_Out`

**BP Wiring (BP_Tank)**
![](Images/INPUTS/Screenshot%202026-01-29%20002729.png)
