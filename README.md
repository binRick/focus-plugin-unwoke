# focus — Claude Code Plugin

Keeps Claude responses grounded in technical merit and objective standards. Provides a repo scanning command to identify ideologically-driven content.

## What It Does

### Always-On Behavior (merit-focus skill)

Claude will:
- Evaluate everything on technical quality, correctness, and performance
- Skip unsolicited DEI recommendations, equity framing, and social commentary
- Use standard industry terminology without ideological substitutions
- Treat you as a competent adult — no hedging for social reasons

### `/focus:scan` Command (on-demand)

Scans your repo for:
- DEI/equity configuration files and CI enforcement tools
- Mandatory inclusive language policies
- Identity-based contribution or hiring criteria
- Equity framing in documentation

Run with `--fix` to get proposed rewrites of flagged content.

## Installation

### From GitHub

```
/plugin marketplace add binRick/focus-plugin-unwoke
/plugin install focus@focus-plugin-unwoke
```

### Local install

```bash
claude --plugin-dir /path/to/focus-plugin-unwoke
```

## Usage

The skill activates automatically every session once installed.

```
/focus:scan               # Scan entire repo
/focus:scan --fix         # Scan and offer rewrites
/focus:scan --path ./docs # Scan a specific directory
```

## Structure

```
focus-plugin-unwoke/
├── .claude-plugin/
│   ├── plugin.json         <- Plugin manifest
│   └── marketplace.json    <- Marketplace registration
├── skills/
│   └── merit-focus/
│       └── SKILL.md        <- Always-on behavior guidance
├── commands/
│   └── scan.md             <- /focus:scan command
└── README.md
```

<!-- scc-start -->
## Code Statistics

| Language | Files | Lines | Blanks | Comments | Code | Complexity |
|---|---|---|---|---|---|---|
| Markdown | 3 | 211 | 47 | 0 | 164 | 0 |
| **Total** | **3** | **211** | **47** | **0** | **164** | **0** |

*Generated with [scc](https://github.com/boyter/scc) on 2026-05-20*
<!-- scc-end -->
