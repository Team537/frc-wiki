# PID

#### PID vs Smart Motion vs Motion Magic

[PID](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/controllers/pidcontroller.html), [Smart Motion](https://github.com/REVrobotics/SPARK-MAX-Examples/blob/master/Java/Smart%20Motion%20Example/src/main/java/frc/robot/Robot.java), and [Motion Magic](https://docs.ctre-phoenix.com/en/stable/ch16_ClosedLoop.html#motion-magic-position-velocity-current-closed-loop-closed-loop) are all examples of motion profiling which smooths the motion of the motors so that there are no sudden stops or instant accelerations. This is very helpful for going to a specific position and using correction to make sure it stays at that exact position. PID stands for Proportional, Integral, and Derivative and is used for position-based motors such as maintaining an arm at a specific position. The algorithm uses a complicated formula which is shown below.

![](./images/pid/pid01.png)

The K’s are all constants that we input and can tune for. This is usually done through the use of Shuffleboard to input positions for the motor to go to and using this you can evaluate how the motor goes to the position, and how it tries to correct the position. This requires intense testing and takes time. Smart Motion is a motion profiling specific to the Sparkmax motor controller. It includes PID but takes less time due to the fact that it is already integrated into the motor controller which makes it more efficient. This is usually for when we don’t have much time and have to spit something out or for something that requires extreme precision. Motion Magic is the least used out of the 3 motion profiling systems and is specific to TalonFX motor controllers. It is mostly used for autonomous which involves having the robot smoothly stop without a lot of drag once the motors stop.