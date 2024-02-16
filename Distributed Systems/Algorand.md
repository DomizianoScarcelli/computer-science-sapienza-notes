---
Exam:
  - Distributed Systems
  - Blockchain and Distributed Ledger Technologies
---
The most important problem with [[Proof of Work]] is the high environmental impact.

On the other hand, the problem with the two types of Proof of Stake are:
- Bonded [[Proof of Stake]]: validators bind their stake to show the commitment they have to the system, misbehaviours are punished with slashes.
	- The participants cannot use the stake
	- The initial stake is very high, creating an economic barrier for entrance
- Delegated [[Proof of Stake]]: users delegate the validation of new blocks to a fixed committee, through weighted voting based on their stakes.
	- The committee is known, and so exposed to DDoS attacks. Because the committee is a small group of nodes, there is centralization of governance.

# Pure Proof of Stake

The consensus mechanism (actually Proof of Stake and Proof of Work are leader election mechanisms, which are fundamental for the consensus mechanism to work) in Algorand is called Pure Proof of Stake.

Each participant has a number of ALGOs. Each ALGO can be seen as a tamper-proof dice that is rolled in a safe and secret cryptographic way. For each new block, dice rolls are performed in a distributed, parallel and secret manner between the participant of the consensus. The winner is then revealed in a safe and verifiable way. A participant can win if they roll a particular number. Of course the range of numbers (faces of the die) is very large.

The more ALGO the participant has at stake, the higher the probability of winning.

The dice is a run of a verifiable random function. If the result fall in a certain range, you win.

> [!Note]
> Unlike Ethereum, there is no minimum amount of stake, and the stake will not be freezed. The more ALGO an account has, the more the probability of proposing a new block.
## How is this VRF used?
1. Block proposal: the node that is selected by the VRF (the node that won) proposes the block and the VRF output, which can be used to prove that they’re a valid winner.
2. Soft Vote:
    1. Since there could be multiple winners in a single round, the this phase filters the winners down to one, in order for only a single block to be certified. The winner is the one with the lowest VRF result. Each node that receives multiple blocks from different winners only proposes the one with the lowest VRF.
    2. In the second part of this phase, a committee is elected running a VRF for each ALGO for every participating account, and they will vote on the best proposal. This is done in order to agree that the block with the lowest hash from the previous part is actually that one, and only one.
3. Certify Vote: A new committee check that the block is valid, checking for overspending, double spending or any other problems.
    ![[Screenshot 2024-01-21 at 3.49.06 PM.png]]

Choosing a node with VRF is smart since no one knows before hand who is the winner (the VRF computation is done offline). Only the node that has a valid VRF result knows it, and then they will propose the block. This mean that they cannot be target of any DDoS attack.

>[!Note]
>Because of how the algorithm work, Algorand blockchain cannot fork. This means that when a block is added, it’s also final. Each block is decided in less than 3 seconds.

![[Screenshot 2024-01-21 at 3.47.17 PM.png]]
Let’s say a user has $w$ Algo, then they have a probability to win from $0$ to $w$ tickets. The VRF hash can be mapped to a $[0,1]$ domain, and so we an map the hash to a number from $[0, w]$ which corresponds to how many tickets the user won.

Note that the VRF is executed just once, and it’s used to sample the number of winning tickets from a distribution which depends on $w$.

## BA* - Modified Byzantine Agreement

This is the real consensus mechanism that Algorand uses, which is a modified version of the Byzantine Agreement. It can tolerate some malicious users, as long as honest users have a super majority ($> {2\over3}$) of the total stake in the system.

BA algorithms have some problems by themselves, but in combination with VRF they can be solved.

## Different Nodes

Algorand network has two kind of nodes:
- Non-Relay Nodes:
    - They partecipate to the PPoS consensus;
    - They connect only to other Relay Nodes;
    - They can have two types of configurations:
        - Light configuration: meaning they store just the latest 1000 blocks;
        - Archival Configuration: meaning they store the entire chain since the genesis block.
- Relay Nodes:
    - At the beginning of the algorand network they couldn’t partecipate to consensus, since the few relay nodes had a lot of ALGO, and so a lot of power. Now this isn’t true anymore so they can also partecipate to consensus.
    - They can communicate with all types of nodes
    - They route the blocks to all the connected non-relay nodes with highly efficient communication paths in order to reduce the communication hops.
    - They have much more power than non-relay nodes.
## Transactions

As any other blockchain protocol, the state of the blockchain is changed via transactions. In the Algorand Protocol there are 6 types of transactions:

- Payment
- Key Registration
- Asset Configuration
- Asset Freeze
- Asset Transfer
- Application Call

Assets are in Algorand what tokens are for the other chains, but they do not require writing a smart contract. By default they are not shareable unless specified.

>[!Note]
Algorand natively support multi signature accounts, which are accounts that requires the signature of multiple accounts in order to emit transactions.

>[!Note]
>It also supports atomic transfers or group transactions, in order to group multiple transactions such that all or none will succeed. This enables the _pooled fee_, which is when a transaction can be used to pay the fee of other transactions.

Fees in Algorand are a way to protect the network from DDoS, and they are not used as validation fee to the miner.

## Algorand Account

The public key is used to generate an Algorand address encoded in base32 with checksum. An Algorand address is 58 characters long.

The private key is used to generate a mnemonic phrase of 25 words. This is generated by converting the private key bytes in to 11 bit integers, and mapping those integers to the bip-0039 english word list of 2048 ($2^{11}$) words.

Algorand accounts in order to work must have a minimum balance of 0.1 ALGOs that will be blocked. This is done in order to pay for the space in the blockchain. The minimum balance increases if the account opts in some assets, and decreases if it opts out of other assets.

## AVM - Algorand Virtual Machine

Just like Ethereum Virtual Machine, the Algorand VM is a Turing-complete secure execution environment that runs on Algorand, which purpose is to approve or reject transactions effects on the blockchain according to the smart contract logic.

The execution is approved if at the end of the execution there is a non-zero character at the top of the stack machine.

You can use the Teal language that directly compiles to AVM Bytecode to write Algorand smart contracts. Since Teal is a stack-based low-level assembly-like programming language, you can also write them using other languages such as PyTeal in Python that compiles to Teal which then compiles to AVM Bytecode.

>[!Note] 
>In algorand a smart contract can write and read something in an user wallet, in a place called local storage.

A smart contract consists in two programs:

- Application Program, which is responsible for processing all calls to the contract, with the exception of the Clear Call.
- Clear Program, which is used to handle the Clear Call, that is a call that remove the smart contract from an account balance record.

If it’s enabled, the application can be deleted and updated without needing to deploy a new copy of it like in ethereum.

You cannot spam Algorand coins (that are not ALGO), since to receive a certain coin the receiver needs to agree (opt-in). This doesn't happen in Ethereum.

An account can only read the local state of an Application, but it can read and write its own local state.

>[!Note]
>In order to avoid what’s called re-entrancy attack, an application cannot call itself, even indirectly. But they can only call other applications up to a stack depth of 8.

## Ethereum vs Algorand

### Fees

Unlike ethereum, where transaction fees are paid whether the transaction is successful or not, in Algorand transaction fees are only paid if the transaction is included in the block.

The minimum amount of transaction fee is 0.001 ALGO, which is independent to the transaction type.

### Smart Contract Storage

Ethereum smart contract storage is a huge array of $2^ {256}$ uint256 elements.

In Algorand, a smart contract can have three different type of storages:

- **Local Storage**: it’s allocated when an account opts in to an app (it does that by sending a transaction), and can include up to 16 key-value pairs. It can be read by any app/account call that has the app ID in its foreign apps/accounts array. Any app can write on it, but it can be deleted only by the owner. Deleting the app doesn't affect the local storage, they have to explicitly clear the app to recover the minimum balance.
- **Global Storage**: it can include up to 64 key-value pairs. Can be read by any app call that has the specified app’s ID in its foreign apps array, but can be written only by the app itself. It’s deleted when the app is deleted, and cannot be deallocated in any other way.
- **Box Storage**: an app can allocate as many boxes as it needs. This is dynamically allocated. A box can be of any size, from 0 to 32K bytes. Only the app that creates the box can read and write on it. Each app can delete its own boxes, but if the app id deleted, the boxes are not affected, and they remain on the blockchain forever.