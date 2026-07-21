# 🕵️ Evidence-Based Hiring

> Don't reward hope. Reward evidence.

An open-source prototype exploring what candidate screening could look like if it evaluated evidence and behavior instead of keywords and job titles.

## Why I built this

This project was inspired by watching candidates struggle with modern hiring systems — not because they lacked ability, but because transferable skills, career gaps, and contextual experience were often reduced to keyword matching.

The goal isn't to replace recruiters. The goal is to help AI reason more like a good human reviewer — and to make its reasoning visible enough that a human can check it, challenge it, and refine it. The system doesn't decide. It exposes its reasoning so a human can judge the judgment.

## What's actually happening today

- A resume says "Client Success Partner." The job post says "Customer Success Manager." No match — even if the work is identical.
- A career gap shows up. No context asked. Silently deprioritized.
- "5–7 years required" becomes a hard cutoff, even for someone with 11 years in an adjacent field.
- A resume gets rejected. The candidate never learns why.

None of this is because recruiters don't care. Keyword matching structurally cannot keep pace with how many ways one job gets named across companies and industries — and static filters can't explain their own decisions.

## Three connected prototypes

**Part 1 — Title Equivalence** (`title-equivalence-demo.html`)
Gets a candidate correctly *into* screening in the first place. Instead of matching literal job titles, it reads for the behaviors behind them. Same job requirement, five resumes, five different titles: a keyword filter passes 1 of 5. Behavior matching passes 5 of 5.

**Part 2 — Evidence-Based Hiring** (`index.html`)
Evaluates a candidate once they've correctly reached screening. Six steps: understand the role, read the resume for behavior, evaluate evidence density, check context (gaps/switches/seniority), generate an explainable verdict, then interview or redirect. Built as a static demo with fixed example resumes.

**Part 3 — The Live Evaluator** (`live-evaluator.html`)
Same six-step flow as Part 2, but wired to a real AI model instead of scripted examples. Paste in any job description and any resume, and it generates a genuine, reasoned evaluation on the spot.

## Quick Start

No build step, no install, no dependencies. Everything here is plain HTML, CSS, and vanilla JavaScript.

**Parts 1 & 2 — fully self-contained, works instantly:**
1. Clone or download this repo
2. Open `title-equivalence-demo.html` or `index.html` directly in any browser
3. That's it — both run entirely client-side with fixed example data, no setup required

**Part 3 — the live evaluator:**
`live-evaluator.html` calls a real AI model to generate evaluations, so it needs an API key to run:

1. Get a free Anthropic API key at [console.anthropic.com](https://console.anthropic.com) (pay-as-you-go, no subscription)
2. Open `live-evaluator.html` in any browser — or visit it directly on the live site
3. Paste your key into the "Your Anthropic API Key" field at the top — it's used only in your browser, sent only to Anthropic's API, and never touches any server of mine. It's saved in your browser's local storage so you don't have to re-enter it next time, but you can clear it anytime by clearing your browser data.
4. Paste in any job description and any resume, hit **Evaluate against evidence, not keywords**, and step through the six tabs: Role → Resume → Evidence → Context → Verdict → Redirect

Note: since this runs entirely in your browser with your own key, your usage is billed to your own Anthropic account under their standard API pricing.

## Part 3 in depth: stress-testing it

Rather than trust the concept, I tried to break it — feeding it resumes specifically designed to fool a naive system in one direction or another.

| # | Scenario | What it tests | Verdict | Redirect |
|---|---|---|---|---|
| 1 | Vague, low-effort resume | Separates "unproven" from "disqualified" | Needs clarity | Internal (junior role) |
| 2 | Keyword-stuffed resume, right title & tenure, no substance | Rewards vocabulary, or evidence? | Amber, flagged as unverified | Not triggered |
| 3 | Career switcher (teacher → CS), zero industry vocabulary | Maps transferable behavior instead of penalizing the title | Amber, confident | Not triggered |
| 4 | Fresh graduate applying to a Senior role | Separates real scope gap from candidate potential | Red, constructive reasoning | Internal + external, both entry-level |
| 5 | Non-IT professional → SaaS CSM | Respects the JD's own stated openness to non-SaaS backgrounds | Amber, confident, names exactly what to probe | Not triggered |
| 6 | Software engineer applying to a CSM role | Identifies a *function* mismatch, not a gap or seniority issue | Red | Fired — correctly pointed to Engineering, not an invented hybrid role |
| 7 | Direct match, strong quantified evidence across every requirement | Does strong evidence get a clean pass, or excessive hedging? | Green / Interview | Not triggered (correctly) |
| 8 | Adjacent function — enterprise sales, pre-sale only | Tells "adjacent audience, wrong side of the contract" apart from a hard mismatch | Amber — a genuinely nuanced middle ground | Not triggered |
| 9 | Adjacent function — technical support, reactive ticket work | Distinguishes reactive support from proactive account ownership | Red, precisely reasoned | Fired — grounded, specific bridge roles |

### A bug found and fixed, live

During Test 6, the redirect logic initially suggested CS-adjacent hybrid roles (Solutions Engineer, Technical Account Manager) instead of the honest answer — this candidate's evidence pointed straight at Engineering. The prompt had no instruction telling it a redirect is allowed to point completely outside the function being screened for, so it defaulted to staying in its own lane even on a hard mismatch.

Fix: an explicit rule that redirects must follow the strongest evidence in the resume, even into an entirely different field, rather than inventing a role that merely sounds adjacent to soften the mismatch. Re-running the same test afterward produced the correct result.

Worth calling out on its own — it's the clearest evidence that adversarial testing isn't optional. The first version *looked* right up until a case exposed exactly where it wasn't.

## Old ATS vs. Evidence-Based Hiring

| Traditional Screening | Evidence-Based Hiring |
|---|---|
| Literal keyword matching | Behavioral equivalence |
| Career gaps highlighted | Career gaps become interview questions |
| Years used as a primary filter | Years become one supporting signal |
| Tool names | Skill categories |
| Resume formatting | Evidence quality |
| Buzzwords | Demonstrated outcomes |
| Job titles | Responsibilities & behaviors |
| Binary recommendation | Explainable recommendation |

## Evidence Density

Instead of "Keyword Match: 87%," the system surfaces something more falsifiable:

A claim like *"converted 3 of 10 pending renewals"* scores higher than *"improved renewals"* — not because it sounds better, but because one is falsifiable and the other is marketing.

## Anticipated questions

**How do you measure evidence?**
By specificity (bounded numbers beat vague claims), scope honesty (admitting partial scope reads as more credible than overclaiming), and internal consistency (do dates, titles, and claims line up). It cannot verify a claim is *true* — only how well-evidenced and self-consistent it looks. That limit is intentional: the system flags claims for a human to verify, it doesn't claim to fact-check them.

**What happens when the resume is weak?**
The same steps run regardless, ending in an honest, specific "not suitable" reason instead of a silent rejection — and the redirect step still runs, since a weak fit for one role doesn't mean the candidate's real skills have nowhere else to go.

**Why recommend interview for a candidate who looks overqualified?**
Because evidence of capability and evidence of fit are different questions. Auto-rejecting for "overqualified" answers a people-risk question (will they stay, will they be satisfied) with a skills-based tool. This system keeps the two separate and asks a human to resolve the second one.

**Is this AI deciding who to hire?**
No. Today's ATS already makes judgments — keyword = match, gap = penalty, formatting = parse failure — it just hides them. This doesn't remove judgment, it shifts it to criteria a human can inspect, challenge, and refine. The recruiter remains responsible for deciding whether the AI's reasoning is convincing.

## Honest positioning

Semantic, skill-based candidate matching already exists — enterprise platforms like Eightfold and HireEZ do versions of this at scale. This project isn't claiming to be the first to attempt it. What's harder to find is an **open, explainable** version — one that shows *why* it thinks two titles are equivalent or a claim is weak, rather than returning a black-box score, and one that smaller companies without enterprise budgets can actually read and adapt.

## Built using

- HTML, CSS, Vanilla JavaScript
- Part 3 additionally calls the Anthropic API (Claude) directly from the browser for live evaluation

## Future roadmap

- ~~AI-assisted evidence extraction~~ ✅ delivered in Part 3
- Resume parsing (PDF/DOCX upload instead of paste-in)
- Behavior mapping at scale
- Explainable hiring decisions in production-style workflows
- Internal role redirection
- JSON-driven candidate profiles

## Contributing

This is an open prototype exploring evidence-based hiring. Ideas, discussions, issues, and pull requests are welcome.

---

*Built by someone who spent eleven years on the other side of this exact filter.*
