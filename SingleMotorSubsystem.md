# Single Motor Subsystem Exercise

In this exercise you will create a command-based robot with a subsystem that controls a single motor with spin forward and spin backward commands.

## Setup 
In VSCode, create a new WPILib project from the CommandRobot template:

Bring up the Command Palette with *View->Command Palette*. In the Command Palette enter **WPILib: Create a new project**. Create a template-type java project based on the Command Robot template. Be sure to enter the team number and to enable desktop support. For see below for example project settings.
<details>
<summary>Project options</summary>

![image](https://github.com/jlpistole/SimpleCmdBasedTraining/assets/88595898/9fffbf36-8340-48ae-a66e-117743fd2761)

</details>

## Create the Subsystem skeleton

In the package java.frc.robot.subsystems, create a new class called SingleMotorSubsystem that extends the class SubsystemBase from the package edu.wpi.first.wpilibj2.command.SubsystemBase. Create empty methods to override the *periodic* and *simulationPeriodic* methods. See [javadoc for SubsystemBase](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/wpilibj2/command/SubsystemBase.html) for method details.

<details>
  <summary>How-to: Creating a new class file</summary>

  Choose New File... from the menu below:
  
![image](https://github.com/jlpistole/SimpleCmdBasedTraining/assets/88595898/de6e411c-591d-4659-b565-294aa6b25d5c)

Enter SingleMotorSubsystem.java in the dialog box.

</details>

<details>
  <summary>How-to: Extending the SubsystemBase class</summary>

  Add *extends SubsystemBase* after *public Class SingleMotorSubsystem*. At the top of the java file below the package declaration, import the SubsystemBase class using *import edu.wpi.first.wpilibj2.command.SubsystemBase*;. Your project and java file should look like this:

  ![image](https://github.com/jlpistole/SimpleCmdBasedTraining/assets/88595898/953a0812-d606-4464-86c6-eef23256e5f1)

</details>

<details>
  <summary>How-to: Overriding the periodic and simulationPeriodic methods</summary>

  Visit the ExampleSubsystem.java file and scroll to the bottom to see an example. You can copy these methods directly from ExampleSubsystem.java into your new subsystem class:

  ![image](https://github.com/jlpistole/SimpleCmdBasedTraining/assets/88595898/6344d3c1-1ce9-424c-afa5-e2380f69b27b)

</details>

## Create subsystem commands

Now you will create the commands that make this systme do things. In this case, you need commands to spin the motor forward, to spin the motor backward, and to stop the motor. For this section, you will not create any actual hardware interactions; instead your commands will set an internal state value indicating the direction of the motor.

1. Every device on the robot's CAN bus needs to be identified uniquely, so each device needs a CAN ID. Create a constant in your subsystem class to specify the ID for this motor. For this example, use ID = 1
2. For this example you will use motor speed as a percentage of the maximum speed of the motor. Create a constant for the absolute value to be used for this motor's speed when spinning. For this example, use 0.75.

<details>
  <summary>How-to: constant definitions in code</summary>

  ![image](https://github.com/jlpistole/SimpleCmdBasedTraining/assets/88595898/771714e3-5123-48c1-86d5-e727c553f1fd)

</details>

3. Create an enumeration to represent the spin direction of the motor and a private class variable to keep track of the current spin direction. Give the variable a default value of no spin.

<details>
  <summary>How-to: an example implementation</summary>

  ```
  enum SpinDirection {
        SpinInDir,
        SpinOutDir,
        SpinNone
  }

  private SpinDirection currentDirection = SpinDirection.SpinNone;
  ```

</details>

4. Create a private helper method to stop the motor that sets the current spin direction to none. Create another private helper method to tell the motor to spin in a specified direction. If the direction for this method is none, call the stop motor method. Otherwise, set the currrent spin direction accordingly.

<details>
  <summary>How-to: an example implementation</summary>

```
private void stopMotor() {
  this.currentDirection = SpinDirection.SpinNone;
}

private void spinMotor(SpinDirection direction) {
  switch (direction) {
    case SpinNone:
      stopMotor();
      break;
    case SpinInDir:
      this.currentDirection = SpinDirection.SpinInDir;
      break;
    case SpinOutDir:
      this.currentDirection = SpinDirection.SpinOutDir;
      break;
  }
}
```
  
</details>

5. In the command-based robot programming framework, commands contain bits of code that are run whenever they are scheduled to do so. Scheduling is handled outside of the subsystem by the CommandScheduler. In your code you do not need to interact directly with the CommandScheduler. Instead, you will create Command objects to do particular tasks. First, create a public method that returns a Command that will spin the motor in the *in* direction until the command is signalled to end by the scheduler. (To do this, you will first need to import the Command class from edu.wpi.first.wpilibj2.command.Command.)  

<details>
  <summary>How-to: Using a lambda expression in Java</summary>

  You will define the "bits of code" that go into a command using [lambda expressions](https://www.w3schools.com/java/java_lambda.asp). For this case, you will use lambda expressions that look like this:

  ```
  () -> { // code to be executed goes here }
  ```

  This expression means that when the code is executed, no arguments will be passed in, hence the () on the left hand side. When the lambda expression is executed at the time the scheduled command runs, the code contained inside the curly braces will run. 
  
</details>

<details>
  <summary>How-to: Using Command::runEnd</summary>

  To create a command that will spin the motor until the scheduler tells it to stop, you need to use this command that your subsystem inherits from its base class:
  
  ```
Command runEnd​(Runnable run, Runnable end)
```

You will pass in lambda expressions for the arguments run and end. The run expression should contain code that will spin the motor in. The end expression should contain code that will stop the motor. 

</details>

<details>
  <summary>How-to: An example implementation</summary>

```
public Command spinIn() {
  return this.runEnd(() -> { this._spinMotor(SpinDirection.SpinInDir);},
    () -> { this._stopMotor();});
}
```

Note: Don't forget to include the semicolons at the end of the line of code inside the right hand side of your lambda expressions!
  
</details>

6. Repeat Step 5 for the spin *out* direction.

## Creating command triggers on the controller

## Instrumenting the code to see current motor direction

## Running in the simulator
