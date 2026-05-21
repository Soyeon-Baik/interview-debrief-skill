---
name: interview-debrief
description: >
  Use this skill whenever the user shares an interview transcript or recording script (e.g., from Otter.ai, 
  Rev, or any speech-to-text tool) and wants a structured debrief. Triggers include: "Analyze my interview", 
  "Interview post mortem", "interview transcript", "Review my interview", or any time the user pastes 
  a raw transcript with speaker labels and asks for feedback or review of their interview.
  Always use this skill — do not attempt to analyze the transcript without following this workflow.
---

# Interview Debrief Skill

Transform raw voice-recording transcripts into structured, actionable interview debriefs for PM candidates.

---

## Input Expectations

- **Format**: Speaker-labeled transcript (e.g., `Speaker 1:`, `Speaker 2:`, or named speakers)
- **Source**: Typically Otter.ai or similar STT tools — expect filler words, false starts, mid-sentence corrections, and run-on sentences
- **Language**: English interview. The candidate is a native Korean speaker — expect non-native speaking patterns such as literal translations from Korean, unnatural word order, overly formal phrasing, or habitual expressions that sound awkward in native English. No Korean words expected mid-interview.

The candidate is likely a non-native English speaker — watch for non-native patterns such as literal translations, unnatural word order, overly formal phrasing, or habitual expressions that sound awkward in native English.

---

## Step 1: Pre-Processing the Transcript

Before structuring anything, mentally parse the transcript with these rules:

**Speaker identification**
- Identify which speaker is the interviewer and which is the candidate. If unclear, infer from context (the person asking structured questions = interviewer).
- Label them consistently as `Interviewer` and `Candidate` throughout the debrief.
- **Extra speakers (Speaker 3, Speaker 4, etc.)**: STT tools frequently split one person's voice into multiple speaker labels due to tone shifts, overlaps, or mic artifacts. If additional speakers appear, silently assign their lines to whichever of the two main speakers makes more sense contextually. Do not flag this to the user or treat it as a notable issue.

**Voice artifact handling — do NOT let these break your understanding:**
- Filler words: `okay`, `um`, `uh`, `you know`, `like`, `so`, `I mean` → strip or absorb into meaning when parsing content
- False starts: `I think — well, what I mean is...` → take the final intended meaning
- Repetitions: `the the way we approached` → collapse to `the way we approached`
- Mid-sentence topic shifts: follow the final direction the speaker landed on
- Trailing thoughts: if a sentence is incomplete but meaning is inferable, infer it
- Interviewer affirmations (`mm-hmm`, `right`, `got it`) during candidate speech → ignore, don't treat as new questions

**Filler word & pause frequency tracking — flag if excessive:**
While fillers are ignored for comprehension, they must be tracked and flagged in the evaluation if problematic. Assess per Q&A block:

- **Excessive fillers**: Count approximate filler density. If fillers appear more than ~2–3 times per 5 sentences, flag it.
  - Note the specific words that repeat most (e.g., "basically" appearing 6 times, heavy "um/uh" clustering at sentence starts)
- **Unnatural pauses mid-answer**: Long pauses in the middle of a response (not at the start where thinking time is acceptable) suggest loss of direction — flag these if they appear to interrupt the flow of a point already being made.
- **Interview-prep pauses — do NOT flag**: A pause at the very beginning of an answer (before the candidate starts speaking) is normal and acceptable thinking time. Do not penalize this.

Flag these under the **English Expression Notes** section of the relevant Q&A block, or in the Overall Summary if it's a consistent pattern across the interview.

**Interviewer accent & STT errors**
Interviewers may be native English speaker or with a strong accent English speakers. For example, some English accent patterns frequently cause STT misrecognition — e.g., retroflex consonants rendered as wrong letters, dropped articles, or run-together words. When the interviewer's question looks garbled or grammatically broken:
- Attempt to infer the intended question from context (topic flow, candidate's response, common PM interview question patterns)
- Reconstruct the most likely intended question and use it as the Question block
- Flag the uncertainty inline with a note, e.g.: `⚠️ STT quality issue — reconstructed from context. Original transcript: "[raw text]". Please verify against recording if needed.`
- **Do not penalize the candidate's answer** based on a question that may have been misread by STT. If the candidate's answer doesn't align with the reconstructed question, note the possible mismatch rather than docking points.
- Each time the interviewer asks a substantive new question, that's a new Q&A block
- Follow-up clarifying questions within the same topic = same block
- If the interviewer asks multiple sub-questions at once, list them together under one Question block

---

## Step 2: Build the Debrief Structure

Produce one block per Q&A exchange. Use this format for each:

**Important — evaluation process**:
Always evaluate based on the **raw transcript** (what was actually said, including delivery issues, filler density, structural problems). The Answer section is a cleaned-up summary for the user's reference only — it must never be used as the basis for scoring. Write the evaluation independently from the cleaned-up summary; a polished Answer should never mask delivery problems present in the actual script.

```
---

### Q[N]: [Short title summarizing the question topic]

**Main Question**
[Cleaned-up version of what the interviewer asked.]

**Answer** *(cleaned-up summary for reference)*
[Cleaned-up summary of the candidate's main response. Remove fillers and false starts, preserve substance. Do not add content that wasn't there.]

**Follow-up Questions**
- [Follow-up question 1] → [Candidate's answer, 1–2 sentences]
- [Follow-up question 2] → [Candidate's answer, 1–2 sentences]
- [...and so on]

[Omit this section entirely if there were no follow-up questions.]

**Evaluation**
- **Rating**: [X / 5]
- **What worked**: [Specific things the candidate did well — structure, examples, metrics, framing, etc.]
- **Clarity & Structure of Thinking**: [Was the answer organized? Was the thinking process visible and easy to follow? Did the candidate lead with the point or bury it? Be specific about what made it clear or unclear.]
- **What to improve**: [Specific, actionable gaps — missing structure (such as STAR) or clarity in the answer, no metrics, didn't directly answer the question first, too abstract, etc.]
- **Overall**: [1–2 sentence summary verdict]

**English Expression Notes**
[Only include this section if there were expressions that were unclear, awkward, or non-native-sounding.]
[If no notable expression issues, write: *No significant expression issues in this exchange.*]

| ❌ Said | ✅ Better | Why |
|---|---|---|
| `exact words from transcript` | `improved version` | brief explanation |

Note: use backtick code blocks for the expressions, but do NOT include quotation marks inside them.
```

---

## Step 3: Summary Section

After all Q&A blocks, add a summary section:

```
---

## Overall Debrief Summary

### Performance Snapshot
| Dimension | Rating | Notes |
|---|---|---|
| Direct answer first | X/5 | ... |
| Structure & clarity | X/5 | ... |
| Use of metrics & impact | X/5 | ... |
| English clarity & fluency | X/5 | ... |
| Filler word / pause control | X/5 | ... |

**Overall seniority impression**: [1–2 sentences on the overall sense of senior PM signal across the interview — ownership, ambiguity handling, strategic framing. Not a score, just a holistic read.]

### Top 3 Strengths
1. ...
2. ...
3. ...

### Top 3 Priority Improvements
1. ...
2. ...
3. ...

### One Thing to Practice Before Next Interview
[Single most impactful thing to work on — be direct and specific]
```

---

## PM Evaluation Rubric

Use these criteria when scoring and giving feedback:

### Structure & Communication
- **Direct answer first**: Does the candidate answer the actual question before elaborating? (Avoid burying the answer at the end)
- **STAR or narrative**: Situation/Task/Action/Result — or a clear story arc with beginning, middle, outcome
- **Concision**: No unnecessary preamble, excessive hedging, or rambling

### PM Substance
- **Metrics & impact**: Quantified outcomes (%, $, time), not just activities
- **Customer/user centricity**: Does the answer center on user problems and needs?
- **Cross-functional awareness**: Evidence of working with eng, design, data, stakeholders
- **Product thinking**: Trade-offs, prioritization reasoning, frameworks where relevant

### English Clarity & Fluency
- **Filler word density**: Occasional fillers are normal; frequent clustering (especially repeated words like "basically", "you know", "like") signals low fluency under pressure
- **Pause pattern**: Starting pauses = acceptable. Mid-answer pauses that break a thought already in progress = flag
- **Expression naturalness**: Korean-influenced phrasing, literal translations, or awkward word choices that reduce clarity

### Rating Scale
- **5/5**: Excellent — clear, structured, specific, strong impact metrics
- **4/5**: Good — solid but missing one key element (e.g., metrics, or slightly indirect)
- **3/5**: Adequate — answers the question but lacks depth, structure, or specificity
- **2/5**: Weak — vague, unstructured, or misses the point of the question
- **1/5**: Poor — doesn't answer, too short, or contradicts the question

---

## Output Format

- Default: **Markdown** (`.md` file) — clean, downloadable, readable in any editor
- If the user requests HTML: produce a self-contained `.html` file with basic styling (readable on mobile too)
- Save the output file and present it to the user via `present_files`
- Filename format: `interview-debrief-[YYYY-MM-DD].md` (use today's date, or ask the user for the interview date)

---

## Important Notes

- **Do not invent content.** If an answer was thin, say so — don't pad it with what the candidate "probably meant."
- **Be direct with feedback.** The user is a senior candidate who wants unfiltered, specific critique — not encouragement for the sake of it.
- **Output language**: Match the language the user is communicating in with Claude. If the user wrote their request in Korean, write the debrief in Korean. If in English, write in English. English quotes and expressions from the transcript are always preserved as-is regardless of output language.
