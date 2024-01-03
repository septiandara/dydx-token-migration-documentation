# Governance

An overview of the governance module.

dYdX Chain is a proof-of-stake blockchain network and holders of DYDX can participate in governing the dYdX Chain. dYdX Chain uses the standard

[x/gov module](https://docs.cosmos.network/main/build/modules/gov)

in the Cosmos SDK.

The governance module empowers DYDX holders to propose and vote on proposals, directly influencing the evolution of the dYdX Chain through a democratic process. The subject matter of proposals can vary from changing a governable parameter on the dYdX Chain, spending dYdX community funds, and updating the software that dYdX Chain nodes are running, among other things.

### Key Concepts and Definitions <a href="#key-concepts-and-definitions" id="key-concepts-and-definitions"></a>

* Deposits: Unstaked DYDX tokens pledged by the proposer and potentially other DYDX holders in support of the creation of a governance proposal.
* Inheritance: If a DYDX staker does not vote on a proposal, they will inherit the vote of their validator for the respective proposal.
* Vote Weight: A DYDX holder's vote weight is equal to the amount of DYDX the user has actively staked (1-1). DYDX tokens that are not staked or are in the unbonding period will not count towards a DYDX holder's vote weight.
*   Tallying: After the voting period concludes, the

    [TallyParams](https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2878-L2880)

    aggregate the vote results to determine if the proposal was accepted or rejected by the dYdX community.
* Execution: If a proposal passes, the execution process depends on the type of proposal.

More information about the governance module is available

[here](https://docs.cosmos.network/v0.46/modules/gov/)

.

These parameters may be adjusted by the dYdX Community with an on-chain governance proposal.

| Title                                                                                                                                                                                                  | Value                                                  | Description                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| DepositParams                                                                                                                                                                                          | ​                                                      | The parameters for deposits on governance proposals.                                                                                                         |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2870"><code>min_deposit</code></a></p><p>​</p>                   | <p>10000000000000000000000 adydx</p><p>10,000 DYDX</p> | The minimum token deposit for a governance proposal to enter the voting period.                                                                              |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2876"><code>max_deposit_period</code></a></p><p>​</p>            | <p>172800s</p><p>~2 days</p>                           | The maximum time permitted for DYDX holders to deposit enough DYDX tokens to satisfy the `min_deposit` for a governance proposal to enter the voting period. |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2881"><code>min_initial_deposit_ratio</code></a></p><p>​</p>     | 0.20000                                                | The percentage of the `min_deposit` that needs to be submitted by the address that creates the proposal.                                                     |
| VotingParams                                                                                                                                                                                           | ​                                                      | The parameter for vote length of governance proposals.                                                                                                       |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2877"><code>voting_period</code></a></p><p>​</p>                 | <p>345600s</p><p>~4 days</p>                           | The duration of the voting period.                                                                                                                           |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2878"><code>quorum</code></a></p><p>​</p>                        | 0.33400                                                | The parameters for tallying votes on governance proposals.                                                                                                   |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2879"><code>threshold</code></a></p><p>​</p>                     | 0.50000                                                | <p>The minimum proportion of <code>Yes</code> votes for a proposal to pass.</p><p>*<code>Abstain</code> votes are not counted.</p>                           |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2880"><code>veto_threshold</code></a></p><p>​</p>                | 0.33400                                                | The minimum percentage of `NoWithVeto` votes required to reject a proposal, regardless of the number of `Yes` votes.                                         |
| BurnableParams                                                                                                                                                                                         | ​                                                      | The parameters for burning or returning a proposal deposit to depositors.                                                                                    |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2884"><code>burn_vote_veto</code></a></p><p>​</p>                | True                                                   | If `True`, this boolean parameter will burn the proposal deposit for any proposals that are vetoed.                                                          |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2882"><code>burn_vote_quorum</code></a></p><p>​</p>              | False                                                  | If `True`, this boolean parameter will burn the proposal deposit if the proposal vote does not reach `quorum`.                                               |
| <p>​</p><p><a href="https://github.com/dydxopsdao/networks/blob/fd7ee6e63e7e4b3ffab4fe600ac7cdb77c28d88d/dydx-mainnet-1/genesis.json#L2883"><code>burn_proposal_deposit_prevote</code></a></p><p>​</p> | False                                                  | If `True`, this boolean parameter will burn the proposal deposit if the proposal does not enter the voting period.                                           |

![](https://3227850899-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FcSd7APxHbsYMlFFAeIMP%2Fuploads%2FYUz56f1Vk4nFIGpnRLWv%2FdYdX%20Chain%20Governance%20Deposits%20and%20Voting\_v9.png?alt=media\&token=fd6ef09c-23a9-4391-b05f-cf2e533103d4)

### Proposal Submission and Deposits <a href="#proposal-submission-and-deposits" id="proposal-submission-and-deposits"></a>

All DYDX holders have the right to create a proposal. A DYDX holder can only use unstaked DYDX tokens to contribute to a given proposal deposit.

To create a proposal, a DYDX holder needs to send a `msgsubmitproposal` transaction and satisfy the `min_initial_deposit_ratio` parameter by sending a `deposit` transaction.

After the proposal is created, any DYDX holder can contribute to the deposit by sending a `deposit` transaction.

For the voting period to start, the `min_deposit` parameter needs to be satisfied within the `max_deposit_period`. Note, (1) the proposal is in an `inactive proposal queue` until the `min_deposit` is satisfied and (2) the `voting_period` will start as soon as the `min_deposit` is reached.

The deposit is kept in escrow and held by the governance `ModuleAccount` until the proposal is finalized (passed or rejected).

If a proposal fails to satisfy the `min_deposit` within the `max_deposit_period` and the `burn_proposal_deposit_prevote` parameter is set “`False`”, any DYDX holder who contributed to the respective deposit of a proposal will have their deposit refunded.

Governance of the dYdX Chain includes 4 distinct types of proposals: text proposals, parameter change proposals, community spending proposals, and software upgrade proposals.

Text proposals are votes that occur on-chain without directly triggering any changes on the dYdX Chain. Text proposals can be used (1) to establish dYdX community consensus for an off-chain matter, such as a strategic plan, a dYdX DAO action, or a dYdX DAO commitment, or (2) as signalling for a future vote that will directly cause changes on the dYdX Chain.

Community Spending Proposals involve a request to spend DYDX from the community treasury, community pool or any other community controlled account. The inputs for a Community Spending Proposal are (1) the number of DYDX and (2) the recipient address.

#### _Parameter Change Proposals_ <a href="#parameter-change-proposals" id="parameter-change-proposals"></a>

Parameter change proposals are for changing one or more of the dYdX Chain parameters that are controlled by the governance module.

If a parameter change proposal is successful, the parameter change takes effect in the block after the voting period ends.

#### _Software Upgrade Proposals_ <a href="#software-upgrade-proposals" id="software-upgrade-proposals"></a>

The

[upgrade module](https://docs.cosmos.network/main/build/modules/upgrade)

facilitates smoothly upgrading a live Cosmos chain to a new (breaking) software version. Software Upgrade Proposals need to be created with a `plan`. Such plan outlines when the update will occur (`block height`), the name of the new version of the software, and the `UpgradeHandler` which instructs the upgrade module how to carry out the upgrade (the latest consensus version of each module and other software).

After the dYdX community accepts a software upgrade proposal there are two important steps:

* Signal - After a `SoftwareUpgradeProposal` is accepted, validators are expected to download and install the new version of the software while continuing to run the previous version. Once a validator has downloaded and installed the upgrade, it will start signaling to the network that it is ready to switch by including the proposal's `proposalID` in its precommits.
* Switch - Once a block contains more than 2/3rd precommits where a common `SoftwareUpgradeProposal` is signaled, all the nodes (including validator nodes and full nodes) are expected to switch to the new version of the software.

The voting options for governance proposals on dYdX Chain are:

* `NoWithVeto` - allows voters to express strong disagreement with a proposal to the extent that if burn\_vote\_veto is “True” and the veto\_threshold is reached the respective deposit in the governance module account for the proposal is burned.
* `Abstain` - allows voters to signal that they do not intend to vote in favor or against the proposal but accept the result of the vote.
