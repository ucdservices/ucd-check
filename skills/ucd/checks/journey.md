# Journey

Check answers and confirmation pages, and the structure of the journey.

## When this check applies

Run this check when the scope covers more than one step: several templates, a router, a task list, check answers, or a confirmation page. Skip it for a single question page with no routing and no check-answers or confirmation code, and say why.

## What to look for

Use [design a journey](../standards/design-a-journey.md), [Patterns that cover a whole journey](../standards/govuk-patterns.md) and [Pages](../standards/govuk-patterns.md).

- A typical service runs: start page, filter questions, one thing per page, check answers, a declaration if one is needed, then a confirmation page plus an email or text message. A longer service wraps the questions in a task list. See [Patterns that cover a whole journey](../standards/govuk-patterns.md) and [Step 4: choose the shape of the journey](../standards/design-a-journey.md).
- Check answers shows every answer in summary lists with "Change" links. Each link returns to the question, pre-filled, then back to check answers. The button says what happens, such as "Accept and send". Each "Change" link has visually hidden text naming the row. See [Help users to...](../standards/govuk-patterns.md) and [Showing information](../standards/govuk-components.md).
- The confirmation page uses the panel component for the confirmation, with a reference number, then what happens next and when. Do not use the panel anywhere else. Also send the reference by email or text message. See [Pages](../standards/govuk-patterns.md) and [Step 7](../standards/design-a-journey.md).
- Back, next and change routes exist for each branch. Back follows the page the user came from, including skipped pages. Opening a page out of order redirects to the first unanswered page. Changing an earlier answer removes answers it makes irrelevant. See [Step 6: define routing](../standards/design-a-journey.md).
- Do not ask for the same information twice. Eligibility questions come first, with a page that explains why someone cannot continue and what to do instead. See [Step 3](../standards/design-a-journey.md) and [Redundant entry](../standards/accessibility-wcag-2.2-aa.md).
- URL paths are lower case words with hyphens and describe the page. No personal data in the URL. See [Step 5: map every page](../standards/design-a-journey.md) and point 9 of [The 14 points](../standards/govuk-service-standard.md).
- Answers are kept on back, on error and across the session. A timeout warns the user and lets them extend it. The final submit cannot run twice. See [Step 7](../standards/design-a-journey.md).
- There is a way forward on every page. Contact details stay in the same place. Error pages exist for page not found, problem with the service, and service unavailable, using the titles in [Pages](../standards/govuk-patterns.md). See [6. Journey](../standards/review-before-merge.md) and [Pages every service needs](../standards/govuk-service-standard.md).
- Do not add a progress bar or "Step 2 of 7". A task list is the pattern when sections can be done in any order. See [Things government services avoid](../standards/choose-a-component.md).

## How to judge severity

Use the ratings in [review before merge](../standards/review-before-merge.md). Report them with the words this skill uses:

- **must fix** — the playbook's Blocker. Examples: a journey that submits with no way to check answers, a dead end, answers lost on back or on error, personal data in the URL.
- **should fix** — harder to use or inconsistent. Examples: a confirmation with no reference number and no "what happens next", "Change" links with no visually hidden text, a skipped page whose back link is wrong, no exit page for someone who is not eligible.
- **consider** — a design choice. Examples: whether this service should be a task list or a linear journey, or whether a declaration is required. Ask, and do not invent the shape.

## The standard fix

Add the missing check-answers or confirmation page from [GOV.UK patterns](../standards/govuk-patterns.md), using the summary list and panel from the installed package. Point "Change" at the question and back to check answers, with visually hidden text. Store the posted answer and redirect. Remove personal data from paths. Do not build a new journey shape without a recorded decision.

## What a human still has to do

A new or reordered journey needs user research, including with disabled users and people with low digital confidence. What the user gets at the end, and who is not eligible, must come from the team. See [User research](../standards/needs-a-human.md) and [Service assessment](../standards/needs-a-human.md). Do not say the journey passes a service assessment.
