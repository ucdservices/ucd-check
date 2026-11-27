# MoJ Design System components and patterns

The Ministry of Justice (MoJ) Design System extends the GOV.UK Design System. It is strongest for staff-facing and caseworking services: screens with lists, filters, tables and actions that people use all day. It is widely used outside MoJ.

Official source: https://design-patterns.service.justice.gov.uk/

## When to use it

1. **GOV.UK first.** If a GOV.UK component does the job, use that.
2. **MoJ second.** Use an MoJ component when GOV.UK has nothing for the need.
3. **Only if it is installed, or the developer agrees to add it.** Check `package.json` for `@ministryofjustice/frontend`. Do not add the dependency without asking.

Before using any MoJ component:

- Open its page and check its status. MoJ labels building blocks by maturity, and some are experimental or archived. Tell the developer if you use one that is not marked as official.
- Check that the installed MoJ Frontend version supports the installed `govuk-frontend` major version. They are released separately and MoJ Frontend can lag behind a new GOV.UK major version.
- Take markup and macro names from `node_modules/@ministryofjustice/frontend/`, not from memory.
- Some MoJ components need their own JavaScript to be initialised. Check the component page.

## Components

Each page is at `https://design-patterns.service.justice.gov.uk/components/[name]/`.

### Finding and filtering

| Component | Use it for |
|---|---|
| Search | A search box with a button, for searching within a service. |
| Filter | A panel of filter controls for a list of results, with selected filters shown as removable tags. |
| Sortable table | A table whose columns can be sorted by the user. |
| Pagination | MoJ's variant for lists of results. Prefer the GOV.UK pagination component unless the project already uses this one. |
| Multi select | Selecting several rows in a table with checkboxes, to act on them together. |
| Scrollable pane | Letting a wide table scroll horizontally inside its container. Try simplifying the table first. |

### Navigating

| Component | Use it for |
|---|---|
| MOJ Header | A header for internal services that do not use GOV.UK branding. |
| Primary navigation | Top-level sections of an internal service. |
| Sub navigation | Sections within one area of a service, shown horizontally. |
| Side navigation | Sections within one area, shown vertically. Suits many links. |
| Organisation switcher | Switching between organisations or locations a member of staff works across. |
| Identity bar | Showing whose record a caseworker is looking at, with key details, on every page about that person. |
| Page header actions | A page heading with action buttons aligned next to it. |
| Button menu | Grouping several related actions under one button. |

### Showing status and information

| Component | Use it for |
|---|---|
| Alert | Telling the user about something on the page: information, success, warning or error. |
| Badge | A short label drawing attention to a status, stronger than a GOV.UK tag. Use sparingly. |
| Notification badge | A count of items needing attention, usually in navigation. |
| Card | A summary of an item that links to more detail. |
| Numeric data | Showing key figures clearly. |
| Ticket Panel | Grouping information and actions for one item. |
| Timeline | A history of events on a case, newest first. |
| Messages | A conversation thread between people. |
| Progress tracker | Showing how far a case or application has got through set stages. |
| Contextual date | Showing a date together with how long ago or how far away it is. |
| Inset text (highlighted) | A stronger variant of inset text. |
| Spinner progress indicator | Showing that something is loading. Only when a wait cannot be avoided, and with text for screen readers. |

### Banners and interruptions

| Component | Use it for |
|---|---|
| Feedback banner | Asking users for feedback on a service or feature. |
| New features banner | Telling returning users about something new. |
| Outage banner | Warning of planned or current disruption. |
| Interruption card | Stopping the user to make them read something before continuing. Rare. |
| Modal dialog | Content that must be dealt with before returning to the page. Avoid if a normal page would work: dialogs are hard to make accessible. |
| Timeout warning | Warning that a session is about to end and letting the user extend it. Use this to meet WCAG 2.2.1. |
| API error | Showing that part of a page could not load data. |

### Entering information

| Component | Use it for |
|---|---|
| Date picker | Choosing a date from a calendar, when users need to see days of the week or pick a date they do not already know. Users can still type the date. Do not use for memorable dates such as date of birth: use the GOV.UK date input. |
| Calendar | Showing dates in a calendar view. |
| Add another | Letting users add more of the same set of fields on one page. Consider the "Add to a list" pattern instead, which works better for most users. |
| Multi file upload | Uploading several files at once with progress. Follow the "Upload files" pattern. |
| Copy button | Copying a piece of text, such as a reference number, to the clipboard. |

## Patterns

Each page is at `https://design-patterns.service.justice.gov.uk/patterns/[name]/`.

| Pattern | Use it for |
|---|---|
| Add to a list | Collecting several of the same thing, such as people or addresses, one at a time across pages, with a summary where users can change or remove them. Prefer this over long repeating forms. |
| Confirm an action | Asking the user to confirm before something that cannot easily be undone, such as deleting a record. Use a separate page, not a browser dialog. |
| Electronic signature | Asking a user to sign or declare something online. |
| Filter a list | Combining search, filter and results so users can narrow down a long list. Filters apply with a button and work without JavaScript. |
| Get help | Giving users a consistent way to find help throughout a service. |
| Upload files | Asking for one or more files, showing what has been uploaded, and letting users remove files. |

## Designing staff-facing screens

Caseworking screens have different needs from public ones, but the same standards apply.

- WCAG 2.2 AA applies fully. Staff include disabled people, and internal tools are covered by the regulations.
- You can show more on one page than in a public service, because users are trained and repeat the task. Still group it clearly with headings.
- Small radios, small checkboxes and denser tables are acceptable in information-dense, frequently used screens.
- Keep the same content rules: plain English, sentence case, no internal jargon unless every user knows it.
- Destructive actions use a warning button and a "Confirm an action" page.
- Still validate on the server, and still use the error summary and error messages.

## Checklist

- [ ] No GOV.UK component could do this job
- [ ] `@ministryofjustice/frontend` is installed, or the developer agreed to add it
- [ ] Component status checked on its page, and flagged if not official
- [ ] Markup taken from the installed version
- [ ] Any JavaScript the component needs is initialised, and the page still works without it
