## UTXOs

Bitcoin uses a _transaction model_, which means that the account doesn’t have an explicit balance, but the current nominal value is computed by summing all the UTXOs the account holds.

An UTXO (Unspent Transaction Output) is a discrete piece of cryptocurrency that has an ownership and can be transferred to another account via a transaction. It’s discrete since it cannot be divided in subparts.

Let’s say an user have an UTXO worth 1 BTC and want to send 0.5 BTC to another user. They will send the entire UTXO, and will receive back as “change” another UTXO of value 0.5 BTC.

Working in floating point is difficult because of approximations. Because of this, the Bitcoin expresses all the values in Satoshi (Sat), which equals to $10 ^{-8}$ BTC.

Since each transaction removes some UTXOs and adds some other ones, it can be considered as a change in the state.

The “input” of a transaction are the UTXOs that are sent to the receiver. The “output” is the UTXOs that the receiver receives. The difference between output and input are the transaction fees that go to the miner of the block where the transaction is located.

### Transaction fees

An user can decide to insert a transaction fee inside of the transaction, by putting a greater input value than the output value. The difference is the transaction fee, which can be seen as an incentive for the miners. An higher transaction fee means that we have an higher probability of the transaction being added to a block faster.
### Signing

In order to verify that an user is authorized to make a transaction, it will sign the transaction using its private key. In this way the transaction cannot be changes by anyone else.

The signing uses the Elliptic Curve Digital Signature Algorithm (ECDSA), which uses a double hashing technique by multiplying the private key $k$ by some number $G$, and then hashing it first with SHA256 and then with RIPEMD160.

When an user makes a transaction, it’s not directly sent to the receiver, instead the sender puts the transaction into a pool of transactions, and only the user which public key matches the private key can use it.