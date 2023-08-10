## BigTreeTech SFS V1.0

### Firmware Config for `Filament blockage detection`
  * Marlin
    1. uncomment `#define FILAMENT_RUNOUT_SENSOR`.<br/>
       <img src=Images/marlin_fil.png width="800" /><br/>
    2. uncomment `#define FILAMENT_RUNOUT_DISTANCE_MM 7` and set it to 7mm (The detection accuracy of SFS V1.0 is 7mm).
    3. uncomment `#define FILAMENT_MOTION_SENSOR`
    4. The filament sensor feature of Marlin also needs to enable `#define NOZZLE_PARK_FEATURE` and `#define ADVANCED_PAUSE_FEATURE`. please uncomment `#define NOZZLE_PARK_FEATURE` and `#define ADVANCED_PAUSE_FEATURE` and set specific parameters according to your printer.
    5. If you are using the Serial Touch Screen of BigTreeTech, please enable the features in Marlin according to the requirements [here](https://github.com/bigtreetech/BIGTREETECH-TouchScreenFirmware#marlin-dependencies)
        * We recommended to plug SFS V1.0 into the motherboard not Touch Screen, In this case, the Marlin configuration is as described above, and the Touch Screen `config.ini` file needs to be set according to [here](https://github.com/bigtreetech/BIGTREETECH-TouchScreenFirmware/blob/f7ccb050a7a2fe78ff5204561113fa0d27b0dd10/Copy%20to%20SD%20Card%20root%20directory%20to%20update/config.ini#L634)
        * When the SFS V1.0 is plugged into the Touch Screen, comment out `#define FILAMENT_RUNOUT_SENSOR` in Marlin to disable detection of Marlin and uncomment `#define M114_DETAIL` for Touch Screen, And enable detection of Touch Screen in `config.ini` file, set `fil_runout:1` to enable detection and `fil_runout_distance:7` for accuracy.
  * RepRapFirmware
    1. Add `M591 D0 P7 C"zstopmax" L7 R75:125 E22 S1` in `config.g`, changing the endstop pin name according to your motherboard.<br/>
    ***If you are using the Serial Touch Screen of BigTreeTech, The SFS V1.0 of RRF can only be plugged into the motherboard, and Touch Screen does not need additional config for SFS V1.0***
  * Klipper
    ```
    [filament_motion_sensor encoder_sensor]
    detection_length: 7
    #   The minimum length of filament pulled through the sensor to trigger
    #   a state change on the switch_pin
    #   Default is 7 mm.
    extruder: extruder
    #   The name of the extruder section this sensor is associated with.
    #   This parameter must be provided.
    switch_pin: PA9
    # changing the switch_pin name according to your motherboard
    #pause_on_runout: True
    #runout_gcode:
    #insert_gcode:
    #event_delay:
    #pause_delay:
    ```

## BigTreeTech SFS V2.0

### Firmware Config for `Filament blockage detection`
  * Marlin
    1. uncomment `#define FILAMENT_RUNOUT_SENSOR`.<br/>
       <img src=Images/marlin_mot.png width="800" /><br/>
    2. uncomment `#define FILAMENT_RUNOUT_DISTANCE_MM 3` and set it to 3mm (The detection accuracy of SFS V2.0 is 2.88mm, We set it to 3mm to leave some error margin).
    3. uncomment `#define FILAMENT_MOTION_SENSOR`
    4. uncomment `#define FILAMENT_SWITCH_AND_MOTION`
    5. uncomment `#define FIL_MOTION1_PIN gpio_xx` set motion pin to actual GPIO of motherboard
    6. The filament sensor feature of Marlin also needs to enable `#define NOZZLE_PARK_FEATURE` and `#define ADVANCED_PAUSE_FEATURE`. please uncomment `#define NOZZLE_PARK_FEATURE` and `#define ADVANCED_PAUSE_FEATURE` and set specific parameters according to your printer.
    7. If you are using the Serial Touch Screen of BigTreeTech, please enable the features in Marlin according to the requirements [here](https://github.com/bigtreetech/BIGTREETECH-TouchScreenFirmware#marlin-dependencies)
        * We recommended to plug SFS V2.0 into the motherboard not Touch Screen, In this case, the Marlin configuration is as described above, and the Touch Screen `config.ini` file needs to be set according to [here](https://github.com/bigtreetech/BIGTREETECH-TouchScreenFirmware/blob/f7ccb050a7a2fe78ff5204561113fa0d27b0dd10/Copy%20to%20SD%20Card%20root%20directory%20to%20update/config.ini#L634)
        * When the SFS V2.0 is plugged into the Touch Screen, comment out `#define FILAMENT_RUNOUT_SENSOR` in Marlin to disable detection of Marlin and uncomment `#define M114_DETAIL` for Touch Screen, And enable detection of Touch Screen in `config.ini` file, set `fil_runout:1` to enable detection and `fil_runout_distance:3` for accuracy.
  * RepRapFirmware
    1. Add `M591 D0 P7 C"zstopmax" L2.88 R75:125 E9 S1` in `config.g`, changing the endstop pin name according to your motherboard.<br/>
    ***If you are using the Serial Touch Screen of BigTreeTech, The SFS V2.0 of RRF can only be plugged into the motherboard, and Touch Screen does not need additional config for SFS V2.0***
  * Klipper
    ```
    [filament_switch_sensor switch_sensor]
    switch_pin: gpio_xx
    pause_on_runout: False
    runout_gcode:
      PAUSE # [pause_resume] is required in printer.cfg
      M117 Filament switch runout
    insert_gcode:
      M117 Filament switch inserted

    [filament_motion_sensor encoder_sensor]
    switch_pin: gpio_xx
    detection_length: 2.88
    extruder: extruder
    pause_on_runout: False
    runout_gcode:
      PAUSE # [pause_resume] is required in printer.cfg
      M117 Filament encoder runout
    insert_gcode:
      M117 Filament encoder inserted
    ```
