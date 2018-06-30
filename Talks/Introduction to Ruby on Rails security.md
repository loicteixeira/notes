---
url: https://youtu.be/Hez1QYc9yo8
---

# Introduction to Ruby on Rails security

## SQL Injection
> Nefarious SQL statements are inserted into an entry field for execution.

- Don't build your query yourself, use the ORM which protects you. That being said, [some methods](http://rails-sqli.org/) are unsafe to use.
- Don't solely rely on the ORM, consider setting users and permissions at the database level so even if someone gets access to the database via SQL Injection, they don't have full access to the database.

## XSS
> If an attacker adds a script and gets it to show to another user, he gets access to that user's session.

- Variables within an html template are automatically escaped.
- Variables used in a helper, within style/script blocks and in non-html templates **aren't** escaped. Use partials instead.
- Whitelist URL from user. Don't blacklist, it's too easy to forget to add a URL to the list or for someone to find a URL which isn't blacklisted.
- Consider CSP as an additional protection.

## CSRF: Cross Site Request Forgery
> Attack that forces an end user to execute unwanted actions on a web application in which they're currently authenticated.

- Rails check tokens for `POST`, `PATCH`, `PUT` and `DELETE` actions but not for `HEAD` and `GET` actions. Therefore, you should never modify the state within `HEAD` and `GET` requests.

## Direct Object Reference
> Request a record by ID allow an attacker to guess and different record ID

- Always scope under current user (e.g. `current_user.invoices.find(params[:id])` instead of `Invoice.find(params[:id])`) which not only will protect the resource, but will raise 404 instead of 403 (unauthorised), leaking the least possible amount of information.
- Basically, filter first and query second.

## Mass Assignment
> A computer vulnerability where an active record pattern in a web application is abused to modify data items that the user should not normally be allowed to access such as password, granted permissions, or administrator status.

Use [strong parameters](http://weblog.rubyonrails.org/2012/3/21/strong-parameters/) to prevent mass assignment.

## Unexpected types
`where` accepts a simple object or an array and use `=` or `IN` accordingly. Again, use strong parameters.

## Arbitrary Objct Deserialisation
YAML can contain artitrary ruby objects which can result in Remote Code Execution (RCE).

## Gems to help
- breakman: static analysis of security vulnerability for Rails app.
- bundle-audit: check dependencies for know security issues.