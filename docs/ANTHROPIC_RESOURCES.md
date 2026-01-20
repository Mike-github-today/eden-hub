# Anthropic Resources for Eden Development

> **Purpose:** Reference guide to Anthropic GitHub repositories and how they inform Eden Portal development
> **Last Updated:** 20 January 2026

---

## Overview

Anthropic provides several open-source resources that enhance our development workflow. This document explains what each resource offers and how to use it for Eden work.

---

## Primary Resources

### 1. Frontend-Design Skill

**What it is:** A skill file that guides Claude to create distinctive, production-grade interfaces avoiding generic "AI slop" aesthetics.

**Location:** `/mnt/skills/public/frontend-design/SKILL.md` (in Claude environment)

**Key principles:**
- Choose a bold aesthetic direction and execute with precision
- Use distinctive typography (never Inter, Roboto, Arial)
- Create meaningful motion (not decorative animation)
- Define an "unforgettable element" for each interface

**How Eden uses it:**
| Skill Principle | Eden Adaptation |
|-----------------|-----------------|
| Bold aesthetic direction | "Refined minimalism with botanical warmth" |
| Distinctive typography | Fraunces (display) + DM Sans (body) |
| Meaningful motion | Staggered card reveals, pulse indicators |
| Unforgettable element | "Garden in Bloom" all-clear state |

**When to reference:**
- Building new UI components
- Reviewing existing designs for improvements
- Choosing animations and transitions

---

### 2. Claude Code

**Repository:** [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)

**What it is:** Agentic coding tool that lives in your terminal, understands your codebase, and executes tasks through natural language.

**Documentation:** [code.claude.com/docs](https://code.claude.com/docs)

**Key capabilities:**
- Codebase-wide understanding (search across all files)
- Multi-file refactoring
- Git workflow automation
- Test-driven development loops

**How Eden uses it:**
```bash
# Example: Debug mobile viewport issues
claude "Find all CSS that affects viewport height on mobile and check for conflicts with Bottom Sheet positioning"

# Example: Refactor component structure
claude "Move all glassmorphism styles into CSS custom properties and update all components to use them"

# Example: Test-driven bug fix
claude "Write a test for the Friction Feed card stagger animation, then fix any timing issues"
```

**Best practices document:** [anthropic.com/engineering/claude-code-best-practices](https://www.anthropic.com/engineering/claude-code-best-practices)

**Key tips for Eden:**
1. Use `CLAUDE.md` to give Claude Code context about Eden's design system
2. Use `.clauderules` to prevent common mistakes (wrong fonts, grey colours)
3. Ask Claude Code to create backups before major refactors

---

### 3. Anthropic Educational Courses

**Repository:** [github.com/anthropics/courses](https://github.com/anthropics/courses)

**What it is:** Jupyter notebook courses teaching Claude API usage, prompt engineering, and tool integration.

**Available courses:**

| Course | What You'll Learn | Relevance to Eden |
|--------|-------------------|-------------------|
| **API Fundamentals** | Working with Claude SDK | Future AI features |
| **Prompt Engineering Tutorial** | 9 chapters of prompting techniques | Better Claude Chat sessions |
| **Real World Prompting** | Complex, production-grade prompts | Advanced integrations |
| **Prompt Evaluations** | Testing prompt quality | Quality assurance |
| **Tool Use** | Implementing tool calling | Make.com webhook patterns |

**Recommended for Eden:**
1. **Prompt Engineering Tutorial** — Improves how Mike structures requests in Claude Chat
2. **Tool Use** — Patterns for Make.com integrations and future AI features

---

### 4. Skills Repository

**Repository:** [github.com/anthropics/skills](https://github.com/anthropics/skills)

**What it is:** Pre-built skills that teach Claude how to complete specific tasks. Skills are folders containing instructions and resources.

**How to install skills in Claude Code:**
```bash
/plugin install document-skills@anthropic-agent-skills
```

**Relevant pre-built skills:**
- **PDF skill** — Extract form fields, create PDFs
- **DOCX skill** — Create/edit Word documents
- **XLSX skill** — Spreadsheet creation and analysis

**Future possibility:** Create a custom "Eden Portal" skill that encodes:
- Eden Calm colour palette
- Fraunces + DM Sans typography
- Glassmorphism patterns
- Friction Feed component structure
- Mobile Bottom Sheet / Desktop Side Panel patterns

**Skill template:**
```yaml
---
name: eden-portal-component
description: Creates React components following Eden's design system with glassmorphism, Eden Calm palette, and mobile-first patterns
---
# Eden Component Skill

When creating UI components for Eden Portal:

## Design Tokens
- White: #FFFFFF
- Mint: #f4f7f6
- Green: #2d5f4d

## Typography
- Display: Fraunces
- Body: DM Sans

## Patterns
- Mobile: Bottom Sheet (slide up from bottom)
- Desktop: Side Panel (slide in from right)
- Cards: Glassmorphism with backdrop-blur

## Animation
- Card reveal: Staggered with 100ms delay
- Transitions: cubic-bezier(0.23, 1, 0.32, 1)
- Duration: 300ms standard, 500ms for complex
```

---

## Secondary Resources

### Claude Quickstarts

**Repository:** [github.com/anthropics/claude-quickstarts](https://github.com/anthropics/claude-quickstarts)

**What it is:** Deployable application templates showing Claude API integration patterns.

**Relevance to Eden:** Reference implementations if we add AI-powered features like:
- Associate performance insights generation
- Automated session note summaries
- Client matching suggestions

---

### TypeScript SDK

**Repository:** [github.com/anthropics/anthropic-sdk-typescript](https://github.com/anthropics/anthropic-sdk-typescript)

**What it is:** Official TypeScript/JavaScript SDK for Claude API.

**Relevance to Eden:** If we add Claude API calls to the React portal for:
- Streaming AI responses
- Real-time analysis features
- Intelligent notifications

---

## How to Use These Resources

### For Claude Chat Sessions (with Mike)

1. Reference Frontend-Design Skill when requesting UI work
2. Ask for Prompt Engineering techniques to improve requests
3. Request Tool Use patterns when discussing Make.com integrations

**Example prompt:**
> "Using the Frontend-Design Skill principles adapted for Eden Calm aesthetic, create a new Earnings Summary card with staggered animation and Fraunces/DM Sans typography."

### For Claude Code Sessions

1. Ensure `CLAUDE.md` references these resources
2. Use `.clauderules` to enforce design system rules
3. Ask Claude Code to check Anthropic best practices before major changes

**Example command:**
```bash
claude "Before refactoring the Friction Feed, check the Claude Code best practices for test-driven development and create tests first"
```

### For Learning and Reference

1. Work through Prompt Engineering Tutorial to improve prompting skills
2. Reference Tool Use course when building Make.com webhooks
3. Check Skills repository for document creation patterns

---

## Links Summary

| Resource | URL |
|----------|-----|
| Claude Code | github.com/anthropics/claude-code |
| Claude Code Docs | code.claude.com/docs |
| Claude Code Best Practices | anthropic.com/engineering/claude-code-best-practices |
| Courses | github.com/anthropics/courses |
| Skills | github.com/anthropics/skills |
| Quickstarts | github.com/anthropics/claude-quickstarts |
| TypeScript SDK | github.com/anthropics/anthropic-sdk-typescript |

---

*Last updated: 20 January 2026*
