# Overview

- Cross-Origin Resource Sharing (CORS)
- https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
    + https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Allow-Origin
    + https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS
- https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/
- https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html

- Best practices
    + https://livebook.manning.com/book/cors-in-action/chapter-6/

- Conversations
    + https://www.reddit.com/r/javascript/comments/2dqioz/bypass_cors_errors_when_testing_apis_locally/

- Local testing
    + https://medium.com/swlh/avoiding-cors-errors-on-localhost-in-2020-5a656ed8cefa

# CORS vs CSP (Content-Security-Policy)

- CSP
    + https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy
    + The HTTP Content-Security-Policy response header allows website
      administrators to control resources the user agent is allowed to
      load for a given page.
    + It controls which external sources that the user agent
- Resources
    + https://stackoverflow.com/questions/39488241/what-is-the-difference-between-cors-and-csps
    + https://www.baeldung.com/cs/cors-csp-differences#:~:text=Cross%2DOrigin%20Resource%20Sharing%20(CORS,acceptable%20in%20an%20HTTP%20response.
    + https://dev.to/sophiekaelin/what-is-the-difference-between-cors-and-csp-i7n
    + https://gist.github.com/kafkahw/2e77abec646e625cda7a930ec5d67555
- CORS and CSP and cyber attacks
    + https://nodeployfriday.com/posts/cors-cyber-attacks/
    + https://security.stackexchange.com/questions/108835/how-does-cors-prevent-xss
    + https://en.wikipedia.org/wiki/Cross-site_scripting

# Tips and Tricks

## Preflight requests (OPTIONS) do not include credentials or require authentication
