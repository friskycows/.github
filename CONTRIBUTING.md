# Contributing to 8780F Friskycows

This is the guide for how we write code, use git, and keep this repo clean. Read it. Follow it.

---

## Comments in your code

**Comment everything.** Seriously. You will forget what your code does in two days. Your teammates will have no idea. Future you will be angry at past you.

### General rule
Every function, every major block of logic, write a short comment above it explaining what it does.

```cpp
// Spins the intake motor forward to pick up a ring
intakeMotor.spin(forward, 100, pct);
```

That's it. One line. It takes five seconds and it will save you hours of debugging.

### Autonomous routines — comment every single action
For autonomous, comment **every motion and action**. When something breaks during a match (and it will), you need to be able to look at your code and immediately know which step failed.

```cpp
// Drive forward 24 inches to reach the goal
chassis.driveFor(24, inches);

// Wait for the robot to fully stop before turning
wait(200, msec);

// Turn 90 degrees right to align with the goal
chassis.turnToHeading(90, 1000);

// Extend the clamp to grab the mobile goal
clampPiston.set(true);

// Drive backward 12 inches to pull the goal into our zone
chassis.driveFor(-12, inches);
```

Don't be lazy about this. The more specific the comment, the easier debugging becomes. If the robot does something wrong, you can check off each comment like a checklist to figure out exactly where it went wrong.

---

## Git workflow

### Setup
- This repo lives on GitHub. Everyone on the team should have access.
- Clone it to your machine before you start writing any code.
- Never write code directly in the GitHub web editor for anything beyond tiny fixes.

### The golden rule: if it works, commit it
Every single time you get something working, a new autonomous routine, a tuned PID value, a fixed bug, **commit it immediately**. Don't wait until "you're done." You're never done, and if you break something later, you want a clean restore point.

---

## Branch strategy

### `main` is sacred
The `main` branch must always be in a working state. It should represent the best version of the code we'd actually run at a competition. Never push broken code to `main`.

### Create a branch for each practice day or task
Before you start working, create a branch. Name it something descriptive:

```
practice/2024-01-15
feature/autonomous-red-side
fix/intake-motor-stalling
tuning/drivetrain-pid
```

The format should make it obvious what the branch is for and roughly when it was created.

### Merging into main
When your work on a branch is tested and working:
1. Open a Pull Request (PR) from your branch into `main`
2. Have at least one other team member review it if possible
3. Make sure it doesn't break anything that was already working
4. Merge it

**Never push directly to `main`.** Even if you're working alone. The discipline matters.

### Main branch protection
We use branch protection rules on `main`:
- Direct pushes to `main` are blocked
- All changes must come through a Pull Request
- At least one approval is required before merging

This isn't bureaucracy, it's how you make sure you never accidentally nuke working code the night before a competition.

---

## Git discipline

Even if you're working alone, treat this repo like a team project. Here's why:

- Sloppy branches and vague commits make it impossible to trace back what changed and when
- You will look at old commits to find code that used to work. You need those commits to make sense
- Good habits here carry over everywhere, not just VEX

### Keep branches clean
- Don't leave dead branches sitting around forever. Delete them after they're merged.
- Don't cram weeks of changes into a single branch. One task or one practice day = one branch.

### Commit often
Small commits are better than big ones. If you commit every 20–30 minutes while you're working, you have much finer control over what you can roll back to.

---

## Writing good commit messages

Bad commit messages are useless. Here's the difference:

| Bad ❌ | Good ✅ |
|---|---|
| `stuff` | `Fix intake motor reversing direction on start` |
| `asdfgh` | `Add red-side autonomous routine for near-goal path` |
| `changes` | `Tune drivetrain PID: lower kD to reduce oscillation` |
| `it works` | `Get 15-point autonomous working with clamp + drive sequence` |
| `fix` | `Fix clamp piston not releasing after grabbing mobile goal` |

### Format to follow
```
Short summary of what changed (under 72 characters)

Optional: longer explanation if needed. Why did you make this change?
What was the problem? What did you try that didn't work?
```

The short summary should complete the sentence: *"If applied, this commit will ______."*

Examples:
- `Add skills autonomous route for near-side rings`
- `Fix robot overshooting turn by adjusting turn timeout`
- `Increase intake speed from 80% to 100% for ring pickup`

---

## Summary checklist

Before you push anything, ask yourself:

- [ ] Did I comment my code, especially every autonomous action?
- [ ] Am I on a branch (not `main`)?
- [ ] Is my branch name descriptive?
- [ ] Have I committed every time something new worked?
- [ ] Are my commit messages actually descriptive?
- [ ] Is the code I'm merging to `main` tested and working?
