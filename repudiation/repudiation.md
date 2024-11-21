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
- The operations and access of the server are not logged and tracked in a robust way. For instance, 'send-message' logs the request, but does so poorly by not indicating the route. In general access to the server is opaque since requests to routes (such as get-messages) have no logging for when they are being accessed or by who. Further, there is no clear error handling. This is problematic for a few reasons, one being that it would make suspicious activity hard to notice. Ultimately, all these factors indicate there is poor repudiation.
2. Briefly explain why the vulnerability is addressed in __secure.ts__.
- This vulnerability is addressed by adding loggers for requests, responses, and errors and also by having much more descriptive log entries. Additionally, since these loggers all log with date times, this lets us identify how and when the server is being accessed, easily identify suspicious activity, and ultimately better secure our server.
3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
- The chain of responsibility pattern is being used in the secure version in the form of middleware to add logging middleware to every request and also add an error handler to every route.  