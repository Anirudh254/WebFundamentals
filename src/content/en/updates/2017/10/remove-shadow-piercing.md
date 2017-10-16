project_path: /web/_project.yaml
book_path: /web/updates/_book.yaml
description: Say goodbye to shadow-piercing CSS selectors.

{# wf_updated_on: 2017-10-16 #}
{# wf_published_on: 2017-10-16 #}
{# wf_tags: javascript #}
{# wf_featured_image: /web/updates/images/2017/10/intl-pluralrules.png #}
{# wf_featured_snippet: Say goodbye to shadow-piercing CSS selectors. #}
{# wf_blink_components: Blink>DOM #}

# Removing ::shadow and /deep/ in Chrome 63 {: .page-title }

{% include "web/_shared/contributors/robdodson.html" %}

Starting in Chrome 63, the shadow-piercing selectors `::shadow` and `/deep/`
will no longer be able to style content inside of a shadow root.

- The `/deep/` combinator will act as a descendant selector. `x-foo /deep/ div`
will work like `x-foo div`.
- The `::shadow` pseudo-element will not match any elements.

Note: If your site uses Polymer, the team has put together [a thorough guide](link tbd)
walking through steps to migrate off of `::shadow` and `/deep/`.

## The decision to remove

The `::shadow` and `/deep/` selectors have been deprecated in Chrome since
version 45. This was decided by all of the participants at the [April 2015
Web Components meetup](https://www.w3.org/wiki/Webapps/WebComponentsApril2015Meeting).

The primary concern with shadow-piercing selectors is that they violate
encapsulation and create situations where a component can no longer change its
internal implementation.

Note: For the moment, `::shadow` and `/deep/` will continue to work with
JavaScript APIs like `querySelector()` and `querySelectorAll()`. Ongoing support
for these APIs is being [discussed on
GitHub](https://github.com/w3c/webcomponents/issues/78).

The [CSS Shadow Parts](https://tabatkins.github.io/specs/css-shadow-parts/) spec
is being advanced as an alternative to shadow piercing selectors. Shadow Parts
will allow a component author to expose named elements in a way that preserves
encapsulation and still allows page authors the ability to style multiple
properties at once.

## What should I do if my site uses ::shadow and /deep/?

The `::shadow` and `/deep/` selectors only affect legacy Shadow DOM v0
components. If you're using Shadow DOM v1 you should not need to change anything
on your site.

You can use [Chrome Canary](https://www.google.com/chrome/browser/canary.html)
to verify your site does not break with these new changes. If you do notice
issues, see if you can remove any usage of `::shadow` and `/deep/`. If not
relying on these selectors is too onerous, you may also consider switching from
native shadow DOM over to the shady DOM polyfill. You should only need to make
this change if your site relies on native shadow DOM v0.

{% include "comment-widget.html" %}