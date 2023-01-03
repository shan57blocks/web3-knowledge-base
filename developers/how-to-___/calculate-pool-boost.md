# Calculate pool boost

{% embed url="https://dev.balancer.fi/resources/vebal-and-gauges/estimating-gauge-incentive-aprs/apr-calculation" %}

```tsx
function getBoost() {
  const adjustedGaugeBalance =
    0.4 * gaugeBalance + ((0.6 * vebalBalance) / vebalTotalSupply) * gaugeTotalSupply;
  
  const workingBalance =
    gaugeBalance < adjustedGaugeBalance ? gaugeBalance : adjustedGaugeBalance;
  
  const zeroBoostWorkingBalance = 0.4 * gaugeBalance;
  const zeroBoostWorkingSupply = gaugeWorkingSupply - workingBalance + zeroBoostWorkingBalance;
  
  const boostedFraction = workingBalance / gaugeWorkingSupply;
  const unboostedFraction = zeroBoostWorkingBalance / zeroBoostWorkingSupply;
  
  return boostedFraction / unboostedFraction;
}
```
