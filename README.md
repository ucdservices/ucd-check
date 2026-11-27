# UCD Check

Type `/ucd`. Check your GOV.UK service against the standards a design team works to.

## What it does

- Decides which of the six checks apply to the code you point it at.
- Reports what it finds against the bundled standard, most serious first.
- Offers fixes and waits for approval before it changes a file.

## Install

`gh skill` is in public preview. It needs GitHub CLI 2.90.0 or later. You need permission to read this repository.

The commands below install the `ucd` skill. Checked against `gh skill install --help` on 27 November 2026. Folder paths are in [docs/platform-notes.md](docs/platform-notes.md).

### GitHub Copilot

Install for the current project. This writes `.agents/skills/ucd/`, which Copilot reads.

```bash
gh skill install ucdservices/ucd-check ucd --agent github-copilot --scope project
```

Install for every project on your machine. This writes `~/.copilot/skills/ucd/`.

```bash
gh skill install ucdservices/ucd-check ucd --agent github-copilot --scope user
```

Or copy the folder yourself:

- Project: `.github/skills/ucd/`, `.agents/skills/ucd/` or `.claude/skills/ucd/`
- Personal: `~/.copilot/skills/ucd/` or `~/.agents/skills/ucd/`

Copilot code review reads skills from the pull request's head branch. The review docs name `.github/skills/` in particular, and they are more likely to pick a skill whose folder is named `code-review`. This skill stays `ucd`. For a review on GitHub, copy it to `.github/skills/ucd/` in the repository. The description tells Copilot it applies to service templates.

In VS Code chat, type `/ucd`. In Copilot CLI, ask it to use the `/ucd` skill, or type `/ucd` with the path.

### Claude Code

Install for the current project. This writes `.claude/skills/ucd/`.

```bash
gh skill install ucdservices/ucd-check ucd --agent claude-code --scope project
```

Install for every project on your machine. This writes `~/.claude/skills/ucd/`.

```bash
gh skill install ucdservices/ucd-check ucd --agent claude-code --scope user
```

Or copy `skills/ucd/` to `.claude/skills/ucd/` or `~/.claude/skills/ucd/`. Type `/ucd`.

### Cursor

Install for the current project. This writes `.agents/skills/ucd/`.

```bash
gh skill install ucdservices/ucd-check ucd --agent cursor --scope project
```

Install for every project on your machine. This writes `~/.cursor/skills/ucd/`.

```bash
gh skill install ucdservices/ucd-check ucd --agent cursor --scope user
```

Or copy `skills/ucd/` to `.agents/skills/ucd/`, `.cursor/skills/ucd/`, `~/.agents/skills/ucd/` or `~/.cursor/skills/ucd/`. Type `/` and choose `ucd`.

## Use

Check the files the tool already has in front of it: the diff, the pull request, or the open file.

```text
/ucd
```

Check a path.

```text
/ucd path/to/file
```

In a pull request review, where there is nobody to ask, UCD Check posts findings as review comments with suggested changes. It does not edit files and it does not commit.

Anywhere else, it reports first and changes a file only after you say which findings to fix.

## The six checks

| File | Check |
|---|---|
| `skills/ucd/checks/components.md` | GOV.UK components first, then MoJ, then custom; markup matches the installed GOV.UK Frontend version |
| `skills/ucd/checks/question-pages.md` | One question per page; labels, hints, legends and fieldsets |
| `skills/ucd/checks/validation.md` | Error summary, error messages, server-side validation |
| `skills/ucd/checks/content.md` | Plain English, sentence case, GOV.UK content style |
| `skills/ucd/checks/accessibility.md` | WCAG 2.2 AA issues that can be found by reading code |
| `skills/ucd/checks/journey.md` | Check-answers and confirmation pages; journey structure |

## Example report

From `evals/fixtures/validation/browser-only.njk`, in a project that has GOV.UK Frontend installed.

### Scope

`evals/fixtures/validation/browser-only.njk`. Template language: Nunjucks. GOV.UK Frontend is installed in the project.

### Checks run and checks skipped

- Components: ran. The input and the button are GOV.UK Frontend macros.
- Question pages: ran.
- Validation: ran.
- Content: ran.
- Accessibility: ran.
- Journey: skipped. One question page, with no check-answers or confirmation code.

### Findings

#### must fix: validation runs in the browser

- **File:** `evals/fixtures/validation/browser-only.njk`, lines 18 and 34
- **What is wrong:** The form relies on the `required` attribute and a submit script. There is no error summary.
- **Standard:** [build a form page](skills/ucd/standards/build-a-form-page.md)
- **Severity:** must fix
- **Proposed fix:** Validate on the server, re-render with an error summary titled "There is a problem", and show the same message next to the field.

#### should fix: the message does not follow the template

- **File:** `evals/fixtures/validation/browser-only.njk`, line 38
- **What is wrong:** The script sets "Please enter a valid value".
- **Standard:** [GOV.UK components](skills/ucd/standards/govuk-components.md)
- **Severity:** should fix
- **Proposed fix:** Use "Enter your email address" when the field is empty, with no "please" and no "valid".

#### should fix: the form does not turn off browser validation

- **File:** `evals/fixtures/validation/browser-only.njk`, line 18
- **What is wrong:** The form has no `novalidate`, so the browser validates the field itself.
- **Standard:** [build a form page](skills/ucd/standards/build-a-form-page.md)
- **Severity:** should fix
- **Proposed fix:** Add `novalidate` to the form and keep the check on the server.

### What still needs a human

- Content accuracy: a content designer should confirm the error wording.
- Testing with assistive technology: a person should confirm focus moves to the error summary.
- Service assessment: this check does not pass one.

### Next step

Say which findings to fix.

UCD Check is independent and not endorsed by GDS, the MoJ or any government department. It does not make a service compliant.

## What it does not do

UCD Check does not do user research, test with assistive technology, or decide that content is accurate. It does not make a service compliant, accessible or able to pass a service assessment.

UCD Check is independent and not endorsed by GDS, the MoJ or any government department. It does not make a service compliant.

## Standards and versions

The versions and the list of copied files are in [VERSIONS.md](VERSIONS.md).

## Update

Update skills that were installed with `gh skill`.

```bash
gh skill update ucd
```

Update every installed skill:

```bash
gh skill update --all
```

If you copied the folder by hand, copy `skills/ucd/` over the installed folder again. `gh skill update` skips a copy that has no GitHub metadata in the frontmatter.

## Related

- [UCD Context](https://ucdcontext.com) gives an agent the standards while it builds. UCD Check verifies what was built. They are separate products.
- [AI Force](https://aiforce.supply)

## Licence and attribution

The skill instructions and the other files written for UCD Check are MIT, © 2026 Vijay Kandhalu. See [LICENSE](LICENSE).

The bundled standards summarise public sector information and WCAG. That text stays under the licences recorded in [ATTRIBUTION.md](ATTRIBUTION.md), including the Open Government Licence v3.0.

## Credit

Made by [Vijay Kandhalu](https://www.vijay.ai)
