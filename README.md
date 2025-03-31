# imu-fusion
This is a portfolio repo. No code is visible.

This project explores the domains of control theory and linear algebra through the use of sensor-fusion, Kalman filters, and other signal processing techniques to develop a small-boat performance tracker capable of dead-reckoning and cm level absolute postional accuracy.

## Hardware
Bosch Sensortec BNO055 9 DoF IMU
u-blox ZED-F9R GNSS and IMU

## Processing
Data streams from the IMU and GNSS co-processors are synthesized in real-time as well as data-logging at 10Hz for asynchronus analysis. The device-level software utilizes gain filtering, Butterworth and Kalman filters to perform real-time sensor fusion and compensate for integration errors.

## Derived Metrics
The primary goal of this project was to develop a performance tracker that could provide root metrics and actionable data for high-performance sailboat racing. 

### Wave Height/Period
The keystone challenge of this implementation was motion seperation and predicting the covariance of vessel motion and wave action. As the device is designed to be affixed to multiple locations of the boat, but generally on or near the mast, we can reasonable assume that the device will be near, but not within the center of mass of the vessel. Using the BNO055's built in sensor fusion we can extract the vertical motion of the vessel into an Earth frame using quaternion orientations from the BNO055. A band pass filter is used to isolate wave-period frequencies.

In addition, we can utilize the pitch and roll of the vessel to calculate the reference frame of the device (sail boats rarely travel directly into waves). The pitch, roll, and time-delay of the pitching moment and vertical motion can be utilized in a lead-lag compensator to further interpolate the wave height.

### Distance Lost, Time Tacking
A key metric in sailing performance analysis is the time it takes to execute tacks, in addition to the distance lost. "The distance lost is calculated post-tack and quantified as the vertical displacement measured parallel to the wind direction between the vessel's actual position and theoretical position after completion of the maneuver. 
