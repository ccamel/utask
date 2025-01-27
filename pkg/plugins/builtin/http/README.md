# `http` Plugin

This plugin permorms an http request.

## Configuration

|Fields|Description
|---|---
| `url` | destination for the http call, including host, path and query params
| `method` | http method (GET/POST/PUT/DELETE)
| `body` | a string representing the payload to be sent with the request
| `headers` | a list of headers, represented as objects composed of `name` and `value`
| `timeout_seconds` | an unsigned int representing a custom HTTP client timeout in seconds
| `basic_auth` | a single object composed of `user` and `password` to enable HTTP basic auth
| `deny_redirects` | a boolean representing the policy of redirects
| `parameters` | a list of HTTP query parameters, represented as objects composed of `key` and `value`

## Example

An action of type `http` requires the following kind of configuration:

```yaml
action:
  type: http
  configuration:
    # mandatory, string
    url: http://example.org/user
    # mandatory, string
    method: POST
    # optional, string as uint16
    timeout_seconds: "5"
    # optional, object of user and password fields
    basic_auth:
      user: {{.config.basicAuth.user}}
      password: {{.config.basicAuth.password}}
    # optional, string as boolean
    deny_redirects: "false"
    # optional, array of key and value fields
    parameters:
    - key: foo
      value: bar
    # optional, array of name and value fields
    headers:
    - name:  x-request-id
      value: xxx-yyy-zzz
    # optional, string
    body: |
      {
        "name": "pablo"
      }
```

## Requirements

None by default. Sensitive data should be retrieved from configstore and accessed through `{{.config.[itemKey]}}` rather than hardcoded in your template.