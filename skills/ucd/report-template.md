# Report template

Use this shape for every report. Keep the headings. Fill the parts in brackets. Delete the bracketed hints.

## Scope

[What was checked: paths, the diff, or the open file. Name the installed GOV.UK Frontend version and, if present, the MoJ Frontend version. Name the template language.]

## Checks run and checks skipped

[One line per check. For a check you ran, say "ran". For a check you skipped, say "skipped" and give a one-line reason.]

- Components: [ran, or skipped because ...]
- Question pages: [ran, or skipped because ...]
- Validation: [ran, or skipped because ...]
- Content: [ran, or skipped because ...]
- Accessibility: [ran, or skipped because ...]
- Journey: [ran, or skipped because ...]

## Findings

[Most serious first. If there are none, write "No findings." Do not pad the list.]

### [must fix | should fix | consider]: [short title]

- **File:** [path and line]
- **What is wrong:** [one or two sentences]
- **Standard:** [link to the file in standards/ that contains the rule]
- **Severity:** [must fix, should fix, or consider]
- **Proposed fix:** [what you would change. Do not apply it yet.]

Severity comes from [review before merge](standards/review-before-merge.md). Report a Blocker as `must fix`, Should fix as `should fix`, and Consider as `consider`.

## What still needs a human

[Only the items this change makes relevant. For each one, say what is needed, why, and who usually does it. Use [What needs a human](standards/needs-a-human.md).]

Include each of these that applies:

- User research
- Testing with assistive technology
- Content accuracy
- Service assessment

Do not say the service is accessible, compliant or ready for assessment.

## Next step

[Ask which findings to fix. In a pull request review where nobody can answer, say that the findings are posted as comments with suggested changes, and that nothing was committed.]

UCD Check is independent and not endorsed by GDS, the MoJ or any government department. It does not make a service compliant.
