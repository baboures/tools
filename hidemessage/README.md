## Secret message hider

Try it: https://baboures.github.io/tools/hidemessage/

**Features**
- The tool allows you to embed a secret message within a string. Only alphabetic lower-case chars are allowed.
- It uses a numeric KEY, which can be arbitrarily chosen by the user.
- Symmetric encryption: the KEY used for encryption is also used for decryption. Therefore, they KEY must be shared between the communicating parties.

**How it works**
- The KEY indicates the relative offsets of the plain text string inside the ciphertext (starting from the right). The KEY is rotated.
- The remaining positions are filled with random characters to add entropy to the ciphertext.

**Example**

Encrypt the string `foobar` using KEY = `345`

Steps:

1. The letter `f` is at position **3** starting from the right: `f..`
2. The letter `o` is at position **4** starting from the previous position: `o...f..`
3. The letter `o` is at position **5** starting from the previous position: `o....o...f..`
4. The letter `b` is at position **3** starting from the previous position: `b..o....o...f..`
5. The letter `a` is at position **4** starting from the previous position: `a...b..o....o...f..`
6. The letter `r` is at position **5** starting from the previous position: `r....a...b..o....o...f..`
7. To prevent leaking the last character, additional padding is added at the beginning of the ciphertext. If there was another letter in the plain text, we should insert it at position 3 starting from the previous position (the position of `r`). Thus, we are free to add 1 or 2 random characters at the beginning of the ciphertext:

`..r....a...b..o....o...f..`

Finally, we have to replace the dots with random characters in the alphabet, obtaining the final ciphertext:

pk**r**znvh**a**dqv**b**fe**o**ciow**o**ctm**f**ns
