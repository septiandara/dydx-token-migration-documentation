# Slashing

The slashing module is a mechanism to penalize validators for a violation of protocol rules by slashing their bonded tokens. Penalties under the slashing module include burning a portion of a validator’s bonded tokens and/or temporarily removing their ability to vote on future blocks.

### Key Concepts and Definitions <a href="#key-concepts-and-definitions" id="key-concepts-and-definitions"></a>

*   States: In the state machine, a variable number of validators are registered, and during each block, the top `max_validators` (defined in the

    [Staking module](broken-reference)

    ) who are not jailed become bonded and can propose and vote on blocks, with a `ValidatorSigningInfo` record tracking their liveness and potential protocol faults.
* Double Signing: When a validator is proven to have signed two blocks at the same height, causing conflicting blocks or transactions on multiple branches of the dYdX Chain.
* Downtime: When a validator does not vote on a dYdX Chain block for a period of time.
* Jailed: A period of time when a validator is not allowed to rejoin the Active Set due to a violation of protocol rules.
*   ​

    [Staking Tombstone](https://github.com/cosmos/cosmos-sdk/blob/6afece635cef9f8e044a04ce67d06e55ca300249/x/evidence/keeper/infraction.go#L27)

    : When a validator is permanently removed from the Active Set due to a double signing infraction. More information about Staking Tombstone is available

    [here](https://docs.cosmos.network/v0.45/modules/slashing/07\_tombstone.html)

    .

More information about the slashing module is available

[here](https://docs.cosmos.network/main/build/modules/slashing)

.

These parameters may be adjusted by the dYdX Community with an on-chain governance proposal.

| Title                                                                                                                                                                                  | Value                                                                   | Definition                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3766">signed_blocks_window</a></p><p>​</p>       | <p>8192</p><p>~ 3 hours 11 minutes</p><p>(assuming 1.4s block time)</p> | The window in terms of the number of blocks for which a validator's signing activity is monitored.                                                        |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3767">min_signed_per_window</a></p><p>​</p>      | 0.2                                                                     | The minimum of blocks in the `signed_blocks_window` that a validator must sign to avoid being jailed.                                                     |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3768">downtime_jail_duration</a></p><p>​</p>     | <p>7200s</p><p>2 hours</p>                                              | The length of time a validator is temporarily removed from the Active Set.                                                                                |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3769">slash_fraction_double_sign</a></p><p>​</p> | 0.0                                                                     | The fraction of a validator's staked tokens that will be slashed in the event of a double signing violation.                                              |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L3770">slash_fraction_downtime</a></p><p>​</p>    | 0.0                                                                     | The fraction a validator will be slashed by if they miss a fraction (`min_signed_per_window`) of blocks within a sliding window (`signed_blocks_window`). |

In every block, validators contribute to a set of precommits for the previous block, forming the `LastCommitInfo` in CometBFT. This `LastCommitInfo` is valid if it includes precommits from +2/3 of the total voting power.

If a validator fails to be included in the `LastCommitInfo` for a certain number of blocks, they will be automatically jailed, slashed or unbonded.

dYdX Chain stores Information about validator's liveness activity on `ValidatorSigningInfo`. At the start of each block, the `ValidatorSigningInfo` for each validator is updated, and their liveness status over `signed_blocks_window` is checked.

The sliding window is defined by `signed_blocks_window` and the index is determined by the `IndexOffset` in each validator’s `ValidatorSigningInfo`. The `IndexOffset` is incremented with each block whether the validator signed or not, and the `MissedBlocksBitArray` and `MissedBlocksCounter` are updated accordingly once the index is determined.

To make sure whether a validator falls below the liveness threshold, the maximum number of blocks missed (`maxMissed`) and minimum height of liveness threshold (`minHeight`) are retrieved.

maxMissed = signed\_blocks\_window - min\_signed\_per\_window \* signed\_blocks\_window

If the current block is past `minHeight` and the `MissedBlocksCounter` exceeds `maxMissed`, the validator is slashed by `slash_fraction_downtime`, jailed for `downtime_jail_duration`, and has their `MissedBlocksBitArray`, `MissedBlocksCounter`, and `IndexOffset` reset.

Note, slashing due to liveness tracking failure does not lead to tombstoning.

Should a validator want to return and potentially rejoin the Active Set after being removed due to Downtime, they must send a `MsgUnjail`.

string validator\_addr = 1;

The extraction of MEV (Maximal Extractable Value) by validators can undermine a fair and transparent trading environment. MEV refers to the profit a dishonest validator can gain by censoring and/or re-ordering orders and cancellations to their advantage. Validators could take advanatge of the architecture of the dYdX Chain - an in-memory orderbook design - to manipulate, re-order, or censor trades before suggesting a new block for profit extraction, resulting in trades executing at worse prices relative to the best price possible and cancellations potentially being ignored.

To show how much MEV value could be extracted by each validator, dYdX Trading, Inc. ("dYdX Trading") and Skip Protocol have collaborated to create a

[dashboard](https://dydx.skip.money/)

that displays data on orderbook discrepancies.

Currently, there is no protocol level solution to mitigate MEV on dYdX Chain, despite MEV extraction being considered a harmful validator behavior. However, the dYdX community through a governance vote could approve the implementation of a social slashing framework to penalize validators engaged in MEV extraction.
