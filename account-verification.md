## Motivation

The number of sybil (fake, duplicate) accounts from which a group of attackers can benefit should be limited. To this end, each account must be *verified* to perform important functions like running a node, or to receive benefits that require a unique identity, such as basic income from a basic income distribution application. This is done by analyzing the social graph.

## Verification Process

Accounts are verified when _v_ (a variable agreed upon by the network) already verified accounts have made a connection to the account (with an additional *non-combining restriction*, outlined below). The newly-verified account is known as a _recruit_ and the accounts used to verify it are known as _verifiers_.

A potential recruit submits the identities (public keys) of the proposed verifiers to the network which checks that the needed connections exist and also checks the non-combining restriction.  If these checks pass, the account is marked as verified and listed as a recruit of each of the verifiers.

The non-combining restriction is as follows. Each verifier has a set of other verifiers with which it can't combine to verify a recruit: these are its _non-combinable-verifiers_. The set of non-combinable-verifiers for verifier __V1__ is created by starting with __V1__, traversing the paths connecting recruits and verifiers for four steps<sup>[1](#foot1)</sup>, and adding all the verifiers encountered.  The number of steps is always four, regardless of _v_.

![figure: non-combinable-verifiers](images/non-combinable-verifiers.svg)

(The verifiers along the top row of the figure make up the set of non-combinable-verifiers for verifier __V1__)

It's the responsibility of a potential recruit (or a client program acting on her behalf) to find and submit verifiers that pass the non-combining restriction; the network is then responsible for checking them.  The network can be queried for any account's non-combinable-verifiers to help with this process.

## Limits to Attackers

The number of sybils a group of colluding attackers can verify is 

![ceil(n/(v-1))-1; v >= 2](images/sybil-formula1.png)

without reusing new sybils for verification, and

![ceil(n/(v-2))-1; v >= 3](images/sybil-formula2.png)

when reusing new sybils for verification, where _v_ is the network variable representing the number of verifiers required per recruit and _n_ is the number of colluding attackers.

For example, with 4 verifications needed per recruit and 300 colluding attackers, 99 sybils could be verified initially and 149 total if the new sybils are reused for verification.

When _v_ >= 3, _s_ will be less than _n_, meaning each attacker will verify less than one sybil account.  This means that to share the benefits of the attack, attackers must continue to collude and share accounts, making the attack more difficult.

----
#### Notes
<a name="foot1">1</a> Adding more than four steps doesn't additionally limit the number of sybils a group of attackers can verify.<sup>[Proof needed]</sup>
