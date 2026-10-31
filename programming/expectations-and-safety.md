---
title: Expectations & Robot Safety
parent: Programming
nav_order: 3
---

# Expectations & Robot Safety

What the programming subteam does through the year, what we expect from members, and how to stay
safe around a robot that runs your code.

## What we do through the year

| Season | When | What programmers do |
|--------|------|---------------------|
| **Fall / preseason** | September → kickoff | Training ([Getting Started](getting-started.md)). Practice projects. Get the drivetrain and tooling ready so they work on day one of build season. |
| **Build season** | Kickoff (early January) → first event | Write code for each new mechanism as it's designed. Work with mechanical and electrical on motors, sensors, and CAN IDs. Build autos. Tune on the real robot. |
| **Competition** | Event weekends | Fix bugs between matches, adjust autos, check logs after every match, and help the drive team. |
| **Offseason** | After the last event → summer | Try new ideas (vision, new path tools), clean up code, and write docs for next year. |

## What we expect

- **Communicate.** If a task is taking longer than expected, say so.
- **Own your tasks.** When you take a task, see it through to a merged PR, or hand it back clearly.
- **Ask for help early.** Being stuck for 20 minutes is fine. Being stuck for two meetings without
  saying anything isn't.
- **Leave things better than you found them.** If you learn something the hard way, add it to these
  docs.
- **Review code** when asked. See [Git workflow](git-workflow.md#reviewing-a-pull-request).

## Robot safety for programmers

Your code moves a heavy machine. Bugs in sim are funny; bugs on a real robot can hurt people or
break parts.

**Before you enable:**
- Make sure you know how to **disable instantly**. On the old NI Driver Station, **Enter** disables
  and the **spacebar** is the emergency stop. Check the shortcuts on the new 2027 Driver Station
  before your first test.
- Put the robot **on blocks** (wheels off the ground) when testing new drive code for the first time.
- Clear the area: hands, cables, tools, and people away from mechanisms.
- **Say "enabling!" out loud** and wait for people to step back.

**While testing:**
- Keep your hands on the keyboard, ready to disable. Watch the robot, not the screen.
- Start slow. Test at low speed or low output first, then increase.
- Test one new thing at a time.

General shop safety (safety glasses, tools, batteries) follows the team's shop rules.

