---
layout: post
title:  "OAuth, OpenID Connect and SAML"
date:   2021-09-29 22:00:00 +0700
categories: misc
---

# Background
- Authenticaion : is the process that to confirm that users are who they claim they are. Think of computer user/password that allow the users who knows user/password to get in.
- Authorization : is about the security to allow/permit users to do action they want to. Think of users right on computer, normal users can't access admin's files

# OAuth
OAuth stands afor Open Authorization. It is commonly used way of grants 3rd party application to access user resources on another server. OAuth is focus on authorization not authenticaion.
- Latest OAuth specification is 2.1 as of now
- The OAuth specification is written base on on HTTP protocal
- It's token based authorization (JWT)
- OAuth specify flows/grants(interaction between roles). Flow is depend on application type( SPA, mobile, so on)

## Roles
OAuth defines 4 roles.
- Resource owner(RO) : A person or entity that have capable of granting access to a protected resource.
- Resource server(RS) : The server that hosting the protected resources.
- Client : An application that makeing request to access the protected resources on bahalf of resource owner. Sometimes called 3rd party application.
- Authorization server(AS) : The server that capable of issue an access token to client.

# OpenID
OpenID Connect is built on top of OAuth. Since OAuth just focus on authorization and leave authenticaion out of scope. OpenID Connect is created to cover authenticaion by extending OAuth protocal.

# SAML
SAML stands for Security Assertion Markup Language. SAML is protocal that help provides authentication. SAML is older and more mature that OpenID.

# OpenID vs SAML

|Type|OpenID|SAML|
|-----|-------|-------|
| Maturity | less | more |
| Protocal based on | JWT(On top of OAuth) | XML
| Purpose | authentication | authentication

