# Exercises: Encrypt Passwords for User Register / Login

In this exercises, you need to improve a weak security implementation of a user password store. Initially, you'll have a **clear-text** implementation which you need to improve by storing the password **hashed** and finally to **hashed with KDF**.

Base implementation of _"Clear-Text Passwords"_: 

```py
# Here the user sore the password
stored_password = ''

def create_password(pwd):
    """definition how a user will create and store"""
    """a password in the system in the registration process"""
    global stored_password
    stored_password = pwd
    return stored_password

def verify_password(stored_pwd, pwd):
    """definition how a user will verify """
    """a password in the system in the authentication process"""
    return stored_pwd == pwd

def register():
    """simulation of registration"""
    password = input('Please create a password: ')
    created_password = create_password(password)
    print('The password in the user\'s store will be: ' + created_password)
    pass

def login():
    """simulation of login"""
    password = input('Please enter your password: ')
    passwordMatch = verify_password(stored_password, password)
    if passwordMatch:
        print('You\'re authenticated')
    else:
        print('Invalid credentials')

register()
login()
```

**Sample output:**

```
$ Please create a password: password123
$ The password in the user's store will be: password123
$ Please enter your password: password123
$ You're authenticated
```

Use the **bad** implementation of the **Clear-Text** example as a skeleton. You have to update the functions `create_password` and `verify_password` in the next sections and make the user store more secure.

## Simple Password Hashing

Change the _Clear-Text Passwords_ example in a way that `stored_password` function, store the password in **SHA-256**. Try other hash functions.

**Sample output:**

```
Please create a password: password123
The password in the user's store will be:  b'ef92b778bafe771e89245b89ecbc08a44a4e166c06659911881f383d4473e94f'
Please enter your password: password123
You're authenticated
```

Hint: You can use the [Calculating Cryptographic Hash Functions in Python](/cryptographic-hash-functions/hash-functions-examples.md#calculating-cryptographic-hash-functions-in-python) example.

Bonus: Add salt to your algorithm. Try to add several times the salt.

Bonus Hint: Use `salt.encode("utf8") + password.encode("utf8")` to add the salt.

## Secure KDF-Based Password Hashing

Change the _Clear-Text Passwords_ example in a way that the `stored_password` function, store the password in **Argon2** hash.

**Sample output:**

_The salt used in the output: **b27c0ecd223943cc8d14ca39aaebd6dd**_

```
Please create a password: password123
The password in the user's store will be: b'9de4645041a19993ab85028bc8ca69070aad0dddbf3e2e01eec0fd1c80b73f8e4f0558973cec9e679ff83675276b6af35c3bcdbd2cf4b40a4afd686bf0f746a0e806cb51c44a82ee9b
13633b65cc1827d641ee28c709f7603c7df923b9d02149cac3915104bd5a084d12c76d5772aa8d8fd9d751916de60503ab399850f1ab40'
Please enter your password: password123
You're authenticated
```

Hint: Use [Argon2 package](https://pypi.org/project/argon2/)

Bonus: Experiment with some of the additional parameters. Learn more about the different Argon2 modes - Argon2d, Argon2id, Argon2i, Argon2ds.