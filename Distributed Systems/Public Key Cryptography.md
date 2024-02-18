---
Exam:
  - Distributed Systems
  - Blockchain and Distributed Ledger Technologies
---
A process has two keys, one private $k_1$ and one public $k_2$. The keys are connected, in a sense that if you encrypt a message $m$ with the public key you obtain $m'= E_{k_2}(m)$ and if you encrypt $m'$ again with the private key you obtain $m$ back $m = E_{k_1}(m')$ and vice versa.

The public key can be available to everybody, meanwhile the private key must be a secret. If someone want to send a secret message that only the one with the private key can decrypt, they encrypt it with the public key, in this way only the person with the private key can get the original message.

This method also allows to sign a message, by just doing the process the other way around, meaning I encrypt the message with the private key, and who wants to read it decrypt it with the public key. Since I am the only person with the private key, the message could only be signed by me.

Signing can also be used to prove that the message hasn’t been compromised: I can hash the message, encrypt it with the private key and attatch this sign at the end of the message. Who wants to read it can decrypt the sign with the public key in order to get the hashed message, to see if the message has been compromised they can just hash the message with the public key and compare the two hashes, and if they’re equal the message is the same that I’ve sent, otherwise it has been compromised.