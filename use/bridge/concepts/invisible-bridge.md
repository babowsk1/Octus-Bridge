---
description: Using Octus Bridge without EVER
---

# Invisible Bridge

One of the remarkable features of Octus Bridge is the **Invisible Bridge**. It enables direct fund transfers from one EVM blockchain to another within a single interface. While the networks are linked via the Everscale network, the cross-chain liquidity flow occurs seamlessly for users, making it appear as a direct transfer. This innovative solution reduces gas fees significantly, allowing users to pay these fees just once, and in the currency of their chosen EVM network.

The **Invisible Bridge** leverages a credit smart contract within the Everscale blockchain, making it possible to transfer funds between Ethereum, Polygon, and other blockchains without the need for EVER tokens in the user's wallet. The smart contract calculates, exchanges, and deducts the necessary amount for deployment and transfer fees, with minimal costs within the Everscale network. Recipients receive the funds minus the amount required for the smart contract's operation. If the user holds EVER tokens, they can use them for the transfer, and the bridge also supports direct token transfers into an EVER Wallet.

The **Invisible Bridge** operates through a separate node known as the credit processor. This node tracks transfers in different networks and provides credit in Everscale for depositing events, exchanging a portion of the transfer on DEX (Decentralized Exchange) platforms to cover these commissions.
