# ERC-20

## **Deploying ERC20 contract manually**

If you need to deploy the `ERC20 contract` manually you will need to pass some parameters. The following command is a template to deploy the `ERC20 contract`.

```bash
sudo casper-client put-deploy \
    --chain-name chain_name \
    --node-address http://$NODE_ADDRESS:7777/ \
    --secret-key path_to_secret_key.pem \
    --session-path path_to_wasm_file \
    --payment-amount 10000000000 \
    --session-arg="public_key:public_key='Public Key In Hex'" \
    --session-arg="name:string='token-name'" \
    --session-arg="symbol:string='token-symbol'" \
    --session-arg="decimals:u8='unsigned integer value'" \
    --session-arg="initial_supply:u256='unsigned integer value'" \
    --session-arg="contract_name:string='contract_name'"
```

## **Entry point methods**

The follow items are the ERC20's entry point methods.

### **transfer**

Let's `self.get_caller()` send pool tokens to a recipient hash.

This is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| recipient      | Key  |
| amount         | U256 |

This method **returns** nothing.

### **transfer\_from**

Sends pool tokens from one hash to another.\
User needs to call approve method before calling the `tranfer_from`.

This is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| owner          | Key  |
| recipient      | Key  |
| amount         | U256 |

This method **returns** nothing.\
**Recommendation:**

Awareness of possible exploits should be taken into account. Usage of functions that increase/decrease the allowance relative to its current value is highly encouraged. We recommend that developers of applications dependant on approve() / transferFrom() should keep in mind that they set allowance to 0 first and verify if it was used before setting the new value.\
**Note:** Teams who decide to wait for such a standard should make these recommendations to app developers who work with their token contract.

### **permit**

Sets the allowance for a spender where approval is granted via a signature.

Following is the table of parameters.

| Parameter Name | Type   |
| -------------- | ------ |
| public         | String |
| signature      | String |
| owner          | Key    |
| spender        | Key    |
| value          | U256   |
| deadline       | u64    |

This method **returns** nothing.

### **approve**

Lets `self.get_caller()` set their allowance for a spender.\
user needs to call this `approve` method before calling the `transfer_from` method.

Following is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| spender        | Key  |
| amount         | U256 |

This method **returns** nothing.\
**Recommendation:**

Awareness of possible exploits should be taken into account. Usage of functions that increase/decrease the allowance relative to its current value is highly encouraged. We recommend that developers of applications dependant on approve() / transferFrom() should keep in mind that they set allowance to 0 first and verify if it was used before setting the new value.\
**Note:** Teams who decide to wait for such a standard should make these recommendations to app developers who work with their token contract.

### **balance\_of**

This method returns the balance of `owner` in `ERC20 Contract`.

Following is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| owner          | Key  |

This method **returns** an U256.

### **nonce**

Returns the current `nonce` for an address for use in `permit`.

Following is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| owner          | Key  |

This method **returns** an U256.

### **allowance**

Returns the amount of liquidity tokens owned by an hash that a spender is allowed to transfer via `transfer_from`.

Following is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| owner          | Key  |
| spender        | Key  |

This method **returns** an U256.

### **total\_supply**

Returns the total amount of pool tokens for a pair.

Following is the table of parameters.

This method **returns** an U256.

### **mint**

This method mints the number of tokens provided by user against the hash provided by user.

Following is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| to             | Key  |
| amount         | U256 |

This method **returns** nothing.

### **burn**

This method burns the number of tokens provided by user against the hash provided by user.

Following is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| from           | Key  |
| amount         | U256 |

This method **returns** nothing.\
**Note:** To `burn` the tokens against the hash provided by user, User needs to `mint` tokens first in `ERC20`.

### **name**

Returns the `name` of tokens for a pair.

Following is the table of parameters.

This method **returns** a String.

### **symbol**

Returns the `symbol` of tokens for a pair.

Following is the table of parameters.

This method **returns** a String.
