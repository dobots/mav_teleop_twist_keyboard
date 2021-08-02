# Keyboard teleop package for mavs (micro-aerial-vehicles)
This package is a modification of the teleop-twist-keyboard package. The message type has been changed from Twist to TwistStamped and it is publishing to the: '/mavros/setpoint_velocity/cmd_vel' topic. Since MAVs require a stream of messages with a given frequency, the default publishing rate is set to 10Hz.

# Launch
To start the mav_teleop_twist_keyboard package with the default parameters run:
```
rosrun mav_teleop_twist_keyboard mav_teleop_twist_keyboard.py
```

To start with custom values run:
```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py _speed:=0.9 _turn:=0.8
```

To publish to a different topic (in this case `my_cmd_vel`) use:
```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py cmd_vel:=my_cmd_vel
```

# Usage
```
Reading from the keyboard  and Publishing to TwistStamped!

---------------------------
Throttle up/down (move up/down) and yaw left/right (rotate left/right):

   q    w    e
   a    s    d
   z    x    c

---------------------------
Pitch up/down(move forward/backward) roll left/right (slide left/right):

   u    i    o
   j    k    l
   m    ,    .


1 : arm and offboard
2: land

r/v : increase/decrease max speeds by 10%
t/b : increase/decrease only linear speed by 10%
y/n : increase/decrease only angular speed by 10%

CTRL-C to quit
```

# Repeat Rate

The teleop\_twist\_keyboard package has the option to be configured to repeat the last command at a fixed interval, using the `repeat_rate` private parameter. Since MAVs require  constant  updates on the /mavros/setpoint\_velocity/cmd\_vel topic, in the  mav\_teleop\_twist\_keyboard package the default has been changed to repeat the last command at 10Hz.

This value can be adjusted for different rates. For example, to repeat the last command at 20Hz, use:

```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py _repeat_rate:=20.0
```

It is _highly_ recommened that the repeat rate be used in conjunction with the key timeout, to prevent runaway robots.

# Key Timeout

Teleop\_twist\_keyboard can be configured to stop your robot if it does not receive any key presses in a configured time period, using the `key_timeout` private parameter.

For example, to stop your robot if a keypress has not been received in 0.6 seconds:
```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py _key_timeout:=0.6
```

It is recommended that you set `key_timeout` higher than the initial key repeat delay on your system (This delay is 0.5 seconds by default on Ubuntu, but can be adjusted).


### Special thanks to the creators of teleop_twist_keyboard package. This package and Readme is based on the teleop_twist_keyboard package, with slight adjustments to suit controlling mavs. The code snippet used to set the mode of the uav to offboard, arm, and land was copied from https://edu.gaitech.hk/gapter/mavros-basics.html Special thanks to the authors of those tutorials as well!
