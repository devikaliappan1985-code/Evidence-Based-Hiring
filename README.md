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

## Two connected prototypes

**Part 1 — Title Equivalence** (`title-equivalence-demo.html`)
Gets a candidate correctly *into* screening in the first place. Instead of matching literal job titles, it reads for the behaviors behind them. Same job requirement, five resumes, five different titles: a keyword filter passes 1 of 5. Behavior matching passes 5 of 5.

**Part 2 — Evidence-Based Hiring** (`index.html`)
Evaluates a candidate once they've correctly reached screening. Six steps: understand the role, read the resume for behavior, evaluate evidence density, check context (gaps/switches/seniority), generate an explainable verdict, then interview or redirect.

## Old ATS vs. Evidence-Based Hiring

| Traditional ATS | Evidence-Based Hiring |
|---|---|
| Exact keyword match | Behavioral equivalence |
| Employment gap = penalty | Gap = interview question |
| Years = hard filter | Years = supporting signal |
| Tool names | Skill categories |
| Formatting | Content quality |
| Buzzwords | Evidence quality |
| Job titles | Responsibilities & outcomes |
| Reject | Explain |

## Evidence Density

Instead of "Keyword Match: 87%," the system surfaces something more falsifiable:

```
Behavior Match        92%
Evidence Strength      88%
Context Confidence     84%
Learning Agility       90%
```

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

## Future roadmap

- AI-assisted evidence extraction
- Resume parsing
- Behavior mapping at scale
- Explainable hiring decisions in production-style workflows
- Internal role redirection
- JSON-driven candidate profiles

## Contributing

This is an open prototype exploring evidence-based hiring. Ideas, discussions, issues, and pull requests are welcome.

---

*Built by someone who spent eleven years on the other side of this exact filter.*
