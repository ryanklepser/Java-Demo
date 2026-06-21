# Slide-by-Slide Talk Track
## Centene Corporation — Java 11 to 17 Demo

> Keep each slide to 30-60 seconds max. The demo is the star, not the deck. Every talk track ends with a hook — a question or statement designed to get a specific persona talking. Refer to DISCOVERY_QUESTIONS.md for the full question bank per slide.

---

## Slide 1 — Title

**Talk Track:**
"Thank you all for making time today. We've got Ajoy, Haseeb, Ethan, and John — which tells me Centene is evaluating this from every angle: business, engineering, security, and the developer experience. That's exactly how this conversation should go."

**Hook → Agenda:**
*No question. Make eye contact with each person as you say their name. Advance quickly.*

---

## Slide 2 — Agenda

**Talk Track:**
"Quick map of the next 40 minutes. We'll start with discovery — I have a few hypotheses about your landscape, and I'd love you to correct me where I'm wrong. Then we'll look at why the timing matters. Then we'll switch to a live demo — real code, real codebase, no slides. And we'll close with what a low-risk first step looks like."

**Hook → Discovery:**
"Before we dive in — does this agenda match what you were expecting, or is there something specific you'd like me to prioritize?" *(All)*

---

## Slide 3 — Why We're Here

**Talk Track:**
"Here's our hypothesis: Centene's engineering org is carrying technical debt that silently taxes every team — and Java modernization is a big piece of that. We're not here to tell you what you already know. We're here to show you a new option for how fast this can move."

**Hook → Get them talking (this is the most important listening moment):**
"Haseeb, roughly how many Java services is your team maintaining today? And of those, what percentage are still on Java 11 or older?" *(HI)*

*Then pivot to John:* "And John — when you hear 'Java 11 to 17 upgrade,' what's the first thing that comes to mind? What part do you dread most?" *(JS)*

---

## Slide 4 — What We're Hearing (Industry Stats)

**Talk Track:**
"You're not alone. 72% of the Fortune 500 is still running Java 11 or older in production. The average manual upgrade takes 4-6 weeks per service. And since Java 11 EOL, CVE volume has tripled. The industry knows it needs to move — the constraint isn't willingness, it's capacity."

**Hook → Validate the pain:**
"Ethan, that 3.2x CVE increase — is your CAM program already flagging these? How are you currently tracking unpatched Java 11 exposure across the portfolio?" *(ES)*

---

## Slide 5 — Your Landscape

**Talk Track:**
"We did our homework. Over 3,100 engineers in your technology org. 313 in application development. 30+ state Medicaid programs, each with dedicated platforms. Java, Spring Boot, Hibernate, AWS, Kafka — this is the stack that runs your core business. I want to make sure we got this right."

**Hook → Confirm and refine:**
"Ajoy, is that 3,100 engineer number directionally right? And of that group, roughly how many are hands-on with Java day-to-day?" *(AK)*

*Then:* "And Haseeb — does each state have its own set of services, or is there a shared platform configured per-state?" *(HI)*

---

## Slide 6 — Java 11 EOL Problem

**Talk Track:**
"Here's the timeline your security team is living with. Java 11 public updates ended September 2023. CVEs are accumulating with no free patches. Spring Boot 2.x lost OSS support in November 2025. Today, right now — you have unpatched Java 11 services running Spring Boot without security updates in HIPAA-regulated production systems. That's not a risk register item. That's an active exposure."

**Hook → Make the risk personal:**
"Ethan, has CMS or any state Medicaid agency raised Java EOL or Spring Boot support status during a recent audit cycle?" *(ES)*

---

## Slide 7 — Migration Tax

**Talk Track:**
"Let me make the manual work tangible. A Java 11 to 17 upgrade isn't one task — it's four. Update compiler settings across every pom.xml. Migrate every javax import to jakarta across thousands of files. Upgrade Spring, Hibernate, and their transitive dependencies. Then validate — build, test, fix, repeat. For a single service: 8-18 engineer-weeks."

**Hook → Validate the estimate:**
"John, which of these four categories is the most painful in your experience — the namespace rename, or the framework compatibility issues?" *(JS)*

*Then:* "Haseeb, does 8-18 engineer-weeks per service match what you've seen internally?" *(HI)*

---

## Slide 8 — Opportunity Cost

**Talk Track:**
"600 engineer-weeks. That's what it costs to upgrade 150 services manually. $4.8 million in engineering capacity consumed by mechanical work. Not designing. Not building product. Not improving the member experience. Just... renaming imports and fixing dependency conflicts."

**Hook → Make it personal:**
"Ajoy, if you could recover even half of that $4.8M in capacity — what would you invest it in? FHIR interoperability? Member portal? Claims processing performance?" *(AK)*

---

## Slide 9 — Why Now (Dark slide)

**Talk Track:**
*(Slow down. Lower your voice slightly.)*

"I want to be direct about timing. Today's CNBC article announced Centene's Voluntary Separation Program. ACA membership projected to fall 40% by year-end. $900 billion in Medicaid cuts over the next decade. You're being asked to do more with fewer people. That's the reality."

*(Pause)*

"Java 11 EOL isn't going away. Spring Boot 2.x isn't getting unpatched. But the engineers who would do that work — some of them might be. Devin doesn't replace your engineers. It multiplies the ones you keep."

**Hook → Empathetic, not predatory:**
"Haseeb, if your team size changes as part of this restructuring — does the modernization backlog get deprioritized, or does it become more urgent because there are fewer people to absorb the risk?" *(HI)*

---

## Slide 10 — Meet Devin

**Talk Track:**
"This is Devin. Not autocomplete. Not a chatbot. An autonomous software engineer. You give it a task — like a Jira ticket — and it reads the codebase, makes changes across dozens of files, runs the build, fixes errors, and delivers a pull request. SOC 2 Type II. Over 100 enterprise customers. And a $10M Productivity Guarantee — if Devin doesn't deliver, you get credits back."

**Hook → Gauge awareness:**
"Has anyone on the team evaluated autonomous AI engineering tools before, or would this be new territory for Centene?" *(All)*

*If John speaks:* "John, you've probably seen Copilot. How was your experience?" *(JS)*

---

## Slide 11 — How It Works

**Talk Track:**
"Four steps. Give Devin a task. It analyzes the codebase. It makes changes and runs the build. It creates a PR for human review. The critical point: your CI runs. Your security scans run. Nothing merges without a human clicking 'approve.' This isn't magic — it's automation with guardrails, inside your existing workflow."

**Hook → Connect to their process:**
"John, your team uses GitHub for PRs and code review, correct? Is there anything in this workflow that would conflict with how you work today?" *(JS)*

*Then:* "Ethan, does the 'nothing merges without human review' model address your initial concern about AI-generated code?" *(ES)*

---

## Slide 12 — Guardrails & Control

**Talk Track:**
"This slide is for Ethan. Scoped permissions — Devin accesses code through GitHub, same permission model as your developers. No production access, no PHI. Configurable guardrails — you define what Devin can and cannot touch in plain English. Full session transcripts — every file read, every command run, logged for your CAM program. SOC 2 Type II. BAA-ready. DPA available."

**Hook → Let Ethan interrogate:**
"Ethan, we told Devin: don't touch security classes, don't modify migration files. Is there a category of code at Centene you'd want to explicitly fence off from any automated tool?" *(ES)*

---

## Slide 13 — Demo Transition (Dark slide)

**Talk Track:**
*(Stand up if you're seated. This is the "moment.")*

"Enough slides. Let's upgrade a real Java healthcare codebase. Right now. 4,500 Java files. 51 Maven modules. Java 11 with Spring Boot 2.6 and Hibernate 5.6. Live."

*(Pause. Let the anticipation build.)*

"Any questions before we switch over?"

**Hook:** None needed. Advance to the live demo. The silence IS the hook.

---

## [LIVE DEMO — ~22 minutes, see DEMO_SCRIPT.md]

---

## Slide 14 — What Just Happened

**Talk Track:**
"Let's put numbers on what just happened. Over 4,500 Java files analyzed. 68 pom.xml files updated. 51 Maven modules migrated. One review-ready pull request. Manual estimate: 4-6 weeks with a team of 2-3 engineers. Devin: under an hour, plus your engineer's review time."

**Hook → Anchor to their reality:**
"John, you just saw the PR. Is that code you'd be comfortable reviewing and merging? Anything that stood out as wrong?" *(JS)*

*Then:* "Haseeb, if that ratio holds across your portfolio — what does it mean for your roadmap?" *(HI)*

---

## Slide 15 — At Centene Scale

**Talk Track:**
"One service was impressive. Now multiply it. 150 services. Manual: 600 engineer-weeks. Eleven and a half engineer-years. $5.2 million in cost. With Devin: 43 engineer-weeks of review. $370K. That's $4.8 million in engineering capacity recovered — capacity that goes back to building product for your 26 million members."

**Hook → Validate the math:**
"Ajoy, we estimated 150 Java services. Is that in the right ballpark? Even at half — 75 services — the math still works: 300 engineer-weeks saved." *(AK)*

*Then:* "Haseeb, the key is parallelization. Devin runs all 150 simultaneously. Your team just reviews PRs. Does that model fit how your org is structured?" *(HI)*

---

## Slide 16 — The Platform, Not the Project

**Talk Track:**
"Java 11 to 17 is the starting point. But Devin is a platform, not a one-time project. Productivity Guarantee — $10M in guaranteed value. Devin Desktop — your engineers manage agents from their IDE. Vulnerability remediation — automated CVE scanning and fix PRs on a schedule. Scheduled automations — recurring dependency bumps across your entire portfolio. Java 21 is next. Spring Boot 4 is coming. This isn't a one-time purchase. It's a permanent engineering multiplier."

**Hook → Expand the vision:**
"Haseeb, beyond Java upgrades — what other mechanical work consumes your team's time? Dependency bumps? Test generation? Bug fixes from Jira?" *(HI)*

*Then:* "Ethan, the vuln remediation capability runs automated CVE scans weekly. Would your CAM program want to plug into that?" *(ES)*

---

## Slide 17 — Security & Compliance

**Talk Track:**
"Ethan, this slide is yours. Data handling: code access through GitHub, standard permissions, no production access, no PHI, isolated environments, no data retention. Certifications: SOC 2 Type II, BAA-ready, DPA available. Auditability: full session transcripts compatible with your CAM program. We're happy to support your vendor security assessment — SOC 2 report, pen test results, security whitepaper. Whatever you need."

**Hook → Invite scrutiny:**
"Ethan, what's missing from your perspective? What would you need to see in a vendor security questionnaire that isn't covered here?" *(ES)*

*Then:* "Does Centene require a BAA for tools that interact with source code that processes PHI, or since Devin only sees code — not data — does it fall outside that scope?" *(ES)*

---

## Slide 18 — Customer Proof

**Talk Track:**
"You'd be in good company. Nubank — 6 million lines of code, 1,000+ engineers unblocked, 8x efficiency, 20x cost savings. athenahealth — healthcare company with HIPAA requirements like yours, using Devin for code modernization. Citi, Goldman Sachs, Dell, Cisco, NASA, U.S. Army. These are large, regulated enterprises with security requirements as strict as — or stricter than — yours."

**Hook → Peer validation:**
"Ajoy, does knowing that Citi, Goldman, and athenahealth have adopted Devin change your risk assessment at all?" *(AK)*

*Then:* "Ethan, would it be helpful if we connected you with athenahealth's security team to hear about their experience?" *(ES)*

---

## Slide 19 — Proposed Pilot

**Talk Track:**
"Here's what a first step looks like. Five services. Two weeks. Measurable results. Haseeb picks 5 non-critical Java 11 services. Devin runs all 5 upgrades overnight — PRs ready by morning. Your engineers review — 2-4 hours each instead of 2-4 weeks. Then we measure together: time saved, code quality, CI pass rate. Low risk. Fast signal. Fully reversible — every change is a PR you can revert. And the $10M Productivity Guarantee backs the value."

**Hook → Make the commitment feel small:**
"Haseeb, if we picked 5 services — do you already have a shortlist in mind? Non-critical services that would be good pilot candidates?" *(HI)*

*Then:* "Ajoy, what would success look like for you? Time saved? Code quality? Something else?" *(AK)*

---

## Slide 20 — Next Steps (Dark slide)

**Talk Track:**
"Three actions, three owners, this week and next. One: Ethan gets our SOC 2 report and security whitepaper today — we start the vendor assessment. Two: Haseeb identifies 5 pilot services by next week. Three: we schedule a technical provisioning call to connect your repos and configure Devin's environment. Clear owners, clear timelines."

*(Pause. Look at the room.)*

"What questions do you have that would prevent us from moving forward?"

**Hook → Close with commitment:**
"Ethan, can your team turn around the vendor assessment within a week?" *(ES)*

*Then:* "Haseeb, can you have 5 candidates identified by next week?" *(HI)*

*Finally:* "Ajoy, who else on your side needs to be involved in the procurement decision? Should we loop in legal or procurement early?" *(AK)*

---

## General Tips

- **Pacing:** If a question gets a strong response, stay there. Don't rush to the next slide.
- **Energy management:** Slides 1-8 should accelerate. Slide 9 (Why Now) slows down. The demo is high energy. Slides 14-18 are "let the data land." Slides 19-20 are calm, confident, closing.
- **If you're losing someone:** Call them by name. People re-engage when personally addressed.
- **The demo is the star.** If you're running long on slides, cut slides 4 and 7 — their content is confirmed during the demo.
