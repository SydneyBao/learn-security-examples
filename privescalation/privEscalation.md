# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

The code doesn't verify the identity of the user making the request. The code also only checks if the user has an 'admin' role, but it doesn't verify if the logged-in user is actually making the request. Lastly, the code doesn't use sessions to maintain user state across requests. 

2. Briefly explain how a malicious attacker can exploit them.

An attacker could forge a request with any user ID to update roles, bypassing authentication. An attacker with knowledge of an admin's users ID could also escalate privileges for any user, including themselves. Lastly, without proper session management, an attacker could impersonate other users by manipulating request parameters. 

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?

The code checks if the user is logged in using `req.session.userId`. It verifies that the logged-in user is an admin before allowing role updates. It also implements secure session handling with HTTP-only and SameSite cookies. Lastly, it checks if the user being updated exists before making changes.