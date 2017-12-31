# Plugging the Security Holes in Your Phoenix Application

## Configuration

- Missing HTTPS/HSTS
- Known Vulnerable Dependencies
- Missing CSRF Protections (`plug :protect_from_forgery`)
- Missing Secure HTTP Headers (`plug :put_secure_browser_headers`)

## Denial of Service

- String.to_atom()
- List.to_atom()
- :"foo#{bar}"
- ~w(#{foo})a

## Directory Traversal

- Don't use user's input directly as file path.
- null(\0) termination

## Cross-Site Scripting

Don't believe any input that user have control of.

ex) content-type. A user can send an image embeds javascript with content-type `plane/text`.

## SQL Injection

fragment

## Sessions

?

## Mass Assignment

A user can update values that they shouldn't.

```elixir
user
|> cast(attrs, [:name, :admin])
```