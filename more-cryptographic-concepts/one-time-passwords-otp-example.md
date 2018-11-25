# One-Time Passwords (OTP) - Examples in Python

In this section we shall provide an **examples** about how to generate and validate One-Time Passwords (OTP) in Python.

Installation:

```py
pip install pyotp
```


## Server Setup

We need to create a base32 secret which has to be shared between the authentication sever and the client. We will follow the Google's OTP model which is based on a uri. It includes the shared secret, client's username and issuer's name.

```py
import pyotp

base32secret = pyotp.random_base32()
print('Secret:', base32secret)

totp_uri = pyotp.totp.TOTP(base32secret).provisioning_uri(
    "alice@google.com",
    issuer_name="Secure App")
print(totp_uri)
```

Sample output:

```py
Secret: S3K3TPI5MYA2M67V
otpauth://totp/Secure%20App:alice%40google.com?secret=S3K3TPI5MYA2M67V&issuer=Secure%20App
```


## User Setup

Once the client store the secret in a secure way it will generate (by default) every 30 seconds a new code.

```py
import pyotp
import time

base32secret = 'S3K3TPI5MYA2M67V'
print('Secret:', base32secret)

totp = pyotp.TOTP(base32secret)
print('OTP code:', totp.now())
time.sleep(30)
print('OTP code:', totp.now())
```

Sample output:

```
Secret: S3K3TPI5MYA2M67V
OTP code: 339838
OTP code: 284911
```


## Working Example

You can install Google Authenticator on Play Store or App Store and scan the QR code below:

![OTP Auth](/assets/one-time-passwords-otp-example-qr-code.png)

Example validation check:

```py
import pyotp


base32secret = 'S3K3TPI5MYA2M67V'
print('Secret:', base32secret)

totp = pyotp.TOTP(base32secret)
your_code = '123456'
print(totp.verify('Code Valid:', your_code))
```

Output:

```
Secret: S3K3TPI5MYA2M67V
Code Valid: True
```