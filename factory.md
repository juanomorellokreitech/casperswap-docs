# Factory

## **Deploying FACTORY contract manually**

```bash
sudo casper-client put-deploy \
    --chain-name chain_name \
    --node-address http://$NODE_ADDRESS:7777/ \
    --secret-key path_to_secret_key.pem \
    --session-path path_to_wasm_file \
    --payment-amount 10000000000 \
    --session-arg="public_key:public_key='Public Key In Hex'" \
    --session-arg="fee_to_setter:Key='Hash of fee-to-setter Contract'" \
    --session-arg="contract_name:string='contract_name'"
```

## **Entry point methods**

Here are the FACTORY's entry point methods.

### **create\_pair**

Creates a pair for `token_a` and `token_b` if one doesn't exist already.\
**Note:** `token_a` and `token_b` are interchangeable and The user needs to deploy the pair contract before calling the create pair method so he can pass the `Pair contract` hash as a parameter which allows the `Factory contract` to call the `initialize` methods of `Pair Contract`.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| token\_a       | Key  |
| token\_b       | Key  |
| pair\_hash     | Key  |

This method **returns** nothing.

### **get\_pair**

Returns the hash of the pair for `token0` and `token1`, if it has been created, else `“Hash-0000000000000000000000000000000000000000000000000000000000000000”`.\
**Note:** `token0` and `token1` are interchangeable.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| token0         | Key  |
| token1         | Key  |

This method **returns** a Key.

### **fee\_to**

Returns the hash of `fee_to`.

Here is the table of parameters.

This method **returns** a Key.

### **fee\_to\_setter**

Returns the hash of `fee_to_setter`.

Here is the table of parameters.

This method **returns** a Key.

### **all\_pairs**

Returns the list of all pairs created.

Here is the table of parameters.

This method **returns** a list of Keys.

### **all\_pairs\_length**

Returns the total number of pairs created through the `factory` so far.

Here is the table of parameters.

This method **returns** a U256.

### **set\_fee\_to**

this will set the hash of `fee_to`\
**Note:** Only `fee_to_setter` can set the `fee_to`

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| fee\_to        | Key  |

This method **returns** nothing.

### **set\_fee\_to\_setter**

this will set the Hash of `fee_to_setter`\
**Note:** Only `fee_to_setter` can set the `fee_to_setter`

Here is the table of parameters.

| Parameter Name  | Type |
| --------------- | ---- |
| fee\_to\_setter | Key  |

This method **returns** nothing.
