# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

    `npm install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

    ```
        <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

The application doesn't sanitize user input in the `/register` endpoint, making it vulerable to Cross-Site Scripting attacks. Additionally, the session configuration doesn't include secure flags like `secure: true` for HTTPS-only cookies. Lastly, the `/sensitive` endpoint relies solely on a session variable for authentication, which could be manipulated.

2. Briefly explain how a malicious attacker can exploit them.

An attacker could inject malicious scripts through the name input in the registration form. For example, entering `<script>alert('XSS')</script>` as a name could execute arbitrary JavaScript when the name is displayed. Additionally, without proper session security, an attacker might be able to hijack a user's session, especially if the app.ication is not using HTTPS. Lastly, an attacker could manipulate the session to set `user` to 'Admin' and gain unauthorized access to sensitive operations.

3. Briefly explain why **secure.ts** does not have the same vulnerabilties?

The `secure.ts` file implements an `escapeHTML` function that sanitizes user input, preventing XXS attacks by escaping special HTML characters. Additionally, `sameSite` is set to `strict`, which helps prevent CSRF attacks and improves session security. The `secure.ts` file uses the `escapeHTML` function on the user input before storing it in the session, adding an extra layer of protection against malicious input.