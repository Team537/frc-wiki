# Driver Station

The Driver Station is what drivers use to enable and disable the robot for testing code and at running it at competitions. Shuffleboard is a visual interface that opens when the robot is enabled and shows live values based on what is happening on the robot currently. This can include encoder values for how far the wheels have rotated or a camera feed. Shuffleboard values are coded into the subsystems are usually part of a void function.

#### Deploying Code and Running it On the Robot

To deploy code to the robot click on the W in the Top Right corner and search “Deploy Robot Code”. Keep in mind that before deploying code you must connect to the rio whether it  be by ethernet or by radio. After this, open the FRC Driver Station. The following interface should show up.

![](/images/driver-station/driver-station01.png)

If you did this correctly, there should be Robot Code, Communications and Joysticks if they are connected. You can then select what Op mode you want to run. Teleop is what is controlled by the driver and Autonomous is what the robot does without any driver input. You can then press Enable to run the code. ALWAYS TELL EVERYONE WHEN YOU ENABLE AS TYPICALLY THE ROBOT CAN CAUSE HARM WHEN TRAVELING AT HIGH SPEEDS. This is simply for safety reasons and for the simple fact we don’t want to hurt anyone. Even if there is no code for driving or an auto doesn’t contain driving, anything can happen so it's always important to alert everyone and take precautions

#### Radios

Radios are the main wireless connection to the robot and are important because of the fact that they require a complex set up both physically and through firmware. You can [refer to this page](https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-3/radio-programming.html) on how to configure them for both direct connection and FMS. To connect to a radio once it is fully turned on, you can use the wifi panel and find it. Make sure you know what the name of the radio is as it can be hard to identify at a competition with a lot more radios operating. It may also be worth it to specify a competition radio that is always configured for FMS and one that is always for recreational purposes such as testing.
