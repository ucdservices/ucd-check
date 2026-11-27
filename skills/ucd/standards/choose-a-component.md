# Playbook: choose a component

Use this when you need to show something or collect something and are not sure what to use, or when you are tempted to build your own.

## The order of preference

Work down this list and stop at the first that fits.

1. **A GOV.UK pattern.** Check `govuk-patterns.md`. A pattern solves the whole problem, not only the widget.
2. **A GOV.UK component.** Check `govuk-components.md`.
3. **A component the project already has.** Search the codebase for existing custom components (often prefixed `app-`) before making another.
4. **A component from the department's own design system**, if the project uses one. Ask the developer which applies.
5. **An MoJ component or pattern.** Check `moj-components-and-patterns.md`.
6. **A combination of GOV.UK components and styles**, with no new CSS or JavaScript.
7. **A new custom component.** Only after the steps above, and only following the rules below.

## Decide by what the user needs to do

| The user needs to... | Use |
|---|---|
| Answer a question | A question page. See `build-a-form-page.md` for which input. |
| Review what they entered | Summary list, in the "Check answers" pattern |
| See progress through sections | Task list |
| Know a task is finished | Confirmation page with a panel |
| Know an action worked, then carry on | Notification banner (success), at the top of the next page |
| Fix a mistake | Error summary and error messages |
| Notice something important before acting | Warning text |
| Read an aside or example | Inset text |
| Get optional help | Details |
| Compare data | Table |
| See key facts about one thing | Summary list |
| Move through a list of results | Pagination |
| Find something in a long list | Search and filter (MoJ "Filter a list" pattern) |
| See the status of an item | Tag |
| Go back a step | Back link |
| Move between sections of a service | Service navigation |
| Confirm a destructive action | A separate confirmation page (MoJ "Confirm an action" pattern) |
| Add several of the same thing | MoJ "Add to a list" pattern |
| Upload files | File upload, or MoJ "Upload files" pattern for several |

## Things government services avoid

These are common in commercial products and almost always wrong here. If you are asked for one, build the alternative and explain why. If the developer still wants it, build it and flag the risk.

| Asked for | Use instead | Why |
|---|---|---|
| Modal or pop-up dialog | A separate page | Hard to make accessible. Breaks back button. Often missed. |
| Tooltip or info icon | Hint text or details | Does not work on touch or keyboard. Hidden content gets missed. |
| Carousel or slider | Show the content, or link to it | Users miss everything after the first item. |
| Multi-step wizard on one page | Separate pages | Breaks back button, saving and errors. |
| Progress bar or "Step 2 of 7" | Nothing, or a task list for long services | Often wrong when the journey branches. Research shows it rarely helps. |
| Dropdown for a few options | Radios | Selects are hard to use and hide the options. |
| Native date picker | Date input | Slow for known dates. Inconsistent across browsers. |
| Toggle switch | Radios or checkboxes | Unclear state. No standard component. |
| Inline validation as you type | Validation on submit | Interrupts users, especially with assistive technology. |
| Disabled button until the form is complete | An enabled button and error messages | Users cannot tell why it is disabled. |
| Placeholder text as label or hint | Label and hint text | Disappears on typing. Poor contrast. |
| Toast or snackbar message | Notification banner | Disappears before it is read. Missed by screen readers. |
| Infinite scroll | Pagination | Keyboard users cannot reach the footer. Position is lost. |
| Hamburger menu on desktop | Service navigation | Hides navigation. |
| Icon-only button | A button with text | Icons are ambiguous. |
| Auto-advancing focus between fields | Let the user tab | Disorients users and breaks correction. |
| CAPTCHA | Other spam controls, such as rate limiting or a honeypot | Blocks disabled users. Fails WCAG 3.3.8 when used for sign-in. |
| "Are you sure?" browser confirm | A confirmation page | Cannot be styled or made consistent. |

## If you must build a custom component

Only when no option above works. Tell the developer before you start.

1. **Write down the user need** it meets and why existing components do not.
2. **Check the community backlog.** Search the GOV.UK Design System's upcoming components and patterns, and other departments' design systems, for prior work: https://design-system.service.gov.uk/community/upcoming-components-patterns/
3. **Start from native HTML elements.** Add ARIA only where HTML cannot express it.
4. **Make it work without JavaScript first.**
5. **Name it with the project's prefix**, such as `app-`, and follow GOV.UK Frontend's naming style.
6. **Use GOV.UK Sass mixins and variables** for colour, type, spacing and focus.
7. **Support keyboard, zoom to 400%, 320 pixel width and forced colours mode.**
8. **Meet target size and focus visibility** from WCAG 2.2.
9. **Document it** in the project the way other components are documented.
10. **Flag it** in your summary as needing review by a designer, testing with assistive technology and testing with users. A custom component is the highest accessibility risk in the service.

## Checklist

- [ ] Patterns and components checked in order, and the first fit used
- [ ] Codebase searched for an existing custom component
- [ ] Nothing from the "avoid" table built without the developer's explicit choice
- [ ] Any custom component follows all 10 rules and is flagged for human review
