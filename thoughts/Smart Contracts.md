In order to deploy a smart contract, a new Contract account has to be made, and because everything that lives on the blockchain is immutable, also smart contracts are immutable. This means that in order to create another version of the smart contract, a new smart contract has to be created.

Smart contract compile code to bytecode which is interpreted by a EVM (Ethereum Virtual Machine). This allows multiple language to compile to bytecode.

## Gas

The execution of running programs on the EVM is measured in _gas_, which is a virtual currency not associated with ETH. Everything has a gas price, and so we need to be careful when creating a smart contract.

The least amount of gas to pay for a transaction is 21,000 units, since this is the unit of gas that is needed in order to issue a new transaction.

We need to find a balance between lowering the gas price in order to run the code, and making it high in order to maximise the chances that the transaction is minted by the miners, since more gas means more transaction fees.

An account that executes the code of a smart contract has a field that specifies the maximum amount of gas they are willing to spend, in order to not execute an infinite loop and run out of funds. This also circumvents the halting problem, since if a contract code does not stop, it will stop after reaching the gas limit.

### Transaction fees before and after the London upgrade

Before the London upgrade in August 2021, the transaction fee was computed as `used_gas_units * gas_price_per_unit`.

After the upgrade, in order to prevent a continuous creation of ETH which will inevitably raise inflation, the fee is computed as `used_gas_unit * (base_fee + priority_fee)`, where the `base_fee` is adjusted according to the network utilization (demand), and the ETH associated are burnt. The address to send ethereum that will be burn is 0x000000000000000000000000000000000000dEaD

The `priority_fee` on the other hands is like a tip that goes into the miner pockets. Higher the tip, higher the probability of the transaction being into the next block.