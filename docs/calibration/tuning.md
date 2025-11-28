
## Resonance
Typically, each toolhead board will have its own accelerometer for resonance testing. 
Because of this, each accelerometer needs to be given a unique name so that it can be called directly.

``` cfg title="Example of tool's Nitehawk36 ADXL345 configuration."
[adxl345 T0]
cs_pin: NHK0:gpio27
spi_software_sclk_pin: NHK0:gpio18
spi_software_mosi_pin: NHK0:gpio20
spi_software_miso_pin: NHK0:gpio19
axes_map: x,z,y
```

Klipper's [resonance_tester](https://www.klipper3d.org/Config_Reference.html#resonance_tester){target="_blank"} module only supports a single `accel_chip` to be set at a time. This means that any time you want to run input shaper, the accelerometer chip needs to be defined so that the correct toolhead board is being used. 

You can swap the accelerometer manually by changing the `accel_chip` in [resonance_tester](https://www.klipper3d.org/Config_Reference.html#resonance_tester){target="_blank"}.

``` cfg hl_lines="4" title="Example [input_shaper] & [resonance_tester] sections."
[input_shaper]

[resonance_tester]
accel_chip: adxl345 T0
probe_points: 175,175,20
sweeping_accel: 400
sweeping_period: 0
```

To run resonance tester without changing the `accel_chip` in [resonance_tester](https://www.klipper3d.org/Config_Reference.html#resonance_tester){target="_blank"}, you can specify the accelerometer in the macro's parameters.

``` cfg { .copy title="Shaketune input shaper example." }
AXES_SHAPER_CALIBRATION ACCEL_CHIP="'adxl345 T0'"
```

## Tool Change Speed