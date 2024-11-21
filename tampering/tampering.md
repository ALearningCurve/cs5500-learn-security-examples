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
 - the potential vulnerability is that the code does not sanitize the input when registering the user, thus letting arbitrary javascript be run on frontend when later displaying the username (XSS).
2. Briefly explain how a malicious attacker can exploit them.
 - a malicious attacker could insert a username containing a script which then modifies the page when it is displayed on the frontend. This is a form of XSS attack.
3. Briefly explain why **secure.ts** does not have the same vulnerabilities?
 - It does not have this issue since it sanitizes the username before creating the cookie. This means that the user is unable to insert scripts since they will be sanitized and thus rendered inert.