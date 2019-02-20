**Warning:** this is an odd job, don't rely on this code for dealing with real passwords.

There are some serious cryptographic concerns to be addressed:

* Replay attacks: a captured code can be replayed multiple times while remaining valid.
  This can probably be avoided by using a secure bidirectional communication scheme involving a strong key exchange algorithm and a good random number generator.
  
* Leak of the master password: anybody with physical access to the key can dump the master password by patching some functions on a copy of the public LessPass code.
  Is possible to mitigate this issue by storing a hash of the master password in the hardware token instead of storing the plaintext. This would break backwards-compatibility with the current algorithm, because the master password should be hashed alone first when entered manually.

* Even if it's possible to overcome the aforementioned potential issues, anybody with physical access to the key or momentary access to the authenticated LessPass client can dump the master password (or its hash), effectively being able to impersonate the legit user.
  The first case (physical access to the key) could be avoided by adding another security measures such as a fingerprint reader on the security token or a multifactor authentication scheme combining the plaintext master password **and** the secret stored into the hardware token, both hashed together (this last factor can be replaced with a long mnemonic pharse in case of emergency).
  The second case enters into the security rabbit hole and can't be solved easily, even if we could run the lesspass algorithm inside the hardware token (although that would be great).

# Usage

Flash the file [Firmware.ino](/LessPass/Firmware/Firmware.ino) into a Atmega-32u4 development board.

## Serving the application locally:
Use some sort of HTTP server pointing its root to the [LessPass](/LessPass) folder:

    cd LessPass; python3 -m http.server

## Opening the application:
Navigate to https://0x2b3bfa0.github.io/lesspass-hardware (or http://localhost:8000/index.html if you're running a local server) and connect the development board into a USB port.

# Design

This code is modifying the LessPass interface dynamically in a really obnoxious way. This proof of concept should be read with indulgence.
