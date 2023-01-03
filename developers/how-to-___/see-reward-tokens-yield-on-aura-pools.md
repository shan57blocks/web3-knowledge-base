# See reward tokens / yield on Aura Pools



*   Select the pool, navigate to the Info tab and open the _**Rewards Contract Address**_ in etherscan



    ![Screenshot 2022-11-01 at 10.53.01.png](<../../.gitbook/assets/Screenshot 2022-11-01 at 10.53.01.png>)

    * `rewardRate` is the reward rate for BAL per second
    * `extraRewards(N)` is the contract address for additional rewards (outside of AURA, BAL, ie. LDO, bb-a-USD)
    *   AURA is minted pro-rata to BAL accrued.

        * The formula for determining how much AURA is emitted per BAL can be found here:[https://etherscan.io/token/0xC0c293ce456fF0ED870ADd98a0828Dd4d2903DBF#code#F1#L85](https://etherscan.io/token/0xC0c293ce456fF0ED870ADd98a0828Dd4d2903DBF#code#F1#L85)
        * A chart can be found here:[https://docs.google.com/spreadsheets/d/16VSvgp-ejkra03ykyh-2nlxeCMEDvBZ-LFjuaQo6Ym8/](https://docs.google.com/spreadsheets/d/16VSvgp-ejkra03ykyh-2nlxeCMEDvBZ-LFjuaQo6Ym8/)
        * A typescript implementation can be found here:



        ```tsx
        export const getAuraMintAmount = (
          balEarned: number,
          global: Omit<Global, 'auraMinter' | 'auraMinterMinted'>,
        ) => {
          const reductionPerCliff = BigNumber.from(global.auraReductionPerCliff);
          const maxSupply = BigNumber.from(global.auraMaxSupply);
          const totalSupply = BigNumber.from(global.auraTotalSupply);
          const totalCliffs = BigNumber.from(global.auraTotalCliffs);
          const minterMinted = BigNumber.from(0);
         
          // e.g. emissionsMinted = 6e25 - 5e25 - 0 = 1e25;
          const emissionsMinted = totalSupply.sub(maxSupply).sub(minterMinted);
         
          // e.g. reductionPerCliff = 5e25 / 500 = 1e23
          // e.g. cliff = 1e25 / 1e23 = 100
          const cliff = emissionsMinted.div(reductionPerCliff);
         
          // e.g. 100 < 500
          if (cliff.lt(totalCliffs)) {
            // e.g. (new) reduction = (500 - 100) * 2.5 + 700 = 1700;
            // e.g. (new) reduction = (500 - 250) * 2.5 + 700 = 1325;
            // e.g. (new) reduction = (500 - 400) * 2.5 + 700 = 950;
            const reduction = totalCliffs.sub(cliff).mul(5).div(2).add(700);
            // e.g. (new) amount = 1e19 * 1700 / 500 =  34e18;
            // e.g. (new) amount = 1e19 * 1325 / 500 =  26.5e18;
            // e.g. (new) amount = 1e19 * 950 / 500  =  19e17;
            let amount = simpleToExact(balEarned).mul(reduction).div(totalCliffs);
         
            // e.g. amtTillMax = 5e25 - 1e25 = 4e25
            const amtTillMax = maxSupply.sub(emissionsMinted);
            if (amount.gt(amtTillMax)) {
              amount = amtTillMax;
            }
         
            return amount;
          }
         
          return BigNumber.from(0);
        };
        ```

