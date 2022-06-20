# Everscale

When some action happens on the Everscale related to the Ethereum, relayers are in charge of notifying the Ethereum. \
To make it happen, they don’t send the transaction from Everscale to Ethereum as is the case in Ethereum → Everscale. Instead of that, they sign a special payload with their private key and that is being sent to Ethereum.

These actions are described in the smart contracts that are located in this folder:

{% embed url="https://github.com/broxus/octusbridge-contracts/tree/master/everscale" %}
