# Switch AI tutors. Keep your learning.

**Live demo:** <https://xd2164.github.io/hcp-tutor-continuity/>

Every AI tutor today starts from zero. When a student moves to a new tutor, it runs a
placement quiz, asks the same intake questions, and knows nothing about what worked last time.

The fix is not a bigger data dump. It is a **minimum viable learner profile**: the five
facts that change a new tutor's first move, carried by **LearnCard + HCP as one bundle**.

## The minimum viable learner profile

| # | Item | Example (synthetic learner Mara) | Trust label | Changes the tutor's first move |
|---|---|---|---|---|
| ① | **Where the learner stands** | Mastered 17 of 23 Grade 8 standards; next up: systems of equations | verified (signed by the school) | Skips mastered work; no placement quiz |
| ② | **Where they left off** | Last tutor, 2 weeks ago: 4 of the last 5 right on systems of equations | inferred (medium confidence, expires) | A 2-problem check instead of re-teaching |
| ③ | **What helps them learn** | "can you explain what its asking first" | learner-declared | How each problem is introduced |
| ④ | **What gets in the way** | "i never know what the word problems are asking" | learner-declared | Practises reading the problem, not more drills |
| ⑤ | **Time available** | About 15 minutes on school nights | learner-declared | Session length |

**Deliberately left out:** the full transcript and every score, demographics, IEP and 504
support plans, chat logs. **Nice to have, not minimal:** interests, longer-term goals.

### One bundle, two jobs

- **LearnCard** holds the learner's profile and proves what is verified: the school's
  signed credentials behind item ①.
- **HCP** ([Human Context Protocol](https://github.com/loyalagents/hcp-spec)) is how a tutor
  asks for the profile: only what the learner and guardian allow, every item labelled with
  its source, inferences with a confidence and an expiry date, and rules (such as "ask me
  first") that travel with the data.

Together they make the profile **portable** (any tutor, no new integration),
**trustworthy** (verified vs inferred vs learner-declared is never blurred) and
**learner-controlled** (share, withhold or withdraw at any time).

## The demo in one minute

One page. Mara asks a **new** AI tutor: *"Can you help me get ready for my next math unit?"*

- **No profile:** the tutor's reply is a placement quiz (about 46 questions), plus questions
  about how Mara learns, what's hard and how much time there is.
- **With Mara's learner profile:** "Picking up where your last tutor left off… a quick
  2-problem check, then the next standard… we'll start each word problem by working out
  what it's asking… 15 minutes tonight." Each sentence is tagged ①–⑤ with the item behind it.

Untick any item and that part of the reply disappears, while the list of what the tutor
*still has to do first* grows. That shows the value of each item, one at a time. A
diagram shows where each item comes from (school, last tutor, the learner), and **Show the
profile as data** shows exactly what the new tutor receives.

Presenting: ← → toggle the profile. Add `#cond=C` to open with the profile on.

## From district data to the AI tools teachers already use

```
District data  →  Alignment  →  Minimum viable learner profile  →  Adapter  →  AI tutor app
(synthetic)       (shared        (LearnCard + HCP, 5 labelled        (keeps the     (educator-built,
                   standard IDs)  items, learner permissions)         labels)        or a tool's API)
                                                    ↑                                    │
                                                    └──────── session result written back as an inferred item
```

Section 5 of the demo, **Hand the profile to an AI tool**, is the adapter:

- **Context block:** a labelled plain-text profile to paste into an educator-built AI tutor app.
  VERIFIED, INFERRED (with confidence and expiry) and LEARNER SAYS are kept distinct, the
  guardian's rule is included, and items the learner withheld are flagged rather than guessed.
- **Structured JSON:** the same profile for a tool's API, with shared standard IDs and a
  report-back shape for the session result.
- **Label checks:** six checks confirm the trust labels survive the handoff.
- **Write-back:** simulate the tool's session result coming back as a new inferred item, and
  the new tutor's reply continues from it.

Copy-paste works today. A live connection, where the tool asks through HCP under a grant, is
the next step. Shared standard IDs use a placeholder namespace (`kg.example`) until an
alignment tool maps them to a real knowledge graph.

## What is real and what is illustrative

| Part | Status |
|---|---|
| Mara's record (standards, last-tutor result, statements) | **Synthetic fixture** from Understudy (seed 2368342781); no real student data |
| Sharing, withholding and withdrawal logic | **Working** in the page |
| HCP access rules | Checked against 123/123 fixture scenarios in the reference provider: [hcp-learner-continuity](https://github.com/xd2164/hcp-learner-continuity) |
| Tutor replies | **Illustrative**: deterministic sample text, not a live AI tutor |
| Adapter (context block, JSON, label checks, write-back) | **Working** in the page; live tool connection **proposed** |
| Live tutor and wallet integrations | **Proposed** |

## The pilot this points to

Two independently built AI tutors, LearnCard holding the minimum viable learner profile,
and a consenting cohort. Measure the time to the first useful practice, accuracy on the
next assessment, and whether students and guardians understand what they shared. Test
each of the five items: if removing one makes no difference, it doesn't belong in the
minimum. If the second tutor isn't measurably better than starting cold, stop.

## Run locally

Open `docs/index.html` in a browser. It is a single self-contained file: no build, no keys,
no network calls. Add `#selftest=1` to the URL to run the built-in checks.

HCP is a working draft (2.0-draft-3); identifiers use the placeholder namespace `hcp.example`.
