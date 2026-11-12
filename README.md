# clone-lin-aave-irm

Experimental LIN clone of Aave V3 `DefaultReserveInterestRateStrategy.calculateInterestRates` **variable** branch (RAY'=1e9, two-slope kink, 128-bit half-up `rayMul`/`rayDiv`/`percentMul`). `IERC20.balanceOf` and immutable slopes are function arguments. Stable-rate branch is out of scope.

- **Upstream:** [aave/aave-v3-core](https://github.com/aave/aave-v3-core) `contracts/protocol/pool/DefaultReserveInterestRateStrategy.sol` commit `782f51917056a53a2c228701058a6c3fb233684a` (MIT after BUSL-1.1 Change Date 2023-01-27). Solidity is not vendored.
- **LIN kernel:** [`src/lin_aave_irm.lin`](src/lin_aave_irm.lin)
- **C11 oracle copy:** [`test/oracles/aave_irm_c11.c`](test/oracles/aave_irm_c11.c)
- **Proofs (lin-open only):** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/aave_irm/` and `python3 test/prove_aave_irm_external.py`
- **Class:** EXPERIMENTAL. Not Ethereum Aave V3 uint256. Not RAY 1e27. Not a production replacement. Distinct from `clone-lin-aave-wadray` / `clone-lin-aave-raytowad` / `clone-lin-aave-percent`.

Named goldens (RAY'=1e9, optimal=0.8e9, slope1=0.04e9, slope2=0.8e9, rf=15%): `rayMul(1, 5e8)` → **1** vs floor **0**; `rayDiv(2, 3)` → **666666667** vs floor **666666666**; variable rate 50% util → **25000000**; 80% kink → **40000000**; 90% → **440000000**; liquidity rate 50% util → **10625000**. Naive i64 `1e10*1e10` wraps; 128-bit `rayMul` → **100000000000**.
