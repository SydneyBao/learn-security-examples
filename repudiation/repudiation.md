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

The vulerability is a lack of authentication for accessing sensitive data. The `\get-messages` route allows anyone to retrieve all messages without authentication, exposing private information to unauthorized users

2. Briefly explain why the vulnerability is addressed in __secure.ts__.

The vulnerability is addressed by implementing authentication for the `'get-messages` route. The simulated authentication mechanism demonstrates the principle of acessing sensitive data only to authenticated users.

3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?

The secure version uses the Middleware pattern. A logging middleware is implemented to record all requests, enhancing security monitoring. An error handling middleware is added to catch and log errors, improving the application's robustness. Authentication middleware is used to check user authentication before allowing access to sensitive data. These middleware functions allow for modular and resuable security measures across different routes.