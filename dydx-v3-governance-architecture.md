# dYdX v3 Governance Architecture

![](https://3227850899-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FcSd7APxHbsYMlFFAeIMP%2Fuploads%2FhkDRkgJmMu7UnU55hVHF%2FdYdX%20v3%20Governance%20Architecture.png?alt=media\&token=a81a2774-2cfa-4bc7-b120-2a4cd036ea1b)

#### V3 Governance Architecture <a href="#v3-governance-architecture" id="v3-governance-architecture"></a>

DYDX grants holders the right to propose and vote on changes to the dYdX v3 protocol on Ethereum. DYDX governance is based on the AAVE governance contracts, and supports voting based on DYDX token holdings.

Proposals must pass a given threshold and percent of yes votes based on the type of

[timelock](https://docs.dydx.community/dydx-governance/voting-and-governance/governance-parameters#timelock-parameters)

that the subject matter of the respective proposal falls under.

Per the V3 governance architecture available

[here](https://docs.dydx.community/dydx-governance/voting-and-governance/governance-process)

, there are 6 smart contracts at the core of dYdX v3 Governance on Ethereum:

* **The `DYDX Token` contract**: has snapshots of each address’ voting power at different blocks in time.
* **The `GovernanceStrategy` contract**: contains logic to measure users' relative power to propose and vote.
* **The `Safety Module` contract**: contains logics to stake DYDX tokens, tokenize the position and get rewards. Token staked the safety module retain full governance rights.
* **The `Governor` contract**: tracks proposals and can execute proposals via the Timelock smart contract.
* **The `Timelock` contracts**: can queue, cancel, or execute transactions voted by Governance. The functions in a proposal are initiated by the Timelock contract. Queued transactions can be executed after a delay and before the expiration of the grace period.
* **The `Priority Timelock` contract**: The same as the timelock contract, but allows a priority controller to execute transactions within the **Priority Period** (7 days) before the end of the timelock delay.

![](https://3227850899-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FcSd7APxHbsYMlFFAeIMP%2Fuploads%2F2GWnl0kO0875In6R51pu%2Fimage.png?alt=media\&token=2f9a859d-46f9-4105-872f-3ee98a955060)

Simplified dYdX v3 Governance Architecture

The following subset of contracts have been deployed on Ethereum mainnet:

| Contract                  | Address                                    |
| ------------------------- | ------------------------------------------ |
| DydxToken                 | 0x92D6C1e31e14520e676a687F0a93788B716BEff5 |
| DydxGovernor              | 0x7E9B1672616FF6D6629Ef2879419aaE79A9018D2 |
| Short Timelock Executor   | 0x64c7d40c07EFAbec2AafdC243bF59eaF2195c6dc |
| Rewards Treasury          | 0x639192D54431F8c816368D3FB4107Bc168d0E871 |
| Community Treasury        | 0xE710CEd57456D3A16152c32835B5FB4E72D9eA5b |
| Safety Module             | 0x65f7BA4Ec257AF7c55fd5854E5f6356bBd0fb8EC |
| GovernanceStrategy        | 0x90Dfd35F4a0BB2d30CDf66508085e33C353475D9 |
| Rewards Treasury Vester   | 0xb9431E19B29B952d9358025f680077C3Fd37292f |
| Community Treasury Vester | 0x08a90Fe0741B7DeF03fB290cc7B273F1855767D8 |

### Open-source code & audited <a href="#open-source-code-and-audited" id="open-source-code-and-audited"></a>

The source code for the governance frontend hosted at dydx.community can be found

[here](https://github.com/dydxfoundation/pnyx)

.

All major smart contracts have been audited by Peckshield. No significant or high priority security issues were found. The core governance and token contracts are forked from the Aave governance contracts which were audited by

[CertiK](https://www.certik.io/)

,

[Certora](https://www.certora.com/)

, and

[Peckshield](https://peckshield.com/en)

and have been battle-tested live on mainnet.
