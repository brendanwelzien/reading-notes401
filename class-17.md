# Hash Tables
What is a hashtable?
**Hash** - result of some algorithm taking in a string and converting it into a value that could be used for security or something else. IF there is a hash table, it is used for determining *index* of an array

**Buckets** - buckets are what is contained in each index of an array of hashtable, each index is a bucket. An index can have multiple key/value pairs if a *collision* occurs

**Collisions** a collisoin is what happens when more than one key gets hashed to same location of the hashtable

## Usage
1. Hold unique values
2. Dictionary
3. Library

## What are they
- a data structure that utilizes key value pairs... This means every `Node` or `Bucket` has both a key, and a value
    - the idea of the hashtable is to store the key into this data structure and then retrieve the value
    - `hash` is ability to encode the key that maps to a location to get the value
- since we are able to hash the key and find the location of value the **TIME COMPLEXITY is O(1)**, ideal for when quick lookups are needed

## Structure
- hash codes are determined by their input

### Creating a Hash
1. add or multiply all the ASCII values together
2. multiply it by a prime number
3. use modula to get the remainder of result, when divided by total size of array
4. insert it into array a that index

- if two keys were to create collision, then solve by changing state of bucket instead of starting them at `null` initialize a `linkedlist` in each one... This allows for key/value to be stored as a node 

Hash maps do this to store values:

- accept a key
- calculate the hash of the key
- use modulus to convert the hash into an array index
- store the key with the value by appending both to the end of a linked list
Hash maps do this to read value:

- accept a key
- calculate the hash of the key
- use modulus to convert the hash into an array index
- use the array index to access the short LinkedList representing a bucket
- search through the bucket looking for a node with a key/value pair that matches the key you were given
[<-- Back](README.md)