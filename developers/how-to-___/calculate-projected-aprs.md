# Calculate projected APRs

Projected APRs are determined by taking the current Balancer APRs & multiplying them by the pool boost. The AURA APR is then calculated by taking the estimated boosted BAL yield per year and passing it to the `getAuraMintAmount()` function to get an estimated AURA yield per year.

To pull the current Balancer APRs, Aura uses Balancer’s `balancer-sdk` ([https://github.com/balancer-labs/balancer-sdk/](https://github.com/balancer-labs/balancer-sdk/))
