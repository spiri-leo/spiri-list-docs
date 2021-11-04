## How to create our filters

1. How to create our filters
   - [The comment](#the-comment)
   - [Block the domain](#block-the-domain)
     - [Block the domain only one protocol](#block-the-domain-only-one-protocol)
   - [Modifiers](#modifiers)
   - [Basic modifiers](#basic-modifiers)
   - [Generic modifiers](#generic-modifiers)
   - [Advanced modifiers](#advanced-modifiers)
   - [Unblock the domain](#unblock-the-domain)
   - [CSS element blocking](#css-element-blocking)
     - [CSS selectors](#css-selectors)

## Note

This documentation page helps to support the function or not, more information on [AdGuard](https://kb.adguard.com/en/general/how-to-create-your-own-ad-filters). If you need Russian, go to this [page](https://kb.adguard.com/ru/general/how-to-create-your-own-ad-filters)

## The comment

```
! The comment!
```

* Supports more adblockers

## Block the domain

```
||example.org^
```

* Supports more adblockers

### Block the domain only one protocol

```
|http://example.org/
```

* Supports more adblockers

## Modifiers

Example:

```
||example.org^$script
```

for another try:

```
||example.org^$script,third-party
```

* Supports more adblockers

## Basic modifiers

### `$domain`

This modifier can block the `baddomain.com` but blocking the domain only on domains.

Example:

```
||baddomain.com^$domain=example.com
```

for another try:

```
||baddomain.com^$domain=example.com|example.org
```

to block this domain on all domains, use `~` (is generic)

```
||baddomain.com^$domain=~example.com
```

or if you need another domains

```
||baddomain.com^$domain=~example.com|example.org
```

* Supports more adblockers

### `$third-party`

Note: On uBlock Origin, you can add `$3p` modifier, this modifier is unlikely to work in other ad blockers. But uBlock Origin will be able to support `$third-party` modifier.

This modifier can block third-party requests.

```
||example.com^$third-party
```

* Supports more adblockers

### `$popup`

This modifier can block and close popups.

```
||example.com^$popup
```

* Supports more adblockers

### `$match-case`

Defines a rule that applies only to addresses with matching case. By default, it is not case sensitive.

Example:

```
*/BannerAd.gif$match-case
```

This code blocks `example.com/BannerAd.gif` not a `example.com/bannerad.gif`

* Supports only AdGuard

### `$image`

This modifier can block images.

Example:

```
||example.com^$image
```

* Supports more adblockers

### `$stylesheet`

This modifier can block CSS styles.

Example:

```
||example.com^$stylesheet
```

* Supports more adblockers

### `$script`

This modifier can block scripts (example: javascript, vbscript)

Example:

```
||example.com^$script
```

* Supports more adblockers

### `$object`

This modifier can block objects (example: Java, Adobe Flash)

Example:

```
||example.com^$object
```

* Supports more adblockers

### `$object-subrequest`

This modifier can block request initiated by plugins (most often Flash)

```
||example.com^$object-subrequest
```

* Supports more adblockers

### `$font`

This modifier can block fonts

```
||example.com^$font
```

* Supports more adblockers

### `$subdocument`

This modifier can block subdocuments (HTML-tags: iframe)

```
||example.com^$subdocument
```

* Supports more adblockers

### `$ping`

This modifier can block request, created or `navigator.sendBeacon()`, or link attribute `ping`

```
||example.com^$ping
```

* Supports more adblockers

### '$xmlhttprequest'

Note: You can use `$xhr` modifier.

This modifier can block "XMLHttpRequests"

```
||example.com^$xmlhttprequest
```

* Supports more adblockers

### `$websocket`

This modifier can block websocket.

```
||example.com^$websocket
```

* Supports more adblockers

### `$webrtc`

This modifier can block WebRTC

```
||example.com^$webrtc
```

Note: This modifier is end of support on a future. If you need block to WebRTC, use `$nowebrtc` modifier.

* Supports only AdGuard

### '$other`

This modifier can block all other objects.

```
||example.com^$other
```

* Supports more adblockers

### `$document`

Note: You can use `$doc` modifier.

This modifier blocks pages.

```
||example.com^$document
```

* Supports more adblockers

### `$elemhide`

This modifier can cancel CSS blocking codes on a filter.

```
@@||example.com^$elemhide
```

This code cancel all CSS blocking codes for pages on a `example.com` website and on more subdomains.

* Supports more adblockers

### `$content`

This modifier disables rules for filtering HTML elements and replace rules on pages that match the rule.

```
@@||example.com^$content
```

This code cancel all HTML elements blocking for pages on a `example.com` website and on more subdomains.

* Supports only AdGuard

### `$jsinject`

This modifier prevents adding javascript code to the page. Javascript rules will be discussed below.

```
@@||example.com^$content
```

This code cancel all javascript rules for pages on a `example.com` website and on more subdomains.

* Supports only AdGuard

### `$urlblock`

This modifier disables blocking of all requests sent from pages matching this rule.

```
@@||example.com^$urlblock
```

Requests, sent from pages on `example.com` and all of its subdomains will not be blocked.

* Supports only AdGuard

### `$extension`

This modifier disables all custom scripts on pages matching this rule. This modifier only makes sense in AdGuard products that can act as userscript hosts (AdGuard for Windows / macOS / Android).

```
@@||example.com^$extension
```

This code, custom scripts won't work on all pages of example.com.

* Supports only AdGuard

### '$stealth'

This modifier disables the "Antitracking" module for all pages and queries matching this rule.

`@@||example.com^$stealth` - completely disables the Anti-Tracking module for requests to example.com and subdomains (except for blocking cookies and hiding tracking parameters, see below).
`@@||domain.com^$script,stealth,domain=example.com` - disables the Antitracking module only for script requests to domain.com (and subdomains) on example.com and all its subdomains.
Blocking cookies and hiding tracking parameters is achieved using rules with the `$cookie` and `$removeparam` modifiers. Exception rules with only the `$stealth` modifier will not give the desired result. If you want to completely disable all Anti-Tracking functions for a specific domain, you need to include all three modifiers in the rule: `@@||example.org^$stealth,removeparam,cookie`.

* Supports only AdGuard

## Generic modifiers

### `$generichide`

Disables all "generic" CSS elements rules on pages that match the exception rule.

`@@||example.com^generichide` - disables "generic" cosmetic rules on example.com pages and all of its subdomains.

* Supports more adblockers

### `$genericblock`

Disables all generic base rules on pages matching the exclusion rule.

`@@||example.com^$genericblock` - disables the "generic" base rules on the pages of example.com and all of its subdomains.

* Supports only AdGuard

### `$specifichide`

Has the opposite effect to generichide. Disables all "specific" element hiding rules and CSS rules, but does not disable "general" rules.

`@@||example.org^$specifichide` - disconnect `example.org##.banner`, but not `##.banner`

Note: Note that the modifier `$elemhide` can disable all cosmetic rules at once.

* Supports more adblockers

## Advanced modifiers

### `$removeparam`

This modifier removes parameters on URL.

```
||example.org^$removeparam=another
```

blocks:

```
example.com/page/?another=2
```

For more information, go to this [link](https://kb.adguard.com/en/general/how-to-create-your-own-ad-filters#syntax), if you need Russian, go to this [link](https://kb.adguard.com/ru/general/how-to-create-your-own-ad-filters#%D1%81%D0%B8%D0%BD%D1%82%D0%B0%D0%BA%D1%81%D0%B8%D1%81).

* Supports more adblockers

### `$important`

The `$important` modifier applied to a rule raises its precedence over any other rule without the `$important` modifier, even over basic exception rules.

Examples:

1:

```
||example.org^$important
@@||example.org^
```

`||example.org^$important` - will block all requests despite the exception rule.

2:

```
||example.org^$important
@@||example.org^$important
```

The exception rule now has the `$important` modifier as well, so it will have higher precedence.

3:

```
||example.org^$important
@@||test.org^$document
```

If a request to `example.org` is sent from the `test.org` domain, the rule will not be applied despite the `$important` modifier.

* Supports more adblockers

### `$badfilter`

The rules with the `badfilter` modifier disable other basic rules to which they refer. It means that the text of the disabled rule should match the text of the `badfilter` rule (without the `badfilter` modifier).

`||example.com$badfilter` disables `||example.com`
`||example.com$image,badfilter` disables `||example.com,image`
`@@||example.com$badfilter` disables `@@||example.com`
`||example.com$domain=domain.com,badfilter` disables `||example.com$domain=domain.com`

Rules with `$badfilter` modifier can disable other basic rules for specific domains if they fulfil the following conditions:

* The rule has a `$domain` modifier
* The rule does not have a negated domain `~` in `$domain` modifier's value.

In that case, the `$badfilter` rule will disable the corresponding rule for domains specified in both the `$badfilter` and basic rules. Please note, that wildcard-TLD logic works here as well.

`/some$domain=example.com|example.org|example.io` is disabled for `example.com` by `/some$domain=example.com,badfilter`
`/some$domain=example.com|example.org|example.io` is disabled for `example.com` and `example.org` by `/some$domain=example.com|example.org,badfilter`
`/some$domain=example.com|example.org` and `/some$domain=example.io` are disabled completely by `/some$domain=example.com|example.org|example.io,badfilter`
`/some$domain=example.com|example.org|example.io` is disabled completely by `/some$domain=example.*,badfilter`
`/some$domain=example.*` is disabled for `example.com` and `example.org` `/some$domain=example.com|example.org,badfilter`
`/some$domain=example.com|example.org|example.io` is NOT disabled for `example.com` by `/some$domain=example.com|~example.org,badfilter` because the value of `domain` modifier contains a negated domain

* Supports more adblockers

### `$empty`

Usually, a blocked request looks like a server error to the browser. If the empty modifier is applied, adblockers emulates an empty server response with a 200 OK status

`||example.org^$empty` - returns an empty response for all requests to the domain `example.org` and all its subdomains.

* Supports more adblockers

### `$app`

This modifier restricts the rule to a specific application (or list of applications). This may not be so critical on Windows or Mac, but on mobile devices, where some rules must be specific to specific applications to work correctly, this feature is extremely important.

Android - use the app package name (for example, org.example.app).
Windows - Use the process name (e.g. chrome.exe).
Mac - use bundle ID or process name (e.g. com.google.Chrome).

`||baddomain.com^$app=org.example.app` - a rule to block requests that match the specified mask and sent by the Android application `org.example.app`.
`||baddomain.com^$app=org.example.app1|org.example.app2` - a similar rule, but it works for both `org.example.app1` and `org.example.app2`.

If you want the rule not to apply to a given application, precede the application name with `~`.

`||baddomain.com^$app=~org.example.app` - a rule that blocks requests that match the given mask and sent by any application other than `org.example.app`.
`||baddomain.com^$domain=~org.example.app1|~org.example.app2` - similarly, but there are two applications in exceptions: `org.example.app1` and `org.example.app2`.

* Supports only AdGuard for Android, Windows, Mac

To next more modifiers, go to this [page](https://kb.adguard.com/en/general/how-to-create-your-own-ad-filters#redirect) goes next modifier `$redirect`. If you need russian, go to this [page](https://kb.adguard.com/ru/general/how-to-create-your-own-ad-filters#redirect)

## Unblock the domain

Unblock domain:

```
@@||example.com^
```

Unblock only websites page:

```
@@||example.com/thepage
```

Unblock with parameters

Example:

```
@@||example.com^$document
```

* Supports more adblockers

## CSS element blocking

Example:

```
example.com##.banner
```

* Supports more adblockers

### CSS selectors

`#banners`                       - CSS selector is blocking element ID

```
blocking: <div id="banners">
```

`.banners`                       - CSS selector is blocking classes element

```
blocking: <div class="banners some other classes">
```

`#div[class="banners"]`          - CSS selector is blocking class element

```   
blocking: <div class="banners">
```

`div[class^="advert1"]`          - CSS selector is blocking subclass element

```
<div id="banners">
  blocking: <div class="advert1">
</div>
```

`div[class$="banners_ads"]`      - CSS selector is blocking attribute ends with the `banners_ads` string

```
blocking: <div id="banners_ads">
   <div class="advert1">
</div>
```

`a[href^="http://example.com/"]` - CSS selector is blocking all links that are loaded from `example.com` domain

```
<a href="https://example.com/advert.html">
```

`a[href="http://example.com/"]`  - CSS selector is blocking to exactly the `example.com` address.

```
<a href="https://example.com/">
```

* Supports more adblockers