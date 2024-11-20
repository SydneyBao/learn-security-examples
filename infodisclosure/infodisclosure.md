# Tampering

This example demonstrates information disclosure by injecting malicious query objects to a NoSQL database.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?username[$ne]=
    ```

4. Do you see user information being displayed despite the malicious request not having a valid username in the request?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

The main vulnerability in insecure.ts is its susceptibility to NoSQL injection attacks. This is due to directly using user-provided input in the database query without proper sanitization or validation. The code directly uses the username from the query parameters in the MongoDB find operation, allowing attackers to manipulate the query.


2. Briefly explain how a malicious attacker can exploit them.

An attacker could craft a malicious query parameter. For instance, if they get userInfo for usernames that aren't null, the MongoDB database will return all user records in the database.


3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?

The secure.ts file checks that the username is a string and rejects non-string inputs. Additionally, there is input sanitization to remove all non-alphanumeric characters from the username, preventing the injection of special characters or MongoDB operators. The error handling prevents detailed error messages being sent to the client, protecting sensitive information about the server or database structure. Lastly, the query uses the sanitized username instead of the raw input, reducing the risk of NoSQL injection attacks.