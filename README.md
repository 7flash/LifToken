# Líf Token

Líf is the token of the Winding Tree platform.

Líf is a SmartToken, based in the ERC20 standard with extra methods to send value and data on transfers and approvals, allowing the execution of calls in those methdos too.

This repository also has all the contracts related to the Token Generation Event (TGE).

[![Build Status](https://travis-ci.org/windingtree/LifToken.svg?branch=master)](https://travis-ci.org/windingtree/LifToken)
[![Coverage Status](https://coveralls.io/repos/github/windingtree/LifToken/badge.svg?branch=master)](https://coveralls.io/github/windingtree/LifToken?branch=master&v=2.0)

## Contracts

- [SmartToken](blob/master/contracts/SmartToken.sol): Token based in the ERC20 standard with extra methods to transfer value and data and execute a call on transfer. Uses OpenZeppelin StandardToken.
- [LifToken](blob/master/contracts/LifToken.sol): Smart token for the Winding Tree platform.
 Uses SmartToken and OpenZeppelin MintableToken and Pausable contracts.
- [LifCrowdsale](blob/master/contracts/LifCrowdsale.sol): Implementation of the Lif Token Generation Event (TGE):
  - 2 weeks duration
  - fixed price (1st week: 1 ETH = 10 lifs, 2nd week: 1 ETH = 9 lifs)
  - soft cap: USD $10M
  - the funds in excess of the soft cap will be automatically transferred to the Market Validation Mechanism smart contract
- [LifMarketValidationMechanism](blob/master/contracts/LifMarketValidationMechanism.sol): The MVM is designed to provide validation to the project by incentivizing the team and at the same time preventing them to control a large sum of money from day one.
  - the MVM will hold funds from the TGE in excess of the soft cap of USD $10M (e.g. if the TGE raised $25M, the MVM would receive $15M)
  - the MVM will be making a certain amount of funds available to the foundation every month, with most of the funds released by the end of the MVM lifetime
  - Líf holders will be able to send their tokens to the MVM in exchange for ETH at a rate that complements the distribution curve (the rate is higher at the beginning of the MVM and goes towards 0 by the end of it). The received tokens are instantly burned
  - The MVM will run for 24 months if the total amount raised is less than $40M, otherwise its duration period will be 48 months
- [VestedPayment.sol](blob/master/contracts/VestedPayment.sol): Handles two time-locked transactions
  - the 20% extra tokens that the foundation will receive immediately after the TGE
  - the 5% extra tokens that the foundation will receive after the MVM finishes, with the same duration as the MVM: 2 or 4 years

## Requirements

Node v7.6 or higher (versions before 7.6 do not support async/await that is used in the LifToken tests)

## Install

```sh
npm install
```

## Test

* To run all tests: `npm test`

* To run a specific test: `npm test -- test/Crowdsale.js`

There are also two environment variables (`GEN_TESTS_QTY` and `GEN_TESTS_TIMEOUT`) that regulate the duration/depth of the property-based tests, so for example:

```sh
GEN_TESTS_QTY=50 GEN_TESTS_TIMEOUT=300 npm test
```

Will make the property-based tests in `test/CrowdsaleGenTest.js` to run 50 examples in a maximum of 5 minutes

## License

Líf Token is open source and distributed under the GPL v3 license.
