# The Service Standard and what it means for your code

Government services are assessed against the 14-point Service Standard. You cannot pass an assessment for the team, but your code can make it easier or harder. This file lists each point and what you should do about it when you write code.

Official sources:

- Service Standard: https://www.gov.uk/service-manual/service-standard
- Service Manual: https://www.gov.uk/service-manual
- Government Design Principles: https://www.gov.uk/guidance/government-design-principles

## The 14 points

| # | Point | What you do in code |
|---|---|---|
| 1 | Understand users and their needs | Do not add features, fields or pages nobody asked for. If a request has no stated user need, ask what it is. Never invent research findings. |
| 2 | Solve a whole problem for users | Think about what happens before and after the page you are building: how the user arrives, and where they go next. Do not leave dead ends. |
| 3 | Provide a joined up experience across all channels | Give users a way to get help or finish the task offline. Do not remove contact details or alternative routes. Keep reference numbers and wording the same in pages, emails and letters. |
| 4 | Make the service simple to use | Use GOV.UK Design System components and patterns. One thing per page. Plain English. See the playbooks. |
| 5 | Make sure everyone can use the service | Meet WCAG 2.2 AA. Works without JavaScript, on small screens and on slow connections. See `accessibility-wcag-2.2-aa.md`. |
| 6 | Have a multidisciplinary team | You are standing in for some design roles, not replacing them. Flag decisions that need a designer, researcher or content designer. See `needs-a-human.md`. |
| 7 | Use agile ways of working | Make small changes that can be released and tested on their own. Do not bundle unrelated changes. |
| 8 | Iterate and improve frequently | Build so content and page order are easy to change: keep content out of logic, and keep routing in one place. |
| 9 | Create a secure service which protects users' privacy | Collect only the data needed. Do not put personal data in URLs, logs or analytics. Use POST for forms. Include CSRF protection. Follow the project's cookie consent approach. |
| 10 | Define what success looks like and publish performance data | Do not remove existing analytics or event hooks. If you add a journey, tell the developer where completion and drop-out could be measured. Only load analytics after consent. |
| 11 | Choose the right tools and technology | Use what the project already uses. Do not add a frontend framework or UI library on top of GOV.UK Frontend. |
| 12 | Make new source code open | Never commit secrets, keys or real personal data, including in fixtures and examples. Write code as if it will be public. |
| 13 | Use and contribute to open standards, common components and patterns | Use GOV.UK components first, then MoJ, then custom. Use platform services the project already has, such as GOV.UK Notify, Pay and One Login. Do not build your own versions of them. |
| 14 | Operate a reliable service | Build the error pages: page not found, problem with the service, and service unavailable. Handle timeouts and failed calls without losing the user's answers. |

## Government Design Principles to apply to every decision

- Start with user needs, not what is easiest to build.
- Do less. Reuse what exists.
- Do the hard work to make it simple. Complexity belongs in the code, not on the page.
- Be consistent, not uniform. Use the same patterns, but adapt when users need something different.
- This is for everyone. Design for the people who find services hardest to use.

## Service phases

Ask the developer which phase the service is in if it is not clear, because it changes what is expected.

| Phase | What it means for you |
|---|---|
| Discovery | No production code. You may be asked for throwaway prototypes only. |
| Alpha | Prototypes to test ideas. Speed matters more than code quality, but accessibility and content rules still apply to anything tested with users. |
| Private or public beta | Production code. Everything in this pack applies. A phase banner with a feedback link is shown. |
| Live | As beta, without the phase banner. Changes need the same care. |

## Pages every service needs

Check these exist before a service goes to beta. Tell the developer if any are missing.

- Start page (often on GOV.UK itself, not in the service)
- Cookies page and cookie banner, if non-essential cookies are used
- Accessibility statement
- Privacy notice
- Page not found
- There is a problem with the service
- Service unavailable
- A way to give feedback

See `govuk-patterns.md` for how to build them.
