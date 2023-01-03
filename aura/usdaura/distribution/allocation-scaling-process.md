---
description: How are balances scaled for airdrops
---

# Allocation scaling process

### Process outline

1. A snapshot of data is gathered for the following, at a block height not made available in advance:
   1. BAL holders (including wallet balances, major BAL liquidity provision, incl. 80BAL-20WETH)
   2. Voters of the Aura proposal on Balancer’s Snapshot
   3. Vote-locked Convex (vlCVX) holders
   4. LobsterDAO NFT holders
2. Holder addresses are filtered:
   1. “Infrastructure” (e.g. CEX) addresses are removed
   2. Addresses which are not either EOAs or Gnosis Safe multi-sigs are removed
   3. Balancer DAO addresses are removed
3. Top-level allocations of AURA are defined for different groups.
4. The allocations are calculated for each group (explained below).
5. The allocations for each group are combined into a single allocation for each user.
6. A Merkle tree is generated for the combined allocations, and a number of artefacts are output:
   1. Address⇒Allocation table as CSV and JSON
   2. Merkle proofs for every address with a claim
   3. Interactive tree map to visualise all holdings

### Calculating allocations

1.  For each group with a top-level allocation (Balancer, Convex, LobsterDAO):
    1. Apply redirections
       * Verified redirections (e.g. for BadgerDAO and individuals) are applied to underlying balances
    2. Initial rescale
       * Considered balances are rescaled in order to reduce whale dominance and create a fairer distribution.
       * Get the relevant unscaled balance for each user (e.g. for Balancer, each user’s total BAL holdings we captured).
       * Get the largest holding value to establish the domain of values (i.e. the considered range of balances).
       * Given the domain, create a power scaling function with an exponential transform which will be applied to each value
         * The exponent being used is `0.75`.
         * Each range value _y_ can be expressed as a function of the domain value _x: y = mx^k + b_, where _k_ is the exponent value.
         * This creates an array of multipliers that scale balances according to the balance and the considered domain.
       * Get the share of the allocation for all the multipliers, and simply multiply the unscaled balances by this share.
       * This yields fairly rescaled values according to the power scale we defined for each group.
    3. Cull shrimp
       * Given a minimum claim size of `50 AURA` per account, remove all claimants under this threshold.
    4. Final rescale
       * Same process as initial rescale; claimants that were not filtered out will receive more AURA.

    At each step, key metrics are logged out and the Gini coefficient is calculated to ensure that rescaling has the desired effect.

**IMPORTANT**: Snapshots of eligible addresses were taken with block heights before this information was posted, to avoid gaming of these airdrop allocations
