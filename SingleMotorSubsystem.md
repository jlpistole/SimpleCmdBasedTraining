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
