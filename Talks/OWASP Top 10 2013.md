# OWASP Top 10 - Wellington Meetup 2016/11/29

Notes from the Wellington meetup on November 29th 2016, discussing the OWASP Top 10  Edition 2013 (2017 is in draft at the time of writing).

Check the [OWASP Top 10 Cheat Sheet](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet) online for the latest version.

Check the [DVWA](dvwa.org.nz) (Damn Vulnerable Web Application) which is specifically designed to teach vulnerabilities.

## A1 - Injections

Vulnerabilities:

- Full Read/Write access to the DB.
- Escalation of privileges.

Prevention:

- Use parameterises queries
- Use your ORM

Verify:

- Put a `'` in your input fields. If it breaks, you're vulnerable.
- Use [sqlmap](http://sqlmap.org/), an open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over of database servers.

## A2 - Weak authentication and session management

HTTP is stateless so we use cookies to remember who someone is.

Vulnerabilities:

- Credentials could be stored insecurely on the server.
- Cookies can be guessed or stolen (control of session, logging in as another user)
- General logic might be flawed.

## A3 - XSS (Cross Site Scripting)

Mixing untrusted data within a webpage. If an attacker can add its own script to a page, he can alter the way it behaves.

Vulnerabilities:

- Runs JS on the user's browser
- Proxy commands through their computer
- Trick them into performing an action
- Redirect to phishing or malware

Where:

- HTML, when displaying user input on the page
  - Form input
  - URI parameters
- CSS, when allowing a user to set custom colours
- JS, when loading data
- HTML attributes, escaping function aren't the same for single or double quotes (i.e. your escaping function should match what your front-end use)

Prevention:

- Don't display user input if possible, otherwise:
  - Whitelist during input validation 
  - Output encode all user supplied data.
- See [OWASP XSS Prevention Check Sheet](www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet)
- Set the right [CSP](https://content-security-policy.com/) (Content Security Policy) headers

Verify:

- Put a `<` in your input fields or url params which are later displayed. If it is shown unescaped, you are vulnerable.
- Use [BeEF](http://beefproject.com/), a browser exploitation framework project.

## A4 - Insecure Direct Object References

Vulnerabilities:

- Accessing objects you're not supposed to by modifying the URI attributes.

Prevention:

- Whitelist rather than blacklist. It's easier to maintain.
- Don't trust user input
- Verify permissions
- Consider mapping database IDs to a temporaty ID per user (see ESAPI)

## A5 - Security Misconfiguration

Software, server platform out of date or misconfigured.

## A6 - Sensitive Data Exposure

Missing encryption allows man in the middle attack.

Prevention:

- Use HTTPS
- Use [HSTS](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security)
  - a web security policy mechanism which helps to protect websites against protocol downgrade attacks and cookie hijacking; it allows web servers to declare that web browsers (or other complying user agents) should only interact with it using secure HTTPS connections,[1] and never via the insecure HTTP protocol 
- Use [key pinning](https://en.wikipedia.org/wiki/HTTP_Public_Key_Pinning)
  - a security mechanism which allows HTTPS websites to resist impersonation by attackers using mis-issued or otherwise fraudulent certificates.
- Only collect what you need
- Use standard strong algorithm
- Generate, distribute and protect keys properly

## A7 - Missing Function Level Access Control

Failing to perform access checks on both client and server

Prevention:
- Do authorisation checks on `GET` and `POST`
- Block functions from certain users
- Users, role or claims-based permission.
- Whitelist rather than blacklist.

## A8 - Cross Site Request Forgery

Forcing a user's browser to make a request.

User access bad website which makes a request to target website and all credentials are passed through with the request

Prevention:

- Don't change data on `GET`, it should be idempotent
- CSRF works when the attacker knows everything
  - Include something unknown in the form like a CSRF token

## A9 - Using Components with Known Vulnerabilities

Out of date components

Prevention:

- Keep components up to date
- Catalogue components you depend on
- Follow security bulletins

Verify:
- [Retire.js](http://requirejs.org/) or [david](https://david-dm.org/) for JavaScript
- Use `pip list --outdated` for Python

## 10 - Unvalidated Redirects and Forwards

Redirecting the browser to an unsafe url; typically, when using a `nextUrl` on a login page.

Prevention:

- Have a whitelist of what it is allowed to redirect to
- Have regular expression to only allow internal urls

# Frameworks

Frameworks are a great way to migitate those risks as most of those issues have been resolved already.

## How to choose a framework?

- Choose a well known and well maintained (no abandonware) framework (it was originally phrased "something new" but we disagree with that)
- Familiarise yourself with built-in protection
- Build common code that new dev will leverage

See [OWASP Framework Security Matrix](https://www.owasp.org/index.php/Category:Framework_Security_Matrix) (still WIP) to check what each framework protects you against.

# Q&A


## Is there a way to scan your application?

There are some code scanners (like [Fortify](https://en.wikipedia.org/wiki/Fortify_Software)) but those solutions are usually expensive.

Linters normally catch stylistic issues but might catch basic security issues as well.

Use the [OWASP Zed Attack Proxy](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project) to pentest your app.

## User Input

It is well known that you should trust user input and sanitise it.

However, user input should be handled carefully even when it comes from your database. You might think that because it comes from the database it is safe, but you can never be too sure of how it was saved.

## Browsers

Vendors play their parts:

- Key pinning was actually introduced by browsers.
- The browser will block script that appears in the url and in the page.
- From January 2017, Chrome will [flag non HTTPS pages with password or credit-card fields as non-secure](https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html).