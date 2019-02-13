**Warning:** this is an odd job, don't rely on this code for dealing with real passwords.

There are some serious cryptographic concerns to be addressed:

* Replay attacks: a captured code can be replayed multiple times while remaining valid.
  This can probably be avoided by using a secure bidiretional communication scheme involving a strong key exchange algorithm and a good random number generator.
  
* Leak of the master password: anybody with physical access to the key can dump the master password by patching some functions on the code.
  Is possible to mitigate this issue by storing a hash of the master password in the hardware token instead of the plaintext. This would break backwards-compatibility with the current algorithm, because the master password should be hashed alone first when entered manually.

* Even if is possible to overcome the aforementioned potential issues, anybody with physical access to the key or momentary access to the authenticated LessPass client can dump the master password (or its hash), effectively being able to impersonate the legit user.
  The first case (physical access to the key) could be avoided by adding another security measures such as a fingerprint reader on the security token, a multifactor authentication scheme combining the plaintext master password **and** the secret stored into the hardware token, both hashed together (this last factor can be replaced with a long mnemonic pharse in case of emergency).
  The second case enters into the security rabbit hole and can't be solved easily, even if we could run the lesspass algorithm inside the hardware token (although that would be great).