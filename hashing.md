# Hashing
When introducing hashing, I like to use a grocery store analogy. When you go to the grocery store to look for apples, you know you can simply go to the fruit section to find apples. However, if organization by aisles did not exist, and all the food is thrown all around the store, you would be forced to traverse the entire store in search of apples (as you would when searching for an item in a linked list). As a result, having organization by aisles makes grocery trips much more efficient and less traumatic. 

**Hashcodes** are integers that represent a specific category, while hashing is the process of giving an object a hashcode. In the grocery store analogy, a hashcode can be thought of as the aisle number, while hashing is the process of determining the aisle in which an object belongs. 

## Hashcodes
The following properties must hold for a _valid_ hashcode:
1. Deterministic (i.e. each time you ask for an object’s hashcode, the same integer is returned)
2. Equal objects must have the same hashcode

A _good_ hashcode is one that distributes object evenly.

## Hash Tables
A hash table is a data structure that uses hashcodes to determine which "bucket" an object hashes. There are no duplicates in hash tables.
```
hashcode % number of buckets = bucket object hashes to
```

**Load factor** is defined as `(number of items) / (number of buckets)`.

### Resizing
To keep the number of items in each bucket relatively small, the hash table is resized when a given load factor is exceeded. If the load factor is 2, for example, the hash table would resize when it contains `2N` items, where `N` is the number of buckets. 

### Runtimes
Assuming a good hashcode, the runtime of hash table operations such as adding, removing, and contains are _amoritized_ `O(1)`. Amoritized means "on average." The number of items in each bucket is relatively small with respect to `N` (the total number of items), and since the hashcode allows us to limit our search to only the items in one particular bucket, operations can be done in constant time. Good hash tables resize by multiplying the number of buckets (e.g. when the load factor is exceeded, the number of buckets double). Resizing takes linear time, since all the items must be rehashed into a larger hash table. But since resizing is rare, the `O(N)` time operation occurs very infrequently, thus the overall runtime is still `O(1)` on average across all operations. 
