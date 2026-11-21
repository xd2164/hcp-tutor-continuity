# Switch AI tutors. Keep your learning.

**Live demo:** <https://xd2164.github.io/hcp-tutor-continuity/>

Every AI tutor today starts from zero. When a student moves to a new tutor, the
new tutor runs a placement quiz, asks the same intake questions, and knows nothing
about what worked last time.

This demo shows the alternative. A student's verified school achievements, learning
history and own words travel with them, through a learner wallet (LearnCard) and an
open context protocol (the [Human Context Protocol, HCP](https://github.com/loyalagents/hcp-spec)),
so a new tutor can pick up where the last one left off. The student and a guardian
decide what each tutor sees.

## The demo in one minute

One page, one switch. Mara, a synthetic grade-7 student taking accelerated grade-8 math,
asks a **new** AI tutor: *"Can you help me get ready for my next math unit?"*

| Switch | What the new tutor gets | Its first reply |
|---|---|---|
| **No context** | The question only | "Let's do a placement quiz": about 46 questions |
| **LearnCard** | Verified school achievements: 17 of 23 standards mastered, 3 near mastery | Skips what's mastered and starts with systems of equations |
| **+ HCP** | Plus learning history (practice estimates, the last tutor's session notes) and Mara's own words | "Picking up where your last tutor left off…": a 2-problem check, then the next standard, explained the way Mara asked, in 15 minutes, with chess problems |

Below the reply, a diagram lights up where each piece of information came from. Each
card has a **Where it comes from** view. The learner controls can withhold a category
or withdraw a tutor's access, and the next reply changes.

Presenting: ← → move the switch. Add `#cond=C` to open on "+ HCP".

## What it demonstrates

- **Continuity:** the new tutor builds on the previous tutor's evidence instead of re-testing.
- **Trust:** every item says how it is known: *verified* (signed by the school),
  *inferred* (practice estimates, tutor notes, with confidence) or *learner-declared*
  (Mara's own words). An inference is never presented as a credential.
- **Control:** the student and a guardian choose what each tutor may see. Support plans
  (IEP/504) are never shared with tutors. Withdrawing access stops future retrieval.
- **No new integration:** the new tutor uses the same HCP request as any other service.

## What is real and what is illustrative

| Part | Status |
|---|---|
| Learner record (standards, practice estimates, Mara's statements) | **Synthetic fixture** from Understudy (seed 2368342781); no real student data |
| Permission logic: what each condition sends, withholding, withdrawal | **Working** in the page |
| HCP access rules | Checked against 123/123 fixture scenarios in the reference provider: [hcp-learner-continuity](https://github.com/xd2164/hcp-learner-continuity) |
| Tutor replies | **Illustrative**: deterministic sample text, not a live AI tutor |
| Live tutor and wallet integrations | **Proposed** |

## The pilot this points to

Two independently built AI tutors, one learner wallet holding a transcript and an
assessment credential, and a consenting cohort. Measure the time to the first useful
practice, accuracy on the next assessment, and whether students and guardians
understand what they shared. If the second tutor isn't measurably better than starting
cold, stop.

## Run locally

Open `docs/index.html` in a browser. It is a single self-contained file: no build,
no keys, no network calls. Add `#selftest=1` to the URL to run the built-in checks.

HCP is a working draft (2.0-draft-3); identifiers use the placeholder namespace `hcp.example`.
