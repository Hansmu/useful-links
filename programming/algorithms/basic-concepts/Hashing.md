### What is hashing?
Hashing is the process of transforming any given key or a string of characters into
another value.

A hash function generates new values according to a mathematical hashing algorithm,
known as a hash value or simply a hash. To prevent the conversion of hash back into
the original key, a good hash always uses a one-way hashing algorithm.

Hashing is not considered encryption, as it's a one way process. It's virtually impossible
the reverse the hash into the original message.

Hashing is relevant to -- but not limited to -- data indexing and retrieval,
digital signatures, cyber-security and cryptography.

In data retrieval, hashing is used to more easily find indexes. [More about it here.](HashingDataRetrieval.md)

In digital signatures, it is used to verify the message contents. [An explanation of it
is here.](DigitalSignatures.md)

In cyber-security, an example would be the storing of data. If data is hashed, then
it cannot be reversed to get the data. For example passwords in a database. If a 
database leaks, and the info is in plaintext, then the hacker will have loads of 
usable information. However, if the passwords are stored as hashes, then it will be
useless. But leaks from multiple places that use the same algorithm can show if a 
password was reused.

In cryptography, it's used to verify the contents of a message. Used in digital signatures
as well.

The main issue with hash functions is the possibility of a collision. This means that
a hash function would produce identical outputs for different inputs.

A good hash function never produces the same hash value from two different inputs. 
As such, a hash function that comes with an extremely low risk of collision is 
considered acceptable.

To further ensure the uniqueness of encrypted outputs, cyber-security professionals 
can also add random data into the hash function. This approach, known as "salting," 
guarantees a unique output even when the inputs are identical.

An example without salting.

Attacker gets DB. Sees duplicate hashes. Attacker can arrive to conclusion that 
there's no salts or using a weak algo to hash the passwords. If they find a lot 
of the same hashes, sign that server has a default password and every new acct 
has a default password. The kinds of attacks we're talking about here are offline 
attacks against compromised/exfiltrated data.

A hash table attack can be used to reverse lookup hashed values without salting.
A hash table is a table with pre-calculated hash values based on known passwords.

Each data entry should have its own unique salt. We store these in plaintext right
next to the data that's being hashed. A salt should be cryptographically secure,
which means that it'd be difficult to predict the values.

We should generate a unique salt upon creation of each stored credential 
(not just per user or system-wide). That includes passwords created during 
registration or as the result of a password reset. If the user eventually cycles 
over the same password, we don't want to give away that the password has already 
been used.

The security of this scheme does not depend on hiding, splitting, or otherwise 
obscuring the salt. Simply put, do not mess with the salt. The salt doesn't need to 
be encrypted, for example. Salts are in place to prevent someone from cracking 
passwords at large and can be stored in cleartext in the database. However, do not 
make the salts readily accessible to the public. For that reason, usernames are bad 
candidates to use as salts.

Reasons as to why scrambling in the source code, and using a pepper, potentially, could
be bad approaches:
* https://security.stackexchange.com/a/266494
* https://en.wikipedia.org/wiki/Kerckhoffs%27s_principle
* https://stackoverflow.com/a/16896216 
