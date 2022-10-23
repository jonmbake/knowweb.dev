---
layout: default
title: OAuth2 for User-to-Service Authentication
parent: Authentication/Authorization
grand_parent: Security
---

OAuth 2 is an [authentication](/posts/index-of-terms#authentication) and [authorization](/posts/index-of-terms#authorization) standard that enables applications to obtain limited access to user accounts on an HTTP service. It works by delegating user authentication to the service that hosts the user account, and authorizing third-party applications to access the user account. OAuth 2 provides a method for clients to access a protected resource on behalf of a resource owner. It also provides a process for end-users to authorize third-party access to their server resources without sharing their credentials (typically, a username and password pair). 

OAuth 2 provides authorization flows for both web and mobile applications. The most common OAuth 2 flow is the authorization code flow. This flow is optimized for server-side applications, where the secret can be stored securely. The authorization code flow begins with the client directing the user to the authorization server. The user authenticates with the authorization server and grants the client permission to access their resources. The authorization server then issues an authorization code to the client. The client can then use the authorization code to request an access token from the authorization server. 

The client presents the access token to the resource server and gains access to the protected resources.

## OAuth 2 Roles

There are four roles in the OAuth 2 framework:

* **Resource owner:** This is the user who grants access to their resources.
* **Resource server:** This is the server that hosts the protected resources.
* **Authorization server:** This is the server that issues access tokens to the client.
* **Client:** This is the application that wants to access the resources on behalf of the resource owner.

## OAuth 2 Endpoints

There are three endpoints in the OAuth 2 framework:

* **Authorization endpoint:** This is the endpoint on the authorization server where the resource owner grants access to their resources.
* **Token endpoint:** This is the endpoint on the authorization server where the client can exchange the authorization code for an access token.
* **Resource endpoint:** This is the endpoint on the resource server that the client can use to access the protected resources.

## OAuth 2 Flows

There are four flows in the OAuth 2 framework:

* **Authorization code flow:** This is the most common flow. It is optimized for server-side applications, where the secret can be stored securely.
* **Implicit flow:** This flow is optimized for mobile applications and web applications.
* **Password flow:** This flow is used when the resource owner has a trust relationship with the client.
* **Client credentials flow:** This flow is used when the client is requesting access to resources that are not owned by a user.