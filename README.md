# Java-Demo

Demo environment for showcasing Devin's Java version upgrade capabilities.

## Use Case

**Java 11 → Java 17 upgrade** on [hapi-fhir](https://github.com/hapifhir/hapi-fhir) (tag `6.1.0`) — a real-world, 3,500+ file healthcare Java project.

## Target Prospect

**Centene Corporation** — St. Louis, MO — Fortune 25 managed healthcare company with 300+ Java application developers.

## Contents

- [`DEMO_PLAN.md`](DEMO_PLAN.md) — Complete 40-minute demo plan including:
  - Meeting agenda & stakeholder roles
  - Step-by-step live demo script (20-25 min)
  - Demo environment setup guide
  - Talking points per stakeholder persona
  - Objection handling playbook
  - Follow-up email template

## Quick Reference

| Item | Detail |
|------|--------|
| Demo repo | Fork of `hapifhir/hapi-fhir` at tag `6.1.0` |
| Source Java | 11 (`maven.compiler.source=11`) |
| Target Java | 17 |
| Key migrations | javax→jakarta, Spring 5→6, Spring Boot 2→3, Hibernate 5→6 |
| Devin docs | [Java Upgrades Guide](https://docs.devin.ai/use-cases/examples/java-upgrades) |
