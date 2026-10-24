# Getting Started (New Programmers)

Welcome to the programming subteam! This page is a roadmap for your first few weeks. You don't need
any robotics experience. Some Python helps, but you can learn it alongside everything else.

Keep the [Glossary](glossary.md) open in another tab. When someone says a word you don't know, look
it up.

> **This year is different.** 2027 brings a brand-new control system (**SystemCore**) and a big
> RobotPy API update that's still in **alpha**. Most tutorials online were written for older seasons.
> The *concepts* still apply, but class and method names often don't. When in doubt, compare
> against our robot code and ask.

---

## Week 0 — Get set up

1. **Get a GitHub account** and send your username to a programming lead so they can add you to the
   [Saint-Francis-Robotics-Team2367](https://github.com/Saint-Francis-Robotics-Team2367) org.
2. **Install the tools.** Follow the
   [setup guide in the robot code README](https://github.com/Saint-Francis-Robotics-Team2367/2026dev#setup--from-a-fresh-windows-11-laptop).
   It walks through Python 3.14, Git, cloning, the virtual environment, and RobotPy.
3. **Install VS Code** and accept the recommended extensions when you open the repo (WPILib,
   Python, Pylance, Black). Then select the `.venv` interpreter.
4. **Prove it works:**
   ```powershell
   robotpy test        # all tests pass
   robotpy sim         # the simulator opens
   ```
   In the sim, click **Autonomous** and watch the robot drive itself on the field view. If you got
   this far, you're set up. 🎉

Stuck? That's normal. Post the exact error message in the team chat or grab a lead.

---

## Week 1 — Python and Git basics

You don't need to master these. You just need to be comfortable reading and changing code.

**Python** (skip whatever you already know):
- [The official Python tutorial](https://docs.python.org/3/tutorial/). Sections 3–9 cover what you'll
  use: variables, functions, `if`/`for`, lists and dicts, and **classes** (our code uses classes
  everywhere).
- Practice by reading `constants.py` and `commands/drive.py` in our repo. Can you explain what each
  line does?

**Git and GitHub:**
- [GitHub Skills — Introduction to GitHub](https://skills.github.com/) (an interactive course that
  takes about an hour).
- [Pro Git, chapters 1–3](https://git-scm.com/book/en/v2) if you want the full picture.
- Our workflow: **make a branch → commit → push → open a pull request → get it reviewed → merge.**
  Never commit directly to `main`.

---

## Week 2 — How FRC robot code works

Read these in order. They're the most important part of this whole page.

1. **[WPILib: What is WPILib?](https://docs.wpilib.org/en/stable/docs/software/what-is-wpilib.html)**
   gives the big picture.
2. **[WPILib: Command-Based Programming](https://docs.wpilib.org/en/stable/docs/software/commandbased/index.html)**.
   Read *What Is "Command-Based" Programming?*, *Commands*, *Subsystems*, *Binding Commands to
   Triggers*, and *Structuring a Command-Based Robot Project*. Our code follows this structure exactly.
   Most pages have a **Python** tab on the code examples.
3. **[RobotPy documentation](https://robotpy.readthedocs.io/)** covers Python-specific setup and the
   API reference.
4. **Tour our code.** Read the files in this order, and follow along with
   [`docs/architecture.md`](https://github.com/Saint-Francis-Robotics-Team2367/2026dev/blob/main/docs/architecture.md):

   | File | What to look for |
   |------|------------------|
   | `robot.py` | The entry point. Notice how short it is. |
   | `robotcontainer.py` | Where subsystems and controllers get created and wired together. |
   | `commands/drive.py` | A command: reads the joysticks and calls the drivetrain. |
   | `subsystems/drivetrain.py` | A subsystem: kinematics, odometry, Field2d. |
   | `subsystems/swervemodule.py` | One swerve wheel: two motors and an encoder. |
   | `commands/auto.py` | A simple autonomous routine built from smaller commands. |
   | `constants.py` | Every number, with units. |

---

## Week 3 — Your first change

Pick a small task from a lead (or one of these) and take it all the way to a merged PR:

- Change the `demo_auto` routine in `commands/auto.py` to drive a square. Check it in `robotpy sim`.
- Add a button binding in `RobotContainer.configure_bindings()`, for example to stop the drivetrain
  while a button is held.
- Plot `Drivetrain/speedMps` in AdvantageScope while the sim runs (see
  [`docs/simulation.md`](https://github.com/Saint-Francis-Robotics-Team2367/2026dev/blob/main/docs/simulation.md#dashboards-elastic--advantagescope)).

Before you open the PR, run the same checks CI runs:

```powershell
robotpy test
pyright
black --check .
```

---

## Going deeper

Once the basics make sense, dig into whatever interests you.

### Drivetrain, kinematics, and odometry
- [WPILib: Kinematics and Odometry](https://docs.wpilib.org/en/stable/docs/software/kinematics-and-odometry/index.html)
  (read the swerve sections)
- [WPILib: Coordinate System](https://docs.wpilib.org/en/stable/docs/software/basic-programming/coordinate-system.html),
  because +y is *left*

### Controls (PID, feedforward, tuning)
- [WPILib: Advanced Controls introduction](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/index.html).
  The interactive PID tuning pages are great.
- [Controls Engineering in FRC](https://file.tavsys.net/control/controls-engineering-in-frc.pdf)
  by Tyler Veness. This is the deep end, so read it after the WPILib pages.

### Simulation and debugging
- [WPILib: Robot Simulation](https://docs.wpilib.org/en/stable/docs/software/wpilib-tools/robot-simulation/introduction.html)
- [AdvantageScope docs](https://docs.advantagescope.org/)
- [Elastic dashboard docs](https://frc-elastic.gitbook.io/docs)
- Our [`docs/simulation.md`](https://github.com/Saint-Francis-Robotics-Team2367/2026dev/blob/main/docs/simulation.md)

### Hardware vendors
- [CTRE Phoenix 6 docs](https://v6.docs.ctr-electronics.com/) for TalonFX, Kraken, CANcoder, Pigeon,
  CANivore, and Tuner X
- [REV Robotics docs](https://docs.revrobotics.com/) for SPARK MAX/Flex and NEO

### Autonomous and vision
- [PathPlanner](https://pathplanner.dev/)
- [Choreo](https://choreo.autos/)
- [PhotonVision](https://docs.photonvision.org/)
- [WPILib: AprilTag introduction](https://docs.wpilib.org/en/stable/docs/software/vision-processing/apriltag/apriltag-intro.html)

### 2027 / SystemCore changes
- Our [`docs/2027-migration.md`](https://github.com/Saint-Francis-Robotics-Team2367/2026dev/blob/main/docs/2027-migration.md)
  has every rename that has affected our code (`ChassisSpeeds` → `ChassisVelocities`, snake_case,
  no `robotInit`, and more). Read it before copying code from any tutorial.

### Examples and community
- [RobotPy examples](https://github.com/robotpy/examples) are small, complete Python robot projects.
  (Check which season they target. Older ones use pre-2027 names.)
- [Chief Delphi](https://www.chiefdelphi.com/) is the FRC forum. Search it before asking, since
  someone has probably hit your bug before.
- Open-source code from top teams (for example 254, 6328, 1678) is great for seeing how experienced
  teams structure things, even when it's in Java.

---

## Tips from older members

- **Read the error message.** The whole thing, especially the last line. Then paste it when you
  ask for help.
- **Sim first.** If it doesn't work in `robotpy sim`, it won't work on the robot.
- **Units are meters, radians, and seconds.** If something is 39× too big, someone mixed up inches
  and meters.
- **On a real robot:** say "enabling!" before you enable, keep the robot on blocks when testing
  drive code, and know how to disable fast. On the old NI Driver Station, **Enter** disables and
  the **spacebar** is the emergency stop. Check the shortcuts on the new 2027 DS before your first
  test.
- **Ask questions.** Nobody expects you to know this yet, and explaining things helps the person
  explaining too.
