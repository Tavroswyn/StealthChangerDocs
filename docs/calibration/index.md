# Calibration Overview



Calibration requires three main steps:

1. [z_offset](z_offset.md)
2. [Docking Path](ToolChanger.md)
3. [Dock calibration](dock_locations.md)
4. [G-code offsets](nozzle_offsets.md)

This page is a high-level overview. Use it to understand what needs to be calibrated and where it lives in the config before diving into the step-by-step guides.

---

## 1. [z_offset](z_offset.md)

The first step is establishing a **probe-based Z reference** for each tool.

- **Config section:** `[tool_probe Tn]` in your tool config
- **Parameter:** `z_offset`

### What is `z_offset`?

The `z_offset` is used when the printer homes or levels the bed, it tells Klipper the vertical distance between your probe's trigger point and the nozzle tip. When the probe triggers during homing or mesh leveling, Klipper uses this offset to calculate where Z=0 is for that specific nozzle.

Each tool could have a different `z_offset` because:

- Assembly tolerances can differ.
- Travel between the nozzle's zero point and the sensor's trigger point can vary


With correct `z_offset` values, probing with any tool produces an accurate nozzle-to-bed reference, which is essential for consistent first layers.

---

## 2. [Docking Settings](toolchanger.md)

- **Config section:** `[toolchanger]`
- **Parameters:** `safe_y`, `close_y`, `dropoff_path`, `pickup_path`

### What are the docking settings?

The docking settings define the Y-axis movement pattern used during tool changes. It includes:

- `safe_y`: Absolute Y position where the shuttle with mounted tool won't hit any docked tools
- `close_y`: absolute Y position where the shuttle can safely move behind the docks
- `dropoff_path`: The path the shuttle follows when dropping off a tool
- `pickup_path`: The path the shuttle follows when picking up a tool

---

## 3. [Dock calibration](dock_locations.md)

Dock calibration ensures the printer can reliably pick up and park tools in their docks without collisions.


- **Config section:** `[tool Tn]` for each tool
- **Parameters:** `params_park_x`, `params_park_y`, `params_park_z`
### What are park positions?

The park position is the exact X/Y/Z coordinate where the shuttle aligns with a docked tool so they can mechanically couple. Think of it as the "pickup point" for that specific dock.

**Why each tool needs its own park position:**

- Docks are physically mounted at different locations along the front of the printer
- Even small positional errors can cause the shuttle to miss the tool or collide with the dock

**Shared parameters** like `params_close_y` and `params_safe_y` can be overiten per tool if needed.

- `params_close_y`: How close the shuttle can safely move behind the docks
- `params_safe_y`: A fully clear Y position where the shuttle won't hit any docked tools

With accurate park positions, tool changes become repeatable and collision-free.

---

## 4. G-code offsets

Finally, you align where each nozzle actually prints so that tools agree on Z height and X/Y position on the bed.

- **Config section:** `[tool Tn]`
- **Typical fields:**
  - `gcode_z_offset`
  - `gcode_x_offset`
  - `gcode_y_offset`

### What are G-code offsets?

G-code offsets compensate for the physical differences between tools so they all behave as if they're in the same position:

- **`gcode_z_offset`**: Adjusts the effective Z height so all tools produce the same first-layer squish. Even after probe calibration, nozzles may sit at slightly different heights due to manufacturing tolerances.

- **`gcode_x_offset` and `gcode_y_offset`**: Shift the tool's X/Y position so all nozzles land on the same spot when given identical G-code coordinates. Without these, a multi-tool print would have visible misalignment between layers printed by different tools.

**Why G-code offsets matter:**

When your slicer generates `G1 X100 Y100`, every tool should deposit filament at exactly the same physical location on the bed. G-code offsets make this possible by telling Klipper "this tool is 0.2mm left and 0.1mm forward of the reference tool, so adjust accordingly."

### Calibration Methods

There are several ways to measure these offsets:

- **SexBall Probe** – Mechanical probe using precision spheres for repeatable measurements
- **Axiscope** – Camera-based visual alignment to printed targets
- **Nudge** – Software-guided iterative calibration using printed patterns

---

See the [Nozzle Offsets](nozzle_offsets.md) page for detailed instructions on each method.
