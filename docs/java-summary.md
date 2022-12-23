# Java Summary

Java is the primary programming language used for Charger Robotics in FRC and it is important to have a basic understanding of the syntax and how the language works. Java itself is a language that many consider to be inefficient in the modern era of software development due to its dated system of memory allocation of data storage, it is still very much an effective tool for any programmer looking to use an OOP (Object-Oriented Programming) Language. 

#### Importing Libraries and Other Classes

Importing libraries is the first thing programmers do when coding as it is what contains all the functions, objects, and commands that may be used in a code. To import a library, type “import” and then the library path that contains the library you need and end with a semicolon, which is a pattern across java code as it is what ends a line of code. The following syntax	is for importing Xbox Controller related code.

```java
import edu.wpi.first.wpilibj.XboxController;
```

One of the most important parts of Java is the ability to import custom classes, commands, and subsystems to simplify using repeated functions which is an integral part of the command-based framework. An example of this is importing the code for Drive Subsystem can be seen below.

```java
import frc.robot.subsystems.DriveSubsystem;
```

#### Defining Variables

Variables are important in Java because they allow Users and Sensors to input varying data that the program can use to produce an output and store the data using the various functions within it. 

The primary syntax for declaring variables is to first define if it is private or public which is part of defining the state of the variable which is essentially the sum of its parts. Private variables can only be used in that class whereas public variables can be called from anywhere in the program.

The next part is to define if it's static, final, both, or global which is the other part of defining the state. Static variables are the same value in every instance of the class whereas final variables are always the same and can never be changed which make variables into constants. Variables that change values between classes usually don’t use these modifiers and are referred to as global variables. 

After that we define the state of the variable. There are many built-in types in java such as int which is for integers, doubles for long decimals, or boolean for true/false. There are also object types which are derived from Libraries, Subsystems, and Commands.  Then you state the name of the variable, insert an equal sign, then state the value for a built-in type or state “new” and then the variable with its selected inputs. Finally, end it with a semicolon. The following are three examples of defining variables.

```java
public static final int rearRight = 7;
private final WPI_TalonFX frontLeft = new WPI_TalonFX(DriveConstants.frontLeft);
UsbCamera cam =  new UsbCamera("Usb Camera 0", 0);
```

As you can see the first statement shows a public static final int named “kRearRight” that is equal to 7. The second statement shows a `private final WPI_TalonFX` motor named `frontLeft` whose CAN ID is defined by `DriveConstants.frontLeft`. This is common to see when declaring a value for a motor as it is easier to define it in a separate Constants Class which can be called into any other class when imported. Keep in mind that each type will have its own separate state based on the object and what it inputs for the function. For example, the next statement shows the declaration of a USB Camera named “cam”. For the USB Camera, the inputs are a string that will show itself in SmartDashboard and the server port to send the footage to. 

#### Creating Functions 

Functions are the basis of making a command-based framework within subsystems as they are what the subsystems do and what makes a command-based framework simpler than stating a function in the same class it is called for. 

Creating a function is very similar to defining a variable with some key differences. The first thing is once again define it as public or private. Refer to “Defining Variables” for a further explanation for these modifiers. Then we define what it returns. If this function returns an integer, for example, we define it as an “int” function. If no value is being returned, it is defined as a “void function”. Then put the name of the function followed by 2 parenthesis closing in on each other. These parentheses are what contain the requirements for the function i.e its inputs. Sometimes a function has no requirements and can function without anything but sometimes they do and this is where they are defined. Then do the same with 2 brackets. 

The important thing here is that all the code that goes in the function is in between the 2 brackets. Keep in mind that all libraries that have been imported into the class are also available in the function so using other functions within a function is also very common. After the actual code for the function is written, remember to state a return at the end of the function. If it is a void function, this is not required. The following is an example of a void function. 

```java
public void intakeOut() {
    intake.set(-1.0);
}
```

As seen here, the function here returns void and is available as a public function. The function itself sets “intake” to -1. The .set function sets a motor to a value between -1 and 1 so here the function sets this motor in the maximum power in reverse. This will happen every time the function is called.

#### Creating Classes 

Classes are what contain all the functions, constants, and variables for a specific object such as a subsystem or command. They make organizing these pieces of code easier and allow for the code to be more readable. To create a new class, right-click on either “subsystems” if you want to make a new subsystem, “commands” if you want to make a new command, or if you want to make a separate class not belonging to those 2 categories, right-click on “java\frc\robot”.

![](/images/java-summary/java-summary01.png)

![](/images/java-summary/java-summary02.png)

Then select “Create a new class/command”. Then, select the type of subsystem you want to create. As stated above, choose which one suits your purpose. Keep in mind that you should always be using the “new” versions of these class templates.

![](/images/java-summary/java-summary03.png)

Once you have created the class it will look like this near the top, with differences if you chose a different template (I chose Command (New)) and whatever name you chose.

```java
package frc.robot.commands;

import edu.wpi.first.wpilibj2.command.CommandBase;

public class ExampleCommand extends CommandBase {
    // Creates a new ExampleCommand
    public ExampleCommand() {
        // Use addRequirements() here to declare subsystem dependencies
    }
}
```

This first function seen is called the constructor. This where all the variables and objects are declared for the class. Here, there is special syntax for “constructing” these variables to be used in the class.

```java
public ArcadeDriveCommand(DriveSubsystem driveSubsystem, Supplier<Double> speedFunction, Supplier<Double> turnFunction) {
    this.speedFunction = speedFunction;
    this.turnFunction = turnFunction;
    this.driveSubsystem = driveSubsystem;
    addRequirements(driveSubsystem);
}
```

What you can see here is that the variables to be constructed are inputted like requirements in a function. Then they are defined to a variable of the same name. To avoid confusion in the compiler, the requirements are stated with a “this.” in front to differentiate it from the variable that is going to be used in the class. The last line is what actually adds the requirements for function and in this case is only for “driveSubsystem” because it itself is a class and needs to be specifically added as a requirement as opposed to the two other variables.

Imports are located at the top of the class, not in any particular order.

```java
package frc.robot.subsystems;

import com.ctre.phoenix.motorcontrol.ControlMode;
import com.ctre.phoenix.motorcontrol.NeutralMode;
import com.ctre.phoenix.motorcontrol.StatusFrameEnhanced;
import com.ctre.phoenix.motorcontrol.TalonFXControlMode;
import com.ctre.phoenix.motorcontrol.TalonFXFeedbackDevice;
import com.ctre.phoenix.motorcontrol.can.WPI_TalonFX;
import com.kauailabs.navx.frc.AHRS;
import edu.wpi.first.math.geometry.Pose2d;
import edu.wpi.first.math.kinematics.DifferentialDriveOdometry;
import edu.wpi.first.math.kinematics.DifferentialDriveWheelSpeeds;
import edu.wpi.first.math.trajectory.TrapezoidProfile;
import edu.wpi.first.wpilibj.drive.DifferentialDrive;
import frc.robot.Constants;
import frc.robot.Constants.DriveConstants;
import edu.wpi.first.wpilibj.motorcontrol.MotorControllerGroup;
import edu.wpi.first.wpilibj.smartdashboard.SmartDashboard;
import edu.wpi.first.wpilibj2.command.SubsystemBase;
import edu.wpi.first.wpilibj.SPI;
```

Next is the main function. It holds all of the runable code for a certain action.

```java
public class DriveSubsystem extends SubsystemBase {
    // TODO: Implementation is left to the imagination of the reader
}
```

After the main function, motors and motor controller groups are defined.

```java
private final WPI_TaloxFX frontLeft = new WPI_TalonFX(DriveConstants.frontLeft);
private final WPI_TaloxFX frontRight = new WPI_TalonFX(DriveConstants.frontRight);
private final WPI_TaloxFX rearLeft = new WPI_TalonFX(DriveConstants.rearLeft);
private final WPI_TaloxFX rearRight = new WPI_TalonFX(DriveConstants.rearRight);
```

Gyros and other sensors are also defined after motors.

```java
private final AHRS gyro = new AHRS(SPI.PORT.kMXP);
```

Action functions are found next, these contain actions that the robot needs to perform when called. They will set motors to positions or activate them.

```java
public DriveSubsystem() {
    frontLeft.configFactoryDefault(Constants.timeoutMs);
    frontRight.configFactoryDefault(Constants.timeoutMs);
    rearLeft.configFactoryDefault(Constants.timeoutMs);
    rearRight.configFactoryDefault(Constants.timeoutMs);

    frontLeft.configSelectedFeedbackSensor(TalonFXFeedbackDevice.IntegratedSensor, Constants.PIDLoopIdx, Constants.timeoutMs);
    frontRight.configSelectedFeedbackSensor(TalonFXFeedbackDevice.IntegratedSensor, Constants.PIDLoopIdx, Constants.timeoutMs);
    rearLeft.configSelectedFeedbackSensor(TalonFXFeedbackDevice.IntegratedSensor, Constants.PIDLoopIdx, Constants.timeoutMs);
    rearRight.configSelectedFeedbackSensor(TalonFXFeedbackDevice.IntegratedSensor, Constants.PIDLoopIdx, Constants.timeoutMs);

    // We need to invert one side of the drive train so that positive voltages
    // result in both sides moving forward. Depending on how your robot's gearbox is constructed, you might have to invert the left side instead.
    frontLeft.setInverted(false);
    frontRight.setInverted(true);
    rearLeft.setInverted(false);
    rearRight.setInverted(true);

    frontLeft.setNeutralMode(NeutralMode.Brake);
    frontRight.setNeutralMode(NeutralMode.Brake);
    rearLeft.setNeutralMode(NeutralMode.Brake);
    rearRight.setNeutralMode(NeutralMode.Brake);
}
```

Classes contain many of these functions:

```java
public void toggleFastMode() {
    isFastModeEnabled = !isFastModeEnabled;
}

@Override
public void periodic() {
    // Update the odometry in the periodic block
    odometry.update(
        gyro.getRotation2d(),
        frontLeft.getSelectedSensorPosition(Constants.PILoopIdx),
        frontRight.getSelectedSensorPosition(Constants.PIDLoopIdx)
    );
    SmartDashboard.putNumber("Front Left Motor Velocity", frontLeft.getSelectedSensorVelocity());
    SmartDashboard.putNumber("Front Right Motor Velocity", frontRight.getSelectedSensorVelocity());
    SmartDashboard.putNumber("Rear Left Motor Velocity", rearLeft.getSelectedSensorVelocity());
    SmartDashboard.putNumber("Rear Left Motor Velocity", rearRight.getSelectedSensorVelocity());

    SmartDashboard.putNumber("Front Left Motor Position", frontLeft.getSelectedSensorPosition());
    SmartDashboard.putNumber("Front Right Motor Position", frontRight.getSelectedSensorPosition());
    SmartDashboard.putNumber("Rear Left Motor Position", rearLeft.getSelectedSensorPosition());
    SmartDashboard.putNumber("Rear Left Motor Position", rearRight.getSelectedSensorPosition());

    SmartDashboard.putNumber("Heading", gyro.getRotation2d().getDegrees());
}

public void driveSlow() {
    frontLeft.set(TalonFXControlMode.PercentOutput, 0.25);
    frontRight.set(TalonFXControlMode.PercentOutput, 0.25);
    rearLeft.set(TalonFXControlMode.PercentOutput, 0.25);
    rearRight.set(TalonFXControlMode.PercentOutput, 0.25);
}

public void driveFast() {
    frontLeft.set(TalonFXControlMode.PercentOutput, 0.55);
    frontRight.set(TalonFXControlMode.PercentOutput, 0.55);
    rearLeft.set(TalonFXControlMode.PercentOutput, 0.55);
    rearRight.set(TalonFXControlMode.PercentOutput, 0.55);
}

public void autoBack() {
    frontLeft.set(TalonFXControlMode.PercentOutput, 0.2);
    frontRight.set(TalonFXControlMode.PercentOutput, 0.2);
    rearLeft.set(TalonFXControlMode.PercentOutput, 0.2);
    rearRight.set(TalonFXControlMode.PercentOutput, 0.2);
}
```

Each function contains a specific action, and each is specific to that robot. There can be as few and as many as you need.

#### Comments

Use comments to describe your code.

```java
// On the right side, increasing is down
// On the right side, decreasing is up
public static final double rightRotationsUp = -90.0;
public static final double rightRotationsDown = 0;
```

If possible, use English so people can understand.

```java
// The robot characterization toolsuite provides a convenient tool for
// obtaining these values for your robot.
```

Not what is written above.
