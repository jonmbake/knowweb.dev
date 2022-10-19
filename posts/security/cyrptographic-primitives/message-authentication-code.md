---
layout: default
title: Message Authentication Code (MAC)
parent: Cryptographic Primitives
grand_parent: Security
---

_Message Authentication Codes_ (MACs) are like [hashes](./posts/security/cyrptographic-primitives/hash/) except they require a secret key to calculate the hash of the message or input.

```
MAC(message, secret_key) = hashValue
```

MACs are useful to verify the integrity of a message after passing through an untrusted medium (where it is possible for something between the sender and receiver to alter the message).

## Example

Let's say we have the message, "Hello, KnowWeb.dev". Let's MAC that message using the secret key, "This is my super secret key":

```
knowweb.dev > echo -n "Hello, KnowWeb.dev" > message.txt
knowweb.dev > hmac256 "This is my super secret key" message.txt 
08ae81e4f7696c4b0c092ad96398bcc1fd09fb64daf1414a04327ea625cfb782  message.txt
```

The MAC of the message is `08ae81e4f7696c4b0c092ad96398bcc1fd09fb64daf1414a04327ea625cfb782`. We can then attach this MAC to the message when sending it through an untrusted medium:

```
{
    "message": "Hello, KnowWeb.dev",
    "mac": "08ae81e4f7696c4b0c092ad96398bcc1fd09fb64daf1414a04327ea625cfb782"
}
```

If the message is returned to the originator, they can verify the message has not changed by MACing the message and verifying it matches the `mac` value returned with the message.


An example of using MACs in web development is [MAC HTTP cookies for flash messages](https://medium.com/@jonmbake/the-why-and-how-of-mac-http-cookies-7fbb2debe47b).