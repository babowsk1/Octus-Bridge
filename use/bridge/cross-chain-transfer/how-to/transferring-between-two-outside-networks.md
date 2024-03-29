# Transferring between two outside networks

### Connect wallets

To get started you need to connect wallets to the Octus Bridge interface, which will be used to interact with the selected networks and pay commissions, respectively.

Click `Connect Wallet` and [connect both wallets](../../../getting-started/how-to-connect-wallets.md#connect-wallets).

### Source and target blockchain

To get started, go to the `Cross-Chain Transfer` page using the `Bridge` button at the top of the page.

Here you can select the source and destination network for the transfer.

`From` refers to the network from which you plan to withdraw tokens, and `To` refers to the network to which tokens will be sent.

You can also enter the `recipient's wallet address` manually, but the gas commission will be debited from the account of the connected wallet.

![](<../../../../.gitbook/assets/image (36).png>)

### Select token and amount

Click `Next` to go to the `Select token and amount` page.\
Here you need to select the token that you want to transfer to another network and also enter the amount of tokens to be transferred.\
You can see a list of all tokens available for sending on the corresponding page.

{% content-ref url="../../concepts/available-chains-and-assets.md" %}
[available-chains-and-assets.md](../../concepts/available-chains-and-assets.md)
{% endcontent-ref %}

Review the number of tokens that you will receive as a result of the operation and click **Next**.

![](<../../../../.gitbook/assets/image (51).png>)

### Permission to use tokens

At this step, you need to grant Octus Bridge permission to use tokens from the balance of your address. There are two types of permission:

1. You can confirm an infinite amount so that you do not have to pay for confirmation later if you decide to make another transfer.
2. You can choose to only confirm the amount required for this transfer.

{% hint style="info" %}
Regardless of your choice, the bridge will only use the amount you ask for.
{% endhint %}

After choosing one of the options, click `Confirm` and confirm the action in your wallet (the window should open automatically).\
Then you can proceed to the next step.

![](<../../../../.gitbook/assets/image (45).png>)

### Transfer status

The `Transfer status` page displays the steps in the transfer process.\
At this step, the tokens are directly sent to the selected network.\
Basically all you have to do is wait. The whole process happens automatically, you only need to make a few clicks on the site itself and inside the wallet to confirm the operation and pay commissions.\
Octus Bridge will keep you informed every step of the transaction so you don't have to worry about getting your funds.

{% hint style="warning" %}
**Please note that all subsequent actions are irreversible!** Tokens will be debited from your wallet and will not be available until you complete the transfer.
{% endhint %}

First, click on `Transfer` to send your tokens to the source network storage.\
Confirm this action in your wallet and wait for a while for the action to complete.

![](<../../../../.gitbook/assets/image (1) (1).png>)

After a while, you will see that the status of this action has changed to `Confirmed.`\
Now you need to prepare tokens for sending to the Everscale network.\
Click `Prepare` and confirm the action in the wallet.

Wait until all statuses change to `Confirmed` - it won't take long.

There will be a notification that the Metamask network is not configured properly, this is not a problem, click `Edit Network` tab, this will take you to a screen that will allow you to change the network in the Metamask.

![](<../../../../.gitbook/assets/image (37).png>)

After successfully completing all the steps, a window will open informing you that the transfer was completed successfully and the corresponding tokens will be added to your balance.
