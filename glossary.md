---
title: Glossary
nav_order: 2
---

# Glossary

Words you'll hear in the shop, on Chief Delphi, and in our code. Terms are grouped by topic. Many entries
have an **In our code** note that points at where the idea shows up in
[`2026dev`](https://github.com/Saint-Francis-Robotics-Team2367/2026dev), our 2027-season robot code.

Entries marked **2027:** changed this season, so older tutorials use different names.

**Jump to:** [FRC basics](#frc-basics) · [Python basics](#python-basics) · [Software stack](#software-stack) ·
[Hardware & electronics](#hardware--electronics) · [Drivetrains](#drivetrains) ·
[Command-based programming](#command-based-programming) ·
[Geometry, kinematics & odometry](#geometry-kinematics--odometry) · [Controls](#controls) ·
[Simulation, telemetry & dashboards](#simulation-telemetry--dashboards) ·
[Autonomous & vision](#autonomous--vision) · [Dev tools & workflow](#dev-tools--workflow)

---

## FRC basics

**FIRST / FRC** — *FIRST* is the nonprofit that runs the program. *FRC* (FIRST Robotics Competition) is the high-school
league we compete in: big robots, alliances of three teams, a new game every year.

**FTC / FLL** — FIRST's other programs: FTC (FIRST Tech Challenge) uses smaller robots, and FLL (FIRST LEGO League) is for younger students. FTC tutorials talk about `OpMode` and `hardwareMap`, which don't exist in FRC.

**Kickoff / build season / competition season** — The game is revealed at **kickoff** in early January. **Build season** follows, when we design, build,
and program the robot. **Competition season** is when we play at events.

**Alliance** — The three teams on your side in a match: red or blue.

**Autonomous (auto)** — The first part of a match (about 15–20 seconds, depending on the game). The robot drives itself
using pre-written code. Nobody touches the controls.

**Teleoperated (teleop)** — The rest of the match. Drivers control the robot with gamepads.

**Disabled / Enabled** — When the robot is *disabled*, motors are not allowed to move. *Enabling* the robot (from the Driver
Station) lets code run motors. Always say "enabling!" out loud before you enable a real robot.

**Test mode** — A fourth robot mode used for checking mechanisms in the pit. It isn't used in matches.

**FMS (Field Management System)** — The field's computer at events. It starts and stops matches and switches robots between auto and
teleop.

**Driver Station (DS)** — The laptop program the drive team uses to connect to the robot, choose a mode, enable or disable,
and read gamepads. **2027:** a new multi-platform Driver Station replaces the old Windows-only NI one.

**Drive team** — The driver, operator, coach, and human player who run the robot during a match.

**Pit** — The team's work area at a competition.

**Brownout** — When battery voltage sags too low (usually because too many motors are pulling hard at once), the
controller cuts motor output to protect itself. A robot that "dies" mid-push is often browning out.

**Bumpers** — The padded fabric frame around the robot. Bumper color (red or blue) shows which alliance you're on.

---

## Python basics

Just enough Python vocabulary to read our code. The [Python tutorial](https://docs.python.org/3/tutorial/) explains each one properly.

**Variable / type** — A named value, like `max_speed = 4.5`. Its *type* is what kind of value it is: `int`, `float`, `str`, `bool`, `list`, `dict`.

**Function / method** — A reusable block of code you call by name. A *method* is a function that belongs to a class, like `drivetrain.drive(...)`.

**Class / object** — A *class* is a blueprint, like `Drivetrain`. An *object* (or *instance*) is one thing built from it, like `self.drivetrain = Drivetrain()`. Subsystems and commands are all classes.

**`self`** — Inside a method, `self` is the object the method was called on. `self._drivetrain` means "this command's drivetrain".

**Constructor (`__init__`)** — The method that runs when an object is created. It sets up the object's starting state.<br>
**2027:** robot setup goes in the robot's constructor now, since `robotInit` was removed.

**Inheritance / `super().__init__()`** — `class DriveByController(Command)` means our class *inherits* from WPILib's `Command` and gets all its behavior. `super().__init__()` runs the parent class's constructor first. Forgetting it causes confusing errors.

**Override** — Defining a method with the same name as one in the parent class, so yours runs instead. That's how `execute()` and `periodic()` work. The name must match *exactly*.

**Module / import** — A *module* is a `.py` file. `from constants import DriveConstants` pulls a name from another file. Don't name your own files after RobotPy packages (like `telemetry.py`), or the import gets confused.

---

## Software stack

**WPILib** — The official FRC software library. It handles robot modes, the main loop, motor and sensor
interfaces, math (kinematics, geometry, PID), simulation, and NetworkTables. It supports Java, C++, and
Python. Its docs, [docs.wpilib.org](https://docs.wpilib.org/), are the main FRC programming reference.

**RobotPy** — The Python version of WPILib, and what our team uses. You install it with `pip`, and you run
everything through the `robotpy` command (`robotpy sim`, `robotpy test`, `robotpy deploy`).<br>
**In our code:** pinned in `pyproject.toml` (`robotpy_version = "2027.0.0a7"`).

**`wpilib` / `wpimath` / `commands2` / `ntcore`** — The main Python packages in RobotPy. `wpilib` covers robot base classes, controllers, and the Driver
Station. `wpimath` covers geometry, kinematics, controllers, and motor models. `commands2` is the
command-based framework. `ntcore` is NetworkTables.<br>
**2027:** `wpimath` was *flattened*, so it's `wpimath.Pose2d`, not `wpimath.geometry.Pose2d`.

**snake_case vs camelCase** — **2027:** RobotPy 2027 alpha 7 renamed the whole API to Python-style `snake_case`
(`get_left_y()`, `autonomous_init`). Old tutorials use `camelCase` (`getLeftY()`, `autonomousInit`).
Watch out: if you override a lifecycle method with the old camelCase name, nothing warns you. The method
just never runs.

**Alpha / beta / RC** — Pre-release software. RobotPy 2027 is **alpha** right now, so APIs may still change before kickoff.
That's why we install it with `pip install --pre`.

**Vendor library / vendordep** — A library from a hardware company that lets code talk to its motors and sensors. In Python these are
pip packages, such as `phoenix6` (CTRE) and `robotpy-rev` (REV).<br>
**In our code:** `phoenix6` is listed under `requires` in `pyproject.toml`.

**Phoenix 6** — CTRE's library for TalonFX motors, CANcoders, Pigeon gyros, and CANivores.<br>
**In our code:** `subsystems/swervemodule.py`.

**`robotpy sync`** — Downloads the exact package versions in `pyproject.toml` so they can be deployed to the robot. Run it
after cloning and whenever dependencies change.

**Deploy** — Copying your code onto the robot's controller so it runs there (`robotpy deploy`). We can't deploy
yet because we don't have SystemCore hardware, so everything runs in simulation for now.

**`TimedRobot` / `TimedCommandRobot`** — Robot base classes that call your code on a fixed loop, by default every **20 ms** (50 times per
second). `TimedCommandRobot` also runs the command scheduler each loop.<br>
**In our code:** `robot.py`.

**Periodic / init methods** — Hooks the robot base class calls for you. `*_init` runs once when a mode starts
(`autonomous_init`, `teleop_init`). `*_periodic` runs every loop during that mode.<br>
**2027:** `robotInit` is gone, so put setup code in `__init__` (after `super().__init__()`).

---

## Hardware & electronics

**SystemCore** — **2027:** the new robot controller, replacing the roboRIO. It has several CAN buses, Smart IO, a
built-in IMU (gyro), and support for an Expansion Hub. It runs Python 3.14.

**roboRIO** — The robot controller teams used through 2026. You'll see it in nearly every older tutorial. Most of
those concepts still apply, but the hardware is different.

**CAN (Controller Area Network)** — The two-wire network (yellow and green) that links the controller to motor controllers and sensors.
Every device on it has a **CAN ID**, a number that must be unique on that bus. Phoenix devices use
IDs 0–62.<br>
**In our code:** `HardwareIds` in `constants.py`.

**CANivore** — A CTRE USB-to-CAN adapter that adds an extra, faster CAN bus (CAN FD). We also use it to test
motors from a laptop.<br>
**In our code:** `bench/`.

**Motor controller** — The box that takes commands from the robot code and drives a motor. Some motors (Kraken, Falcon)
have the controller built in.

**TalonFX / Kraken X60 / Falcon 500** — CTRE's motor controller, built into the Kraken X60 and Falcon 500 motors. In code, you control both
through the `TalonFX` class.<br>
**In our code:** each swerve module has two (drive and steer).

**SPARK MAX / SPARK Flex / NEO** — REV's motor controllers and brushless motors. They're another very common FRC setup, controlled
through `robotpy-rev`.

**Encoder** — A sensor that measures rotation. A **relative** encoder counts how far it has turned since power-on,
which works for measuring speed and distance. An **absolute** encoder knows its exact angle even right
after power-on.

**CANcoder** — CTRE's absolute magnetic encoder on the CAN bus. On swerve modules it reports which way each wheel
is pointing.<br>
**In our code:** used for steering feedback in `swervemodule.py`.

**Magnet offset** — The value that tells an absolute encoder where "zero" is, so 0° means the wheel points straight
forward. You measure it once per module.

**Gyro / IMU** — A sensor that measures the robot's rotation (heading). Field-relative driving depends on it.<br>
**2027:** SystemCore has a built-in IMU. Before that, teams used a separate Pigeon 2 or NavX.

**Mechanism** — A physical part of the robot that does one job: an intake, arm, elevator, or shooter. Usually each mechanism becomes one subsystem in code.

**Gear ratio / reduction** — How many motor rotations it takes to turn the output once. Our drive reduction of 6.75 means the
motor spins 6.75 times for each wheel rotation.<br>
**In our code:** `ModuleConstants.DRIVE_GEAR_RATIO`.

**Brake vs coast mode** — What a motor does when it gets zero output. In **brake** it resists turning, so the robot stops
fast. In **coast** it spins freely.

**Current limit** — A cap on how much current a motor can draw. Current limits protect motors and breakers and help
prevent brownouts.

**Phoenix Tuner X** — CTRE's app for updating firmware, setting CAN IDs, and testing devices. Close it before running our
bench scripts, because both need the CANivore and only one can use it at a time.

**Firmware** — The software that runs on the device itself. Its version must match the vendor library version
your code uses.

---

## Drivetrains

**Drivetrain / chassis** — The part of the robot that moves it around the field: wheels, motors, and frame.

**Tank / differential drive** — Left and right wheel sets, like a tank. It's simple and strong, but it can't move sideways.

**Mecanum drive** — Angled rollers on each wheel let the robot strafe. It's cheaper than swerve but gets pushed around
more easily.

**Swerve drive** — Each wheel can steer independently, so the robot can drive in any direction while facing any
direction. It's the most common top-team drivetrain and what we run.<br>
**In our code:** `subsystems/drivetrain.py`.

**Swerve module** — One corner of a swerve drive: a wheel, a **drive** motor that spins it, a **steer** (azimuth)
motor that points it, and an absolute encoder. We have four, labeled FL, FR, BL, and BR.<br>
**In our code:** `subsystems/swervemodule.py`. The geometry is based on the SDS MK4i module.

**Holonomic** — A drivetrain that can move in any direction without turning first. Swerve and mecanum are holonomic.
Tank isn't.

**Field-relative vs robot-relative** — With **field-relative** driving, pushing the stick "up" always moves the robot away from the driver,
whichever way the robot faces. That requires a gyro. With **robot-relative** driving, "up" means
toward the robot's front. Our teleop drives field-relative.

**Track width / wheelbase** — Track width is the left-to-right distance between wheel centers. Wheelbase is the front-to-back
distance. Kinematics needs both.

**Desaturate** — If any wheel is asked to go faster than it can, scale *all* wheel speeds down together so the robot
still moves in the direction you asked for.

**Optimize (swerve)** — Instead of steering a wheel more than 90°, reverse it and steer the shorter way. This keeps steering
fast.

**Skew / discretize** — A correction applied to the velocity command each loop so the robot doesn't drift sideways while
driving and spinning at the same time.

---

## Command-based programming

WPILib's recommended way to organize robot code, and the way ours is organized. It's covered on
[docs.wpilib.org](https://docs.wpilib.org/en/stable/docs/software/commandbased/index.html).

**Subsystem** — A class for one physical part of the robot (drivetrain, intake, arm) that owns its motors and
sensors. Other code asks the subsystem to do things and never touches its motors directly.<br>
**In our code:** `Drivetrain`.

**Command** — A single action or behavior, such as "drive with the joysticks", "intake until a game piece is
detected", or "raise the arm to 90°". A command has `initialize()`, `execute()` (every loop),
`is_finished()`, and `end()`.<br>
**In our code:** `commands/drive.py` (`DriveByController`).

**Requirements** — The subsystems a command uses. Only one command can use a given subsystem at a time. If a new
command needs it, the old one gets interrupted.<br>
**In our code:** `self.add_requirements(drivetrain)`.

**Default command** — The command a subsystem runs whenever nothing else is using it. Our drivetrain's default command is
teleop driving.

**Command scheduler** — The engine that runs scheduled commands every loop, checks triggers, and resolves requirement
conflicts. `TimedCommandRobot` runs it for you.

**Trigger / button binding** — Connects a condition, usually a button press, to a command. An example is "while A is held, run the
intake".<br>
**In our code:** goes in `RobotContainer.configure_bindings()`.

**Command composition / command groups** — Building bigger commands out of smaller ones: `sequence` (one after another), `parallel` (at the
same time), `race`, `deadline`, plus helpers like `.and_then()` and `.with_timeout()`.<br>
**In our code:** `commands/auto.py` builds an auto routine as a sequence.

**RobotContainer** — The class that creates subsystems and controllers, sets default commands, and wires up button
bindings. It keeps `robot.py` small.<br>
**In our code:** `robotcontainer.py`.

**Iterative vs command-based** — Two ways to structure robot code. *Iterative* code puts all logic directly in `teleop_periodic()` and similar methods. That's fine for tiny robots but gets messy fast. *Command-based* splits it into subsystems and commands. We use command-based.

**State machine** — Logic that's always in exactly one named state ("idle", "intaking", "holding", "shooting") and moves between states on conditions. It's useful for mechanisms with several steps.

**Debounce** — Requiring a condition (a sensor or button) to stay true for a short time before acting on it, so a quick flicker doesn't trigger anything.

**Command factory / inline command** — A short function that returns a command built from helpers like `cmd.run_once(...)`, instead of a
whole new class.

**`CommandNiDsXboxController`** — An Xbox controller wrapper with button triggers.<br>
**2027:** renamed from `CommandXboxController`.

---

## Geometry, kinematics & odometry

**Coordinate system (WPILib convention)** — **+x is forward**, **+y is left**, and **counterclockwise rotation is positive**. This trips up
everyone at least once.

**Units** — WPILib uses **meters, radians, and seconds**, so speeds are in m/s and rad/s. Convert inches and
degrees at the edges of the code and nowhere else.

**`Translation2d` / `Rotation2d` / `Pose2d`** — A position (x, y), an angle, and the two combined (where the robot is *and* which way it faces).

**Kinematics** — Converting between "how the whole robot should move" and "what each wheel should do". *Inverse
kinematics* turns robot velocity into wheel commands. *Forward kinematics* turns wheel readings into
robot velocity.<br>
**In our code:** `SwerveDrive4Kinematics` in `constants.py`.

**`ChassisVelocities`** — Robot velocity: vx (forward), vy (left), and omega (rotation).<br>
**2027:** renamed from `ChassisSpeeds`.

**`SwerveModuleVelocity` / `SwerveModulePosition`** — A wheel's speed and angle, and a wheel's distance traveled and angle.<br>
**2027:** `SwerveModuleVelocity` replaces `SwerveModuleState`.

**Odometry** — Estimating where the robot is on the field by adding up wheel movement and gyro heading over time.
It drifts slowly, especially after collisions.<br>
**In our code:** `SwerveDrive4Odometry` in `Drivetrain.periodic()`.

**Pose estimation** — Odometry corrected with vision measurements (usually AprilTags) so the position estimate stays
accurate.

---

## Controls

**Open loop vs closed loop** — **Open loop** means "apply 50% power" and hope for the best. **Closed loop** means "go to 2 m/s",
with a sensor measuring what actually happens and correcting.

**Setpoint / reference** — The target value a closed-loop controller is trying to reach.

**Error** — Setpoint minus measurement, or how far off you are right now.

**PID (Proportional, Integral, Derivative)** — The standard feedback controller. **P** pushes harder the farther you are from the target. **I**
fixes small errors that stick around. **D** slows things down to keep the mechanism from overshooting.
Gains are named kP, kI, and kD.

**Feedforward (kS, kV, kA, kG)** — Predicting the voltage a mechanism needs *before* any error shows up. kS overcomes friction, kV holds
speed, kA accelerates, and kG holds against gravity. Feedforward does most of the work, and PID cleans
up what's left.

**Tuning** — Adjusting gains until a mechanism tracks its setpoint well. Our current gains are simulation
starting points and still need tuning on the real robot.

**On-controller closed loop** — Running the PID loop on the motor controller itself (for example `VelocityVoltage` and
`PositionVoltage` on a TalonFX), which is faster than running it in robot code.<br>
**In our code:** both swerve motors do this.

**Motion profile / Motion Magic** — Planning a smooth path to a setpoint (accelerate, cruise, decelerate) instead of jumping straight
to it. In WPILib, `TrapezoidProfile` generates the profile and `ProfiledPIDController` follows it.
Motion Magic is CTRE's version that runs on the motor controller.

**SysId** — A WPILib tool that runs test motions on a mechanism and calculates feedforward and PID gains from
the data.

**Deadband** — Ignoring tiny joystick values near zero so the robot doesn't creep when nobody is touching the stick.<br>
**In our code:** `apply_deadband` in `commands/drive.py`.

**Slew rate limiter** — Caps how fast a value can change, for example to smooth sudden stick movements.

**Continuous input / wrap** — Treating angles as circular, so the controller knows 359° and 1° are 2° apart, not 358°.

---

## Simulation, telemetry & dashboards

**Simulation (sim)** — Running robot code on your laptop with physics models instead of real hardware. `robotpy sim` opens
the WPILib Simulation GUI. Our code is built "simulation-first".<br>
**In our code:** `simulation_periodic()` in `drivetrain.py`, and `simulate(dt)` in `swervemodule.py`.

**`DCMotorSim`** — A WPILib physics model of a motor plus gearbox, used to fake realistic motion in sim.

**Field2d** — A widget that draws the robot's pose on a field image. It's the easiest way to see whether odometry
looks right.

**NetworkTables (NT)** — The live key/value system that robot code, dashboards, and vision coprocessors use to share data.<br>
**2027:** NT4 only.

**Telemetry** — Data the robot publishes so people can watch what it's doing.<br>
**2027:** `SmartDashboard` was removed. Use `telemetry.log(...)` and NT topics instead.<br>
**In our code:** `drivetrain_telemetry.py`.

**AdvantageScope** — A tool for viewing live or logged data as graphs, a 2D/3D field, swerve module views, and more. It's
the go-to tool for debugging.

**Elastic** — A driver dashboard for showing key info during matches.

**Glass / Shuffleboard / SmartDashboard** — Older or alternative dashboards that show up in tutorials. SmartDashboard *the API* is gone in 2027.

**Logs / `.hoot` files** — Recorded data from a run that you can replay later in AdvantageScope. `.hoot` files are CTRE's
signal logs.

---

## Autonomous & vision

**Auto routine** — A pre-planned sequence of actions for the autonomous period.<br>
**In our code:** `demo_auto` in `commands/auto.py`, a placeholder that drives forward, strafes, and
spins.

**Trajectory / path following** — Driving a planned curve through the field, with controllers correcting toward it.

**PathPlanner / Choreo** — Popular tools for drawing autonomous paths and generating trajectories. Choreo optimizes paths for
time.

**AprilTag** — The square black-and-white markers placed around the field. Cameras use them to work out exactly
where the robot is.

**PhotonVision / Limelight** — Vision systems that run on a coprocessor or smart camera, detect AprilTags or game pieces, and send
results over NetworkTables.

**Coprocessor** — An extra computer on the robot, such as an Orange Pi, that handles heavy work like vision.

**`SwerveDrivePoseEstimator`** — WPILib's class that combines swerve odometry with vision measurements into one pose estimate. It replaces plain odometry once we add cameras.

**Kalman filter** — The math behind pose estimators. It blends several noisy measurements, weighting each one by how much it's trusted.

**Standard deviations (std devs)** — In a pose estimator, how much you *distrust* a measurement. Larger values mean the estimator trusts it less. Vision measurements from far away usually get larger std devs.

**Latency compensation** — Camera results arrive a little late. The pose estimator uses the measurement's timestamp to apply it where the robot *was* when the picture was taken.

**MegaTag2** — Limelight's AprilTag localization mode. It uses the robot's gyro heading to give more stable pose estimates.

**Vision dropout** — When the camera loses sight of tags and stops giving measurements. Odometry has to carry the estimate until tags are visible again.

---

## Dev tools & workflow

**Python virtual environment (venv)** — A project-local folder (`.venv`) that holds this project's Python and packages, so it doesn't
interfere with anything else on your computer. Activate it before working:
`.\.venv\Scripts\Activate.ps1`.

**pip** — Python's package installer.

**`pyproject.toml`** — The project config file. It lists the RobotPy version, components, vendor libraries, and settings
for Black and pyright.

**Git / commit / branch / pull request (PR)** — Git tracks every change to the code. A **commit** is a saved snapshot. A **branch** is a separate
line of work. A **pull request** asks to merge your branch into `main` and is where code review
happens. Never push straight to `main`.

**CI (Continuous Integration)** — GitHub Actions automatically runs our checks on every PR (`black`, `pyright`, `robotpy test`).
A red ❌ means fix it before merging.

**Black** — The automatic code formatter. Run `black .` and stop arguing about spacing.

**pyright / Pylance** — Static type checkers that catch mistakes such as typos and wrong 2027 API names before you run
anything. Pylance is the VS Code version, so errors in your editor match the ones in CI.

**pre-commit** — Runs Black automatically every time you commit. Set it up once with `pre-commit install`.

**`robotpy test`** — Runs our automated tests, including a full robot boot plus 15 seconds of autonomous in sim. If it
passes, the robot at least starts up.

**Type hints** — Notes in the code like `def drive(self, vx: float) -> None` that say what types go in and out.
pyright checks them.

**Magic number** — An unexplained number buried in code. Put it in `constants.py` with a name and units instead.
