---
description: |
  Scans the current repository for ideologically-driven content: DEI configuration files,
  equity-framing in documentation, mandatory inclusive language policies, identity-based
  hiring or contribution requirements, and similar content. Reports findings with file
  locations and excerpts so the user can review and decide what to change.
argument-hint: "[--fix] [--path <dir>]"
---

# /focus:scan

## Purpose
Scan the repository for content that prioritizes identity-based or ideological considerations over technical merit. Report findings clearly so the user can review and act.

## Arguments
- `--fix` — After reporting, offer to rewrite flagged content in a merit-focused, neutral style
- `--path <dir>` — Limit scan to a specific directory (default: entire repo)

## What to Scan For

### 1. Configuration & Tooling Files
Look for files whose primary purpose is ideological enforcement:
- `diversity.yml`, `dei.yml`, `inclusion.md`, `equity-policy.*`
- `.github/CONTRIBUTING.md` sections mandating identity-based language or representation goals
- `CODE_OF_CONDUCT.md` that go beyond "don't harass people" into speech restriction or ideological compliance
- CI/CD steps that run inclusive language linters (e.g., `alex`, `textlint` with identity rules, `woke` linter)
- `package.json` / `requirements.txt` / `Gemfile` dependencies that are purely inclusive-language enforcement tools

### 2. Documentation with Equity/DEI Framing
Search `.md`, `.rst`, `.txt`, `.html` files for:
- Sections explicitly about "diversity goals", "representation targets", "equity initiatives"
- Language mandating contributors use specific identity-related terminology
- Hiring or contribution criteria that include identity characteristics as requirements or preferences
- Framing of technical disparities primarily through oppression/privilege language

### 3. Mandatory Language Policies
Look for enforced word replacement lists that go beyond technical clarity:
- Bans on "master/slave", "whitelist/blacklist", "sanity check" etc. without technical justification
- Required use of specific pronouns or identity terminology in code comments or docs
- Automated PR checks that block merges based on language ideology

### 4. Identity-Based Access or Contribution Rules
- Maintainer selection criteria referencing demographic characteristics
- Contribution tiers based on identity group membership
- Grant or sponsorship programs restricted by demographic

## Output Format

For each finding, report:

```
[CATEGORY] path/to/file.ext (line N)
Brief description of what was found
---
```

Group findings by category. At the end, provide a summary count.

If `--fix` is passed:
- For each flagged item, show the original and propose a rewritten version
- Focus rewrites on: removing ideological framing, replacing with merit/quality/behavior-based language, preserving any legitimate anti-harassment or conduct content
- Ask the user to confirm before making any changes

## Scan Execution

Use Grep and Glob tools to search efficiently.

**Key patterns to grep for:**
- `diversity|equity|inclusion|DEI|DEIB` (in non-trivial contexts)
- `marginalized|underrepresented|privileged|oppressed` (in policy/doc context)
- `inclusive language|gendered language|preferred pronouns` (in policy context)
- `alex\b|woke-checker|textlint.*identity` (in package files / CI configs)
- `whitelist|blacklist|master|slave` (in language ban contexts — distinguish from legitimate technical use)
- `representation goal|diversity target|demographic` (in contribution/hiring docs)

**Do not flag:**
- Legitimate technical uses of flagged terms (e.g., `master` branch, `whitelist` in network config)
- Basic anti-harassment conduct rules ("don't insult people", "be respectful")
- Accessibility considerations that affect actual functionality (WCAG, screen reader support, etc.)
- Internationalization/localization work

## Example Output

```
[CI TOOLING] .github/workflows/lint.yml (line 34)
Runs 'alex' inclusive language linter as required PR check — blocks merges on flagged terms.

[LANGUAGE POLICY] CONTRIBUTING.md (lines 45-67)
Mandates replacement of "whitelist/blacklist" and "master/slave" throughout codebase.
Requires use of specific pronouns in all documentation.

[DEI CONFIG] diversity.yml
Dedicated file setting representation targets by demographic group for maintainer recruitment.

[CODE OF CONDUCT] CODE_OF_CONDUCT.md (lines 12-28)
Extends beyond conduct into mandatory ideological affirmations and speech restrictions.

---
Summary: 4 findings across 4 files
Categories: CI Tooling (1), Language Policy (1), DEI Config (1), Code of Conduct (1)
```
