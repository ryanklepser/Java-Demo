# Devin Demo Plan: Java 11 → 17 Upgrade for Centene Corporation

## Target Company Profile

**Company:** Centene Corporation (NYSE: CNC)  
**Headquarters:** St. Louis, Missouri  
**Revenue:** ~$195B (Fortune 25)  
**Employees:** ~70,000+ (including ~20,000 in IT/technology)  
**Industry:** Managed healthcare — Medicaid, Medicare, Health Insurance Marketplace  

Centene operates one of the largest healthcare IT organizations in the U.S. Their technology division maintains Java-based platforms for claims processing, member enrollment, care management, and FHIR-based health data interoperability across 30+ state programs. They have a dedicated Java Development team of 23+ engineers, an Application Development group of 313+, and a broader IT & Development org of 400+ people. Their tech stack includes Java, Spring Boot, AWS, and Backstage for internal developer platforms.

**Why Centene cares about Java upgrades:**
- Java 11 reached end of public updates — compliance and security risk for HIPAA-regulated systems
- Centene's claims and enrollment platforms are Java/Spring Boot monoliths that need modernization
- Developer productivity: Java 17 features (records, sealed classes, pattern matching) reduce boilerplate
- Spring Boot 2.x → 3.x is required for continued security patch support
- Manual upgrades across hundreds of microservices consume months of engineering capacity

---

## Mock Demo Stakeholders (Roles to Play)

| # | Role | Name (suggested) | Key Concerns |
|---|------|-------------------|--------------|
| 1 | **SVP, CTO — Technology Advancement** | "John" | AI ROI, developer velocity metrics, strategic modernization roadmap, how Devin fits into their existing SDLC. Wants to see time-to-completion data and parallelization across services. |
| 2 | **SVP & CIO — Markets & Health Products** | "Ajoy" | Risk mitigation for production systems, impact on sprint velocity during migration, rollback strategy, compliance with Centene's change management process. Needs to justify budget. |
| 3 | **Sr. Director, Information Security** | "Maria" | Java 11 EOL CVE exposure, HIPAA audit implications, security of AI-generated code, data residency (does Devin see PHI?), javax→jakarta security class changes, SOC 2 compliance of Devin platform. |

**Dynamics to expect:**
- "John" (CTO) will be most enthusiastic — lean into developer productivity and AI-augmented engineering
- "Ajoy" (CIO) will ask about cost, timeline, and organizational impact — have TCO comparisons ready
- "Maria" (Security) will probe on data handling, code review process, and whether Devin modifies security/auth classes — emphasize Devin's configurable guardrails and that all changes go through standard PR review

---

## Meeting Agenda (40 Minutes Total)

| Time | Duration | Section | Description |
|------|----------|---------|-------------|
| 0:00 | 5 min | **Welcome & Discovery** | Introductions. Confirm Centene's modernization priorities. Ask: "How many Java services are you running on 11 or older? What's your current upgrade timeline?" |
| 0:05 | 5 min | **The Problem** | Frame the Java 11 EOL challenge at scale. Show the scope: javax→jakarta namespace migration, Spring Boot 2→3, Hibernate 5→6. Reference Centene's 300+ app dev engineers who could be unblocked. |
| 0:10 | 3 min | **Devin Overview** | Brief intro to Devin as an AI software engineer. Autonomous agent that understands codebases, creates PRs, runs tests, iterates on CI failures. Not a copilot — a teammate. |
| 0:13 | 22 min | **Live Demo: Java 11→17 on hapi-fhir** | *(see detailed script below)* |
| 0:35 | 5 min | **Wrap-Up & Next Steps** | Recap value. Propose a paid pilot: pick 5 of Centene's Java 11 services, run Devin on them in parallel, measure time saved vs. manual. Offer to set up a sandbox environment. |

---

## Live Demo Script (20–25 Minutes)

> **Reference:** [Devin Java Upgrades Guide](https://docs.devin.ai/use-cases/examples/java-upgrades)

### Demo Repository

**Repo:** Fork of [hapifhir/hapi-fhir](https://github.com/hapifhir/hapi-fhir) at tag `6.1.0`  
**Why this repo:**
- Real-world, production-grade Java healthcare project (FHIR standard — directly relevant to Centene's interoperability work)
- 3,572 Java files across 51 Maven modules and 64 pom.xml files
- Currently on Java 11 (`maven.compiler.source=11`) with javax.* dependencies
- Uses Spring 5.3, Spring Boot 2.6, Hibernate 5.6 — all need major version bumps for Java 17
- Open source (Apache 2.0) — no IP concerns for demo

### Pre-Demo Setup (done before the meeting)

1. Fork `hapifhir/hapi-fhir` to your GitHub account
2. Create a branch from the `6.1.0` tag: `git checkout -b java-11-baseline 6.1.0`
3. Push this branch and set it as the default branch on the fork
4. Confirm the fork builds on Java 11: `mvn -P FASTINSTALL install`
5. Have the Devin web app open and authenticated
6. Have a second browser tab with the fork's GitHub page open
7. Pre-load the Devin session page so you can immediately start typing the prompt

### Step-by-Step Demo Flow

#### Step 1: Set the Scene (2 min)
**[Show the repo in browser]**

> "This is hapi-fhir — an open-source Java implementation of the HL7 FHIR standard that your interoperability teams may already be familiar with. It's a large, real-world codebase: 3,500+ Java files, 51 Maven modules, and it's currently on Java 11 with Spring Boot 2.6 and Hibernate 5.6. This is representative of the kind of services you'd need to upgrade."

**[Show the pom.xml]** — Point out:
```xml
<maven.compiler.source>11</maven.compiler.source>
<maven.compiler.target>11</maven.compiler.target>
<spring_version>5.3.20</spring_version>
<spring_boot_version>2.6.7</spring_boot_version>
<hibernate_version>5.6.2.Final</hibernate_version>
```

> "A manual upgrade of this codebase would typically take a team of 2-3 engineers 4-6 weeks. Let's see what Devin can do."

#### Step 2: Launch Devin with a Prompt (2 min)
**[Switch to Devin web app]**

Type the following prompt (or use a pre-built playbook):

```
Upgrade this Java project from Java 11 to Java 17.

## Procedure
1. Verify the project is currently on Java 11
2. Update maven.compiler.source, maven.compiler.target, and maven.compiler.release to 17 in all pom.xml files
3. Migrate all javax.* imports to jakarta.* equivalents (javax.servlet → jakarta.servlet, javax.annotation → jakarta.annotation, etc.)
4. Update Spring Framework from 5.x to 6.x and Spring Boot from 2.x to 3.x
5. Update Hibernate from 5.x to 6.x
6. Replace any deprecated Java 11 APIs with Java 17 equivalents
7. Update any remaining dependency versions for Java 17 compatibility
8. Run mvn -P FASTINSTALL install to verify the build compiles
9. Fix any compilation errors iteratively until the build passes

## Important
- Do NOT modify any security-related classes (containing Security, Permission, Authorization, Authentication, etc.)
- Do NOT modify database migration classes
- Create a single PR with all changes
```

> "Notice I'm giving Devin a structured prompt — just like you'd give a ticket to a junior developer. I'm telling it what to do, in what order, and what constraints to respect. This is aligned with Devin's [prompting best practices](https://docs.devin.ai/learn-about-devin/prompting)."

#### Step 3: Watch Devin Work (10-12 min)
**[Narrate as Devin works in real-time]**

Devin will typically:

1. **Explore the codebase** — Read pom.xml, identify the module structure, check current Java version
   > "Devin is doing what any engineer would do first — understanding the project before making changes."

2. **Update compiler settings** — Modify all 64 pom.xml files to set Java 17
   > "It found all 64 pom.xml files across the project and is updating them systematically. No missed modules."

3. **Migrate javax → jakarta** — Find and replace namespace imports across thousands of files
   > "This is the most tedious part of a Java 11→17 upgrade — the javax to jakarta namespace migration. Devin is handling this across 3,500+ files. This alone would take an engineer days of find-and-replace work."

4. **Update dependency versions** — Spring, Hibernate, and transitive dependencies
   > "Now it's updating the major framework versions. Notice it's not just bumping numbers — it's checking compatibility between Spring 6, Hibernate 6, and the rest of the dependency tree."

5. **Attempt a build** — Run `mvn -P FASTINSTALL install`
   > "Devin is now running the build to see if everything compiles. With a project this size, there will likely be some compilation errors to fix."

6. **Iterate on failures** — Fix compilation errors, re-run build
   > "It hit a compilation error — and now it's reading the error, understanding the fix, and applying it. This iterate-until-green loop is where Devin really shines. A human would do exactly this, but Devin does it without context-switching or getting frustrated."

#### Step 4: Show the PR (3-5 min)
**[Switch to GitHub when the PR is created]**

> "Devin has created a pull request with all the changes. Let's look at what it did."

Walk through:
- **PR description** — Devin generates a summary of all changes
- **Files changed** — Show the scope (dozens of files across multiple modules)
- **Specific diffs** — Show a few key changes:
  - pom.xml compiler settings: `11` → `17`
  - An import change: `javax.servlet` → `jakarta.servlet`
  - A Spring configuration update
  - A Hibernate entity annotation change

> "Every one of these changes goes through your normal PR review process. Your engineers review the diff, your CI runs, your security scans execute — Devin doesn't bypass any of your existing quality gates."

#### Step 5: Address the Security Question (2 min)

> "Maria, I know you're thinking about security. A few things to note:
> 1. Devin was instructed NOT to touch security classes — and it respected that constraint. You can verify in the diff.
> 2. All changes are in a PR — nothing goes to production without human review.
> 3. Devin runs in an isolated environment. It accesses your repo through standard Git — it doesn't have access to your production systems or data.
> 4. Devin is SOC 2 Type II compliant. We can share our security documentation."

---

## Demo Environment Setup Guide (Step-by-Step)

### Prerequisites
- GitHub account with fork permissions
- Devin account with active subscription ([app.devin.ai](https://app.devin.ai))
- Java 11 JDK installed locally (for verifying the baseline build)
- Java 17 JDK installed locally (for verifying the upgraded build)
- Maven 3.8+ installed locally

### Step 1: Fork and Prepare the Repository

```bash
# 1. Fork hapifhir/hapi-fhir on GitHub (use the GitHub UI)
# 2. Clone your fork
git clone https://github.com/<your-username>/hapi-fhir.git
cd hapi-fhir

# 3. Create a branch from the Java 11 version (tag 6.1.0)
git checkout -b java-11-baseline 6.1.0

# 4. Push the branch
git push origin java-11-baseline

# 5. On GitHub, set java-11-baseline as the default branch
#    (Settings → Branches → Default branch → change to java-11-baseline)
```

### Step 2: Verify the Baseline Builds

```bash
# Ensure JAVA_HOME points to Java 11
export JAVA_HOME=$(/usr/libexec/java_home -v 11)

# Run the fast build (skip tests — full test suite takes 1+ hour)
mvn -P FASTINSTALL install

# Expected: BUILD SUCCESS
# This confirms the 6.1.0 baseline compiles on Java 11
```

### Step 3: Configure Devin Environment

1. **Connect the repo to Devin:**
   - Go to [app.devin.ai](https://app.devin.ai)
   - Navigate to Settings → Repositories
   - Connect your forked `hapi-fhir` repo

2. **Set up a Devin blueprint** (optional but recommended for repeatable demos):
   - Go to Settings → Environment → Blueprints
   - Add a repo-level blueprint for your fork:
   ```yaml
   initialize:
     - apt-get update && apt-get install -y openjdk-11-jdk openjdk-17-jdk maven
     - update-java-alternatives -s java-1.11.0-openjdk-amd64
   ```

3. **Pre-build a Devin Playbook** (optional — for polished demos):
   - Go to Playbooks in the Devin sidebar
   - Create a playbook titled "Java 11 to 17 Upgrade" with the prompt from Step 2 above
   - Reference: [Devin Playbooks Guide](https://docs.devin.ai/product-guides/creating-playbooks)

### Step 4: Pre-Demo Dry Run

**CRITICAL: Always do a full dry run before the customer meeting.**

1. Launch a Devin session with the upgrade prompt against your fork
2. Let it run to completion (expect 30-60 min for a repo this size)
3. Review the resulting PR — note which files were changed and any issues
4. Keep the session URL handy — if the live demo hits issues, you can show the pre-recorded session
5. Take screenshots of key moments (Devin analyzing code, creating PR, fixing build errors)

### Step 5: Day-of-Meeting Checklist

- [ ] Laptop charged, reliable internet connection
- [ ] Browser tabs pre-loaded:
  - [ ] Devin web app (logged in)
  - [ ] GitHub fork (on `java-11-baseline` branch, pom.xml open)
  - [ ] This demo plan (for reference)
- [ ] Backup: pre-recorded Devin session URL ready in case live demo stalls
- [ ] Backup: screenshots of a successful PR from dry run
- [ ] Slide deck loaded (if using one for the intro)
- [ ] Verify Devin account has available session capacity

---

## Key Talking Points by Stakeholder

### For the CTO ("John")
- **Developer velocity:** "Your 300+ app dev engineers spend weeks on manual upgrade work. Devin parallelizes this — run 10 services simultaneously, get PRs for all of them overnight."
- **Scale:** "This isn't a copilot that helps one developer type faster. This is an autonomous agent that takes tickets off your backlog."
- **Adoption:** "Devin integrates into your existing workflow — GitHub PRs, CI/CD, code review. No new tools to learn."
- **Competitive reference:** Other Fortune 50 healthcare organizations are already using AI-assisted code modernization to hit their Java 17 deadlines ahead of schedule.

### For the CIO ("Ajoy")
- **Cost model:** "Compare the cost of Devin licenses vs. the engineering hours saved. A manual upgrade of 50 Java services at 4 weeks each = 200 engineer-weeks. Devin can reduce that to 20 engineer-weeks of review."
- **Risk mitigation:** "Every change goes through your existing PR review, CI, and security scanning. Devin doesn't bypass your process — it accelerates it."
- **Rollback:** "Each upgrade is a PR. If something breaks, revert the PR. No different from any other code change."
- **Phased rollout:** "Start with 5 non-critical services. Measure results. Then expand."

### For the Security Director ("Maria")
- **Data handling:** "Devin accesses your code through GitHub — the same permissions model your developers use. It doesn't access production databases, PHI, or internal networks."
- **SOC 2:** "Devin is SOC 2 Type II certified. We can provide our security whitepaper and respond to your vendor security questionnaire."
- **Code guardrails:** "As you saw in the demo, we instructed Devin not to modify security classes — and it complied. You can enforce these constraints via playbooks and knowledge notes."
- **Audit trail:** "Every Devin session has a full transcript — every file read, every command run, every decision made. Complete auditability."
- **javax→jakarta security impact:** "The namespace migration from javax.security to jakarta.security is a mechanical change. Devin flags these for human review rather than auto-applying them."

---

## Objection Handling

| Objection | Response |
|-----------|----------|
| "How do we know the generated code is correct?" | "Same way you know any code is correct — code review, CI, tests. Devin creates PRs that go through your standard process. Nothing merges without human approval." |
| "What if Devin makes a mistake in a critical system?" | "Devin doesn't deploy. It creates PRs. Your team reviews and merges. The blast radius of a Devin mistake is identical to a developer mistake — caught by your existing quality gates." |
| "We already use GitHub Copilot." | "Copilot helps developers type faster. Devin takes entire tasks off your plate. They're complementary — Copilot for in-IDE autocomplete, Devin for autonomous ticket completion." |
| "Our codebase is proprietary." | "Devin runs in isolated environments. Your code is processed in transit for the session and not retained. We're SOC 2 certified and can sign your DPA/BAA." |
| "This seems expensive for a migration we'll do once." | "Java upgrades are never 'once.' Java 21 is next. Spring Boot 4 is coming. Devin is a permanent team member for ongoing modernization, test generation, bug fixes, and more." |

---

## Follow-Up Email Template

**Subject:** Devin Demo for Centene — Java Modernization at Scale

Hi [CTO/CIO/Security Lead names],

Thank you for your time today. As discussed, here's a summary of what we covered:

**The Challenge:** Centene's Java 11 → 17 upgrade across your claims, enrollment, and care management platforms represents months of manual engineering effort, with each service requiring pom.xml updates, javax→jakarta migration, Spring Boot 2→3, and Hibernate 5→6 changes.

**What We Demonstrated:** Devin autonomously upgrading hapi-fhir (3,500+ Java files, 51 Maven modules) from Java 11 to 17, including dependency updates, namespace migrations, and iterative build fixes — producing a reviewable PR through your standard GitHub workflow.

**Proposed Pilot:**
- Select 5 Java 11 services from your portfolio
- Devin runs upgrade sessions in parallel (overnight)
- Your engineers review the PRs (estimate: 2-4 hours per service vs. 2-4 weeks manually)
- Measure: time saved, code quality, CI pass rate

**Next Steps:**
1. Schedule a technical deep-dive with your platform engineering team
2. Complete Centene's vendor security questionnaire
3. Provision a Devin sandbox for your team to test with non-critical repos

Session recording from today's demo: [link]

Best regards,
[Your name]

---

## Appendix: hapi-fhir 6.1.0 → HEAD Migration Delta

| Dimension | Java 11 (6.1.0) | Java 17 (HEAD) |
|-----------|-----------------|-----------------|
| `maven.compiler.source` | 11 | 17 |
| `maven.compiler.target` | 11 | 17 |
| Spring Framework | 5.3.20 | 6.2.18 |
| Spring Boot | 2.6.7 | 3.5.14 |
| Hibernate ORM | 5.6.2.Final | 6.6.4.Final |
| Hibernate Search | 6.1.4.Final | 7.2.1.Final |
| Java EE namespace | javax.* | jakarta.* |
| Java files | 3,572 | — |
| Maven modules | 51 | 60+ |
| pom.xml files | 64 | — |
| Root pom.xml diff | — | +1,179 / -830 lines |
