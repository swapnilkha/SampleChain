# SampleChain
Simple Blockchain Transaction Validator and Miner Implementation

[input] array.integer startBalances
An array representing starting balances. The element with index i and value x initializes the balance of the node with address i to x.

[input] array.array.integer pendingTransactions
A two dimensional array of integers, where each subarray is of the form [fromAddress, toAddress, value]

[input] integer blockSize
An integer specifying the maximum number of transactions that can be included in a block

[output] string
A string representing the encoded block, e.g.
"00000d03a1ce56a06bfdbceb0249bbb2204a6f22, 0000000000000000000000000000000000000000, 28427, [[0, 1, 5], [1, 2, 5]]"
"blockHash, prevBlockHash, nonce, blockTransactions"
blockHash: The value returned by sha1(“prevBlockHash, nonce, transactions”)[2], e.g. sha1("0000000000000000000000000000000000000000, 28427, [[0, 1, 5], [1, 2, 5]]").
prevBlockHash: The blockHash of the previous block. Should be 0000000000000000000000000000000000000000 for the first block.
nonce: The lowest integer for which the first four characters of blockHash are equal to 0000
blockTransactions: A string encoded representation of the transactions included in this block. Each individual transaction takes the form [fromAddress, toAddress, value], where fromAddress, toAddress, and valueare each integers, e.g. [0, 1, 5].
Each block should have blockSize transactions if there are >= blockSize transactions that have yet to be included in a block. If there are fewer than blockSize transactions remaining, all remaining transactions should be included in the final block.

Transactions
A transaction ti is valid if the address at from has a balance >= value after processing all transactions tj for which j < i. Some transactions in pendingTransactions may be invalid. These transactions should be omitted from all blocks. You can assume that from and to will have entries in startBalances.

Example Outputs:

getLastBlock([5, 0, 0], [[0, 1, 5], [1, 2, 5]], 2) = "00000d03a1ce56a06bfdbceb0249bbb2204a6f22, 0000000000000000000000000000000000000000, 28427, [[0, 1, 5], [1, 2, 5]]"

getLatestBlock([1,7], [[1, 0, 4], [1, 0, 3], [1, 0, 2]], 2) = "000034820d4fc67dc28e109dc01a44c2dab76ad0, 0000000000000000000000000000000000000000, 12643, [[1, 0, 4], [1, 0, 3]]"

getLatestBlock([3, 10, 10, 3], [[3,2,2], [2,3,5], [3,2,4], [3,0,2], [1,2,2]], 2) = "00007e4b79c454ea24b9824d2f87a4cff40a2081, 0000d3d78687ff2328f9ade77994622cb254f934, 1155, [[1, 2, 2]]"
