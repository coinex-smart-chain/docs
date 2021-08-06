# Genesis Block

## What is Genesis File

The Genesis file defines the initial state of CoinEx Smart Chain (CSC), which may be viewed at block height `0`. `CSC`s first block starts from `1`, whose parent block is Genesis Block.

To facilitate user operation, `CSC` directly integrates Genesis Block into the binary package `cetd` and no download is required when setting up the node. If you are interested in Genesis Block, you can download and view the details via [GitHub]( https://github.com/coinex-smart-chain/csc). For those who want to build their own chain with CSC, Genesis File is also available for customization and editing. Refer to [Private Chain](/en-us/node_private_chain.md).

The following is the interpretation of parameters in Genesis File.

## Parameter interpretation

* chainId - Chain ID
  * `CSC` Mainnet: `52`
  * `CSC` Testnet: `53`

* senatus - `CSC` Consensus configuration
  * period - Time period for block generation, 3 seconds for `CSC`
  * epoch - The number of block intervals between validators updates, 200 blocks for `CSC`

* nonce - `CSC` is set to `0x0`
* timestamp - Block time
* extraData - Containing 3 parts of data
  * The first 32 bytes represent the fixed data reserved for the signature user
  * Validator address
  * The 65 bytes at the end form the node signature upon block generation
* gasLimit - Gas limit in the block
* difficulty - Block difficulty so far
* coinbase - Block node address
* alloc - Pre-allocation address
* number - Block height, `0` for Genesis Block
* parentHash - The parent block hash of the current block, `0` for Genesis Block
