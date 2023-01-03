# Security

Smart contract security is a top priority for those working on Aura Finance. All reasonable precautions must be taken to ensure the protocol is safe to use. Below is a list of some of the things we believe make smart contract systems secure.

### Audits

#### Audit 1 - Peckshield (4-18th Apr 2022)

{% file src="../../.gitbook/assets/PeckShield-Audit-Report-AuraFinance-v1.0.pdf" %}

#### Audit 2 - Code4rena (11-25th May 2022)

A $150k, 2 week long audit competition ran on [https://code4rena.com/](https://code4rena.com/) allowed anyone with knowledge of the system, or just general bug hunters, a chance to come and contribute to the security of the Aura system before launch.

{% file src="../../.gitbook/assets/Code4rena-Audit-Report-AuraFinance-v1.0.pdf" %}

#### Audit 3 - Halborn (12th May - 23rd June 2022)

A 6 week audit has been performed by Halborn Security ([https://twitter.com/HalbornSecurity](https://twitter.com/HalbornSecurity)).

{% file src="../../.gitbook/assets/Halborn-Audit-Report-AuraFinance-v1.0.pdf" %}

### Bug bounties

External bug bounties are essential for projects. Aura has placed a $1m critical bug bounty payout on Immunefi.

{% embed url="https://immunefi.com/bounty/aurafinance" %}

###

### Internal processes

#### Codebase

Some practices employed on Aura Finance smart contract repositories:

* protected `master` branch with mandatory peer reviews and passing CI (including linting, compiling, and testing)
* \>98% code coverage (using coveralls) and comprehensive integration tests
* Strict linting rules
* Code commented using the Natspec standard

#### Fork testing

Fork testing is helps simulate contract deployments and functionality in a live environment, accounting for external dependencies. Aura comprehensively tests deployments using fork tests.

#### Internal auditing

Developers know their code best, and dedicated time has been taken to manually review all code in the system.



### Contact

If you have any feedback or concerns, reach out to `security@aura.finance` or to an admin on Discord

