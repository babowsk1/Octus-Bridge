# Octus Bridge relayers

The job of a bridge relayer (aka validator) is to come to a consensus about whether a transaction was actually made in one network and issue the appropriate amount of tokens in the other.

Failure to do so will cause the bridge to fail. However, interest in becoming validation nodes is fueled by issuing rewards for proper operation. Therefore, the bridge will never stop.

Technically, you shouldn't compare a relayer to a stacker. Although the former also receives cryptocurrency, but by a different algorithm. Mining nodes appear to be a subset of validator nodes.

The system also accounts for irresponsible users getting into relayers. The protection against unscrupulous relayers is a slashing mechanism, thanks to which relayer loses part or all of its steak if it tries to send a transaction that doesn't exist. And that's why you have to have a minimum steak size of 100,000 BRIDGE to be a bridge relayer.
