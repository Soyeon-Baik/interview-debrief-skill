# interview-debrief-skill

A Claude skill that transforms raw interview transcripts (Otter.ai, Rev, or any STT tool) into structured, actionable PM interview debriefs.

---

## What it does

Paste a speaker-labeled transcript and get back:

- **Per-question breakdown** — cleaned-up question, your answer summary, follow-up Q&As
- **Evaluation** — rating (1–5), what worked, clarity & structure of thinking, what to improve
- **English expression notes** — specific phrases that were unclear or non-native sounding, with better alternatives
- **Overall summary** — performance snapshot across 5 dimensions + top strengths, improvements, and one thing to practice

Designed for PM interviews, but works for any behavioral or product interview format.

---

## How to use

1. Install the skill in Claude
2. Paste your transcript (speaker-labeled format works best)
3. Say: `"Analyze this interview transcript"` or `"Review my interview"`

Claude will produce a downloadable `.md` debrief file.

---

## Key features

- **Raw transcript evaluation** — evaluates based on what was *actually said*, not a cleaned-up version. Delivery problems aren't masked.
- **Voice artifact handling** — filler words (`um`, `like`, `you know`) are parsed for meaning but tracked and flagged if excessive
- **STT error recovery** — handles garbled questions from accent-related misrecognitions
- **Follow-up Q&A structure** — main answer + each follow-up shown separately so nothing gets buried
- **English expression table** — ❌ Said / ✅ Better / Why format for targeted language improvement
- **Output language** — matches whatever language you use to ask (Korean request → Korean debrief, English request → English debrief)

---

## Output example

```
### Q1: Describe a time you influenced your team

**Main Question**
"Describe a time when you influenced and drove new thinking and innovation for your team."

**Answer** *(cleaned-up summary for reference)*
...

**Follow-up Questions**
- What data did you use? → ...
- How did you present to leadership? → ...

**Evaluation**
- **Rating**: 3 / 5
- **What worked**: Strong ownership signal; concrete persuasion methodology
- **Clarity & Structure of Thinking**: Core insight buried after 2 minutes of context...
- **What to improve**: Lead with the point first; "like" appeared 30+ times
- **Overall**: Strong story, delivery needs work

**English Expression Notes**
| ❌ Said | ✅ Better | Why |
|---|---|---|
| `I framed it as differently as a discovery system` | `I reframed it as a Discovery System` | "as differently as" is ungrammatical |
```

---

## Evaluation dimensions

| Dimension | What's assessed |
|---|---|
| Direct answer first | Does the candidate lead with the point? |
| Structure & clarity | Is the thinking organized and easy to follow? |
| Metrics & impact | Are outcomes quantified? |
| English clarity & fluency | Non-native patterns, grammar, word choice |
| Filler word / pause control | Density of `like`, `um`, `and then`, mid-answer pauses |

---

## Compatibility

Works with Claude.ai (Pro, Max, Team, Enterprise). Requires Skills to be enabled.

---

## License

MIT
