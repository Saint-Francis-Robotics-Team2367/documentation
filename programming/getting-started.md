---
title: Getting Started
parent: Programming
nav_order: 1
---

# Getting Started (New Programmers)

Welcome to the programming subteam! This page is a set of lessons that take you from a fresh laptop to
a full software member. You don't need any robotics experience. Some Python helps, but you can learn
it alongside everything else.

Each lesson has a **goal**, some **reading**, and a **checkpoint**. Show your checkpoint to a
programming lead before moving on. Keep the [Glossary](../glossary.md) open in another tab, and look up
any word you don't know.

> **This year is different.** 2027 brings a brand-new control system (**SystemCore**) and a big
> RobotPy API update that's still in **alpha**. Most tutorials online were written for older seasons.
> The *concepts* still apply, but class and method names often don't. When in doubt, compare
> against our robot code and ask.

**Training goals.** By the end, you should be able to:
1. Read and change our command-based robot code in Python.
2. Use Git and GitHub with our [workflow](git-workflow.md): branch, commit, pull request, review.
3. Debug problems yourself with simulation, dashboards, tests, and error messages.

| Lesson | Topic | Checkpoint |
|--------|-------|------------|
| [0](#lesson-0--tooling-setup) | Tooling setup | `robotpy test` passes and the sim opens |
| [1](#lesson-1--python-basics) | Python basics | Explain `commands/drive.py` line by line |
| [2](#lesson-2--git-and-github) | Git and GitHub | A merged PR to this docs repo |
| [3](#lesson-3--how-robot-code-works) | How robot code works | Draw how our code fits together |
| [4](#lesson-4--codebase-and-simulation) | Codebase and simulation | Change the auto and watch it in sim |
| [5](#lesson-5--drivetrain) | Drivetrain | Explain one loop of swerve driving |
| [6](#lesson-6--autonomous) | Autonomous | Write your own auto routine |
| [7](#lesson-7--becoming-a-software-member) | Becoming a software member | Your first real PR to the robot code |

---

## Lesson 0 — Tooling setup

**Goal:** a laptop that can run our robot code.

1. **Get a GitHub account** and send your username to a programming lead so they can add you to the
   [Saint-Francis-Robotics-Team2367](https://github.com/Saint-Francis-Robotics-Team2367) org.
2. **Install the tools.** Follow the
   [setup guide in the robot code README](https://github.com/Saint-Francis-Robotics-Team2367/2026dev#setup--from-a-fresh-windows-11-laptop).
   It walks through Python 3.14, Git, cloning, the virtual environment, and RobotPy.
3. **Install VS Code** and accept the recommended extensions when you open the repo (WPILib,
   Python, Pylance, Black). Then select the `.venv` interpreter
   ([details](https://github.com/Saint-Francis-Robotics-Team2367/2026dev/blob/main/docs/development.md#vs-code)).

> **You don't need the full WPILib installer.** It's built for Java and C++. For Python, VS Code
> plus our `.venv` is enough.

**Checkpoint:**
```powershell
robotpy test        # all tests pass
robotpy sim         # the simulator opens
```
In the sim, click **Autonomous** and watch the robot drive itself. Stuck? That's normal. Post the
*exact* error message in the team chat or grab a lead.

---

## Lesson 1 — Python basics

**Goal:** be comfortable reading and changing Python code. You don't need to master it.

**Read** (skip whatever you already know):
- [The official Python tutorial](https://docs.python.org/3/tutorial/), sections 3–9: variables,
  functions, `if`/`for`, lists and dicts, modules, and **classes**. Our code uses classes
  everywhere, so spend extra time on section 9.
- The [Python basics](../glossary.md#python-basics) part of the glossary.

**Practice:** small programs help a lot. Try a "vending machine" program: a class that tracks
inventory and money, with methods to insert coins and buy items. It uses the same ideas as a
subsystem (an object that holds state and exposes methods).

**Checkpoint:** open `constants.py` and `commands/drive.py` in our robot code and explain to a lead
what each line does. Include what `self`, `__init__`, and `super().__init__()` mean.

---

## Lesson 2 — Git and GitHub

**Goal:** be able to make a change and get it merged the way we do it.

**Read:**
- Our [Git workflow](git-workflow.md). This is required.
- [GitHub Skills — Introduction to GitHub](https://skills.github.com/), an interactive course that
  takes about an hour.
- Optional: [Pro Git, chapters 1–3](https://git-scm.com/book/en/v2) if you want the full picture.

**Checkpoint:** make a branch in *this* docs repo, add a glossary term you had to look up (or fix
anything confusing), and open a pull request. Get it reviewed and merged.

---

## Lesson 3 — How robot code works

**Goal:** understand the command-based framework before reading our code.

**Read**, in order:
1. [WPILib: What is WPILib?](https://docs.wpilib.org/en/stable/docs/software/what-is-wpilib.html)
2. [WPILib: Command-Based Programming](https://docs.wpilib.org/en/stable/docs/software/commandbased/index.html).
   Read *What Is "Command-Based" Programming?*, *Commands*, *Subsystems*, *Binding Commands to
   Triggers*, and *Structuring a Command-Based Robot Project*. Most code examples have a
   **Python** tab.
3. [WPILib: Coordinate System](https://docs.wpilib.org/en/stable/docs/software/basic-programming/coordinate-system.html).
   Remember that +x is forward and +y is *left*.

**Key ideas:** a **subsystem** owns hardware, a **command** is a behavior that *requires*
subsystems, the **scheduler** runs commands every 20 ms loop, and **triggers** start commands
from buttons.

**Checkpoint:** draw (on paper or a whiteboard) how `robot.py`, `RobotContainer`, `Drivetrain`,
and `DriveByController` relate. Then compare it with the diagram in our
[`docs/architecture.md`](https://github.com/Saint-Francis-Robotics-Team2367/2026dev/blob/main/docs/architecture.md).

---

## Lesson 4 — Codebase and simulation

**Goal:** know your way around our code and use the simulator and dashboards to see what it does.

**Tour the code** in this order:

| File | What to look for |
|------|------------------|
| `robot.py` | The entry point. Notice how short it is. |
| `robotcontainer.py` | Where subsystems and controllers get created and wired together. |
| `commands/drive.py` | A command: reads the joysticks and calls the drivetrain. |
| `subsystems/drivetrain.py` | A subsystem: kinematics, odometry, Field2d. |
| `subsystems/swervemodule.py` | One swerve wheel: two motors and an encoder. |
| `commands/auto.py` | A simple autonomous routine built from smaller commands. |
| `constants.py` | Every number, with units. |

**Read:** our [`docs/simulation.md`](https://github.com/Saint-Francis-Robotics-Team2367/2026dev/blob/main/docs/simulation.md).
It covers driving with the keyboard in sim and connecting AdvantageScope and Elastic.

**Checkpoint:**
1. Drive the robot in teleop using the keyboard in `robotpy sim`.
2. Plot `Drivetrain/speedMps` in AdvantageScope while it drives.
3. Change a value in `demo_auto` (`commands/auto.py`), run the sim, and confirm the robot does
   what you expected. Don't commit this change; it's just practice.

---

## Lesson 5 — Drivetrain

**Goal:** understand how a joystick push becomes four wheel commands.

**Read:**
- [WPILib: Kinematics and Odometry](https://docs.wpilib.org/en/stable/docs/software/kinematics-and-odometry/index.html),
  the intro and the swerve pages. Remember that our 2027 code uses different class names (see the
  [2027 migration notes](https://github.com/Saint-Francis-Robotics-Team2367/2026dev/blob/main/docs/2027-migration.md)).
- [WPILib: PID introduction](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/index.html).
  Try the interactive tuning pages.
- The *Data flow each loop* section of our
  [`docs/architecture.md`](https://github.com/Saint-Francis-Robotics-Team2367/2026dev/blob/main/docs/architecture.md#data-flow-each-loop-teleop).

**Checkpoint:** explain to a lead, step by step, what happens in one loop when the driver pushes the
left stick forward: deadband, field-relative to robot-relative conversion, kinematics,
desaturation, optimize, and the TalonFX closed loops.

---

## Lesson 6 — Autonomous

**Goal:** write a routine that drives the robot with no driver.

**Read:**
- [WPILib: Command Compositions](https://docs.wpilib.org/en/stable/docs/software/commandbased/command-compositions.html)
  (sequence, parallel, race, deadline).
- Skim [PathPlanner](https://pathplanner.dev/) and [Choreo](https://choreo.autos/). We'll likely
  use one of them for real autos.

**Checkpoint:** write a new auto routine that drives a square, ending where it started and facing the
same way. Then watch it in sim and check the final pose in AdvantageScope. This one can be a real PR.

---

## Lesson 7 — Becoming a software member

**Goal:** contribute to the real robot code on your own.

You're a full software member when you've done all of these:

- [ ] Finished the checkpoints for lessons 0–6.
- [ ] Merged one PR to the robot code that a lead assigned (a bug fix, a small feature, or tests),
      with CI passing.
- [ ] Reviewed someone else's PR and left at least one useful comment.
- [ ] Read the [expectations and safety](expectations-and-safety.md) page.

After that, pick an area to go deeper in (see [Resources](resources.md)): controls, vision,
autonomous, simulation, or tooling.

---

## Tips from older members

- **Read the error message.** The whole thing, especially the last line. Then paste it when you
  ask for help.
- **Sim first.** If it doesn't work in `robotpy sim`, it won't work on the robot.
- **Units are meters, radians, and seconds.** If something is 39× too big, someone mixed up inches
  and meters.
- **Copy from tutorials carefully.** Check every name against the 2027 migration notes.
- **Ask questions.** Nobody expects you to know this yet, and explaining things helps the person
  explaining too.
