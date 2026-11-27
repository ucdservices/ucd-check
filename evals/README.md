# Evals

Fixtures for a manual run of `/ucd`. They are not part of the skill. Installing `skills/ucd/` must not copy this folder.

Run each fixture in a GOV.UK prototype that has `govuk-frontend` in `package.json`, except `not-govuk/`, which must be its own project.

A faithful run reports the findings below. It may split or join sentences. It must not miss a row, and it must not report a finding on the clean page. Severity uses `must fix`, `should fix` and `consider`.

## How to run

Install the skill first. See the root [README](../README.md).

### GitHub Copilot

In VS Code chat, with the prototype open:

```text
/ucd evals/fixtures/validation/browser-only.njk
```

In Copilot CLI:

```text
Use the /ucd skill to check evals/fixtures/validation/browser-only.njk
```

For code review, open a pull request that contains the fixture and let Copilot review the head branch. It should comment and must not commit.

### Claude Code

```text
/ucd evals/fixtures/validation/browser-only.njk
```

### Cursor

Type `/ucd` and the fixture path. Choose `ucd` from the `/` menu if the name is not taken.

Repeat for each file below. For the journey, pass the folder `evals/fixtures/journey`. For the non-GOV.UK case, open `evals/fixtures/not-govuk/` as the project and run `/ucd signup.html`.

## Components

### `fixtures/components/select-for-country.njk`

| Severity | Finding |
|---|---|
| should fix | A select is used for three options. Radios fit. England is pre-selected only as part of that select. The rule against pre-selecting is about radios and checkboxes, so do not add a separate finding for `selected`. |
| should fix | The continue button is disabled. |

### `fixtures/components/modal-and-tooltip.html`

| Severity | Finding |
|---|---|
| should fix | A dialog asks "Are you sure?" instead of a separate page. |
| should fix | The question mark uses a `title` tooltip instead of hint text or details. |

## Question pages

### `fixtures/question-pages/name-and-email.njk`

| Severity | Finding |
|---|---|
| must fix | Full name and email are two unrelated questions on one page. |
| should fix | The name field uses placeholder text instead of a hint. |
| should fix | The `<h1>` is "Your details", not the question. The labels are not the heading. |

### `fixtures/question-pages/radios-without-legend.html`

| Severity | Finding |
|---|---|
| must fix | The radios have no fieldset and no legend. |
| should fix | The `<h1>` is "Question". The question itself is an `<h2>`. |

## Validation

### `fixtures/validation/browser-only.njk`

| Severity | Finding |
|---|---|
| must fix | The form uses `required` and a submit script. There is no error summary and no server-side error path. |
| should fix | The form has no `novalidate`. |
| should fix | The script sets "Please enter a valid value". |

### `fixtures/validation/please-enter.html`

| Severity | Finding |
|---|---|
| must fix | The field has the error classes and no error message, and the page has no error summary. |
| should fix | The title does not start with "Error: " while the field is in an error state. |

## Content

### `fixtures/content/title-case.njk`

| Severity | Finding |
|---|---|
| should fix | The heading is title case: "What Is Your National Insurance Number?" |
| should fix | "Please enter your number" and the link "click here". |
| should fix | The button says "Click Here". |

### `fixtures/content/jargon.html`

| Severity | Finding |
|---|---|
| should fix | "Utilise", "in order to", "commence" and "e.g." |
| should fix | The button says "SUBMIT". |

## Accessibility

### `fixtures/accessibility/no-label.html`

| Severity | Finding |
|---|---|
| must fix | The reference input has no label. |
| must fix | `.govuk-input:focus` sets `outline: none`. |

### `fixtures/accessibility/div-button.html`

| Severity | Finding |
|---|---|
| must fix | A `<div>` with `onclick` is used as the continue control. |
| must fix | The image of the letter has no `alt`. |
| should fix | `tabindex="2"` and `<html>` has no `lang`. |

## Journey

Run `/ucd` on the folder `fixtures/journey/`.

| Severity | Finding |
|---|---|
| must fix | `national-insurance.njk` posts to `/confirmation` with "Submit application". Nothing in the folder lets the user check their answer first. |
| should fix | `confirmation.njk` is a heading, not the panel component. It has no reference number, no "what happens next", no contact details and no feedback link. Nothing in the folder sends the reference by email or text message. |

## Clean

### `fixtures/clean/email.njk`

No findings.

Skip the journey check. It is one question page and does not include check answers, confirmation or routing to another step.

The template already renders an error summary and passes `errorMessage` into the input macro. Do not report a missing server-side path that the template cannot show.

## Not a GOV.UK service

### `fixtures/not-govuk/`

Open this folder as the project. `package.json` depends on React and not on `govuk-frontend`. `signup.html` does not use GOV.UK Frontend.

`/ucd signup.html` must say this is not a GOV.UK service and stop. No findings.

## Results

`/ucd` was not run in GitHub Copilot, Claude Code or Cursor. Those CLIs are not installed here. None of the rows below is a pass.

| Fixture | GitHub Copilot | Claude Code | Cursor |
|---|---|---|---|
| `components/select-for-country.njk` | Not run | Not run | Not run |
| `components/modal-and-tooltip.html` | Not run | Not run | Not run |
| `question-pages/name-and-email.njk` | Not run | Not run | Not run |
| `question-pages/radios-without-legend.html` | Not run | Not run | Not run |
| `validation/browser-only.njk` | Not run | Not run | Not run |
| `validation/please-enter.html` | Not run | Not run | Not run |
| `content/title-case.njk` | Not run | Not run | Not run |
| `content/jargon.html` | Not run | Not run | Not run |
| `accessibility/no-label.html` | Not run | Not run | Not run |
| `accessibility/div-button.html` | Not run | Not run | Not run |
| `journey/` | Not run | Not run | Not run |
| `clean/email.njk` | Not run | Not run | Not run |
| `not-govuk/signup.html` | Not run | Not run | Not run |

Install check, 27 November 2026, from this checkout with `gh skill install /workspace ucd --from-local --scope project --force`:

| Agent | Installed path | Eval fixtures in the installed folder |
|---|---|---|
| `github-copilot` | `.agents/skills/ucd/` | None. 22 files: `SKILL.md`, `report-template.md`, six checks, 14 standards files |
| `claude-code` | `.claude/skills/ucd/` | None. Same 22 files |
| `cursor` | `.agents/skills/ucd/` (shared with Copilot at project scope) | None. Same 22 files |

The source `skills/ucd/SKILL.md` did not gain install metadata. The installed copy did, which is what `gh skill install` does.
