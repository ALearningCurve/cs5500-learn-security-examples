# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.
- The operations and access of the server are not handled in a robust way. This means there is not repudiation.
2. Briefly explain why the vulnerability is addressed in __secure.ts__.
- This vulnerability is addressed by adding loggers for requests, responses, and errors. This lets us identify how the server is being accessed, easily identify suspicious activity, and ultimately better secure our server.
3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
- Middleware, chain of responsibility, is used to add logging to the request, response, and errors we catch. 