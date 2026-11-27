# Content

Plain English, sentence case, and GOV.UK content style.

## When this check applies

Run this check when the files in scope contain words a user reads: headings, labels, hints, buttons, links, error messages, emails or text messages. Skip it for code with no user-facing text, and say why.

## What to look for

Follow [GOV.UK content style](../standards/govuk-content-style.md) and [write page content](../standards/write-page-content.md). Do not judge whether a fact is true. Flag text that was invented.

- Plain English, sentences of about 25 words or fewer, one idea per sentence, active voice, "you" and "we". Put the important words first. See [The basics](../standards/govuk-content-style.md).
- Sentence case for headings, buttons, labels, links, table headers, tags and navigation. No all-capitals text. No full stop on headings, labels, button text, link text, list items or error messages. See [Capitals](../standards/govuk-content-style.md) and [Punctuation and formatting](../standards/govuk-content-style.md).
- Use the simple word in the table in [Words](../standards/govuk-content-style.md). Do not use the words that page says to avoid, Latin abbreviations, or internal team names. Spell out an abbreviation the first time unless it is better known short, such as UK, MP or VAT.
- "cannot" and "do not", not "can't" and "don't". See [Contractions](../standards/govuk-content-style.md).
- Numbers, dates, times and money follow [Numbers, dates and money](../standards/govuk-content-style.md): "6 April 2026", "5:30pm", "£75", "50%".
- No exclamation marks, no ampersands in place of "and", no semicolons, no italics, no underlining except links, no bold for emphasis in body text. See [Punctuation and formatting](../standards/govuk-content-style.md).
- Headings say what the section is about in the user's words. Question pages use the question. No "Introduction", "Overview" or "Welcome". See [Headings](../standards/govuk-content-style.md).
- Link text says where the link goes. Not "click here" or "more information". Buttons start with a verb, in sentence case. The same action uses the same words. See [Links](../standards/govuk-content-style.md) and [Buttons](../standards/govuk-content-style.md).
- Do not use "please" or "sorry" in instructions or error messages. Do not thank users for routine steps. Do not apologise except on a "problem with the service" page. See [Words](../standards/govuk-content-style.md) and [Tone](../standards/govuk-content-style.md).
- Do not invent eligibility, fees, dates, legal wording or contact details. If a fact is missing, use a visible placeholder such as `[CONTENT NEEDED: processing time]` and list it. Do not rewrite legal or statutory text. Do not machine-translate. See [Step 2: find the facts](../standards/write-page-content.md) and [Welsh and other languages](../standards/govuk-content-style.md).
- Use the same name for the same thing on every page, and in emails. Do not show internal field names. See [Step 3: write it](../standards/write-page-content.md).
- Inclusive language follows [Inclusive language](../standards/govuk-content-style.md): "disabled people", "they", no "suffering from", no title or gender unless the service needs it.

## How to judge severity

Use the ratings in [review before merge](../standards/review-before-merge.md). Report them with the words this skill uses:

- **must fix** — the playbook's Blocker. Examples: invented eligibility, a fee, a deadline or legal wording presented as fact; text the user must act on that is only in an image.
- **should fix** — harder to use or inconsistent. Examples: title case headings, "Please enter a valid value", "click here", jargon from the avoid list, a date or amount in the wrong format.
- **consider** — a shorter sentence or a plainer word where the meaning is already clear. Say so, and do not treat house style as a blocker.

## The standard fix

Rewrite the string in place using the style guide: sentence case, the simple word, active voice, and the button or link pattern. Replace a missing fact with a `[CONTENT NEEDED: ...]` placeholder and list it in the report. Leave statutory text unchanged and flag it. Put new strings where the project already keeps content, such as locale files.

## What a human still has to do

A content designer checks clarity. The policy or legal owner checks accuracy of eligibility, fees, deadlines and declarations. Welsh or other languages need a translator, not a machine. See [Content review](../standards/needs-a-human.md) and [Translation](../standards/needs-a-human.md). Do not say the content is correct or that the service is compliant.
