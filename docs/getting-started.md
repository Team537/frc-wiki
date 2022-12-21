# Getting Started

### Required Software

* WPILib and VScode
    * This is the main library and IDE (Integrated Development Environment) for Charger Robotics. It is the most important piece of software for coding as it is the main interface we use to write code for the robot. 

* FRC Game Tools
    * These Game tools take up a lot of space and take a long time to download. They are most helpful for imaging the roborio, Viewing CAN assignments, and operating the Robot using Driver Station.

* Github Desktop or GitKraken
    * While not necessary as its functionality is available in VScode, some people prefer the interface of Github Desktop as it is more streamlined and its design is easier to view and use. It is important for committing new and modified code and pushing it to separate branches as well pulling down new code to work on.

* REV Hardware Client
    * Hardware Client is used for operations for REV components. These include burning flashes, updated firmware, and toying simple PID controllers.

###### Additional Libraries

* [CTRE Library](https://maven.ctr-electronics.com/release/com/ctre/phoenix/Phoenix-frc2022-latest.json)
* [REV Library](https://software-metadata.revrobotics.com/REVLib.json)
* [Gyro Library](https://www.kauailabs.com/dist/frc/2022/navx_frc.json)

#### Installing New Libraries

To Start Installing New Libraries, Click on the W in the Top Right.

![](/images/getting-started/getting-started01.png)

Then Search for “Manage Vendor Libraries” and Click it

![](/images/getting-started/getting-started02.png)

Then Select “Install new libraries (Online)”

![](/images/getting-started/getting-started03.png)

Then Paste the Links put above for each corresponding library (CTRE in this example)

![](/images/getting-started/getting-started04.png)

Press Enter to confirm and install the library. Keep in mind that libraries are tied to branches and pushing code up also pushes the libraries up but also keep in mind that opening code in a different branch may result in certain libraries being absent.
