# QA templates

## Criteria file: `qa-<brief name>-criteria.md`

```markdown
# Acceptance criteria: <brief title>

**Brief:** <path or wiki link> · **Build:** <URL or file> · **Drafted:** <date> · **Status:** Draft / Approved by <student> on <date>

## Summary
| | Must | Should | Could | Total |
| --- | --- | --- | --- | --- |
| UI-testable | | | | |
| Not testable here | | | | |

## Criteria
| ID | Pri | Area | Title | Given | When | Then | Source |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AC-01 | Must | Phone | ... | ... | ... | ... | brief.md L18 |

## Not testable here
| ID | Requirement | Why not | Who can verify |
| --- | --- | --- | --- |

## Too vague to test as written
| Brief says | Suggested testable version |
| --- | --- |

## Open questions (with suggested default)
1. ...
```

## Findings file: `qa-<brief name>-findings.md`

```markdown
# QA findings: <brief title>

**Verdict: <Ready / Ready with fixes / Not ready>**
- <why, 3–5 bullets>

## What was tested
Brief · build · environment · date · browser · viewports · criteria version

## Results summary
| | Pass | Fail | Blocked | Not testable | Total |
| --- | --- | --- | --- | --- | --- |
| Must | | | | | |
| Should | | | | | |
| Could | | | | | |

## Defects
### D-01 · <Severity> · <short title>
- **Criterion:** AC-xx · **Brief:** <source>
- **Steps:** 1. … 2. …
- **Expected:** … · **Actual:** …

## Gaps between brief and build
- **In brief, not in build:** …
- **In build, not in brief:** …

## Not testable here
| ID | What | Who can verify |
| --- | --- | --- |

## Exploratory findings
- …

## Full results
| ID | Pri | Title | Verdict | Evidence |
| --- | --- | --- | --- | --- |

## Suggested next steps
- …
```
