# Interview Self Introduce Skill

`interview-self-introduce` is a Codex skill for turning “please introduce yourself” into a concise, job-specific interview opening. It helps agents combine a target role, JD or resume evidence, interview context, and duration constraints into a truthful spoken self-introduction.

The skill is designed for interview preparation scenarios where candidates need a natural 30s / 60s / 90s / 120s answer rather than a chronological resume read-through.

## What it does

- Generates role-specific self-introductions from a JD and resume or from lightweight role notes.
- Supports HR, hiring-manager, technical, final, and English interview rounds.
- Produces 30s / 60s / 90s / 120s spoken versions with duration guidance.
- Maps role requirements to candidate evidence before drafting.
- Rewrites weak or chronological drafts into theme-based, speakable intros.
- Handles incomplete or ordinary experience without inventing achievements.
- Adds likely follow-up questions, risky wording notes, and rehearsal guidance.
- Supports Chinese, English, and bilingual output.

## Core principles

1. **Evidence before polish**  
   Every meaningful claim should trace back to resume text, project notes, or user-provided facts.

2. **Speakable, not decorative**  
   The final answer should sound natural when spoken aloud, not like a formal bio or keyword stack.

3. **Role-fit proof, not resume replay**  
   The skill compresses experience into 2–3 job-relevant themes instead of listing jobs by year.

4. **Risk control**  
   It avoids unsupported claims such as “expert”, “fully owned”, or “guaranteed outcome”.

5. **Intake first for full JD/resume workflows**  
   When a JD and resume are provided, the agent must confirm interview round, target duration, and language before producing the full bundle.

## Package structure

```text
.
├── SKILL.md                         # Main skill instructions
├── README.md                        # Public overview
├── agents/
│   └── openai.yaml                  # Display metadata
├── assets/                          # Reusable output templates
│   ├── bilingual-template.md
│   ├── rehearsal-card-template.md
│   └── self-intro-template.md
└── references/                      # Task-specific guidance loaded on demand
    ├── anti-patterns.md
    ├── evidence-rules.md
    ├── examples.md
    ├── intake-gate.md
    ├── interview-rounds.md
    ├── output-contracts.md
    ├── quality-checklist.md
    ├── resume-input.md
    └── tone-guide.md
```

This release package intentionally excludes local development tests, fixtures, reports, generated candidate outputs, and other non-runtime files.

## How to use in Codex

Place this directory under a Codex skills directory, for example:

```bash
~/.codex/skills/interview-self-introduce
```

Then invoke it by name in a prompt:

```text
Use $interview-self-introduce to create a 90s Chinese hiring-manager self-introduction from this JD and my resume.
```

For full JD/resume workflows, the expected intake fields are:

- `interviewRound`: `hr | hiring-manager | technical | final | english`
- `duration`: `30s | 60s | 90s | 120s`
- `language`: `zh-CN | en | bilingual`

If these are missing, the skill instructs the agent to ask before generating the final self-introduction bundle.

## Typical output

A full Markdown response usually includes:

- Input summary
- Role understanding
- Evidence mapping table
- Recommended spoken self-introduction
- Optional shorter / alternative versions
- Likely follow-up questions
- Risky or omitted content
- Quality check

For lightweight prompts without a complete JD or resume, the skill can produce a provisional QuickStart version and clearly mark assumptions.

## Resume handling

This skill is documentation-first. It does not ship a resume parser or require bundled Python scripts.

Recommended behavior:

- Markdown / pasted text: use directly as resume evidence.
- PDF / DOCX / DOC: use a separate resume-conversion skill if available, or a local parser such as `pymupdf4llm` / `markitdown`.
- Scanned or image-only resumes: ask the user for pasted text or explicit OCR consent.
- Never invent resume content when extraction fails.

See [`references/resume-input.md`](references/resume-input.md) for the full protocol.

## License

No license file is included yet. Add a license before publishing this skill for reuse outside your own projects.
