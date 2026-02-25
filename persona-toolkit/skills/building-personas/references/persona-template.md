# Persona Template

Use this template when creating a new persona via `/persona:create`. Fill in all sections. Leave nothing as placeholder text — if you don't know something, state the assumption explicitly and mark it for validation.

---

```markdown
# [Persona Name] — [One-Line Role Description]

> "[Representative quote in their voice — captures their worldview or core frustration]"

**Role**: `primary` | `secondary` | `anti-persona`
**Type**: `user` | `buyer` | `user+buyer`
**Confidence**: `proto-persona` | `interview-informed` | `data-validated`

---

## Identity

- **Name:** [Fictional but memorable — first name + last initial is fine]
- **Role:** [Job title + seniority level]
- **Company context:** [Stage, size, industry vertical]
- **Reports to / works with:** [Organizational context — who they collaborate with]

---

## Technical Profile

- **Languages / frameworks:** [Primary tools they work in daily]
- **Infrastructure / stack:** [Cloud provider, CI/CD, observability, deployment]
- **AI tools in use:** [Which AI coding agents, if any]
- **Experience level:** [Years + domain depth — "8 years, 3 in platform engineering"]
- **Build vs. buy:** [Do they prefer building internal tooling or integrating third-party?]
- **How they learn new tools:** [Docs-first? Run the quickstart? Search GitHub? Ask in Discord?]

---

## Jobs to be Done

> When [triggering situation],
> I want to [action / capability],
> So that [expected outcome / motivation].

**Job 1 (Primary):**
When [situation],
I want to [action],
So that [outcome].

**Job 2:**
When [situation],
I want to [action],
So that [outcome].

**Job 3:**
When [situation],
I want to [action],
So that [outcome].

---

## Goals

- **Primary goal:** [The one thing that makes their day successful]
- **Secondary goal:** [What they're also trying to accomplish]
- **Success looks like:** [Concrete, observable description of the outcome they want]

---

## Pain Points

1. **[Pain point name]** — [Specific description. Not "wants better tools" but "spends 2 hours every Monday manually triaging Sentry alerts into Linear because there's no automated connection"]
2. **[Pain point name]** — [Specific description]
3. **[Pain point name]** — [Specific description]

---

## Triggers

- **Discovery trigger:** [What specific event or threshold causes them to start looking for a solution in this category? Be concrete — "third post-mortem in 2 months where nobody caught the regression before users reported it"]
- **Decision trigger:** [What causes them to commit, sign up, or pay? "Sees the demo where a signal auto-creates an issue with full context and thinks 'that's what I've been doing manually'"]

---

## Information Sources

- **Communities:** [Specific subreddits, Discord servers, Slack groups — e.g., "r/devops, Hacker News, Claude Code Discord"]
- **Content:** [Specific newsletters, blogs, podcasts — e.g., "TLDR newsletter, Changelog podcast, Simon Willison's blog"]
- **Social proof:** [Whose opinion matters to them? "Respected OSS maintainers, YC founders they follow on Twitter"]
- **Search behavior:** [What would they Google? "ai agent project management", "automated issue triage from sentry"]

---

## Relationship to Product

- **Role:** [Daily user / Evaluator / Champion / Buyer / All of the above]
- **Usage frequency:** [Daily / Weekly / Per-incident]
- **Entry point:** [How do they first interact with the product? CLI? Dashboard? API docs?]
- **Adjacent tools:** [What else is in their workflow that we integrate with or compete with?]

---

## Decision-Making Context

- **Budget authority:** [Do they control budget? Need approval? Self-serve pricing acceptable?]
- **Stakeholders:** [Who else influences the decision? "CTO reviews tool additions but trusts their judgment"]
- **Evaluation criteria:** [Their explicit must-haves vs. nice-to-haves for this category]
- **Biggest adoption blocker:** [Most likely reason they DON'T commit — "not enough signal integrations for their stack" or "worried about adding another tool to maintain"]

---

## Research Basis

- **Data sources:** [Interviews: N, Support tickets: N, Survey responses: N, Behavioral analytics: Y/N]
- **Confidence level:** [Proto-persona (assumption-based) / Interview-informed / Data-validated]
- **Key assumptions to validate:** [List the top 2-3 assumptions that, if wrong, would change this persona significantly]
- **Created:** [Date]
- **Last reviewed:** [Date]
- **Next review:** [Date — 6-month cadence recommended]
```
