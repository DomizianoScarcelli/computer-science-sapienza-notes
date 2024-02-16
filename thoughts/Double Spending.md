In the context of the [[The Blockchain Technology|Blockchain]] technoloty, double spending is a flaw that allows an individual to spend more coins that they posses.

Let’s assume we have an user $A$ that with a balance of 100 BTC that makes a transaction of 90 BTC to an user $B$, and then makes a transaction to another account of 50 BTC. The user $B$ receives the payment and ships the package. If the network then decides that the second transaction has happened before the first one, then the first one won’t be valid because user $A$ won’t have 90 BTC in the wallet, but they will have the package.

This happens because we need to wait more or less 6 blocks to be sure that the transaction is in the main branch, and not in some secondary branch.