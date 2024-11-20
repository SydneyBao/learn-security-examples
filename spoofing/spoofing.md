# Spoofing

This example demonstrates spoofind through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies

    `$ npx install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. Start the malicious server **mal.ts**

    `npx ts-node mal.ts`

4. Open __http://localhost:8000__ in a browser, type a name and Submit.

5. Open the __Application__ tab in the Browser's inspect pane. Find the __Cookies__ under __Storage__. You should see a __connect.sid__ cookie being set.

6. Open the HTML file __mal-steal-cookie.html__ file in the same browser (different tab). Open inspect and view the console.

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?

8. Open the HTML file __mal-csrf.html__ file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out? 


## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.

The `httpOnly` flag for the session cookie is set to `false`, which allows client-side scripts to access the cookie. This makes the application vulberable to the cross-site scripting attacks and session hijacking

2. Briefly explain different ways in which vulnerability can be exploited.

An attacker could inject malicious JavaScript code that reads the session cookie and sends it to a remote server. Since the cookie is accessible to client-side scripts, an attacker could also steal the session ID and impersonate the user. Lastly, without proper encryption, an attacker could intercept and modify the session data in transit.

3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.

secure.ts implements several security measures. The `httpOnly` flag is set to `true` preventing client-side access to the session cookie. The `sameSite` attribute is set to `true`, which helps prevent cross-site request forgery attacks. The session secret is passed as a command-line argument rather than being hardcoded, improving security. 