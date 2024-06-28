---
title: "Intro to CSP report-to and report-uri HTTP headers"
date: 2024-06-27T13:43:47-05:00
draft: true
ShowToc: true
---

## CSP Directives: `report-to` and `report-uri`

The Content Security Policy (CSP) directives `report-to` and `report-uri` are used to specify where the browser should send violation reports when a content security policy is violated on a website.

**Why Use Them:**

- Helps in identifying and fixing security issues on a website.
- Provides insights into potential attacks or vulnerabilities.
- Enhances the overall security posture of the website.
- PCI Compliance

## `report-uri` - CSP Directive

- Legacy CSP directive that is used for reporting violations
- Deprecated but not all browsers support the newer directives so it is still recommended to be used

![Image showing report-uri CSP directive support via Can I Use ](/images/report-uri-Can-I-use.jpg#center)

### `report-uri` Example

```HTTP Header
Content-Security-Policy: ...; report-uri https://kevinpatel.xyz/report-csp-violation/
```

## `report-to` - CSP Directive

- Replacement of `report-uri`
- Not supported by Firefox
- Will need either `Report-To` or `Reporting-Endpoint` HTTP header to go along with this

![Image showing report-to CSP directive support via Can I Use ](/images/report-to-Can-I-use.jpg)

### `report-to` Example

```HTTP Header
Report-To: { "group": "csp-endpoint", "max_age": 10886400, "endpoints": [ { "url": "https://kevinpatel.xyz/report-csp-violation/" } ] }
Content-Security-Policy: ...; report-to csp-endpoint;
```

or

```HTTP Header
Reporting-Endpoints: csp-endpoint="https://kevinpatel.xyz/report-csp-violation/";
Content-Security-Policy: ...; report-to csp-endpoint;
```

## `Report-To` - HTTP Header

- Not widely supported
- Dedicated MDN Doc doesn't exist

![Image showing Report-To HTTP Header support via Can I Use ](/images/Report-To-header-Can-I-use.jpg)

### `Report-To` Example

```HTTP Header
Report-To: { "group": "csp-endpoint", "max_age": 10886400, "endpoints": [ { "url": "https://kevinpatel.xyz/report-csp-violation/" } ] }
Content-Security-Policy: ...; report-to csp-endpoint;
```

## `Reporting-Endpoints` - HTTP Header

- "Chrome 96+ and Edge 96+. Firefox is supportive. Safari doesn't object"
- Dedicated MDN Doc doesn't exist

### `Reporting-Endpoints` Example

```HTTP Header
Reporting-Endpoints: csp-endpoint="https://kevinpatel.xyz/report-csp-violation/"; Content-Security-Policy: ...; report-to csp-endpoint;
```

## **Full Coverage Examples:**

```HTTP Header
Report-To: { "group": "csp-endpoint", "max_age": 10886400, "endpoints": [ { "url": "https://kevinpatel.xyz/report-csp-violation/" } ] }
Reporting-Endpoints: csp-endpoint="https://kevinpatel.xyz/report-csp-violation/";
Content-Security-Policy: ...; report-to csp-endpoint; report-uri https://kevinpatel.xyz/report-csp-violation/
```

## What do the reports look like

Chrome

```json
{
  age=0,
  body={
    blockedURL=https://example.com/script.js,
    columnNumber=121,
    disposition=report,
    documentURL=https://kevinpatel.xyz/,
    effectiveDirective=<your original CSP policy>; report-uri https://kevinpatel.xyz/report-csp-violation; report-to csp-endpoint;,
    referrer=,
    sample=,
    statusCode=200
  },
  type=csp-violation,
  url=https://kevinpatel.xyz/,
  user_agent=Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
}
```

Firefox

```json
{
  csp-report={
    blocked-uri=https://example.com/script.js,
    column-number=121,
    disposition=report,
    document-uri=https://kevinpatel.xyz/,
    effective-directive=script-src-elem,
    line-number=1,
    original-policy=<your original CSP policy>; report-uri https://kevinpatel.xyz/report-csp-violation/,
    referrer=,
    source-file=debugger eval code,
    status-code=200,
    violated-directive=script-src-elem
  }
}
```

## Resources

[Monitor your web application with the Reporting API](https://developer.chrome.com/docs/capabilities/web-apis/reporting-api)

[CSP: report-to | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-to)

[CSP: report-uri | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-uri)
