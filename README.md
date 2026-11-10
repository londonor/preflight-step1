# Gate 1 — Is the problem real?

A Claude skill that runs **Step 1 of the Biotech Venture Qualification Framework**: before you talk to anyone, it reads the published record and tells you whether your biotech or medtech idea addresses a problem people in the field need solved — or one that would never get your technology adopted.

It returns a verdict (**advance / stop / hold**), the evidence behind it, and a **customer-discovery kit** built around what the desk research could not find. The kit exists because desk research is the first pass, not the test. The test is five conversations with people who have the problem, and the skill's job is to make those conversations sharper.

Part of the *Pre-Flight Checklist* article series on LinkedIn: [Before You Jump](LINK-TO-ARTICLE-1) · [Well-Funded. FDA-Approved. Still Failed.](LINK-TO-ARTICLE-3) (the Step 1 deep dive).

---

## What it does

- **Writes the fail conditions before it looks anything up.** Three of them, in plain words, each with a bold header naming what it tests — *Is the problem real? Is there one place to start? Is the problem serious?* — and marks each **cleared** or **triggered** with one line of evidence.
- **Resolves what you left open, from sources.** Give it a category and it builds a candidate table and picks a first indication. Give it a technology and it restates the problem without the technology. Everything it decides is tagged `agent-resolved` so you can override it.
- **Answers the seven customer-discovery questions from the desk.** Can the problem be stated without the technology? Who has it? How often and how bad, with a verified number? How is it solved today? What is wrong with today's solution, in the field's own words? Is anyone looking to change? Any obvious contradiction with a business?
- **Argues against you first.** Before any verdict it writes the strongest honest case that the problem is not real, not consequential, already solved, or owned by no one.
- **Hands back a discovery kit.** The sentence to test, who to talk to (five people, independent of each other and of you), one question per gap in the evidence with what answer would close it and what answer would be a warning, five core questions, the findings that should make you doubt the thesis, pointers on running the conversations (*do not pitch your technology*), and a form to bring back so the gate can be re-run on what you heard.

## What it does not do

- It does **not** evaluate your technology, how plausible it is, or whether others have tried and failed. That is Step 2.
- It does **not** size the market, name buyers, judge your IP, map the regulatory path, or assess you as a founder. Those are later gates. If your input contains any of that, the skill records a flag and moves on.
- It does **not** replace talking to people. Every run says so on the sheet, and the kit is the next step, not an option.
- It does **not** make numbers up. A number it did not read on a page it opened does not exist for this gate. You will see "not found" where the record is silent, and that is the point: every "not found" becomes an interview question.

---

## Install

### Claude (web and desktop) — any plan

1. Download **`gate-1-venture-thesis.zip`** from the [Releases](https://github.com/OWNER/REPO/releases) page. (Or zip the `skills/gate-1-venture-thesis/` folder yourself; the folder must be the root of the ZIP, with `SKILL.md` inside it.)
2. If you have never used skills: **Settings → Capabilities** and turn on code execution / file creation.
3. **Customize → Skills** (claude.ai/customize/skills) → the **+** button → **Create skill** → **Upload a skill** → choose the ZIP.
4. Start a new chat and say *run gate 1 on …*

Skills work on Free, Pro, Max, Team, and Enterprise plans. On individual plans each person uploads the ZIP to their own account.

### Claude Code

```bash
claude plugin marketplace add OWNER/REPO
claude plugin install biotech-preflight@preflight-checklist
```

Then, in any session: `/biotech-preflight:gate-1-venture-thesis bioengineered meniscus`, or just describe the idea and ask for gate 1.

---

## How to run it

Say any of: **run gate 1** · **is this a real problem** · **qualify this idea** · **step 1** · **prep my customer discovery** — followed by the idea.

### The input can be as short or as long as you like

A few words is enough. The skill resolves the rest from sources and shows you every decision it made.

```
run gate 1 on a synthetic vessel for CABG
```

```
run gate 1: bioengineered meniscus
```

A full product description works too. Anything about buyers, regulation, market size, or your own background is recorded as a flag for the later gates and is not evaluated here.

```
Run gate 1 on this. A resorbable collagen patch for staple-line
reinforcement in sleeve gastrectomy, applied intraoperatively to
reduce leak rates. We think the buyers are the two big stapler
companies and the path is 510(k). I'm a bariatric surgeon with
twelve years in practice.
```

Several ideas at once also work; each gets its own record and the run ends with a one-line-per-idea table.

### Optional inputs

| Input | What it does |
| --- | --- |
| `mode: autonomous` (default) | Researches and decides without asking you anything. |
| `mode: interactive` | Asks at most four questions, one at a time, only for things research cannot resolve. |
| `mode: eval` | Autonomous, plus a comparison line against a verdict you expected. |
| `origin: …` | Where the idea came from (a partnering page, a clinic, a paper). Recorded verbatim, never evaluated. |
| `interview findings: …` | Your notes from the five conversations, on a re-run. They can close gaps and change the verdict. |

---

## What you get back

Two files per idea — `ideas/<slug>/gate1.md` (the sheet, written to be read) and `ideas/<slug>/gate1.json` (the record, written to be processed) — and a condensed version in the reply.

The sheet opens with the verdict and an **at-a-glance** block, so a busy reader can stop after ten lines. Here is the one from a real run:

> **Verdict — Advance.** A real, recognized, counted problem on the desk evidence, with one large question routed to the interviews and to gate 3: how many patients actually live with it. The five conversations in the discovery kit are the next step, not an option.
>
> - **The problem** — When a torn meniscus cannot be repaired, the tissue is removed, and the knee that loses it develops arthritis and comes to replacement at many times the rate of an intact knee; the only tissue replacement in use — a donor meniscus — reaches a tiny fraction of patients, is sized with error, and survives in about three of four patients at ten years and six of ten at fifteen.
> - **Where to start** — patients under about 55 with a symptomatic meniscus-deficient knee after subtotal or total meniscectomy: the population the field already treats with meniscal allograft transplantation.
> - **The numbers** — 13.49% of 120,493 patients had a knee replacement within 15 years of a partial meniscectomy, 10 times the general population and 40 times for those aged 30–39 (UK national cohort, 2019); 48% of open-meniscectomy knees had radiographic arthritis at 21 years vs 7% of matched controls (1998); MAT survives in 73.5% at 10 years and 60.3% at 15 (systematic review, 2019).
> - **What the desk could not find** — how many patients have a symptomatic meniscus-deficient knee · why MAT is so rare · what the problem costs · how often a young patient's tear is irreparable · a US arthroplasty-after-meniscectomy rate.
> - **Next step** — five independent conversations, built around the eight gap questions below.

Below that, in order: the three fail conditions with their results · the problem, the proposed technology (recorded, not evaluated), and the first indication, each tagged with where it came from · the candidate indications considered · the seven questions, each answered **Yes / No / Open** with evidence · the case against · the verdict and what you can override · the customer-discovery kit · flags for later gates · a research log listing every page opened and every search that found nothing.

The full example sheet is in [`examples/bioengineered-meniscus/gate1.md`](examples/bioengineered-meniscus/gate1.md).

### Reading the verdict

| Verdict | Meaning |
| --- | --- |
| **advance** | A real, numbered, unsolved, owned problem on the desk evidence. Go run the five conversations, then Step 2. |
| **stop** | The problem is not real, not consequential, or already solved — on evidence. Usually carries a **park note**: the one observable event that would re-open the idea, and a date to check. |
| **hold** | The evidence could not settle it within budget, or the first indication is yours to choose. The sheet names what is owed and routes it to the interviews. |

Every result on the sheet reads without knowing the test's direction: fail conditions are **cleared** or **triggered**, questions are **Yes**, **No**, or **Open**, and every decision the skill made for you is tagged `agent-resolved` or `agent-selected` so you can see it and reverse it.

---

## The discovery kit

The part that makes this complementary to customer discovery rather than a substitute for it. For each gap in the evidence — a number nobody published, a cost only practitioners know, a rate borrowed from another population, data older than ten years — you get:

| gap | why it matters | ask | closes the gap if | warning if |
| --- | --- | --- | --- | --- |
| Harvest time, staff, and setup per case | Not found in any source | "Walk me through the harvest on your last three-vessel case — who did it, when it started relative to the chest, how long it took." | They give minutes, people, and a sequence, and someone describes it as a cost | The harvest adds no time, no dedicated person, and nobody in the institution can name what it costs |

Plus who to talk to (always including someone who lives with the current workaround and someone who pays for it), five core questions for every conversation, the disqualifying findings written down before you talk to anyone, and the pointers:

- Do not pitch. Do not describe, name, or hint at the technology.
- Ask about the last time, not the usual case.
- Ask what it cost, and who paid. When someone says a step costs nothing, ask who pays for the people and the time — a cost the speaker doesn't feel is usually a cost someone else does.
- "That sounds interesting" means nothing. A story about a recurring complication with its consequences is a signal.
- Write down their words, not your summary.
- Five conversations are a screen, not a validation; they decide whether the idea earns thirty more.

When the conversations are done, fill in the bring-back form (closed / still open / contradicted, with the quote) and run the gate again with those notes as input.

---

## Rules it holds itself to

1. Fail conditions are written before any research, and they are about the problem only — never about a technology, a market, a buyer, or a founder.
2. Every number comes from a page the skill opened. Search snippets are not sources. Conflicting sources are both reported.
3. "Not found" is never estimated. "No evidence found" and "evidence of absence" are kept apart.
4. The strongest case against the problem is written before the verdict.
5. The budget is about 45 minutes and 10 opened pages per idea. The research log says what was spent.
6. Anything belonging to a later gate — technology plausibility, prior attempts, market size, buyers, IP, regulation, the founder — is flagged, not evaluated. Mentioning it in a verdict is a defect.

## Limits worth knowing

- It reads what it can open. Some publishers and PubMed Central block automated access; when that happens the log says so and an alternate source is used or the number is marked not found.
- It is only as current as the pages it finds. A registry report from last month beats a review from 2013, and the skill prefers it, but it cannot read what is not online.
- An **advance** is a verdict on desk evidence. It has never been wrong about whether to go talk to people; it can only be wrong about what they will say.

---

## Repository layout

```
skills/gate-1-venture-thesis/SKILL.md   the skill
gate-1-venture-thesis.zip               the same skill, packaged for upload to Claude
examples/                               full output from real runs
.claude-plugin/                         plugin and marketplace manifests for Claude Code
README.md
LICENSE
```

## License

MIT. Use it, fork it, run your ideas through it. If you improve the fail conditions or the discovery questions, open a pull request with a run in `examples/` that shows the difference.
