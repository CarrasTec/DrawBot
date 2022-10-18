Para más información de cómo instalar librerías, mire: http://www.arduino.cc/en/Guide/Libraries

GRLB_Scara_ArduinoUno

Video:
https://youtu.be/O2PyCFvjfS4

Using diferents versions of GRBL, Scara, ServoTimer2 From this pages:

https://github.com/grbl/grbl
https://github.com/Uniquemf/grbl-stm32-scara
https://github.com/nabontra/ServoTimer2

I build a gbrl library to use GRBL in Arduino uno to control the Drawbot From;

https://www.thingiverse.com/thing:3096135

It has a few details to improve, like the calibration, its dificult to have the real measurements.
If you want to draw a big square is dificult to do just one trace along the paper, because the line is going to be a curve, if you want to have a straight line of 50mm, you have to do it in small steps of 10mm, like:

G01 X0 Y0
G01 X0 Y10
G01 X0 Y20
G01 X0 Y30
G01 X0 Y40
G01 X0 Y50

in my configuration pencil up is Z0, if i want to start writting use Z-1

In the file scara.h you have to edit the parameters according to you configuration, this is the part of the calibration, i hope to find a better method instead of try and measure, my configuration is:

// Length of inner and outer support arms. Measure arm lengths precisely.
#define SCARA_LINKAGE_1 202.0f //200mm
#define SCARA_LINKAGE_2 196.0f //196mm

// SCARA tower offset (position of Tower relative to bed zero position)
// This needs to be reasonably accurate as it defines the printbed position in the SCARA space.

#define SCARA_OFFSET_X -64.41 //-64.41mm
#define SCARA_OFFSET_Y 138.59//138.59mm	

#define MANUAL_X_HOME_POS -57.30f //angle theta in home position: -57.30f
#define MANUAL_Y_HOME_POS 93.83f //angle psi in home position: 93.83f

The pinout is in the file ArduinoUno-DrawBot

My configuration is:

$0=30 (step pulse, usec)
$1=25 (step idle delay, msec)
$2=0 (step port invert mask:00000000)
$3=4 (dir port invert mask:00000100)
$4=0 (step enable invert, bool)
$5=0 (limit pins invert, bool)
$6=0 (probe pin invert, bool)
$10=3 (status report mask:00000011)
$11=0.020 (junction deviation, mm)
$12=0.002 (arc tolerance, mm)
$13=1 (report inches, bool)
$20=0 (soft limits, bool)
$21=1 (hard limits, bool)
$22=1 (homing cycle, bool)
$23=3 (homing dir invert mask:00000011)
$24=25.000 (homing feed, mm/min)
$25=1500.000 (homing seek, mm/min)
$26=250 (homing debounce, msec)
$27=1.000 (homing pull-off, mm)
$100=21.870 (x, step/mm)
$101=21.870 (y, step/mm)
$102=160.000 (z, step/mm)
$110=1500.000 (x max rate, mm/min)
$111=1500.000 (y max rate, mm/min)
$112=200.000 (z max rate, mm/min)
$120=10.000 (x accel, mm/sec^2)
$121=10.000 (y accel, mm/sec^2)
$122=5.000 (z accel, mm/sec^2)
$130=200.000 (x max travel, mm)
$131=200.000 (y max travel, mm)
$132=200.000 (z max travel, mm)

![Drawbot](https://github.com/criscol64/DrawBot/blob/main/Drawbot1.JPG)
