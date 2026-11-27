# Components

GOV.UK components first, then MoJ, then custom. Markup must match the installed GOV.UK Frontend version.

## When this check applies

Run this check when the files in scope render interface elements: templates, partials, components, or CSS that styles them. Skip it for work with no user-facing interface, such as a migration or an internal API, and say why.

## What to look for

Read [choose a component](../standards/choose-a-component.md) and stop at the first option that fits. Then check the markup against the installed package.

- The order is: a GOV.UK pattern, a GOV.UK component, a component the project already has, the department's own design system if the project uses one, an MoJ component or pattern, a combination of GOV.UK components with no new CSS or JavaScript, and only then a custom component. See [The order of preference](../standards/choose-a-component.md).
- If a GOV.UK component does the job, do not use an MoJ one. Use MoJ only when GOV.UK has nothing for the need, and only if `@ministryofjustice/frontend` is installed or the developer agrees to add it. See [When to use it](../standards/moj-components-and-patterns.md).
- Take Nunjucks macros, option names, classes and HTML from the installed `govuk-frontend` (and from the installed MoJ package if one is used). Do not mix a different major version. See [How to use a component](../standards/govuk-components.md) and [Check the version first](../standards/govuk-design-system-foundations.md).
- With Nunjucks, call the macro. Do not hand-write HTML that a macro can produce. With plain HTML, keep every class, attribute and visually hidden element from the installed version. See [How to use a component](../standards/govuk-components.md).
- Do not restyle a component, override `govuk-` or `moj-` classes, or remove ARIA, visually hidden text or `data-module` attributes. See [How to use a component](../standards/govuk-components.md) and [Writing your own CSS](../standards/govuk-design-system-foundations.md).
- Match the component to the job in [Asking for information](../standards/govuk-components.md), [Navigation](../standards/govuk-components.md), [Showing information](../standards/govuk-components.md) and [Decide by what the user needs to do](../standards/choose-a-component.md). In particular: radios for one choice from a short list, checkboxes for one or more, select only as a last resort in a public service, no `type="number"`, no placeholder text, no pre-selected radio or checkbox, no disabled button, no icon-only button.
- Do not build anything in the avoid list in [Things government services avoid](../standards/choose-a-component.md): modal or pop-up, tooltip, carousel, multi-step wizard on one page, progress bar, dropdown for a few options, native date picker, toggle, inline validation as you type, disabled button until the form is complete, placeholder as label or hint, toast, infinite scroll, hamburger menu on desktop, icon-only button, auto-advancing focus, CAPTCHA, or a browser "Are you sure?" confirm.
- A custom component is allowed only after that list is exhausted, and it must follow [If you must build a custom component](../standards/choose-a-component.md). Flag it.
- MoJ components that are not marked official on their page must be flagged. Date picker is not for memorable dates such as date of birth. Modal dialogs are a last resort. See [MoJ components and patterns](../standards/moj-components-and-patterns.md).
- Pages extend the project's layout, which provides the skip link, header and footer. Do not rebuild those by hand. See [Page template](../standards/govuk-design-system-foundations.md).

## How to judge severity

Use the ratings in [review before merge](../standards/review-before-merge.md). Report them with the words this skill uses:

- **must fix** — the playbook's Blocker. It stops some users completing the task, or breaks a legal requirement. Examples for this check: a control with no accessible name, a keyboard trap, a component that cannot be used without a mouse, markup so changed that the GOV.UK focus style or name is gone.
- **should fix** — harder to use or inconsistent with the Design System. Examples: a select where radios fit, a disabled submit button, a modal or tooltip, placeholder text, markup from the wrong major version, a custom element where a GOV.UK component exists.
- **consider** — an improvement that needs a design decision. Example: a custom component that follows the custom-component rules but has not been reviewed.

## The standard fix

Replace the element with the first fitting GOV.UK pattern or component. If the project uses Nunjucks, use the macro from the installed package and check the option names in `node_modules`. If it uses plain HTML, copy the HTML for that installed version and keep every class and visually hidden element. Do not invent markup. For an MoJ component, take the macro and HTML from the installed `@ministryofjustice/frontend` package. Delete overrides of `govuk-` and `moj-` classes. If the result is still custom, record why nothing in the order of preference fitted.

## What a human still has to do

A custom component, changed component markup, or a page no pattern covers needs a designer and testing with assistive technology and with users. See [What needs a human](../standards/needs-a-human.md) and [If you must build a custom component](../standards/choose-a-component.md). Say what you checked. Do not say the component is accessible or compliant.
