# FLASH SWAPPER

## **Deploying FLASH SWAPPER contract manually**

If you need to deploy the `Flash swapper contract` manually you need to pass the hashes of the other contracts as parameters. Here is the command to deploy the `Flash Swapper contract`.

```bash
sudo casper-client put-deploy \
    --chain-name chain_name \
    --node-address http://$NODE_ADDRESS:7777/ \
    --secret-key path_to_secret_key.pem \
    --session-path path_to_wasm_file \
    --payment-amount 10000000000 \
    --session-arg="public_key:public_key='Public Key In Hex'" \
    --session-arg="uniswap_v2_factory:Key='Hash of factory Contract'" \
    --session-arg="wcspr:Key='Hash of WCSPR Contract'" \
    --session-arg="dai:Key='Hash of DAI Contract'" \
    --session-arg="contract_name:string='contract_name'"
```

Before deploying `Flash Swapper Contract`, you will need to deploy other contracts first and pass hashes of these contracts to the respective parameters above. We have already deployed these contracts and the tables below display the hashes of the contracts.

| Name    | Network | Account info contract hash                                              | Contract owner     |
| ------- | ------- | ----------------------------------------------------------------------- | ------------------ |
| Factory | Testnet | `hash-13cc83616c3fb4e6ea22ead5e61eb6319d728783ed02eab51b1f442085e605a7` | Casper Association |
| Wcspr   | Testnet | `hash-4f2d1b772147b9ce3706919fe0750af6964249b0931e2115045f97e1e135e80b` | Casper Association |
| Dai     | Testnet | `hash-ffb8fa3073c7623484f76d79bc8baad110b24936b92d5ebc854d401895e88c95` | Casper Association |

For manual deployments of these contracts, here are the command templates.

#### Factory

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

#### Wcspr

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

#### Dai

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

Here are the Flash Swapper's entry point methods.

### **start\_swap**

This method will start swap.\
Special Instructions: The user needs to call this (start\_swap) method first to call the `uniswap_v2_call` method. `Start_swap` method will further call 3 methods

* simple\_flash\_loan This method will be invoked if both tokens (token\_borrow and token\_pay) are the same.
* simple\_flash\_swap This method will be invoked if both tokens (token\_borrow and token\_pay) are not the same. one of them must be equal to “Hash-0000000000000000000000000000000000000000000000000000000000000000”
* triangular\_flash\_swap This method will be invoked if both tokens (token\_borrow and token\_pay) are not the same. The above methods will invoke the swap methods of `Pair` Contract by using the `permissioned_pair_address`. And then the `swap` method will invoke the `uniswap_v2_call` method.

Here is the table of parameters.

| Parameter Name | Type   |
| -------------- | ------ |
| token\_borrow  | Key    |
| amount         | U256   |
| token\_pay     | Key    |
| user\_data     | String |

This method **returns** nothing.

### **uniswap\_v2\_call**

This method calls the `swap` method of `pair contract`.\
the sender must be a `Flash Swapper Contract` hash if user data has some value. `Uniswap_v2_call` must be called from a contract. Users cannot directly invoke this method.

Here is the table of parameters.

| Parameter Name | Type   |
| -------------- | ------ |
| sender         | Key    |
| amount0        | U256   |
| amount1        | U256   |
| data           | String |

This method **returns** nothing.
