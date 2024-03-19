This repository contains sample code aiming to solve some of the problems presented by tracking position with an IMU (inertial navigation). The repostitory has a website example that can be run from a mobile phone, utilizing the phone's built in IMU.

# Basic Rundown
Inertial navigation uses a 3-axis gyroscope and accelerometer (6-axis IMU) to track the position of a robot from a known starting location.

This repository attempts to implement inertial navigation in these steps:
1. calibrate gravity vector by averaging accel data from a few hundred samples while IMU is still. The gravity vector found in this step defines the negative z-axis in the robot's inertial frame.
2. track rotation by integrating gyroscope data over time. In this step we also rotate our calibrated gravity vector in the opposite direction of the robot's rotation.
3. subtract rotated gravity vecotor from current accelerometer data.
4. rotate the accelerometer data by the robot's current roation to put it back int the robot's frame of refernce. This step is done because the accelerometer only outputs data in it's fixed x,y,z axis. E.g. if robot moving flat in +x direction accelerometer reports +1 m/s^2 in x direction. If robot then goes up hill the accelerometer will still report +1 m/s^2 in the x-dir even though we now have a z and x component to our movement. ***TODO: check out direction cosine matrix, not sure if this rotaing idea good***
6. track position by double integrating the rotated accelerometer data.

# Benefits
The benefits of using inertial navigation over other forms of position tracking is the ability to use inertial data which will include no external errors, for example error from slipage of robot wheels if using encoders for distance tracking.
Inertial navigation can also be applied to many different systems including wheeled robots/ vehicles, flying vehicles, and underwater vehicles.

# Drawbacks
Inertial navigation is only reliable with verrrrrrrrry good sensors. It is very difficult to get rid of the internal error introduced by cheap sensors such as those in phones or the MPU6050 integrated sensor.

# Problems We Try to Solve in this Repository
- filtering gravity from acceleration data, leaving only linear acceleration data
- dealing with gyroscopic drift and error accumulation over time
- put acceleration data in robot's inertial reference frame. We tried rotating the acceleration vector by the current tracked rotation of the robot, but could also look into direction cosine matrix, DCM.
