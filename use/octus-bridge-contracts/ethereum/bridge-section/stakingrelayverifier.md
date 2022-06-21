# StakingRelayVerifier

#### **`verify_relay_staker_addres`**

Emits the event for verifying relayer address.

```
function verify_relay_staker_address(int8 workchain_id, uint256 address_body) external
```

**Parameters:
**
| Name         | Type    | Description               |
|--------------|---------|---------------------------|
| workchain_id | int8    | Id of the workchain       |
| address_body | uint256 | Address body of the relay |

**Events emitted:**
- RelayAddressVerified
