//
M591 D0 P7 C"e0stop" L7 R50:200 E15 S0 ; M591: Configure BTT Smart Filament Sensor
//


M591
Back to the Gcode Dictionary

M591: Configure filament sensing
This configures filament sensing for the specified extruder. The sensor may be a simple filament presence detector, or a device that measures movement of filament, or both. The action on a filament error is to run filament-error#.g (RRF 3.2 and later, where # is the extruder number), failing that run filament-error.g (RRF 3.2 and later), or failing that run pause.g (RRF 1.19 and later) to pause the print and advise you that there has been a filament error. Note that filament monitoring in RRF is only active when printing from SD card.

M591 - RepRapFirmware 3
Parameters

Dnn Extruder drive number (0, 1, 2...),
Pnn Type of sensor:
0=none
1=simple sensor (high signal when filament present)
2=simple sensor (low signal when filament present)
3=Duet3D rotating magnet sensor
4=Duet3D rotating magnet sensor with microswitch
5 = Duet3D laser sensor
6 = Duet3D laser sensor with microswitch
7 = pulse-generating sensor
C"name" Pin name the filament sensor is connected to (RRF3 only), see Pin Names
Sn 0 = disable filament monitoring (default), 1 = enable filament monitoring when printing from SD card. Supported for all filament sensor types in firmwares 1.21.1 and in 2.0 and later. In firmware 1.21 this parameter is not supported for sensor types 1 and 2. Filament monitors accumulate calibration data (where applicable) even when filament monitoring is disabled.
Additional parameters for Duet3D laser filament monitor

Raa:bb Allow the filament movement reported by the sensor to be between aa% and bb% of the commanded values; if it is outside these values and filament monitoring is enabled, the print will be paused
Enn minimum extrusion length before a commanded/measured comparison is done, default 3mm
An (firmware 2.03 and later) 1 = check All extruder motion, 0 (default) = only check extruder motion of printing moves (moves with both movement and forward extrusion)
Lnn (firmware 3.2 and later) Calibration factor, default 1.0. The filament movement reported by the laser sensor is multiplied by this value before being compared with the commanded extrusion. Intended for use with sensors that use the laser to read movement of a wheel that is turned by the filament.
Additional parameters for Duet3D rotating magnet filament monitor

Lnn Filament movement per complete rotation of the sense wheel, in mm
R, E, A As for Duet3D laser filament monitor
Additional parameters for a pulse generating filament monitor

Lnn Filament movement per pulse in mm
R, E As for Duet3D laser filament monitor
Example

M591 P3 C"e0stop" S1   D0 ; filament monitor connected to E0 endstop
M591 - RepRapFirmware 1.21 to 2.x
Parameters

As RRF3, except 'C' parameter is the endstop number.

Cnn Which input the filament sensor is connected to. On Duet electronics: 0=X endstop input, 1=Y endstop input, 2=Z endstop input, 3=E0 endstop input etc. If you have a Duex 2 or Duex 5 in your system, note that C5 thru C9 (the endstop inputs on the DueX) cannot be used for filament monitors, but C10 and C11 (the endstop inputs on the CONN_LCD connector) can.
Example

M591 D0 P3 C3 S1 R70:130 L24.8 E3.0   ; Duet3D rotating magnet sensor for extruder drive 0 is connected to E0 endstop input, enabled, sensitivity 24.8mm.rev, 70% to 130% tolerance, 3mm detection length


M591 D0    ; display filament sensor parameters for extruder drive 0
M591 - RepRapFirmware 1.20 and earlier
Parameters

Dnn Extruder drive number (0, 1, 2...),
Pnn Type of sensor, where:
0=none,
1=simple sensor (high signal when filament present)
2=simple sensor (low signal when filament present)
3=Duet3D rotating magnet sensor
4=Duet3D rotating magnet sensor with microswitch
Cn Which input the filament sensor is connected to. On Duet electronics: 0=X endstop input, 1=Y endstop input, 2=Z endstop input, 3=E0 endstop input etc.
Additional parameters for Duet3D rotating magnet filament monitor

Snn Sensitivity, in mm of filament movement per complete rotation of the sense wheel.
Rnn Tolerance as a percentage of the commanded extrusion amount. A negative value puts the firmware in calibration mode.
Enn minimum extrusion length before a commanded/measured comparison is done, default 3mm
Examples

M591 D0 P5 C3  R70:140 E3.0 S1   ; Duet3D rotating magnet sensor for extruder drive 0 is connected to E0 endstop input, sensitivity 1.05, tolerance 70% to 140%, 3mm detection length
M591 D1 ; display filament sensor parameters for extruder drive 1
Documentation

Duet3d Filament Monitor: Rotating Magnet Version
Duet3d Filament Monitor: Laser Version
Connecting and configuring filament-out sensors

M591 D0 P7 C"e0stop" L7 R50:200 E15 S0
