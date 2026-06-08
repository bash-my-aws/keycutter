# Skill Review: keycutter

**Grade: A (96%)**
**Status: Excellent**
**Reviewed:** 2026-02-23

## Summary

The keycutter SKILL.md is an exemplary project-embedded skill that serves as a lean, well-structured cheat sheet index. At 294 words, it provides immediate value through a quick reference table and copy-paste workflows while linking out to 8 verified documentation files for deeper content.

## Attribute Scores

| Attribute | Score | Max | Grade | Notes |
|-----------|-------|-----|-------|-------|
| Metadata Quality | 25 | 25 | A | Valid frontmatter, 99-char description with clear trigger phrases |
| Structure Quality | 25 | 25 | A | Minimal index with progressive disclosure via 8 doc links |
| Content Quality | 25 | 25 | A | Quick reference, copy-paste commands, Quick Setup workflow |
| Organization | 12.5 | 15 | B | Thematic ordering preferred over alphabetical; all links explicit |
| Token Efficiency | 8.3 | 10 | B | ~382-601 tokens (borderline on 500 threshold); no redundancy |
| **Total** | **95.8** | **100** | **A** | |

## Detailed Assessment

### Metadata Quality (25/25)

| # | Question | Answer | Notes |
|---|----------|--------|-------|
| 1 | Valid YAML frontmatter? | Yes | `name` and `description` present |
| 2 | Name is kebab-case? | Yes | `keycutter` (single word, valid) |
| 3 | Description under 100 chars? | Yes | Exactly 99 characters |
| 4 | Description explains when to use? | Yes | "Use for key setup, YubiKeys, agents, or SSH troubleshooting" |

### Structure Quality (25/25)

| # | Question | Answer | Notes |
|---|----------|--------|-------|
| 5 | Minimal index (not monolithic)? | Yes | 294 words, links to 8 docs |
| 6 | Progressive disclosure? | Yes | Quick ref -> Key concepts -> Documentation links |
| 7 | Detailed docs in separate files? | Yes | All 8 links verified to resolve |

### Content Quality (25/25)

| # | Question | Answer | Notes |
|---|----------|--------|-------|
| 8 | Quick Reference section? | Yes | 8-entry command table + YubiKey essentials table |
| 9 | Copy-paste commands? | Yes | Backtick formatting, fenced code block for Quick Setup |
| 10 | Human-readable? | Yes | Clean tables, concise prose |
| 11 | Examples provided? | Yes | Quick Setup (5-step workflow), keytag example |
| 12 | Accurate and up-to-date? | Yes | All 8 doc links verified; commands match project CLI |

### Organization (12.5/15)

| # | Question | Answer | Notes |
|---|----------|--------|-------|
| 13 | Items alphabetized? | Partial | Workflow-priority ordering, not alphabetical |
| 14 | Links include explicit filenames? | Yes | All links include `.md` filenames |
| 15 | Docs directory well-organized? | Yes | Subdirectories for config, yubikeys, design, etc. |

### Token Efficiency (8.3/10)

| # | Question | Answer | Notes |
|---|----------|--------|-------|
| 16 | Under 500 tokens? | Borderline | ~382 by word estimate, ~601 by char/4 estimate |
| 17 | Claude can load just what's needed? | Yes | Index pattern with topic-specific linked docs |
| 18 | No redundant sections? | Yes | Each section serves a distinct purpose |

## Findings

### Issues (must fix)

- [ ] None identified -- the skill meets all critical criteria

### Improvements (should consider)

- [ ] **Token budget awareness:** At ~2400 characters, the SKILL.md sits near the 500-token threshold depending on tokenizer. Consider whether the YubiKey essentials table (lines 26-27) could be moved to a linked doc to create more headroom, though its presence as "CRITICAL" info justifies inline placement.
- [ ] **Command table ordering:** Consider alphabetizing the command table (`agents`, `config`, `create`, `git-signing`, `hosts`, `keys`, `push-keys`, `update`) for faster scanning, or add a note explaining the workflow-priority ordering.
- [ ] **Documentation link descriptions:** The link labels are clear but could include one-line summaries (e.g., "[Tutorial](../../../docs/tutorial.md) -- Multi-account GitHub, key creation workflows") to help Claude decide which doc to load without following every link.

### Strengths

- **Lean and focused:** 294 words is an excellent size for a skill index -- provides immediate utility without bloating Claude's context window.
- **Smart description field:** The 99-character description packs in four specific trigger phrases ("key setup, YubiKeys, agents, SSH troubleshooting") that maximize auto-loading accuracy.
- **Practical Quick Setup section:** The 5-step YubiKey + GitHub workflow gives Claude an immediately actionable recipe for the most common use case.
- **All links verified:** All 8 documentation links resolve to existing files, demonstrating careful maintenance.
- **Progressive disclosure:** The three-tier structure (quick reference -> key concepts -> deep docs) matches the ideal skill pattern perfectly.
- **YubiKey "yubisneeze" callout:** Including OTP disable as "CRITICAL" inline rather than buried in a linked doc shows good judgment about what deserves prime real estate.
- **No anti-patterns:** No monolithic content, no hardcoded absolute paths, no missing frontmatter, no verbose descriptions.

## Files Reviewed

- `/Users/admin/Code/github.com/mbailey/keycutter/.claude/skills/keycutter/SKILL.md` (primary target)
- `/Users/admin/Code/github.com/mbailey/keycutter/docs/tutorial.md` (link verification)
- `/Users/admin/Code/github.com/mbailey/keycutter/docs/ssh-keytags.md` (link verification)
- `/Users/admin/Code/github.com/mbailey/keycutter/docs/config/README.md` (link verification)
- `/Users/admin/Code/github.com/mbailey/keycutter/docs/yubikeys/ykman-yubikey-manager.md` (link verification)
- `/Users/admin/Code/github.com/mbailey/keycutter/docs/yubikeys/fido2-on-yubikeys.md` (link verification)
- `/Users/admin/Code/github.com/mbailey/keycutter/docs/troubleshooting.md` (link verification)
- `/Users/admin/Code/github.com/mbailey/keycutter/docs/tips-and-tricks.md` (link verification)
- `/Users/admin/Code/github.com/mbailey/keycutter/docs/development.md` (link verification)
