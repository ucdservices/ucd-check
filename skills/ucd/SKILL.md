---
name: ucd
description: Check a UK government service front end against user-centred design standards. It looks at GOV.UK and MoJ components, question pages, validation, content style, WCAG 2.2 AA issues that can be read from code, and journey structure, then reports and waits before editing. Use when someone types /ucd, asks for a design review of a GOV.UK service, or reviews a pull request of service templates. Do not use it for general front-end work, marketing sites, or projects that are not UK government services.
license: MIT
---

# UCD Check

Check the code in scope against the standards in this skill. Report first. Do not change a file until the person asks you to.

The standards files are copies from UCD Context 1.0.0. Their sources and the Open Government Licence notice are in [ATTRIBUTION.md](standards/ATTRIBUTION.md). Read a file only when a step below tells you to.

## Scope the check

1. If the message names a path or a file after `/ucd`, check that.
2. Otherwise check the files in the current diff or pull request.
3. Otherwise check the open file.
4. If none of those is clear, ask one question: which files should be checked? Then stop until there is an answer.

## Detect the project

Read `package.json` and, if it is installed, `node_modules`.

- Note the installed `govuk-frontend` version and the version of `@ministryofjustice/frontend` if it is there. The version in `node_modules` is the one to judge markup against. A range in `package.json` is not a version.
- Note the template language from the files in scope: Nunjucks (`.njk`), plain HTML, or both.

If `govuk-frontend` is not a dependency and the files do not use GOV.UK Frontend classes or macros, say that this does not look like a GOV.UK service and stop. Do not run the checks.

## Choose the checks

From the files in scope, choose only the checks that apply. Read that check's file before you judge. Do not read the other check files.

| If the code... | Read |
|---|---|
| Renders a component, or styles one | [Components](checks/components.md) |
| Asks the user a question | [Question pages](checks/question-pages.md) |
| Submits a form or validates an answer | [Validation](checks/validation.md) |
| Contains words a user reads | [Content](checks/content.md) |
| Is a user-facing template, stylesheet or client script | [Accessibility](checks/accessibility.md) |
| Covers more than one step, check answers, or confirmation | [Journey](checks/journey.md) |

Each check file says when to skip it. Follow its links into `standards/` only for the rules you are applying. If a check file has no rule for something, do not invent one.

## Report

Fill in [the report template](report-template.md). List findings, most serious first. Do not edit files in this step.

## Offer fixes

Ask which findings to fix. You may group them so the person can say "all" or name a few.

Apply only the findings they approve. For each one, follow "The standard fix" in the check file and take markup from the installed package, not from an example.

Then run the affected checks again and report what changed, using the same template.

## Pull request mode

Use this when you are reviewing a pull request and there is nobody to ask. It is different from the steps above.

Post each finding as a review comment on the line, with the proposed fix as a suggested change. Do not edit files. Do not commit. Do not push.

## Priority rules

When two instructions disagree, use this order:

1. The project's own instructions and conventions.
2. The official GOV.UK, MoJ or W3C page, when it differs from a file in `standards/`.
3. The installed package, when a markup example differs from it.
4. The files in this skill.

If the person asks for something a check file warns against, do not apply it until they confirm. Record the conflict in the report. In pull request mode, comment and do not change the branch.

## Limits

UCD Check is independent and not endorsed by GDS, the MoJ or any government department. It does not make a service compliant.

It cannot do user research, test with assistive technology, or decide that content is accurate. It cannot pass a service assessment. Say what a person still has to check. Do not say a page is accessible, compliant or ready for assessment.
