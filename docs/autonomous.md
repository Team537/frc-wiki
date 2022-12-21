# Autonomous

Autonomous

#### Path-based auto

Pathweaver is an application that can be used to build pre-determining, complex paths on the field. It is a very complex tool and is something we were not able to fully achieve in the 21-22 season. It allows users to input points and path weaver designs paths for how to move to these points. For more information, read this page. A picture of the user interface is shown below.

![](/assets/images/autonomous/pathweaver01.png)

Above you can see a map of the field, as well as coordinates with paths and autonomous routines on the right. Paths are defined as the movement of the robot from 1 point to another point and a routine is defined as a collection of paths meant to run in 1 autonomous mode in a competition.

![](/images/autonomous/pathweaver02.png)

Here we can see a routine with each colored vector being a path. Here the routine shows the robot going to a ball and returning to the hub. The reason the routine splits when the robot gets to the ball is because the intake and arm need to run to pick up the ball before the robot continues the routine so the routine needs to reflect that. These paths are used in the code in the form of a JSON file with thousands of points and can be used with a ramsete controller.

#### Time-based Auto

The auto that was used for the 21-22 season was time-based running commands for a certain time and then transitioning to the next command. An example of this is shown below.

```java
return new SequentialCommandGroup(
    new RunCommand(m_Intake::intakeOut).withTimeout(5),
    new RunCommand(m_Intake::intakeOff).withTimeout(1),
    new RunCommand(m_robotDrive::AutoBack).withTimeout(3)
);
```

As seen above, the commands are separated by a withTimeout function with the number in the parenthesis is the number of seconds the command runs for. This can also be used with custom command classes as seen with “AutoBack”.
