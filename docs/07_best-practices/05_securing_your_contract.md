---
content_title: Securing your contract
---

## Basic Recommendations

The following are basic recommendations which can be the foundation for securing your smart contract.

### 1. Authorization Checks

The following methods are available in the `EOSIO` library and they can be used to implemented authorization checks in your smart contracts:

- [`has_auth`](http://docs.eosnetwork.com/reference/mandel-cdt/group__action.html#ga9e4650a61bbe0809cc62e6b2af8252d3)
- [`require_auth`](http://docs.eosnetwork.com/reference/mandel-cdt/group__action.html#ga47b4afe79f1de07376e2ecdd541f92c7)
- [`require_auth2`](/eosdocs/smart-contracts/mandel-cdt/how-to-guides/authorization/how_to_restrict_access_to_an_action_by_user/#3-using-require_auth2)
- [`require_recipient`](http://docs.eosnetwork.com/reference/mandel-cdt/group__action.html#ga4e1838d05857e38ddf8916e616698460)

### 2. Resource Management

Understand how each of your contracts' actions is impacting the RAM, CPU, and NET consumption, and which account ends up paying for these resources.

### 3. Secure by Default

Have a solid and comprehensive development process that includes security considerations from day one of the product planning and development.

### 4. Continuous Integration And Continuous Delivery

Test your smart contracts with every update announced for the blockchain you have deployed to. To ease your work, automate the testing as much as possible so you can run them often, and improve them periodically.

### 5. Security Audits

Conduct independent smart contract audits, at least two from different organizations.

### 6. Bug Bounties

Host periodic bug bounties on your smart contracts and keep a continuous commitment to reward real security problems reported at any time.
