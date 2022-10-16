---
layout: default
title: Index of Web Dev Terms
nav_order: 3
---

## Authentication

A user verifies their identity.

## Authorization

A user has permission to perform an action.

## Database Breach

Contents of a secured database are accessed by a unauthorized party.

## Dictionary attack

An attack performed against a set of hashes to try to determine the input of the hash. For example, if a list of unsalted password hashes were obtained through a database breach.

## Hash

A one-way function that takes an input of arbitrary size and produces an output of fixed size. Hashes have certain properties (such as collision resistance) that make them useful for cryptographic purposes (such as storing passwords).

## HTTP Cookie

A small piece of state data (< 4093 bytes) that a server can set; the data is then returned by the browser on each subsequent request to the server domain (until the cookie expires). A cookie is set with the `set-cookie` response header. The cookie value is returned to the server via the `cookie` request header.

## Salt

A bit of extra data appended to a value before being [hashed](#hash), in order to protect against a [dictionary attack](#dictionary-attack).
