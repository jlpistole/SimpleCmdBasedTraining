# Single Motor Subsystem Exercise Part 2: Adding a real motor

[Part 1](SingleMotorSubsystem.md)

In this portion of the exercise you will connect a TalonFX-controlled motor to the subsystem developed in [part 1](SingleMotorSubsystem.md). You will use the [Phoenix 6 framework API](https://pro.docs.ctr-electronics.com/en/latest/index.html) to interact with the motor.

## Setup

Using WPIlib vendor library management in VSCode, add the Phoenix 6 library to your project. In the Command Palette, chose *WPILib: Manage Vendor Libraries*, then choose *Install new libraries (online)*. Enter the following URL:

https://maven.ctr-electronics.com/release/com/ctre/phoenix6/latest/Phoenix6-frc2024-latest.json

## Create a TalonFX motor

In SingleMotorSubsystem, add a private member variable of type [TalonFX](https://api.ctr-electronics.com/phoenix6/release/java/com/ctre/phoenix6/hardware/TalonFX.html) for the motor. At this point, you will also want to create a constructor for the SingleMotorSubsystem class. Inside the constructor, create a new TalonFX motor with ID = MOTOR_ID (the constant defined in part one to hold the motor's CAN ID). Remember to import the TalonFX class at the top of the SingleMotorSubsystem.java file.

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

Update SingleMotorSubsystem's spinMotor and stopMotor methods to set the motor speed with appropriate direction and to stop the motor. Use the [TalonFX javadoc](https://api.ctr-electronics.com/phoenix6/release/java/com/ctre/phoenix6/hardware/TalonFX.html) for reference.

<details>
  <summary>How-to: Stop Motor implementation</summary>

  ```
    private void stopMotor() {
        this.currentDirection = SpinDirection.SpinNone;
        this.motor.stopMotor();
    }
  ```
</details>

<details>
  <summary>How-to: Spin Motor implementation</summary>

  ```
    private void spinMotor(SpinDirection direction) {
        switch (direction) {
            case SpinNone:
                stopMotor();
                break;
            case SpinInDir:
                this.currentDirection = SpinDirection.SpinInDir;
                this.motor.set(MOTOR_SPEED);
                break;
            case SpinOutDir:
                currentDirection = SpinDirection.SpinOutDir;
                this.motor.set(-1.0*MOTOR_SPEED);
                break;
        }
    }
  ```
</details>

## Add motor speed to the dashboard

Update SingleMotorSubsystem's periodic method to post the motor's current speed to the test board. Use the [TalonFX javadoc](https://api.ctr-electronics.com/phoenix6/release/java/com/ctre/phoenix6/hardware/TalonFX.html) and the [SmartDashboard javadoc](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/wpilibj/smartdashboard/SmartDashboard.html) for reference.

<details>
  <summary>How-to: Dashboard update implementation</summary>

  ```
    @Override
    public void periodic() {
        // This method will be called once per scheduler run
        SmartDashboard.putString("Motor Spin Direction", currentDirection.toString());
        SmartDashboard.putNumber("Motor Speed", this.motor.get());
    }
  ```
</details>

## Deploy and test on test board

Ensure you have a motor with the desired motor ID in the CAN chain on the test board. If you want to use a motor with a different CAN ID, just change the value of MOTOR_ID in SingleMotorSubsystem.java. Power on the test board, connect to the test board Wifi, and deploy your code using the directions found [here](https://docs.wpilib.org/en/stable/docs/software/vscode-overview/deploying-robot-code.html).

While running the FRC Driver Station and the SmartDashboard, enable the robot and verify the behavior using controller 0.
