---
Title: Hashing Strings with Python
menu:
    ai_notes:
        parent: Software Engineering
draft: True
---

Hash functions map sequences of bytes to fixed length sequences. The value returned by a hash function is often called a hash, message digest, hash value, or checksum. 

## MD5

## binascii

If you're looking to hash a string, you'll need to convert your string to binary.


```python
# Convert string to binary
binary_string = b'abcd'
print(binary_string)
```

    b'abcd'



```python
# Generate hexadecimal from binary string
import binascii
binascii.hexlify(binary_string)
```




    b'61626364'



## hashlib


```python
import hashlib
m = hashlib.md5()
m.update(binary_string)
m.hexdigest()
```




    'e2fc714c4727ee9395f324cd2e7f331f'


