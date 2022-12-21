# Code Process

The software team of Charger Robotics has a very specific purpose, to animate the parts given to it by the rest of the team. Our job is to take in hardware and turn them into functioning systems.

#### Engineering 

It starts with a specific design given to us by the engineering team such as an arm design and necessary specifications for the code such as angles at which the arm should be positioned when in the “Up” position or the gear ratio for a motor. This would usually happen near the beginning of the season when the CAD of the robot is made. This allows the software team to visualize the systems they will be coding. 

#### Electrical

This results in close-collaboration with the electrical team once code is actively being written which allows us to communicate with them how certain components are going to be placed on the robot and how this influences the code. This usually results in the creation of a test board, which allows things to be tested on physical components without being on the robot. This allows the system to be the most efficiently designed and operated without the risk of breaking things. 

This process takes some time and usually includes looking at the WPI Documentation to learn the syntax of specialized functions and running virtual simulations to check it works before deploying to the test board and eventually the robot.

#### Testing

The next step is to test it on the robot. This is the most important part as this when the functionality is fully developed and ironed out which leads to its most successful implementation. Before testing, always tune down the values so that if things don’t go to plan, they don’t utterly wreck the prototyping hardware. These values can increase once there is a level of assurance that it won’t break.

This eventually will lead to the finalization of the mechanism once the final tuning has been made. This is usually in the form of a motion profiling when working with motors or having a stable feed from the camera.
