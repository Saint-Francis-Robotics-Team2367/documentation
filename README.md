---
title: Home
nav_order: 1
permalink: /
---

# Saint Francis Robotics — Team 2367 Docs

Welcome to the Lancers' FRC team handbook. It's the place to learn how we build, wire, and program
our robot. It's written for new members, and kept up to date by everyone.

**New programmer? Start with [Getting Started](programming/getting-started.md).**

## Sections

| Section | What's there |
|---------|--------------|
| [Programming](programming/index.md) | Lessons from fresh laptop to software member, our Git workflow, robot safety, and resources. |
| [Glossary](glossary.md) | Plain-English definitions for FRC, Python, WPILib, swerve, controls, vision, and more. |
| [Mechanical](mechanical/index.md) | *Coming soon.* |
| [Electrical](electrical/index.md) | *Coming soon.* |

**Robot code:** [Saint-Francis-Robotics-Team2367/2026dev](https://github.com/Saint-Francis-Robotics-Team2367/2026dev)
is our 2027-season code (Python / RobotPy, command-based swerve). Its `docs/` folder has the deep
technical details.

## Contributing

These docs are Markdown files in
[this repository](https://github.com/Saint-Francis-Robotics-Team2367/documentation), published
with GitHub Pages. To fix or add something, use **Edit this page on GitHub** at the bottom of any
page, or follow our [Git workflow](programming/git-workflow.md). If you just learned something the
hard way, write it down for the next person.

- **Write for someone in their first month.** Define jargon or link to the [glossary](glossary.md).
- **Mark 2027 changes** with **2027:** so readers know older tutorials differ.
- **Link, don't copy.** Point to the robot code's docs or vendor docs instead of duplicating them.
- **New page?** Put it in the right folder and start it with front matter so it shows up in the
  sidebar:

  ```yaml
  ---
  title: Intake Wiring
  parent: Electrical
  nav_order: 2
  ---
  ```

## Credits

The structure of these docs borrows ideas from other teams' public training material, especially
[971](https://github.com/frc971/training-2026/wiki), [3603](https://cybercoyotes.github.io/Programmers-Handbook/glossary/),
[4459](https://frc-4459.github.io/LGTR), and [573](https://team573programmingdocs.readthedocs.io/).
See [Resources](programming/resources.md#other-teams-training-guides).
