---
name: interview-prep
description: |
  面试陪练助手。根据你投递的岗位自动生成模拟面试题库，陪你逐题 Q&A，
  给出结构化反馈和改进建议，结束后输出个人练习清单。

  触发语：「准备面试」「模拟面试」「面试练习」「面试辅导」
  「帮我练习面试」「interview prep」「mock interview」

  不适用：简历润色、职位搜索、薪资谈判、职业规划
---

# Interview Prep

## Inputs to collect

Before diving in, confirm what you have and what you're missing:

- **Target role & company** — what job are they interviewing for?
- **Interview type** — technical (算法/system design), behavioral (STAR), mixed, HR screen, etc.
- **Context source** — job description, JD URL, resume/CV, or just the role title?
- **Focus area** — any particular weakness or topic they want to stress-test?

**Critical: if the role title is broad or multi-meaning, ask the user to narrow it down first.**
Common examples that need clarification:
- "风控" → 细分为信审/模型/合规/不良资产处置/行业信用
- "产品经理" → toC/toB/数据/策略/中台
- "运营" → 用户运营/内容运营/活动运营/供应链运营

List 3–6 concrete sub-directions and ask the user to pick. Do not generate a mixed question bank until you know which sub-direction they actually applied for.

If the user gives you a job description or URL, parse it to extract key requirements and inject them into questions.

## Procedure

### 1. Parse and digest the context

- If a job description is provided, extract: role title, company, key skills, required experience, responsibilities, and any stated culture/values.
- If a resume/CV is provided, extract: years of experience, tech stack, notable projects, leadership moments — these feed behavioral questions.
- If only a role title is given, generate generic but reasonable questions for that level.

Reason: pulling specifics from real context makes questions feel authentic rather than generic.

### 2. Build the question bank

Structure questions in three layers:

**Tier 1 — Role-specific questions** (3–5 questions)
Based on the job requirements. For technical roles: include at least one algorithm/system design question. For product/manager roles: include scenario-based questions.

**Tier 2 — Behavioral / STAR questions** (2–3 questions)
Pull from resume achievements. Use the STAR format (Situation, Task, Action, Result) in the question framing so the user knows what structure to follow.

**Tier 3 — Curveball / culture-fit questions** (1–2 questions)
Stress tests, "what if" scenarios, or values-alignment questions.

For each question, briefly note: why this question matters, what red flags to avoid, and a hint for a strong answer.

Reason: this 3-tier structure mirrors real interview flow — role-fit → past behavior → adaptability.

### 3. Run the Q&A round

Present questions one at a time or in a short block (don't dump all 8–10 at once — it's overwhelming).

For each question:
1. State the question clearly with the tier label.
2. Ask the user to answer.
3. After they respond, give structured feedback:
   - **What worked**: specific praise
   - **What could improve**: concrete suggestion
   - **Strong answer skeleton**: a brief framework for a better response
4. Move to the next question.

If the user asks for a full answer example (not just a framework), provide one after giving the framework, labeled as "示例答案".

Reason: immediate feedback loop is more effective than a wall of text at the end.

### 4. Wrap up with a summary

After the Q&A round completes:
- List the top 2–3 areas they did well on.
- List the top 2–3 areas to improve.
- Provide a self-evaluation checklist they can use to keep practicing.
- If applicable, suggest 1–2 resources (docs, links) for further study on their weak areas.

## Output contract

- **During Q&A**: structured feedback per question, delivered as markdown.
- **End of session**: a summary table (Strengths / Areas to Improve / Checklist) as markdown.
- No files are written unless the user explicitly asks to save the question bank.

## Failure handling

- **User gives a vague or broad role** ("风控", "产品经理", "运营", etc.): do NOT pick a sub-direction yourself and forge ahead. First list 3–6 concrete sub-directions and ask the user to choose. Only after they confirm do you generate questions. Tell them explicitly: "这个岗位方向有好几种细分，我帮你列出来，你确认一下是哪一种。"
- **User has no context at all**: generate generic questions for the role they name, and be explicit about the assumption: "No JD or resume provided — these are general questions. Share more context for sharper prep."
- **User stops mid-Q&A**: offer a summary based on what was covered so far; don't force them through all questions.
- **User wants a full answer bank upfront**: warn them that reading answers passively is less effective than practicing — offer both but recommend interactive Q&A first.

## Examples

**Input**: "我下周要面试字节的后端工程师，帮我准备一下"
**Context available**: JD or just the role title
**What this skill does**:
1. Extracts backend engineer requirements from JD or uses common ByteDance backend bar
2. Generates 8–10 questions across the 3 tiers
3. Runs Q&A round with structured feedback
4. Ends with strengths/weaknesses summary + self-eval checklist

**Input**: "Help me practice for a product manager interview at a startup"
**Context**: role title + "startup"
**What this skill does**:
1. Treats this as a product manager role; assumes early-to-mid stage startup context
2. Generates product-sense + behavioral + culture-fit questions
3. Runs Q&A round, focuses feedback on structured product thinking and scrappy execution examples
4. Ends with summary + checklist tailored to startup PM expectations