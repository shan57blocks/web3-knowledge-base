# Calculate APRs from Aura pool yield



*   BAL APR

    ```tsx
    const rewardPerYear = exactToSimple(rewardRate) * (86_400 * 365);
    const rewardPerYearUsd = rewardPerYear * rewardTokenPrice;
    const value = (rewardPerYearUsd / poolTVL) * 100;
    ```
* AURA APR

💡 Use the `getAuraMintAmount()` mentioned in the first section

```tsx
const auraPerYear = getAuraMintAmount(balApr.rewardPerYear, auraStaticQuery.data.global);
const auraPerYearUsd = exactToSimple(auraPerYear) * auraPrice;
const value = (auraPerYearUsd / tvl) * 100;
```
