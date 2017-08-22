# Kottans Front End 2017 &mdash; test assignment

Hello and welcome to the next step of our selection process.
The goal is to determine if we are a good match.

## Flow

*mini [GitHub API](https://developer.github.com/v3/) client*

**First screen**: owner (organization or user) name input and submit button.

**On submit**: show [cards](#cards) with repositories, [filters](#filters), and [sorting](#sorting).

> Only public repos of the owner are shown.
> Please, do not waste your time on auth.

**Pagination**: render "Load more" button at the bottom.

**On card click**: [dialog](#dialog) with repo details is shown.

### Cards

Pretty much resembles GitHub's [repositories tab](https://github.com/shvaikalesh?tab=repositories):

* repo name
* description
* forked from
* stars count
* updated date
* language

### Filters

Multiple filters can be selected at the same time: they are applied in conjunction (`&&`).
All filters should be implemented on the client, without using [`type` parameter](https://developer.github.com/v3/repos/#list-user-repositories).

* has open issues
* has topics
* starred >= *X* times
* updated after *X* date
* type (`all`, `forks`, or `sources`)
* language

> Language options should be determined using downloaded dataset.
> They should stay in sync when new repos are fetched.
> Do not hardcode them.

### Sorting

Order: ascending or descending. Only one of the following can be selected.
Sorting should be implemented on the client, without using [`sort` parameter](https://developer.github.com/v3/repos/#list-user-repositories).

* repo name
* open issues count
* stars count
* updated date

### Dialog

* contributors table (username | contributions) of the most active (top <= 3) contributors, with profile links
* languages table (language | Kb) of the most used languages (more than 1Kb)
* list of the most popular (top <= 5, only currently open) PRs, with links

## Bonus points

The list below is quite extensive: we want to give you space to show your motivation and current skill level.
Also, sections below will make reviewing process more transparent.

### User experience

* long repo descriptions are nicely trimmed
* progress indicator (for slow connections)
* network failures are handled in user-friendly way
* date can be entered in user-preferred locale or with datepicker
* relative date (updated) formatting
* stars count is nicely rounded (5627 => 5.6k)
* repos' languages are hidden if filter by language is active

### Accessibility

* color contrast ratio is acceptable
* owner name input is accessible with screen reader
* submit button is pressed with "Enter" key
* progress indicator is accessible with screen reader
* when tabbing, focus order is sensible
* dialog is accessible with keyboard and screen reader
* pie chart is read by screen reader
* icons are read by screen reader

### Router

URL should precisely reflect application state:

1. owner was selected

`/kottans`

2. sorting was enabled

`/kottans?sort=updated`

3. sorting order was reversed

`/kottans?sort=updated&order=desc`

4. filter was applied

`/kottans?sort=updated&order=desc&has_open_issues`

5. another filter was applied

`/kottans?sort=updated&order=desc&has_open_issues&starred_gt=200`

6. scrolled to the next page

`/kottans?sort=updated&order=desc&has_open_issues&starred_gt=200&page=2`

Other considerations:

* application state is restored after reloading
* history navigation is sensible
* [History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API) is used

### Performance

* total app size (HTML+CSS+JS) <= 14Kb
* when getting top <= *X*, use [query parameter](https://developer.github.com/v3/#pagination) to limit payload
* PWA, high [Lighthouse](https://developers.google.com/web/tools/lighthouse/) scores

### Code

* modern HTML/CSS (semantic markup, flex/grid, w/o framework)
* ES6, new browser APIs
* no direct DOM manipulation
* data access layer for GitHub API

### Tests

End-to-end and (or) unit tests is a huge :+1:. GitHub API imposes [rate limiting](https://developer.github.com/v3/#rate-limiting) (60 rph), so make sure you cache requests (for example, with service worker). [Headless Chrome](https://developers.google.com/web/updates/2017/04/headless-chrome) is the best option for running integration tests.

### Other

Not less important improvements, just uncategorized.

* `master` is automatically rebuilt on every commit to `source`
* neat commits: small, targeted, with good messages
* the app is served over `https://`
* infinite scroll
* languages table is replaced with pie chart
* fancy UI

## Browser support

Apps will be tested only in latest stable Google Chrome with default feature flags.
While it is not the way web apps should be shipped, we would like to see how good you are with new APIs.
Surely you can include couple shims if you are up to.

## Deployment

We expect to receive at least 250 submissions.
Our resources are quite limited, and reviewing tasks is extremely boring.
With that said, we **will ignore** submissions that do not satisfy the following requirements:

* `source` should contain source code of the app
* `source` should be [default branch](https://help.github.com/articles/setting-the-default-branch/)
* `master` should contain built app
* `master` should be hosted with [GitHub Pages](https://pages.github.com/)
* `README.md` should include a link to hosted app (somewhere at the top)

## Deadline

You have 14 days after you receive this task.
We **will ignore** submissions that have major code changes after the deadline.

Have fun and learn something new!