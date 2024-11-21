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
- There is no session being used to authenticate users, so the userId and the newRole are attacker defined, thus allowing an attacker to arbitrarily change the role of users when invoking the 'update-role' route since they can just invoke the route with an admin userId themselves.
2. Briefly explain how a malicious attacker can exploit them.
- An attacker can brute force user ids until one of them gives them authorized access to change the role of a user. This allows the attacker use 'admin' powers to change the role of some users even if their own user is not an admin.
3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
- Rather than letting the user tell us who they are (as they do in the insecure sever with the userId property), we can use a session to authorize users. Because the session is controlled by the server, we can trust that value to identify who is making the request. The modified server code uses the userId in the request session to authorize the action of changing user's roles. Assuming our session logic is robust and some additional logic is added to securely log users in, this prevents this vulnerability by not allowing the attacker to arbitrarily specify their identity in the request.