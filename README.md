# mag3110-python
A python driver for the mag3110 magnetometer 

# Usage:
Assuming you've downloaded the repo to somewhere in your $PYTHONPATH

```python
import mag3110

compass = mag3110.compass()
print compass.rawMagnetometer()

```
This will print out the x,y,z and temperature of the sensor. However this isn't much good becuase its uncalibrated. Fearnot! I have implmented a basic calibration system that will allow you to create, save and load calibrations at will!

## Calibration:

```python
import mag3110

compass = mag3110.compass()
print compass.calibrate()
```
This will print out `Starting Debug, please roate the magnetomiter about all axis` Everytime the sensor moves it will then print out a JSON dump of the high and low for each dimension x, y & z. Rotate the sensor to cover as many different rotations as possible.

You'll reach a point where the min/max JSON dumps will stop updating, `ctrl-c` to exit the calibration and save the result.

## using calibration:
```python
import mag3110

compass = mag3110.compass()
compass.loadCalibration()
print compass.rawMagnetometer()
```
The output should be roughly calibrated. Well at least all axes will roughly line up around 0,0

## Finding north:
Assuming the sensor is perfectly flat, you can get a bearing between magnetic north and the direction the X axis is pointing in by doing this:

```python
import mag3110

compass = mag3110.compass()
compass.loadCalibration()
while True:
  print compass.getBearing()
```
Sadly I've not managed to integrate the Z axis to compensate for tilting. If you manage the maths (It should be possible, Plotting on a 3D scatter shows a nice spheroid.) please let me know!

