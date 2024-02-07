# Single Motor Subsystem Exercise Part 2: Adding a real motor

[Part 1](SingleMotorSubsystem.md)

In this portion of the exercise you will connect a TalonFX-controlled motor to the subsystem developed in [part 1](SingleMotorSubsystem.md). You will use the [Phoenix 6 framework API](https://pro.docs.ctr-electronics.com/en/latest/index.html) to interact with the motor.

## Setup

Using WPIlib vendor library management in VSCode, add the Phoenix 6 library to your project. In the Command Palette, chose *WPILib: Manage Vendor Libraries*, then choose *Install new libraries (online)*. Enter the following URL:

https://maven.ctr-electronics.com/release/com/ctre/phoenix6/latest/Phoenix6-frc2024-latest.json

## Create a TalonFX motor

In SingleMotorSubsystem, add a private member variable of type [TalonFX](https://maven.ctr-electronics.com/release/com/ctre/phoenix6/latest/Phoenix6-frc2024-latest.json) for the motor. At this point, you will also want to create a constructor for the SingleMotorSubsystem class. Inside the constructor, create a new TalonFX motor with ID = MOTOR_ID (the constant defined in part one to hold the motor's CAN ID). Remember to import the TalonFX class at the top of the SingleMotorSubsystem.java file.

<details>
  <summary>How-to: Example implementation</summary>

  ```
  private TalonFX motor;

  public SingleMotorSubsystem() {
    motor = new TalonFX(MOTOR_ID);
  }
  ```
</details>

## Set the motor speed and direction
## Add motor speed to the dashboard
## Deploy and test on test board
