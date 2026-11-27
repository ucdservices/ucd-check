# GOV.UK content style

Rules for every word a user reads: headings, labels, hints, buttons, links, error messages, emails and text messages. Apply them to new text and to any text you touch.

Official sources:

- Style guide A to Z: https://www.gov.uk/guidance/style-guide/a-to-z
- Content design guidance: https://www.gov.uk/guidance/content-design
- Writing for user interfaces: https://www.gov.uk/service-manual/design/writing-for-user-interfaces

## The basics

- **Plain English.** Write so a 9 year old could read the words, even when the subject is complicated.
- **Short sentences.** Aim for 25 words or fewer. One idea per sentence.
- **Active voice.** "We will send you a letter", not "A letter will be sent".
- **Address the user as "you"** and the organisation as "we".
- **Front-load.** Put the most important words at the start of headings, links and sentences.
- **Be direct.** Say what the user must do. "You must tell us if..." rather than "It is advisable to notify...".
- **Cut.** If a word or sentence does not help the user do the task, remove it.

## Capitals

- **Sentence case everywhere**: headings, buttons, labels, links, table headers, tags, navigation.
- Capital letters only for proper nouns: names of people, places, organisations and official names of things, such as "Universal Credit" or "Blue Badge".
- Lower case for "government", "minister", and job titles used generally.
- Never write in all capitals.

## Words

Use the simple word.

| Do not use | Use |
|---|---|
| assist, facilitate | help |
| commence | start |
| complete (a form) | fill in |
| in order to | to |
| obtain | get |
| prior to | before |
| provide | give |
| purchase | buy |
| require | need |
| submit | send, apply (or keep "submit" only for a final button) |
| terminate | end |
| utilise | use |
| e.g., i.e., etc. | for example, that is, and so on (or rewrite) |
| log in, login | sign in |
| click | select |
| please, sorry (in errors and instructions) | (leave out) |

Avoid: "deliver" (unless it is post), "drive", "leverage", "streamline", "robust", "key" (as an adjective), "going forward", "in terms of", "simply", "just", "easy". Do not tell users something is quick or easy.

Do not use Latin, jargon or internal team names for things. Use the words your users use.

Spell out an abbreviation the first time, with the short form in brackets, unless it is better known shortened, such as "UK", "MP" or "VAT". No full stops in abbreviations.

## Contractions

- Simple positive contractions are fine: "you'll", "we'll", "it's".
- Avoid negative contractions, which some users misread: write "cannot" and "do not" rather than "can't" and "don't".
- Avoid "should've", "could've", "would've", "they've".

## Numbers, dates and money

- Use numerals: "3 documents", "10 days". Write "one" as a word when it is part of a phrase, such as "one of the following".
- Thousands with a comma: "1,500". Millions as "£2.5 million".
- Ordinals: "first" to "ninth" in words, then "10th".
- Dates: "6 April 2026". No "th". No leading zero. Include the day of the week only if it helps: "Monday 6 April 2026".
- Date ranges: "6 to 10 April", using "to", not a dash.
- Times: "5:30pm", "9am". Use "midday" and "midnight", not "12pm" or "12am".
- Money: "£75", "£75.50", with no ".00". Use "p" for pence under £1: "50p".
- Percentages: "50%".
- Phone numbers: "0300 123 4567", in readable groups.
- Use "to" in ranges of numbers, not a dash: "aged 16 to 24".

## Punctuation and formatting

- No exclamation marks.
- No ampersands. Write "and", unless it is part of an official name.
- No semicolons. Split into 2 sentences.
- Avoid brackets for anything the user needs to know. Use them for abbreviations.
- Do not use bold for emphasis in body text. No italics. No underlining apart from links.
- Use single quotes when referring to interface text or titles in body content. Use double quotes for speech.
- No full stop at the end of headings, labels, button text, link text, list items or error messages.

## Headings

- Describe what the section is about in the user's words.
- Question pages use the question as the heading.
- Do not use questions as headings on content pages if a statement is shorter.
- No "Introduction", "Overview" or "Welcome" headings.

## Lists

Bulleted lists break up long sentences.

- Start with a lead-in line that ends in a colon.
- Each item completes the lead-in line and makes sense read with it.
- Start each item in lower case.
- No full stop, comma or "and" at the end of items.
- One sentence per item.

Use numbered lists for steps that happen in order. Each step is a full sentence with a capital letter and full stop.

## Links

- Link text describes where the link goes: "Check if you can get Child Benefit", not "click here" or "more information".
- Do not use the same link text for different places.
- Do not put links in the middle of instructions where they will take users away from the task.
- Do not write out URLs as link text.
- Say if a link opens a file, with its type and size.

## Buttons

- Start with a verb: "Continue", "Save and continue", "Send application", "Add another person".
- Sentence case. 1 to 3 words where possible.
- The same action uses the same words throughout the service.

## Labels, legends and hints

- Labels and legends say what to enter, as a question or a short noun phrase.
- Do not end labels with a colon.
- Mark optional fields with "(optional)" at the end of the label. Do not mark required fields. Do not use asterisks.
- Hints are short, with no full stop if they are a single phrase. Give the format or an example only where it helps.

## Error messages

See the templates in `govuk-components.md`. In short: say what happened and how to fix it, use the words from the question, and leave out "please", "sorry", "valid" and "invalid".

## Tone

- Calm, clear and respectful. Never chatty, clever or jokey.
- Do not thank users for routine steps. A confirmation page can say what was received.
- Do not apologise, except on a "problem with the service" page.
- Say "you must" for legal requirements, "you need to" or "you should" for the rest. Be consistent.
- Be honest about how long things take and what happens next.

## Inclusive language

- Write about people, not categories: "disabled people", "people with sight loss".
- Do not assume gender. Use "they". Do not ask for a title or gender unless the service needs it.
- Do not use "normal" to mean non-disabled. Do not use "suffering from".
- Avoid idioms and metaphors, which translate badly and confuse some users.

## Emails and text messages

- Subject lines say what the message is about and include the service name.
- Lead with what the user needs to do or know.
- Text messages: say who it is from at the start. Keep to one message length where possible. Never ask for personal or payment details. Avoid links in text messages unless the team has decided to use them.
- Include the reference number and how to get help.
- Use the project's GOV.UK Notify templates if it has them. Do not hard-code message text in application code.

## Welsh and other languages

- Do not machine-translate content into Welsh or any other language. Flag that translation is needed.
- Keep content in translation files if the project uses them, and add new strings in the same way.
- Set the `lang` attribute on any text in another language.

## Checklist

- [ ] Sentence case throughout
- [ ] Sentences under about 25 words, active voice, "you" and "we"
- [ ] No jargon, Latin abbreviations or words from the avoid list
- [ ] Numbers, dates, times and money in GOV.UK format
- [ ] Links and buttons describe what they do
- [ ] No "please" or "sorry" in instructions or errors
- [ ] No invented facts, rules, dates or contact details
- [ ] New strings added to translation files where the project uses them
