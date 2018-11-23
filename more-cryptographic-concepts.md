# More Cryptographic Concepts for Developers

...

## Digital Certificates, the X.509 Standard and PKI

...

[https://cryptography.io/en/latest/x509/](https://cryptography.io/en/latest/x509/)

## Transport Layer Security \(TLS\) and SSL

...

[https://en.wikipedia.org/wiki/Transport\_Layer\_Security](https://en.wikipedia.org/wiki/Transport_Layer_Security)

## External Authorization and OAuth

...

## Two-Factor Authentication and One-Time Passwords

Multi-Factor authentication add additional layers of identity authentication. Usually those factors should be added in some of the following catagories:

  * What I know
  * What I have
  * What I am

Two-Factor require one of those tree categories. The most common case of **Two-Factor Authentication** is a **user password** and a device on which will be send/generate **one-time-password**. For generating one-time-password (OTP) the HMAC-based One-time Password algorithm is used. 


### HMAC-based One-time Password (HOTP)

HOTP algorithm based on [HMAC](https://en.wikipedia.org/wiki/HMAC) and provide a symmetric generation of human-readable passwords, each used for only one authentication attempt. Key parameter of HTOP is a secret which has to be exchanged between the parties in advance:

```
HTOP(has_function, secret, value_length) -> htop
htop.generate() -> auth_code
htop.validate(auth_code) -> true/false

```

The **hash_func** can be any cryptographic hash function. The **secret** is the arbitrary byte string, and must remain private. **value_length** define the **auth_code** length.


[https://cryptography.io/en/latest/hazmat/primitives/twofactor/](https://cryptography.io/en/latest/hazmat/primitives/twofactor/)

[https://tools.ietf.org/html/rfc4226.html](https://tools.ietf.org/html/rfc4226.html)

Infected Cryptosystems and Crypto Backdoors

[https://en.wikipedia.org/wiki/Kleptography](https://en.wikipedia.org/wiki/Kleptography)

