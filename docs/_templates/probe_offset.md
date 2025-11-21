### Probe offset
The last step before being able to print again is to calibrate your probe offsets. This procedure is different depending on whether you are using TAP or an Eddy current sensor for probing.

=== "TAP"
    1. Ensure that your [tool_probe](../configuration/tool.md#tool_probe) section's `z_offset` variable is set to `0`.
    2. Home the printer with `G28`.
    3. Run `QUAD_GANTRY_LEVEL`.
    4. Run `G28 Z`.
    5. Run `PROBE_CALIBRATE`.
    6. Change the `z_offset` variable in the tool's [[tool_probe]](../configuration/tool.md#tool_probe) section.

    !!! caution "SAVE_CONFIG"
        Because klipper-toolchanger-easy reroutes probe to each tool object, when you run `SAVE_CONFIG` it saves the values to `[probe]`. Having a `[probe]` section in your config while also having `[tool_probe]` will cause issues with Klipper. `SAVE_CONFIG` should be avoided.

        If you do save the values, you will need to move the offset from the bottom of `printer.cfg` to your tools `[tool_probe]` section.

=== "Eddy Current"
    Set the probe offset as per your Sensor's documentation.