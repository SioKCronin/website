---
title: Hashing
menu:
    ai_notes:
        parent: Software Engineering
---
# Hashing

Hash functions map sequences of bytes to fixed length sequences. The value returned 
by a hash function is often called a hash, message digest, hash value, or checksum. 

Underlying a hash table is a large array of length $N$, where most of the slots are
empty. To resolve collisions (which happen when we go to enter a value at a particular position,
and there is already a value there), we can either implement chaining (where we turn
each slot into a linked list) or open addressing where we place the value in the next empty
slot. If we use chaining, we'll have to tack on a 32 or 64 bit pointer to our space bill
for each element in our linked list. And if we use open addressing and do not keep a
spacious amount of space (storing a lot of empty slots) our clever hash table will
devolve to a structure with $O(n)$ traversal. Tradeoffs to consider!

## MD5

## binascii

If you're looking to hash a string, you'll need to convert your string to binary.

```python
# Convert string to binary
binary_string = b'abcd'
print(binary_string)

>>>
b'abcd'
```

```python
# Generate hexadecimal from binary string
import binascii
binascii.hexlify(binary_string)

>>>
b'61626364'
```

## hashlib

```python
import hashlib
m = hashlib.md5()
m.update(binary_string)
m.hexdigest()

>>>
'e2fc714c4727ee9395f324cd2e7f331f'
```

## sparsehash

Before you get to thinking that these Python built-ins are all there is to know
in the world of hash functions, let me dazzle before your eyes Google's
[sparsehash](https://github.com/sparsehash/sparsehash), which offers one of the
most space efficient hashmap implementations known to humankind, requiring a mere
2 bits of overhead per entry. It does, however, clock up to 2 to 3 times slower
than the implementations explored above, but if space is your concern, I suggest
you check it out. 




