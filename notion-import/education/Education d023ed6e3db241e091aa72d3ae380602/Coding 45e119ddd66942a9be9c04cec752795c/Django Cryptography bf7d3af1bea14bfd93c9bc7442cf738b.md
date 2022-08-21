# Django Cryptography

Last Edited: December 19, 2019 11:43 PM

## Protecting the **SECRET_KEY[¶](https://docs.djangoproject.com/en/2.0/topics/signing/#protecting-the-secret-key)**

When you create a new Django project using **[startproject](https://docs.djangoproject.com/en/2.0/ref/django-admin/#django-admin-startproject)**, the **[settings.py](http://settings.py/)** file is generated automatically and gets a random **[SECRET_KEY](https://docs.djangoproject.com/en/2.0/ref/settings/#std:setting-SECRET_KEY)** value. This value is the key to securing signed data – it is vital you keep this secure, or attackers could use it to generate their own signed values.

## Using the low-level API**[¶](https://docs.djangoproject.com/en/2.0/topics/signing/#using-the-low-level-api)**

Django’s signing methods live in the **django.core.signing** module. To sign a value, first instantiate a **Signer** instance:

**>>> from** **django.core.signing** **import** Signer

**>>>** signer = Signer()

**>>>** value = signer.sign('My string')

**>>>** value

'My string:GdMGD6HNQ_qdgxYP8yBZAdAIV1w'

The signature is appended to the end of the string, following the colon. You can retrieve the original value using the **unsign**method:

**>>>** original = signer.unsign(value)

**>>>** original

'My string'

If the signature or value have been altered in any way, a **django.core.signing.BadSignature** exception will be raised:

**>>> from** **django.core** **import** signing

**>>>** value += 'm'

**>>> try**:

**...**  original = signer.unsign(value)

**... except** signing.BadSignature:

**...**  print("Tampering detected!")

By default, the **Signer** class uses the **[SECRET_KEY](https://docs.djangoproject.com/en/2.0/ref/settings/#std:setting-SECRET_KEY)** setting to generate signatures. You can use a different secret by passing it to the **Signer** constructor:

**>>>** signer = Signer('my-other-secret')

**>>>** value = signer.sign('My string')

**>>>** value

'My string:EkfQJafvGyiofrdGnuthdxImIJw'

***class* `Signer`(*key=None*, *sep=':'*, *salt=None*)[[source]](https://docs.djangoproject.com/en/2.0/_modules/django/core/signing/#Signer)[¶](https://docs.djangoproject.com/en/2.0/topics/signing/#django.core.signing.Signer)**

Returns a signer which uses **key** to generate signatures and **sep** to separate values. **sep** cannot be in the [URL safe base64 alphabet](https://tools.ietf.org/html/rfc4648#section-5). This alphabet contains alphanumeric characters, hyphens, and underscores.