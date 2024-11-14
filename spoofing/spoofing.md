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
    - The vulnerability is that the user's session cookie is not being securely managed. 

2. Briefly explain different ways in which vulnerability can be exploited.
    - First, the cookie can be accessed cross site. Because of this, a bad actor can leverage cross site request forgery. In this case, the user does not even need to click on anything. Just loading the malicious page on another domain causes a request to the backend to be made and processed. This lets a bad actor access sensitive data.
    - Another way is that the cookie can be stolen. In this case, since the cookie is stored in a way accessible by javascript wets lets bad actors use malicious javascript to steal cookies.

3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.
    - `secure.ts` does not have the vulnerability for two reasons:
        1. it has `httpOnly: true`, which prevents malicious javascript from accessing, and thus stealing, the cookie
        2.  it has `sameSite: true`, which prevents CSRF attacks