# Explanation

## What was the bug?

The OAuth2 refresh logic in `Client.request()` mishandled tokens that were plain dictionaries. The original code only set the `Authorization` header when the token was an instance of `OAuth2Token`. As a result:

1. Dictionary tokens were treated as valid, so no refresh occurred.
2. The `Authorization` header was never added for these tokens, causing API requests to fail.

The test case using a dictionary token exposed this issue.

---

## Why did it happen?

The original code attempted to check expiration like this:

````python
if isinstance(self.oauth2_token, OAuth2Token) and self.oauth2_token.expired:
    self.refresh_oauth2()


## Why does the fix solve it?

The condition was updated to:

```python
if not isinstance(self.oauth2_token, OAuth2Token) or self.oauth2_token.expired:
    self.refresh_oauth2()


This ensures refresh occurs only when:

- the token is missing or invalid, or
- the token is expired.

The `instanceof` check safely narrows the type before accessing `.expired`, preventing incorrect behavior and guaranteeing a valid Authorization header is produced.

All tests now pass:

- valid tokens are reused,
- missing tokens are refreshed,
- invalid tokens are refreshed safely.

---

## Remaining edge case not covered

The tests do not simulate a token expiring during a request (e.g., clock skew or near-expiry timing). In real systems, a safety buffer is often used to refresh slightly early. This timing-related edge case is outside the scope of the current tests.
````
