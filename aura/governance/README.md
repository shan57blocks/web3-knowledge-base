# Governance

### Context

Aura is a decentralised and community governed protocol. All actions undertaken are directed by token holders through [Aura Vote Locking](../usdaura/vote-locking.md).

The core things to be governed in the Aura system are as follows:

1. Internal proposals (e.g. setting fee rates)
2. [Aura treasury](broken-reference)
3. Balancer Snapshot voting
4. [Balancer Gauge voting](gauge-voting.md)



### How does it work

Aura has prepared for full on chain governance through the implementation of vote delegation on the Vote Locked Aura contract. With that being said, until the Aura voter base matures, a safer method will be used for executing governance decisions.

#### Phase 1 - Snapshot & multisigs

****[Snapshot](https://snapshot.org/) page will be used for all aspects (1-4) listed above. To participate in snapshot voting, community members must lock their AURA and delegate it.  Self delegation is permitted.   Results of the snapshot proposals will be executed by one of two multisigs. These entities and individual signers will be required to execute transactions in accordance with snapshot vote outcomes.

**Protocol Multisig -** Internal proposals, Gauge votes

**Treasury Multisig -** Treasury&#x20;

Read more about the [multisig composition here](multisig-composition.md).



#### Phase 2 - Full on chain voting

Provided it is technically feasible and doesn't require compromising on security, Aura is committed to transitioning this mechanism on-chain via the likes of _Governor bravo_ in the forthcoming months when appropriate.&#x20;

"Internal governance proposals (e.g. setting fee rates)" - this can be moved on chain with GovernorBravo implementation once the vote distribution is sufficiently mature

"Aura treasury" - this can be moved forward with either [Gnosis SafeSnap](https://docs.snapshot.org/plugins/safesnap) or some sort of on chain treasury management solution

"Balancer Gauge voting" - custom smart contracts can be used for this. Given the uptick in gas costs involved in voting for gauges each week, this solution may be deployed on a cheaper L2 and forwarded.

&#x20;

