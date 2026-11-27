# Versions

| Item | Value |
|---|---|
| UCD Check | 1.0.0 |
| UCD Context the standards were copied from | 1.0.0 |
| Last checked against official sources, as recorded by UCD Context | 25 November 2026 |
| Date the standards were copied into UCD Check | 27 November 2026 |
| GOV.UK Frontend | v6.1.0 (released 2 March 2026). The current major version is 6 |
| GOV.UK Design System | 37 components and 30 patterns listed on the date above |
| MoJ Design System | 38 components and 6 patterns listed on the date above |
| MoJ Frontend | Not pinned. Check the installed version and its supported GOV.UK Frontend version |
| WCAG | 2.2, level AA |
| Service Standard | 14 points |

The version rows above are copied from the UCD Context `VERSIONS` file. UCD Check did not re-check the official sites on 27 November 2026.

No local `ucd-context/` folder was on this machine. Each file below was downloaded unchanged from the public pack preview, which serves the v1.0.0 markdown (`Content-Type: text/markdown`). The byte size of each download matched the size published on ucdcontext.com.

## Files copied

Paths are the path inside UCD Context 1.0.0, then the preview URL they were taken from. They now live in `skills/ucd/standards/` under the file name only.

| Source path | Preview URL |
|---|---|
| `standards/accessibility-wcag-2.2-aa.md` | https://www.ucdcontext.com/pack-preview/standards/accessibility-wcag-2.2-aa.md |
| `standards/govuk-components.md` | https://www.ucdcontext.com/pack-preview/standards/govuk-components.md |
| `standards/govuk-content-style.md` | https://www.ucdcontext.com/pack-preview/standards/govuk-content-style.md |
| `standards/govuk-design-system-foundations.md` | https://www.ucdcontext.com/pack-preview/standards/govuk-design-system-foundations.md |
| `standards/govuk-patterns.md` | https://www.ucdcontext.com/pack-preview/standards/govuk-patterns.md |
| `standards/govuk-service-standard.md` | https://www.ucdcontext.com/pack-preview/standards/govuk-service-standard.md |
| `standards/moj-components-and-patterns.md` | https://www.ucdcontext.com/pack-preview/standards/moj-components-and-patterns.md |
| `playbooks/build-a-form-page.md` | https://www.ucdcontext.com/pack-preview/playbooks/build-a-form-page.md |
| `playbooks/choose-a-component.md` | https://www.ucdcontext.com/pack-preview/playbooks/choose-a-component.md |
| `playbooks/design-a-journey.md` | https://www.ucdcontext.com/pack-preview/playbooks/design-a-journey.md |
| `playbooks/needs-a-human.md` | https://www.ucdcontext.com/pack-preview/playbooks/needs-a-human.md |
| `playbooks/review-before-merge.md` | https://www.ucdcontext.com/pack-preview/playbooks/review-before-merge.md |
| `playbooks/write-page-content.md` | https://www.ucdcontext.com/pack-preview/playbooks/write-page-content.md |
| `ATTRIBUTION.md` | https://www.ucdcontext.com/pack-preview/ATTRIBUTION.md |

Not copied: adapters, `INSTALL.md`, evals, examples, stacks, `START-HERE.md`, `README.md` and `VERSIONS.md`. The version table above is the part of that `VERSIONS` file this repo needs.

## Link fixes

Copied files are unchanged apart from relative links, so they still resolve now that standards and playbooks sit in one folder.

- `` `standards/ `` and `` `playbooks/ `` at the start of a path were removed. The files they named are in the same folder.
- In `build-a-form-page.md`, the path `` `examples/question-page.md` `` pointed at an example that is not bundled. That sentence now points at the question pages pattern: https://design-system.service.gov.uk/patterns/question-pages/

`skills/ucd/standards/ATTRIBUTION.md` still mentions the original pack's `examples/` folder in prose. Those examples are not part of UCD Check.
