---
layout: default
title: Cross-site Request Forgery (CSRF)
parent: Mitigations
grand_parent: Security
---

**Web dev concern level:** 3/10 (Less of a concern with the new browser default cookie same-site behavior.)

When logging into a web application, like a bank account, a [HTTP cookie](/posts/index-of-web-dev-terms/#http-cookie) is set. This special type of cookie is often referred to as a session cookie. The HTTP reponse when logging in may look something like:

```
POST https://mybank.com/login
Set-Cookie: bank.session=ba243488-ff6e-4956-8aa3-1aeb15eb982d; Domain=mybank.com; Secure; HttpOnly
```
The browser will then return the `bank.session` cookie as a header with each request to mybank.com to maintain the user session.

The problem is that the cookie will also be sent from other origins. For example, evilsite.com could have a form on the page like:

```
<form action="https://mybank.com/transfer-funds">
    <input type="hidden" name="transfer-to" value="evilsite.com">
</form>
```

If the user is authenticated to mybank.com, then navigates to evilsite.com, and submits the form, the mybank.com session cookie will get passed. The funds will be transferred to evilsite.com:(

## Mitigations

The best mitigation is to set the `SameSite` attribute on the session cookie to either `lax` or `strict`. This will tell the browser not to send the cookie on cross-origin requests. `lax` is now the default behavior for all browsers, making CSRF less of an issue.

A second approach (which should be done in parallel to approach #1-- see [swiss cheese modal for security](https://en.wikipedia.org/wiki/Swiss_cheese_model)) is to use the [synchronizer token pattern](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#synchronizer-token-pattern), where the server creates a CSRF token (a securely-generated random value) that is passed to the browser client either on a per-request or per-session basis. The CSRF token is then passed with each request (either as a request header or hidden form input) and verified by the server.

