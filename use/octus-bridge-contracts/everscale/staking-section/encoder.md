# Encoder

#### **`encode_uint8`**	

Converts uint8 to cell.

```
function encode_uint8(uint8 num) external responsible pure returns (TvmCell)
```

**Parameters:**

| Name | Type  | Description               |
|------|-------|---------------------------|
| num  | uint8 | uint8 value to be encoded |

**Return value:**

| Type    | Description                   |
|---------|-------------------------------|
| TvmCell | Encoded number to cell format |

#### **`encodeEthereumStakingEventData`**	

Converts Ethereum staking event data to cell.

```
function encodeEthereumStakingEventData(uint160 eth_addr, int8 wk_id, uint256 ton_addr_body) public pure returns (TvmCell data)
```

**Parameters:**

| Name          | Type    | Description             |
|---------------|---------|-------------------------|
| eth_addr      | uint160 | Ethereum address        |
| wk_id         | int8    | Workchain id            |
| ton_addr_body | uint256 | Body of the ton address |

**Return value:**

| Name | Type    | Description                                 |
|------|---------|---------------------------------------------|
| data | TvmCell | Ethereum staking event data encoded to cell |
