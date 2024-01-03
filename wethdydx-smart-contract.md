# wethDYDX Smart Contract

![](https://3227850899-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FcSd7APxHbsYMlFFAeIMP%2Fuploads%2F4UH1zjvTC2dNjjmCA9hP%2FwethDYDX%20Smart%20Contract.png?alt=media\&token=b10bdc90-c9dd-4bbd-9f03-3318c28320fc)

**The `wethDYDX Smart Contract` enables a permissionless and autonomous one-way bridge for the `ethDYDX` token to be migrated from Ethereum to the dYdX Chain. The dYdX Foundation will not provide a user interface or front-end related to access the `wethDYDX Smart Contract`.**

**Neither the dYdX Foundation or any other party will be able to exercise any kind of power over the `wethDYDX Smart Contract`. Consequently, the dYdX Foundation does not make any representations, warranties, or covenants as to the technical properties, performance and will not be responsible for the use made by the people of the `wethDYDX Smart Contract`, including, without limitation, with regard to (i) potential deployments of the `wethDYDX Smart Contract`, (ii) potential adaptations, forks or modified versions of the `wethDYDX Smart Contract`, and its deployment, or (iii) users’ interactions with the `wethDYDX Smart Contract`.**

**Note, users should refrain from interacting with the `wethDYDX Smart Contract` without proper knowledge of how to derive private keys on the dYdX Chain.**

When interacted with, the one-way bridge `wethDYDX Smart Contract` would carry out the following functions in a fully permissionless and automated manner:

**Step 1:** Receive and permanently lock the `ethDYDX` tokens sent by the user to the `wethDYDX Smart Contract,`

![](https://3227850899-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FcSd7APxHbsYMlFFAeIMP%2Fuploads%2FgzxIkOwSyHvlPc0TDrze%2FBridging%20Step%204.png?alt=media\&token=93b129ae-2c53-4102-8100-942ea3fa0943)

**Step 2:** Send `wethDYDX` to the user on a 1-1 proportion basis on Ethereum, and

![](https://3227850899-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FcSd7APxHbsYMlFFAeIMP%2Fuploads%2FRJQZ8MAkfVL83xoz9VpY%2FBridging%20Step%205.png?alt=media\&token=65c64c7c-880e-43a7-8e1b-7e73692a5075)

**Step 3:** dYdX Chain validators can also read and ingest the information in the `wethDYDX Smart Contract` such that corresponding DYDX can be distributed to users by validators on the dYdX Chain once there is confirmation that Step 1 above is complete and the ethDYDX is permanently locked in the `wethDYDX Smart Contract`.

For users who migrate(d) their `ethDYDX` tokens to the dYdX Chain using the `wethDYDX Smart Contract`referred to in this documentation, the method that users would be credited with DYDX tokens on the dYdX Chain is expected to depend on when they interact with the `wethDYDX Smart Contract`, as follows:

* **Step 3(a):** If a user interacted with the `wethDYDX Smart Contract` before a certain cut-off date prior to the genesis of the dYdX Chain (“Genesis”), the amount of `ethDYDX` tokens sent by the user to the `wethDYDX Smart Contract` was registered as event information in the `wethDYDX Smart Contract`. At this point, the user’s dYdX Chain wallet could not be allocated with DYDX tokens because the dYdX Chain did not exist yet.

![](https://3227850899-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FcSd7APxHbsYMlFFAeIMP%2Fuploads%2FxubMPtHnw5WUOUEGz7MX%2FBridging%20Step%203\(a\)%20\(2\).png?alt=media\&token=adc12c8a-fd59-4e2a-8f2d-2fc2209a7f97)

* **Step 3(b):** If a user interacts with the `wethDYDX Smart Contract` (after Genesis), then each dYdX Chain validator participating in the consensus process would read the event information of the `wethDYDX Smart Contract` and allocate DYDX tokens on the dYdX Chain to a given user’s dYdX Chain address based on the corresponding amount (1-1) of `ethDYDX` tokens that the user sent to the `wethDYDX Smart Contract`.

![](https://3227850899-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FcSd7APxHbsYMlFFAeIMP%2Fuploads%2Fdh0ghpQfbWw70cIdEViO%2FBridging%20Step%203\(b\)%20\(4\).png?alt=media\&token=fb29a20f-c746-493f-beed-4d44c909dca3)

#### `Wrapped Ethereum DYDX (wethDYDX)` <a href="#wrapped-ethereum-dydx-wethdydx" id="wrapped-ethereum-dydx-wethdydx"></a>

`The wethDYDX` token contract is a new ERC-20 contract that is similar to the`DYDX` token contract with the following specifications:

* A new `bridge()` function that takes `ethDYDX` tokens from the caller and mints them an equivalent amount of `wethDYDX` tokens
  * This function will emit an event log indicating it has occurred
  * **Note, there is no way to reverse the bridge function**
* No transfer or minting restrictions
*
  * `NAME`: Wrapped Ethereum DYDX

**Transferability and Utility**

The `wethDYDX` token is freely transferable like a normal ERC-20 contract.

On September 24, 2023, the dYdX community almost unanimously

[supported](https://dydx.community/dashboard/proposal/15)

upgrading the `GovernanceStrategy Smart Contract` to v2. This upgrade ratified the implementation of wethDYDX into dYdX v3’s governance system so that wethDYDX has the same voting and proposal power as ethDYDX.

Similar to `DYDX`, if the market value of `wethDYDX` drops, it may introduce a governance security issue because the `wethDYDX` tokens retain the same voting rights as the `ethDYDX` token.

The `wethDYDX Smart Contract` emits an event log in order for the dYdX Chain to understand when a call to `bridge()` has occurred.

Below are some helpful links that describe Ethereum logs:

*   Event logs on the Ethereum blockchain (

    [link](https://medium.com/mycrypto/understanding-event-logs-on-the-ethereum-blockchain-f4ae7ba50378)

    )
*   Deep-dive on `eth_getLogs` RPC call (

    [link](https://docs.alchemy.com/docs/deep-dive-into-eth\_getlogs)

    )

The following log would be emitted:

The description of each field in the log is as follows:

* `id` is an incrementing number guaranteed to be unique for each log with no gaps.
  * `id` allows anyone to refer to a unique event easily.
  * `id` allows de-duplication of event processing by the v4 chain without requiring additional storage for each unique event. If the chain processes each `eventId` in order, then it can store a single integer of the most recently processed`eventId`.
* `amount` is the amount of `ethDYDX`tokens that was transferred.
* `from` is the Ethereum address the `ethDYDX` tokens were transferred from.
* `accAddress` is the address to which the **L1 token of the dYdX Chain** should be minted. This field is an arbitrary value provided by the caller of the function.
* `data` is additional arbitrary data that the caller provides. This field can be used to signal additional intent. For example, it can be used when migrating funds from a treasury to indicate that the funds should not go to a normal end-user account and instead should be bridged to a module account.

### Locked Tokens Transfer Restrictions <a href="#locked-tokens-transfer-restrictions" id="locked-tokens-transfer-restrictions"></a>

Per the original blog

[post](https://dydx.foundation/blog/introducing-dydx-token)

introducing `ethDYDX`, 50% of the 1 billion supply of `ethDYDX` was reserved for:

* past investors of dYdX Trading Inc. (27.7%),
* founders, employees, advisors, and consultants of dYdX Trading Inc. and dYdX Foundation (15.3%); and,
* future employees and consultants of dYdX Trading Inc. or dYdX Foundation (7.0%).

Certain `ethDYDX` tokens held by investors and team members are subject to transfer restrictions. Those `ethDYDX` tokens are referred to as locked tokens (the "**Locked Tokens**"). The transfer restriction shall expire pursuant to a schedule that is publicly available and can be viewed

[here](https://dydx.foundation/blog/lock-up-extension)

.

Locked Tokens will be released from the transfer restrictions on the same schedule as follows:

* 30% on December 1, 2023 (the “Initial Unlock Date”);
* 40% in equal monthly installments on the first day of each month from January 1, 2024, to June 1, 2024;
* 20% in equal monthly installments on the first day of each month from July 1, 2024, to June 1, 2025; and
* 10% in equal monthly installments on the first day of each month from July 1, 2025, to June 1, 2026.

All employees and consultants with ethDYDX tokens are also subject to various vesting schedules that could result in them losing their right to receive Locked Tokens.

**Bridging & Staking Locked Tokens**

Locked Tokens can still be bridged from Ethereum to the dYdX Chain via the `wethDYDX Smart Contract`, and like all other `ethDYDX` token-holders, the locked ethDYDX token-holders will be entitled to receive:

1.  1\.

    `wethDYDX`, on a 1-1 proportional basis, on Ethereum, and
2.  2\.

    `DYDX` tokens, on a 1-1 proportional basis, on the dYdX Chain.

Any `wethDYDX` and/or dYdX-Chain `DYDX` tokens received in exchange for locked `ethDYDX` tokens shall continue to be subject to the same transfer restrictions and release schedule. As with the current locked `ethDYDX` tokens, locked wethDYDX tokens and locked dYdX-Chain `DYDX` tokens may also be bridged to another blockchain, used for voting or delegating purposes and/or staked to a validator, if applicable.

How is accAddress on the dYdX Chain derived?

Interacting with the `wethDYDX Smart Contract` will involve using an Ethereum private key to generate a mnemonic/master private key and that mnemonic can be used to create accounts across any Cosmos chain.

What fees are payable in connection with the token migration (gas fees on either of the two networks and/or other applicable fees)?

`ethDYDX` holders that are transfering `ethDYDX` to the `wethDYDX Smart Contract` will only need to pay gas fees one time to send ethDYDX to the `wethDYDX Smart Contract` and to receive `wethDYDX`.

Is wethDYDX transferable?

`wethDYDX` is an ERC-20 token and is freely transferable.

Can wethDYDX be sent to the bridge (`wethDYDX Smart Contract)` ?

No. `wethDYDX` can not be sent to the bridge (`wethDYDX Smart Contract)`. Note, there is no way to reverse the bridge function.

Can wethDYDX be staked / sent to the Safety Module?

Initially, `wethDYDX` cannot be staked to the Safety Module. The Safety Module on dYdX v3 is no longer active as of November 28, 2022. In

[DIP 17](https://dydx.community/dashboard/proposal/9)

, the dYdX community

[voted](https://dydx.community/dashboard/proposal/7)

to effectively wind down the Safety Module by setting the Safety Module rewards per second to 0. The dYdX community through dYdX Governance on dYdX v3 could upgrade the Safety Module to accept `wethDYDX` as another form of collateral.
