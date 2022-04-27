# WCSPR

## **Deploying WCSPR contract manually**

If you need to deploy the `WCSPR contract` manually add some of these parameters. Here is the command template to deploy the `WCSPR contract`.

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
    --session-arg="contract_name:string='contract_name'"
```

## **Entry point methods**

Here are the WCSPR's entry point methods.

### **transfer**

Let `self.get_caller()` send pool tokens to a recipient hash.

Hare is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| recipient      | Key  |
| amount         | U256 |

This method **returns** nothing.

### **transfer\_from**

Sends pool token's from one hash to another.\
User needs to call `approve` method before calling the `tranfer_from`.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| owner          | Key  |
| recipient      | Key  |
| amount         | U256 |

This method **returns** nothing.\
**Recommendation:**

Awareness of possible exploits should be taken into account. Usage of functions that increase/decrease the allowance relative to its current value is highly encouraged. We recommend that developers of applications dependant on approve() / transferFrom() should keep in mind that they set allowance to 0 first and verify if it was used before setting the new value.\
**Note:** Teams who decide to wait for such a standard should make these recommendations to app developers who work with their token contract.

### **approve**

Let `self.get_caller()` set their allowance for a spender.\
the user needs to call this `approve` method before calling the `transfer_from` method.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| spender        | Key  |
| amount         | U256 |

This method **returns** nothing.\
**Recommendation:**

Awareness of possible exploits should be taken into account. Usage of functions that increase/decrease the allowance relative to its current value is highly encouraged. We recommend that developers of applications dependant on approve() / transferFrom() should keep in mind that they set allowance to 0 first and verify if it was used before setting the new value.\
**Note:** Teams who decide to wait for such a standard should make these recommendations to app developers who work with their token contract.

### **balance\_of**

This method will return the balance of the owner in `WCSPR Contract` .

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| owner          | Key  |

This method **returns** an U256.

### **allowance**

Returns the amount of liquidity tokens owned by a hash that a spender is allowed to transfer via `transfer_from`.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| owner          | Key  |
| spender        | Key  |

This method **returns** an U256.

### **total\_supply**

Returns the total amount of pool tokens for a pair.

This method **returns** an U256.

### **deposit**

This method deposits the number of tokens against the hash, both provided by the user.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| to             | Key  |
| purse          | URef |

This method **returns** nothing.

### **withdraw**

This method withdraws the number of tokens against the hash, both provided by the user.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| to             | Key  |
| amount         | U256 |

This method **returns** nothing.\
**Note:** To `withdraw` the tokens against the hash provided by the user, User needs to `deposit` tokens first in `WCSPR`.

### **name**

Returns the `name` of tokens for a pair.

Here is the table of parameters.

This method **returns** String.

### **symbol**

Returns the `symbol` of tokens for a pair.

Here is the table of parameters.

This method **returns** String.
