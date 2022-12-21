# What is WPILib?

#### Subsystems vs Commands

Subsystems and Commands are both types of classes that are used in FRC Java coding. However, they are both different in what their function is. Briefly, a subsystem usually corresponds to a system on the robot such as an intake or drivetrain. The class itself would contain functions that relate to that system such as moving an arm up and moving it down. Below is an example of an Intake subsystem.

```java
package frc.robot.subsystems;

import com.ctre.phoenix.motorcontrol.NeutralMode;
import com.ctre.phoenix.motorcontrol.can.WPI_TalonFX;
import edu.wpi.first.wpilibj2.command.SubsystemBase;
import frc.robot.Constants;


public class Intake extends SubsystemBase { 
    WPI_TalonFX intake = new WPI_TalonFX(Constants.IntakeConstants.intake);

    public Intake() {
        intake.configFactoryDefault(Constants.timeoutMs);
        intake.setNeutralMode(NeutralMode.Brake);
    }

    @Override
    public void periodic() {
        // This method will be called once per scheduler run
    }
    
    public void intakeIn() {
        intake.set(0.5);
    }
    public void intakeOff() {
        intake.set(0.0);
    }
    public void intakeOut() {
        intake.set(-1.0);
    }
}
```

As seen above, the libraries are defined above followed by the constructor and the “main” function which configures the intake. There are three other functions that are used (periodic has nothing in it so it doesn’t count). IntakeIn runs the intake so it takes in balls, IntakeOff turns off the intake, and IntakeOut runs the intake so it spits out balls. The reason for IntakeOff was because the controller scheme was made so that the button was set to a toggle which meant you pressed the button once and it would spin without the need to hold down. To accomplish this, the code was written so that once the button was pressed, IntakeIn was run, when it was pressed again, IntakeOff ran. Keep in mind that there were 2 buttons, one for IntakeIn and IntakeOut. 

On the other hand, commands are different. They are similar to functions themselves but are more complicated and can be more customized. They allow different actions to occur on initialization, execution, and finish which can be helpful for autonomous when there are multiple moving parts throughout the entire sequence. The sequence can be broken down into what actions happen and these actions can be made into separate commands which then with the use of a command or time-based structure can be pulled together using something like a Sequential Command Group.

```java
package frc.robot.commands;

import java.util.function.Supplier;
import edu.wpi.first.wpilibj2.command.CommandBase;
import frc.robot.subsystems.DriveSubsystem;

public class ArcadeDriveCommand extends CommandBase {
    private final DriveSubsystem driveSubsystem;
    private final Supplier<Double> speedFunction, turnFunction;

    public ArcadeDriveCommand(DriveSubsystem driveSubsystem, Supplier<Double> speedFunction, Supplier<Double> turnFunction) {
        this.speedFunction = speedFunction;
        this.turnFunction = turnFunction;
        this.driveSubsystem = driveSubsystem;
        addRequirements(driveSubsystem);
    }

    @Override
    public void initialize() {
        System.out.println("ArcadeDriveCmd started!");
    }

    @Override
    public void execute() {
        double realTimeSpeed = speedFunction.get();
        double realTimeTurn = .95 * turnFunction.get();

        double left = realTimeSpeed - realTimeTurn;
        double right = realTimeSpeed + realTimeTurn;
        driveSubsystem.setMotors(.4 * left, .4 * right);
    }

    @Override
    public void end(boolean interrupted) {
        System.out.println("ArcadeDriveCmd ended!");
    }

    @Override
    public boolean isFinished() {
        return false;
    }
}
```

As can be seen, there are separate functions for the initialization, execution, and finish. However, another thing that is also represented as a function, is an interrupt command which runs when the command is stopped unexpectedly. This usually is an error message which can be seen in the console and can be useful for debugging.

There is also the Command Loop which runs the entire program when it is enabled. The command loop checks what is happening and refreshes the program to suit the circumstances. For example, the command loop checks if a button is pressed, and if it is it triggers a command which is written in configureButtonBindings. To integrate into that you send code from the RobotConatiner in Robot.Java and this runs it on initialization. You can push use a Command schedule in the periodic function to make sure everything is configured correctly all the time and everything is running smoothly.
 
#### Joysticks and Controllers

Joysticks and Controllers are an integral part of our control scheme as they are the main input that direct the robot where to go, what to do, and at what speed (with specified tuning for the optimal driver experience of course). The syntax for Joysticks is not very hard and is mainly used in a couple of functions. The first thing to do is to declare an Xbox Controller (Which is what we use). It is declared just like any other object, usually in a Robot Container. Within this object we can get the button and joystick inputs from the controller. This is how we code what happens when a joystick is moved or button pressed. Within the configureButtonBindings function, we can use the toggleWhenPressed or whenPressed functions to define the actions that run on actuation. This is usually in the form of a `StartEndCommand`, an example of which is shown below.

```java
bButton = new JoyStickButton(driverController, Button.kB.value)
    .whenPressed(new StartEndCommand(arm::ArmDown, arm::ArmUp, arm));
```

The syntax inside of the StartEndCommand is called a lambda expression, and is an alternative to taking an input and giving it to a function. The first lambda is what happens when the button is pressed, the second lamba is when the button is let go, and the object in the end is the requirement needed. Joysticks are similar in a way but you get the position of the joystick in the x and y axises. The example below shows an arcade drive, in which the left joystick controls forward and backward movement in the Y-axis, and the right joystick controls left and right movement in the X-axis.

```java
robotDrive.arcadeDrive(
    -leftRateLimiter.calculate(driverController.getLeftY()),
    -rightRateLimiter.calculate(driverController.getRightX()),
)
```

Here the function to get the position of the joystick is written that shows which Joystick is used and what axis is being measured. You can ignore the calculate function as it pertains to Slew Rate Limiters and how they smooth out driver controls by adjusting the actuation curve. 

#### Motors

Motors are one of the most important components on the robot due to the simple fact they make parts of the robot move. There are 2 main types of motors, Falcons and Neos with their own motor controllers. Falcons have an inbuilt TalonFX motor controller which tells it what to do. Neos have an external Sparkmax which is responsible for PID and smart motion. Both of these require what is called a CAN ID which is what port the motors are connected to on the PDH. Generally to declare a motor object in the code you define its port number in a separate constants class which is called though an import. An example of this is shown below.

```java
private final WPI_TalonFX frontLeft = new WPI_TalonFX(DriveConstants.frontLeft);
private final WPI_TalonFX frontRight = new WPI_TalonFX(DriveConstants.frontRight);
private final WPI_TalonFX rearLeft = new WPI_TalonFX(DriveConstants.rearLeft);
private final WPI_TalonFX rearRight = new WPI_TalonFX(DriveConstants.rearRight);
```

For drive motors, of which there are usually 4, they are grouped into motor controller groups such for the left and right side as shown here.

```java
private final MotorControllerGroup leftMotors = new MotorControllerGroup(frontLeft, rearLeft);
private final MotorControllerGroup rightMotors = new MotorControllerGroup(frontRight, rearRight);
```

For tank or arcade drive, there are methods inbuilt into WPIlib that make life easier. You simply input the 2 motor controller groups and then the drive is done. You might also want to consider the gear ratios because when coding the drive and assigning modifiers to change the velocity and acceleration, the gear ratios scale these values either down or up based on the ratio itself.
