# What needs a human

This pack lets a developer and a coding agent build pages that follow government design standards. It does not replace a design team. Some things can only be done by people, and a service cannot pass an assessment or go live without them.

Use this file to decide what to flag at the end of a task. Be specific about what is needed and why. Do not add every item to every summary: list the ones the change makes relevant.

## What you can do, and what you cannot

| You can | You cannot |
|---|---|
| Apply standard components and patterns correctly | Know whether this pattern works for these users |
| Write clear content in GOV.UK style | Know which words these users use, or check facts you were not given |
| Check code against WCAG rules that can be read from markup | Experience the page with a screen reader, voice control or magnification |
| Plan a journey from stated requirements | Find out what users need |
| Review a diff against checklists | Make a design decision that trades off user needs |
| Flag risks | Accept risks on behalf of the service |

## User research

**Why:** Point 1 of the Service Standard is to understand users and their needs. Standards tell you what usually works. Only research tells you what works for this service.

**Flag when:**

- you built a new journey or changed the order of an existing one
- you chose between two reasonable designs
- you built a custom component or a page no pattern covers
- you wrote content for a complicated or sensitive topic
- a request seemed to be based on an assumption about users

**Say:** "This has not been tested with users. A user researcher should test it, including with disabled users and people with low digital confidence."

## Accessibility testing

**Why:** Automated tools and code review find only some problems. Regulations require the service to meet WCAG 2.2 AA and publish an accessibility statement.

**Flag when:** any user-facing change is made. How much to say depends on the change.

| Change | What to ask for |
|---|---|
| A new page using only standard components | Manual keyboard and screen reader check before release |
| A custom component, or changed component markup | Testing with a range of assistive technology: screen readers on desktop and mobile, voice control and screen magnification |
| A new journey or a new service | A full accessibility audit by a specialist before public beta, plus research with disabled users |
| Anything that changes what is or is not accessible | An update to the accessibility statement |

The Service Manual lists which assistive technologies and browsers to test with: https://www.gov.uk/service-manual/technology/testing-with-assistive-technologies

## Content review

**Why:** Wrong content in a government service can cost someone money, a deadline or a legal right.

**Flag when:**

- you used a placeholder for a fact you did not have
- you wrote or changed anything about eligibility, deadlines, fees, penalties or legal obligations
- you touched a declaration, privacy notice or statutory wording
- you wrote emails, letters or text messages
- you named something users will see throughout the service

**Say who:** a content designer for clarity and style, a policy or legal colleague for accuracy.

## Translation

**Why:** Services for Wales, and some others, must be available in Welsh. Machine translation is not acceptable for a government service.

**Flag when:** you add or change any user-facing string in a service that has more than one language.

## Design decisions

**Why:** Some choices weigh one user need against another, or against cost and policy. Those belong to the team.

**Flag when:**

- the developer asked for something on the "avoid" list in `choose-a-component.md`
- you departed from a GOV.UK pattern
- the request conflicts with the project's existing conventions
- you had to guess what was wanted

## Privacy and data

**Why:** Collecting personal data has legal requirements you cannot assess.

**Flag when:**

- you add a new piece of personal data to collect or store
- you add or change cookies, analytics or third-party scripts
- you add special category data, such as health or ethnicity

**Say:** "This changes what personal data is collected. The data protection lead should check whether the privacy notice and data protection impact assessment need updating."

## Service assessment

**Why:** Services are assessed against the Service Standard at alpha, beta and live. Assessors look for evidence from research, testing and iteration.

**What helps the team:** keep a short record of the design decisions you made and why, in the pull request or wherever the project keeps design history. Do not claim the service meets the standard.

## How to write the flag

Put it under "Needs a human" in your summary. For each item give:

1. What needs doing
2. Why, in one line
3. Who usually does it

Example:

> **Needs a human**
> - Test the new "Add a dependant" loop with a screen reader. It uses the MoJ "Add another" component, which changes the page without a reload. An accessibility specialist or a developer with screen reader experience.
> - Confirm the processing time on the confirmation page. I used a placeholder. The policy team or product manager.
> - Welsh translation for 14 new strings in `locales/cy.json`. A Welsh translator.

## What not to do

- Do not say a page is accessible, compliant or assessment-ready.
- Do not say research supports a design unless you were given the research.
- Do not leave this section out because the change seems small.
- Do not bury flags in the middle of a long summary. Put them at the end under their own heading.
