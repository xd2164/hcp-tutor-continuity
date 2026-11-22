# From district data to the AI tools teachers use

**Live demo:** <https://xd2164.github.io/hcp-tutor-continuity/>

Districts already know a lot about each learner, but it sits in separate systems, in
different formats, and every new AI tool starts from zero. This demo shows one simple flow
that fixes that: align the record once, export a small learner profile the learner
controls, and let each AI tool use only what it needs.

## The flow

```
1 District data   →   2 Alignment   →   3 HCP export          →   4 AI tools
what schools          maps records      a minimal profile          each tool gets only
already have          to shared skills  the learner controls       what it needs
```

| Step | What happens | What comes out | Status |
|---|---|---|---|
| **1. District data** | Assessment results, gradebook, standards tracker and a student survey, for one synthetic learner (Mara) | Useful records, spread across systems with different codes | Synthetic data |
| **2. Alignment** | An alignment service maps each record to a shared skill ID, so "8.EE.C.8" or "L.7.2" means the same thing to every tool | The same skills, named the same way | Proposed (IDs are placeholders) |
| **3. HCP export** | A minimal learner profile is exported through the [Human Context Protocol (HCP)](https://github.com/loyalagents/hcp-spec), held in LearnCard: the school record (strengths and next skills, *verified*) and the learner's own words (what helps, what's hard, time available). The learner and a guardian choose what goes in. | One small, labelled profile | Working in the page |
| **4. AI tools** | A math tutor app (built by a teacher) gets the math part; a writing-practice tool gets the ELA part. Each tool's HCP grant covers only its purpose. | Each tool starts from what the learner already knows | Proposed (replies illustrative) |

**Never exported:** IEP and 504 support plans, demographics, the full transcript and every score.

## Try it

Click through the four steps (or use ← →). In step 3, untick **School record** or
**Mara's own words**, then go to step 4: what each tool receives, and its first
message, change straight away. Expand **The HCP export (JSON)** or **What the tool
receives** to see the exact data.

## What is real and what is illustrative

| Part | Status |
|---|---|
| Mara's record (math 17/23 and ELA 14/16 standards, near-mastery skills, survey answers) | **Synthetic fixture** from Understudy (seed 2368342781); no real student data |
| Sharing choices, purpose-scoped profiles, export | **Working** in the page |
| Shared skill IDs | **Placeholders** (`kg:ccss/...`) until mapped by a real alignment service |
| Tool replies | **Illustrative** sample text, not live AI tools |
| Tool and alignment integrations | **Proposed** |

A reference HCP provider that checks access rules against 123/123 fixture scenarios is in
[hcp-learner-continuity](https://github.com/xd2164/hcp-learner-continuity).

## The pilot this points to

Synthetic district data aligned to shared skills, exported as a learner profile, and used
by two independently built AI tools: one for math and one for writing. Measure whether
each tool's first session is better targeted than starting cold, and whether learners and
guardians understand what they shared. If neither tool improves, stop.

## Run locally

Open `docs/index.html` in a browser. It is a single self-contained file: no build, no keys,
no network calls. Add `#selftest=1` to the URL to run the built-in checks.

HCP is a working draft (2.0-draft-3); identifiers use the placeholder namespace `hcp.example`.
