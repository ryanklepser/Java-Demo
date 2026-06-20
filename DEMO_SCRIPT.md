# Live Demo Script
## Centene Corporation — Java 11 to 17 Upgrade

> Total demo time: ~22 minutes. This script covers three phases:
> 1. **Pre-Launch Platform Walkthrough** (~4 min) — show the platform, differentiate from copilots
> 2. **Launch & Narrate** (~14 min) — kick off the prompt, narrate while Devin works
> 3. **PR Review** (~4 min) — walk through the output, tie back to value
>
> The goal: by the end, every person in the room has seen something that answers their #1 concern.

---

## Phase 1: Platform Walkthrough (~4 min)

> You're still on the slides at this point. Slide 12 says "Let's upgrade a real Java healthcare codebase. Right now." Pause. Let it land. Then say:

### 1A. Show the Repo Complexity (~60 sec)

**[Open GitHub tab: `github.com/ryanklepser/Java-Demo`]**

> SAY: "Before I start Devin, I want to show you what we're working with. This isn't a toy demo."

**[Click into the file tree — show the module folders]**

> SAY: "This is hapi-fhir at version 6.1.0 — an open-source implementation of the HL7 FHIR standard. Your interoperability teams may already use something like this. It has 51 Maven modules, over 3,500 Java files, and 64 pom.xml configurations."

**[Click into the root `pom.xml` — scroll to the properties section]**

> SAY: "Here's what matters. Java 11 source and target. Spring 5.3. Spring Boot 2.6. Hibernate 5.6. This is the starting point. Everything you see here needs to change."

> POINT TO: `<maven.compiler.source>11</maven.compiler.source>`

> SAY: "A manual upgrade of a codebase like this — 2-3 engineers, 4-6 weeks. That's for one service. Centene has a hundred fifty of these."

**[Pause. Let the scale register.]**

---

### 1B. Show the Devin Workspace (~60 sec)

**[Switch to Devin tab: `app.devin.ai` — the sessions page or a new session]**

> SAY: "This is Devin. It runs in the browser — no IDE plugins, no local installs, nothing for John's team to set up."

**[If possible, show a completed session from a dry run, or show the session history]**

> SAY: "Every session Devin runs is fully logged. You can see exactly what files it read, what commands it ran, what decisions it made, and why. Ethan, this is your audit trail."

**[Navigate to Knowledge section]**

> SAY: "These are guardrails — we call them Knowledge. I've configured Devin with explicit constraints: don't touch security classes, don't modify database migrations, always use Maven for builds. These aren't suggestions — they're enforced. Your security team defines the boundaries, and Devin operates within them."

> SAY: "And in a moment, I'll show you Playbooks — reusable procedures your team writes once and runs across every service."

> DIFFERENTIATION: "This is fundamentally different from GitHub Copilot or Amazon Q. Those tools suggest lines of code while you type. Devin takes a task — like a Jira ticket — and completes it end-to-end. It reads the codebase, makes changes across dozens of files, runs the build, fixes errors iteratively, and delivers a pull request. It's the difference between autocomplete and a teammate."

---

### 1C. Show Where the Output Goes (~45 sec)

**[Switch to GitHub tab — go to the Pull Requests tab (should be empty)]**

> SAY: "Right now there are zero pull requests. When Devin finishes, the PR will appear here — in your GitHub, in your repo, through your normal workflow."

**[Click into the Actions tab]**

> SAY: "Your CI pipeline runs on every PR. Your security scans run. Your code quality gates run. Devin doesn't bypass anything. John, you'd review this PR exactly like you review any other PR from a teammate."

> TO JOHN: "Nothing merges without your approval. You are the quality bar."

---

### 1D. Launch via Playbook (~60 sec)

**[Switch back to Devin — start a new session on `ryanklepser/Java-Demo`]**

> SAY: "Now let's kick it off. But instead of typing a prompt from scratch, I want to show you something."

**[In the new session input area, look for the playbook attachment option — click "Team" playbooks]**

> SAY: "These are Playbooks — reusable, standardized procedures that your team defines once and runs across any repo. Think of them as codified engineering runbooks."

**[Select "Java 11 → 17 Upgrade" — it appears as a blue tag attached to the session]**

> SAY: "We've built a Java 11 to 17 upgrade playbook. Let me walk you through what's in it."

**[Click the blue playbook tag to expand/preview the content so the room can see the structure]**

> SAY: "It's structured like a well-written Jira ticket — numbered steps, clear acceptance criteria. Update all pom.xml files, migrate javax to jakarta, upgrade Spring and Hibernate, run the build, fix errors iteratively. And notice the constraints at the bottom: don't touch security classes, don't touch database migrations. These are enforced guardrails."

> ENGAGE HASEEB: "Haseeb, this is where it gets interesting for your org. You define this playbook once — your best engineer writes the procedure — and then you run it against all 150 services. Same steps, same constraints, same quality bar. No copy-pasting prompts, no missed steps, no variation between teams."

> TO AJOY: "From a governance perspective, you're standardizing how upgrades are done across the org. One playbook, one process, fully auditable."

**[Hit Submit to launch the session with the playbook attached]**

> SAY: "One click. It's running. Let's watch."

---

## Phase 2: Narrate While Devin Works (~14 min)

> This is the longest phase. Your job: keep the room engaged without over-talking. Narrate key moments, ask the room questions, let silence build occasionally so they can watch. Don't explain every line — explain the pattern.

### Stage: Codebase Analysis (~2-3 min)

Devin will start by reading files — typically `pom.xml`, the module structure, and a few Java files to understand the codebase.

> WHEN DEVIN READS POM.XML:
> SAY: "Devin is doing exactly what any engineer would do on day one of an upgrade — reading the project configuration to understand what it's working with. It's checking the Java version, the dependency tree, the module structure."

> WHEN DEVIN EXPLORES THE FILE TREE:
> SAY: "It's mapping out the 51 modules. This is important because a Java upgrade isn't just changing one file — you need to update every module's pom.xml consistently, or you get version mismatches that break the build."

> ENGAGE JOHN: "John, when your team does a manual upgrade, do you start the same way? Reading the root pom first, then working through the modules?"

> OPTIONAL — IF ROOM IS QUIET:
> SAY: "One thing I want to point out — Devin isn't using a template or a script. It's reading this specific codebase and making decisions based on what it finds. If this project used Gradle instead of Maven, Devin would adapt. If it used Spring Boot 3 already, it would skip that step."

---

### Stage: pom.xml Updates (~2-3 min)

Devin will start modifying pom.xml files — changing compiler source/target, updating dependency versions.

> WHEN DEVIN STARTS EDITING POM FILES:
> SAY: "Now it's making changes. Watch the file list on the left — you'll see it working through the pom.xml files one by one. There are 64 of them across this project."

> WHEN MULTIPLE POMS ARE UPDATED:
> SAY: "It just updated the root pom and is now working through the child modules. Notice it's setting `maven.compiler.source` and `target` to 17 consistently. In a manual upgrade, missing one pom.xml is a classic mistake — it causes inconsistent bytecode versions that can fail silently until production."

> DIFFERENTIATION:
> SAY: "This is where the autonomous model really matters. Copilot can suggest a version number change if you're already in the file. Devin found all 64 pom files on its own, determined what needed to change, and is updating them systematically. Nobody had to open each file and ask for a suggestion."

> ENGAGE HASEEB: "Haseeb, when your team does this manually, how do they track which pom.xml files they've updated? Spreadsheet? Checklist? Or do they just hope they got them all?"

---

### Stage: javax to jakarta Migration (~3-4 min)

This is the most visually impressive part — Devin will be modifying import statements across hundreds of files.

> WHEN DEVIN STARTS IMPORT CHANGES:
> SAY: "Now we're into the big one — the javax-to-jakarta namespace migration. This is arguably the most tedious part of any Java 11 to 17 upgrade. Every `javax.servlet` becomes `jakarta.servlet`. Every `javax.persistence` becomes `jakarta.persistence`. Across thousands of files."

> AS FILES SCROLL BY:
> SAY: "Watch the file count. Devin is working through these systematically — it's not doing a blind find-and-replace. It's reading each file, understanding the context, and making the right substitution. Some javax packages stay javax — `javax.crypto`, for example, doesn't move to jakarta. Devin knows the difference."

> ENGAGE JOHN: "John, have you ever done a javax-to-jakarta migration by hand? How long did it take, and what went wrong?"

> COMPETITIVE DIFFERENTIATION:
> SAY: "If you tried to do this with a regex or a find-and-replace script, you'd break things. Some javax packages don't migrate. Some have different jakarta equivalents depending on the version. Devin understands the semantic meaning, not just the text pattern."

> OPTIONAL — IF ETHAN LOOKS ENGAGED:
> SAY: "Ethan, notice that Devin is not touching any files in the security packages. We told it not to modify classes containing Security, Authorization, or Authentication keywords — and it's respecting that constraint. You'll be able to verify this in the PR diff."

---

### Stage: Framework Version Updates (~2-3 min)

Devin will update Spring, Hibernate, and other dependency versions.

> WHEN SPRING/HIBERNATE VERSIONS CHANGE:
> SAY: "Now it's handling the framework upgrades — Spring 5 to 6, Spring Boot 2 to 3, Hibernate 5 to 6. This isn't just changing version numbers — these are major version bumps with breaking API changes. Spring 6 requires Jakarta EE 9+. Hibernate 6 changes the session factory API. Devin is updating the versions and the code that depends on them."

> SAY: "This is the part of an upgrade where things get complicated. The dependency tree has to be internally consistent — you can't run Spring 6 with Hibernate 5. Devin is resolving these transitive dependency conflicts as it goes."

> ENGAGE HASEEB: "Haseeb, when your team does framework upgrades, how long does the dependency resolution phase usually take? Is it the kind of thing that burns a few days of back-and-forth with Maven?"

---

### Stage: Build Attempt & Error Fixing (~3-4 min)

This is the most compelling stage. Devin will run `mvn install`, hit compilation errors, read them, fix them, and re-run.

> WHEN DEVIN RUNS THE BUILD:
> SAY: "Devin is now running the Maven build to see if everything compiles. With a project this size and this many changes, there will almost certainly be compilation errors on the first pass. That's expected — it's the same thing that would happen to a human."

> WHEN THE BUILD FAILS:
> SAY: "There it is — compilation errors. Now watch what happens next. This is the part that really differentiates Devin."

**[Pause. Let them watch Devin read the error, navigate to the file, make a fix.]**

> SAY: "It read the error message, identified the file, understood the root cause, and applied a fix. Now it's going to re-run the build. This iterate-until-green loop is where Devin really earns its keep. A human would do exactly this — but Devin does it without context-switching, without getting frustrated, and without needing a coffee break."

> ENGAGE JOHN: "John, does this look like your debugging workflow? Read the error, find the file, fix the issue, rebuild?"

> IF MULTIPLE ITERATIONS:
> SAY: "It's iterating again. This is normal — complex upgrades often take several passes. The important thing is that Devin doesn't give up. It keeps going until the build passes or it exhausts its approaches and asks for help."

> DIFFERENTIATION:
> SAY: "This is the core difference between Devin and every other AI coding tool. Copilot can suggest a line. Devin completes a task. It has a terminal, a browser, a file system — it's a full software engineer, not a text predictor."

> WHEN THE BUILD PASSES (or mostly passes):
> SAY: "Build success. [Or: 'Most modules are passing — there are a few edge cases it's still working through.'] That's a codebase with 3,500 Java files, 51 modules, and a major version upgrade — compiled and validated."

---

### Stage: PR Creation (~1 min)

> WHEN DEVIN CREATES THE PR:
> SAY: "And there's the pull request. Let's go look at it."

---

## Phase 3: PR Review & Close (~4 min)

**[Switch to GitHub — open the PR that Devin just created]**

### 3A. PR Overview (~1 min)

> SAY: "Here's what Devin delivered. Let's look at the summary."

**[Read or paraphrase the PR description]**

> SAY: "Devin generated this description automatically — it summarizes every category of change. This is what your engineers would see in their review queue. No different from any other PR."

**[Show the file count]**

> SAY: "X files changed across Y modules. That's the scope of a manual 4-6 week project, delivered as a single reviewable PR."

---

### 3B. Key Diffs (~2 min)

**[Click into a few specific file changes]**

> SHOW: A `pom.xml` diff — `11` changed to `17`
> SAY: "Compiler version — straightforward but has to be done consistently across all 64 files."

> SHOW: A Java file with `javax.servlet` changed to `jakarta.servlet`
> SAY: "Namespace migration — this happened across hundreds of files. Each one done correctly in context."

> SHOW: A Spring configuration or Hibernate entity change
> SAY: "Framework-level API changes — this is the hard part of any upgrade. Devin didn't just change the version number; it updated the code that depends on the new API."

> ENGAGE JOHN: "John, what do you think? Is this code you'd be comfortable reviewing and merging? Anything here that looks wrong or that you'd want to change?"

---

### 3C. Security Callout (~1 min)

> TO ETHAN: "Ethan, I want to address security explicitly."

> SAY: "First — Devin respected the constraints. You can search this diff for any security-related class. It didn't touch them."

**[Optional: Use Ctrl+F in the diff to search for 'Security' or 'Authorization' to prove the point]**

> SAY: "Second — this is a standard GitHub PR. Your CI runs on it. Your security scans run on it. Your code review happens on it. Nothing goes to production without human approval."

> SAY: "Third — the full session transcript is available. Every file Devin read, every command it ran, every decision it made is logged. If you need to audit this for your CAM program, it's all there."

> SAY: "And fourth — Devin ran in an isolated environment. It accessed the repo through standard GitHub permissions — the same way your developers do. No production access. No database access. No PHI."

---

## Transition Back to Slides

> SAY: "Let me switch back to the deck for a moment — I want to put what we just saw in the context of Centene's portfolio."

**[Switch back to slides — advance to Slide 14: "What Just Happened"]**

> Continue with the deck from here.

---

## Contingency Plans

### If the build doesn't pass within the demo window:

> SAY: "The build is still iterating — which is expected for a codebase this complex. Rather than wait, let me show you a completed session from a previous run."

**[Open a DryRun repo with a completed PR, or show screenshots]**

> SAY: "This is the same codebase, same prompt, completed run. Here's the PR, here's the diff, here's the build result. The live session will finish in the background, and I'll share the result with you after the meeting."

### If Devin gets stuck:

> SAY: "Devin hit a tricky edge case. In production use, you'd either refine the prompt to give more guidance, or a human would handle this specific file. The point isn't that Devin handles 100% of edge cases — it's that it handles 95%, and your engineers spend their time on the interesting 5% instead of the mechanical 95%."

### If someone asks "can it do X?":

> SAY: "Great question. Let me note that down — we can either try it right now if there's time, or we can set up a follow-up session focused on [X]. Part of the pilot is discovering exactly which use cases work best for your team."

### If Ethan pushes hard on security:

> SAY: "Ethan, I respect the thoroughness. Rather than try to answer every question right now, can we schedule a dedicated security review call? I'll bring our security engineering lead, we'll share our SOC 2 report and pen test results, and we can go through your vendor security questionnaire line by line. That's a more productive way to do justice to your concerns."

---

## Key Phrases to Have Ready

| Situation | Phrase |
|-----------|--------|
| Showing scope | "3,500 Java files, 51 modules, 64 pom configurations — this is real enterprise complexity." |
| After javax migration | "That namespace migration alone would take an engineer 2-3 days of find-and-replace. Devin did it in minutes." |
| Build error → fix cycle | "Read the error, find the file, fix the issue, rebuild. Exactly what a human would do — but without context-switching." |
| Copilot comparison | "Copilot suggests lines. Devin completes tasks." |
| Security reassurance | "Nothing goes to production without your team's review. Full stop." |
| Audit trail | "Every action is logged. Every file read, every command run. Ethan, this is your audit trail." |
| Scale | "What you just saw was one service. Devin runs 150 of these in parallel. 150 PRs, overnight." |
| Urgency | "The Voluntary Separation Program means you need to do more with fewer people. Devin multiplies the engineers you keep." |
| ROI | "$5.2M manual. $370K with Devin. $4.8M in engineering capacity recovered." |
| Risk mitigation | "The pilot is 5 services, 2 weeks, non-critical workloads. If it doesn't work, you've lost nothing." |
