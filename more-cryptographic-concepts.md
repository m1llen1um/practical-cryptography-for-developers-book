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

Multi-Factor authentication adds additional layers of identity authentication. Usually, those factors should be added to some of the following categories:

  * What I know
  * What I have
  * What I am

Two-Factor requires one of those three categories. The most common case of **Two-Factor Authentication** is a **user password** and a device on which will be sent/generate **one-time-password**. For generating one-time-password (OTP) the HMAC-based One-time Password algorithm is used. 


### HMAC-based One-time Password (HOTP)

HOTP algorithm is based on [HMAC](https://en.wikipedia.org/wiki/HMAC) and provides a symmetric generation of human-readable passwords, each used for only one authentication attempt. The key parameter of HTOP is a secret which has to be exchanged between the parties in advance:

```
HTOP(has_function, secret, value_length) -> htop
htop.generate() -> auth_code
htop.validate(auth_code) -> true/false
```

The **hash_func** can be any cryptographic hash function. The **secret** is the arbitrary byte string which must be shared between the parties and kept private. **value_length** defines the **auth_code** length.


### Counter-based One-Time Password algorithm (COTP)

The HTOP function contains an internal counter. In order bout parties to authenticate each other, they have to keep in sync their counters. Each time when HOTP was requested to generate an **auth_code** the counter iterates.


### Time-based One-Time Password Algorithm (TOTP)

Time-based One-Time Password Algorithm (TOTP) is an extension of COTP, where the **counter** is the current time, defined as **Unix time**. The **time-interval** is another parameter used for the generation of TOTP, which defines a period of time of which a given authentication code will be valid. 

```
htop_counter = (current_time - initial_time) / time_interval
```

For TOTP to work correctly the bout parties must have synchronized clocks with minimal verification window (delay based on user's input, network latency and unsynchronised clocks).

```
otp = TOTP(hash_function(secret), htop_counter)
```


### Time-based One-Time Password  in practice

A popular use case of Two-Factor Authentication is the Google Authenticator. A server generates a secret and shares it as a QR code with the client. The client scan and store the secret in the [Google Authenticator](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2) application on a phone. After that, the server and the phone start to generate the same one-time passwords.

A web-based JavaScript [example](http://blog.tinisles.com/2011/10/google-authenticator-one-time-password-algorithm-in-javascript/) for using and testing TOTP

![Time-based One-time Password example](/assets/OTP-secret-QR-code.png)


## Infected Cryptosystems and Crypto Backdoors

[https://en.wikipedia.org/wiki/Kleptography](https://en.wikipedia.org/wiki/Kleptography)

