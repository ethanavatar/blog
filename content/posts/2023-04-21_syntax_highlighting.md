+++
title = "Syntax highlighting"
draft = true
+++

This is a page summary, it should show up in the main posts area and provide
readers with a preview.

<!-- more -->

## Some examples

### With Line Numbers

```python,linenos,linenostart=98
class MockResponse:
    """Wraps a `httplib.HTTPMessage` to mimic a `urllib.addinfourl`.
    ...what? Basically, expose the parsed HTTP headers from the server response
    the way `cookielib` expects to see them.
    """

    def __init__(self, headers):
        """Make a MockResponse for `cookielib` to read.
        :param headers: a httplib.HTTPMessage or analogous carrying the headers
        """
        self._headers = headers

    def info(self):
        return self._headers

    def getheaders(self, name):
        self._headers.getheaders(name)
```
