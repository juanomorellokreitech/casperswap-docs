# PAIR

## **Deploying PAIR contract manually**

If you need to deploy the `PAIR contract` manually you will need to pass the hashes of the other contracts as parameters. Here is the command template to deploy the `PAIR contract`.

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
    --session-arg="factory_hash:Key='Hash of factory Contract'" \
    --session-arg="callee_contract_hash:Key='Flash Swapper Contract Hash'" \
```

Before deploying `PAIR Contract`, you will need to deploy other contracts first and pass hashes of these contracts to the respective parameters above. We have already deployed these contracts and the tables belows displays the hashes of the contracts.

| Name          | Network | Account info contract hash                                              | Contract owner     |
| ------------- | ------- | ----------------------------------------------------------------------- | ------------------ |
| Factory       | Testnet | `hash-13cc83616c3fb4e6ea22ead5e61eb6319d728783ed02eab51b1f442085e605a7` | Casper Association |
| Flash Swapper | Testnet | `hash-1c23f9e89033e5c2d2a21a6926411b2645c000cf43fc0db495821633da2aed6e` | Casper Association |

### Manual Deployment <a href="#pair-manual-deployment" id="pair-manual-deployment"></a>

For manual deployments of these contracts, refer to the following sections.

## **Entry point methods**

Here are the PAIR's entry point methods.

### **transfer**

Let `self.get_caller` send pool tokens to a recipient hash.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| recipient      | Key  |
| amount         | U256 |

This method **returns** nothing.

### **transfer\_from**

Sends pool tokens from one hash to another.\
**Note:** User needs to call the `approve` method before calling the `tranfer_from` .

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| owner          | Key  |
| recipient      | Key  |
| amount         | U256 |

This method **returns** nothing.

### **swap**

Swaps tokens. For regular swaps, `data.length` must be `0`.\
**Note:** To call this method explicitly, User needs to deploy a `Factory contract` first and call a method `create_pair` which invokes the `initialize` methods of `Pair contract`. That's how the `Pair contract` can access the `token0` and `token1`. After this, the user needs to mint `token0` and `token1` by calling an `erc20_mint` method in `pair contract` or you can transfer some tokens to it, so they have some balance in them. To call the `swap` method the user needs to have some balance in `reserve0` and `reserve1`.

Here is the table of parameters.

| Parameter Name | Type   |
| -------------- | ------ |
| amount0\_out   | U256   |
| amount1\_out   | U256   |
| to             | Key    |
| data           | String |

This method **returns** nothing.

### **skim**

\
**Note:** To call this method explicitly, User needs to deploy a `Factory contract` first and call a method `create_pair` which invokes the `initialize` methods of `Pair contract`. That's how the `Pair contract` can access the `token0` and `token1`. After this, the user needs to mint `token0` and `token1` by calling an `erc20_mint` method in `pair contract` or you can transfer some tokens to it, so they have some balance in them. To call the `skim` method the user needs to have some balance in `reserve0` and `reserve1`.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| to             | Key  |

This method **returns** nothing.

### **sync**

\
**Note:** To call this method explicitly, User needs to deploy a `Factory contract` first and call a method `create_pair` which invokes the `initialize` methods of `Pair contract`. That's how the `Pair contract` can access the `token0` and `token1`. After this, the user needs to mint `token0` and `token1` by calling an `erc20_mint` method in `Pair contract` or you can transfer some tokens to it, so they have some balance in them.

Here is the table of parameters.

This method **returns** nothing.

### **permit**

Sets the allowance for a spender where approval is granted via a signature.

Here is the table of parameters.

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

Returns the amount of pool tokens owned by a hash.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| owner          | Key  |

This method **returns** an U256.

### **nonce**

Returns the current `nonce` for an address for use in `permit`.

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

This method **returns** an U256.\
**Recommendation:**

Awareness of possible exploits should be taken into account. Usage of functions that increase/decrease the allowance relative to its current value is highly encouraged. We recommend that developers of applications dependant on approve() / transferFrom() should keep in mind that they set allowance to 0 first and verify if it was used before setting the new value.\
**Note:** Teams who decide to wait for such a standard should make these recommendations to app developers who work with their token contract.

### **total\_supply**

Returns the total amount of pool tokens for a pair.

Here is the table of parameters.

This method **returns** an U256.

### **mint**

Creates pool tokens.\
**Note:** To call this method explicitly, User needs to deploy a `Factory contract` first and call a method `create_pair` which invokes the `initialize` methods of `Pair contract`. That's how the `Pair contract` can access the `token0` and `token1`. To call the mint, user needs to do all the above steps so he can proceed flawlessly.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| to             | Key  |

This method **returns** an U256.

### **burn**

Destroys pool tokens.\
**Note:** User needs to mint tokens before burning them. And the user needs to deploy a `Factory contract` first and call a method `create_pair` which invokes the `initialize` method of `Pair contract`. That's how the `Pair contract` can access the `token0` and `token1`. To call the burn user needs to do all the above steps so he can proceed flawlessly.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| to             | Key  |

This method **returns** a Tuple(U256, U256).

### **treasury\_fee**

Returns the Treasury Fee for a pair.

Here is the table of parameters.

This method **returns** an U256.

### **set\_treasury\_fee\_percent**

sets the treasury fee for a pair.\
**Note:** treasury\_fee\_percent Cannot be more than `30` and less than 3. If it’s more than `30` it will set it as `30` and if it's less than 3 it will set it as '3'.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| treasury\_fee  | U256 |

This method **returns** nothing.

### **token0**

Returns the hash of the pair token with the `lowest sort order`.

Here is the table of parameters.

This method **returns** a Key.

### **token1**

Returns the address of the pair token with the `highest sort order`.

Here is the table of parameters.

This method **returns** a Key.

### **initialize**

Sets the `token0` and `token1` in a pair contract.\
**Note:** This method will be called by `Factory contract` only and the user needs to pass the factory hash to make sure it's a factory or not.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| token0         | Key  |
| token1         | Key  |
| factory\_hash  | Key  |

This method **returns** nothing.

### **get\_reserves**

Returns the reserves of token0 and token1 used to price trades and distribute liquidity. Also returns the block\_time\_stamp `(mod 2**32)` of the last block during which an interaction occured for the pair.

Here is the table of parameters.

This method **returns** a Tupe3(U128, U128, U64).

### **erc20\_mint**

This method mints the number of tokens against the hash, both provided by the user.

Here is the table of parameters.

| Parameter Name | Type |
| -------------- | ---- |
| to             | Key  |
| amount         | U256 |

This method **returns** nothing.
