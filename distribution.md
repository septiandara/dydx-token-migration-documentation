# Distribution

An overview of the Distribution Module.

The distribution module enables a simple collection and distribution mechanism to passively distribute rewards between validators and delegators.

### Key Concepts and Definitions <a href="#key-concepts-and-definitions" id="key-concepts-and-definitions"></a>

* Community Pool: a pool of tokens funded by a portion of staking rewards (`community_tax`) that the dYdX community could use to fund contributor grants, community initiatives, liquidity mining, and other initiatives.
* Distribution `ModuleAccount` Account: an account that collects and distributes trading and transaction fees among validators, delegators, and the community pool.
* Staking Rewards: the total portion of the Fee Pool that a DYDX staker can claim at a given block.
* Fee Pool: fee pool from maker trading fees (USDC), taker trading fees (USDC), DYDX denominated gas fees from transactions, and USDC denominated gas fees from transactions for a given block.
* Staking Rewards Withdrawal: each block a DYDX staker may claim their portion of Fee Pool. If a DYDX staker does not claim staking rewards, their respective rewards will accrue in the Distribution `ModuleAccount` Account.
* Total Bonded Power: the sum of all tokens that are currently staked by validators to themselves and tokens staked to validators by DYDX holders.
* Block Rewards: fees distributed to validators and delegators for successfully proposing and validating a new block on the blockchain.

More information about the distribution module is available

[here](https://docs.cosmos.network/main/build/modules/distribution)

.

These parameters may be adjusted by the dYdX Community with an on-chain governance proposal.

| Title                                                                                                                                                                                                                                              | Value | Description                                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------ |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R1142"><code>community_tax</code></a></p><p>​</p>         | 0     | A tax that directs a percentage of the fee pool to the community pool.                                             |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R1143"><code>base_proposer_reward</code></a></p><p>​</p>  | 0     | Part of the block reward reserved for the validator that proposes a given block.                                   |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/pull/39/commits/8915a65da04932dfdedea255feadd6b380c94865#diff-74b06241cbb20c39839cc9341cc4cb5ed24a9f290cc61435d29094f9af70afe3R1144"><code>bonus_proposer_reward</code></a></p><p>​</p> | 0     | Bonus incentive for block proposers based on the number of transactions included in a given block.                 |
| <p>​</p><p><a href="http://withdraw_addr_enabled/"><code>withdraw_addr_enabled</code></a></p><p>​</p>                                                                                                                                              | True  | Whether a delegator can set a different withdrawal address (other than their delegator address) for their rewards. |

![](https://3227850899-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FcSd7APxHbsYMlFFAeIMP%2Fuploads%2Fo1ADS3Kii6u2YionOXU6%2FStaking\_Rewards\_on\_dYdX\_Chain\_v5%20\(1\).png?alt=media\&token=288d0da9-e218-4936-847a-0a871313da59)

On the dYdX Chain, all transaction fees (trading fees denominated in USDC, DYDX denominated gas fees from transactions, and USDC denominated gas fees from transactions) collected by the protocol will be distributed to validators and DYDX holders that stake to dYdX Chain validators.

The Cosmos

[x/distribution module](https://docs.cosmos.network/main/modules/distribution)

is a simple mechanism to allocate rewards earned by Validators and Stakers. For a detailed understanding of the Cosmos rewards mechanism, read

[here](https://github.com/cosmos/cosmos-sdk/blob/main/docs/spec/fee\_distribution/f1\_fee\_distr.pdf)

.

### How rewards are distributed on dYdX Chain <a href="#how-rewards-are-distributed-on-dydx-chain" id="how-rewards-are-distributed-on-dydx-chain"></a>

![](https://3227850899-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FcSd7APxHbsYMlFFAeIMP%2Fuploads%2FvZ72Hwb5g5Nqh4rWmOYR%2FFee\_Distribution\_on\_dYdX\_Chain\_v6%20\(1\).png?alt=media\&token=a922bc3b-ac4a-46f9-b77c-6bd8678d7990)

DYDX holders who stake to (a) validator(s) are entitled to a portion of the following fees:

* DYDX denominated gas fees from transactions,
* USDC denominated gas fees from transactions,
* USDC maker trading fees, and

Fees will accrue in the `Distribution ModuleAccount Account` each block. Each block a DYDX staker may claim their portion of Staking Rewards. If a DYDX staker does not claim Staking Rewards, their respective rewards will accrue in the `Distribution ModuleAccount Account`.

Note, Staking Rewards are not automatically staked to a dYdX Chain validator. Any DYDX earned by a staker as Staking Rewards will need to be claimed from the `Distribution ModuleAccount Account` and staked to a dYdX Chain validator to contribute to the security of the network and qualify to earn staking rewards.

### How staking rewards are calculated <a href="#how-staking-rewards-are-calculated" id="how-staking-rewards-are-calculated"></a>

![](https://3227850899-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FcSd7APxHbsYMlFFAeIMP%2Fuploads%2Flni5AwZrmXI39zsxR4bX%2FStaking%20Rewards%20Formula.png?alt=media\&token=51185cf2-79a4-42f5-bf6b-9aa155b6e211)

* Fee Pool = fee pool from maker trading fees (USDC), taker trading fees (USDC), DYDX denominated gas fees from transactions, and USDC denominated gas fees from transactions for a given block.
* Number of DYDX staked by DYDX holder = total DYDX tokens that a dYdX Chain address has staked to (a) validator(s) at a given block.
* Total bonded power = the sum of all DYDX that are currently staked by validators to themselves and DYDX staked to validators by DYDX holders.
* Staking Rewards = the total portion of the Fee Pool that a DYDX staker can claim at a given block.
* Community tax = A tax that directs a percentage of the fee pool to the community pool.
* Validator commission rate = commission set by each validator and applied to the staking rewards of each delegator. Validators are required to follow the `min_commission_rate` parameter, but are otherwise free to set their own commission rates.
