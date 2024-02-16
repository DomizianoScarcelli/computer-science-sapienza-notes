---
Exam:
  - Blockchain and Distributed Ledger Technologies
---
Bitcoin uses a non-Turing complete language called _script_ as a scripting language to make the protocol work. The non-Turing completeness is a choice to make the programming language less powerful in order to avoid exploits.

Script is a stack based language, meaning operations are put and removed from a stack. The execution has to end with just one value on the stack, which is what the function returns.

### Locking and Unlocking script

Inside the UTXO there is a `scriptPubKey` field, which is the locking-script, which specifies the conditions to spend the output in the future.

The unlocking-script (defined in the field `scriptSig`), on the other hand, decides if the spender can actually spend its UTXOs in the current transaction. Unlocking scripts are always executed before the locking scripts. It’s used to verify the conditions inside of a locking script (it gives the solution for the locking script, that’s also why it's executed before).

An example of locking script is `3 OP_ADD 5 OP_EQUAL`, which means find a value such that added to 3 is equal to 5. This syntax is because script is a stack language, meaning values are put onto a stack and operations pop the values on the stack and push new values.

### Unlocking script based on public key hash

Also called Pay to Script Hash (P2SH), the spender of an output is required to include a set of operations in their unlocking script.

The operations in the locking-script are: `OP_DUP OP_HASH160 <PubKHash> OP_EQUALVERIFY OP_CHECKSIG`where `PubKHash` is the RIPEMD160 digest of the SHA256 hash of the recipient’s public key.

The unlocking-script is: `<sig> <pubK> OP_DUP OP_HASH160 <PubKHash> OP_EQUALVERIFY OP_CHECKSIG` where `sig` is the signature provided by the spender, and `pubK` is the spender’s public key.