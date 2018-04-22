let's deploy a simple contract

```
pragma solidity ^0.4.18;

contract Foo {
}
```

compile it to bytecode:

```
solc --bin Foo.sol

======= Foo.sol:Foo =======
Binary:
60606040523415600e57600080fd5b603580601b6000396000f3006060604052600080fd00a165627a7a7230582080f56e7215a3ec57420aa547eb6cb315f0b7ce974c1ec26c0fabf48c2c9518d40029
```

The compiled bytecode:

```
qcli createcontract \
  60606040523415600e57600080fd5b603580601b6000396000f3006060604052600080fd00a165627a7a7230582080f56e7215a3ec57420aa547eb6cb315f0b7ce974c1ec26c0fabf48c2c9518d40029

{
  "txid": "16445e0f15414a346b44faf17921aef926f0452a6fe818dae5eaa3b9ff0b77b7",
  "sender": "qetGKE4oSS2UYDkW9eAx97Tfnw8EDaCN2f",
  "hash160": "e9ecd571722bf4278919fca8fc54f28701dd14c0",
  "address": "a2c6724fa323d1dff73082fa85300c820f7225b7"
}
```


```
qcli decoderawtransaction \
  02000000014395845c62a7a80219f1b8adb79d0edd4252272e7cc0893e0b46b26fbf280d95010000006a473044022035d35946d9854007d3c16d294418312eec5710964cf1f372c935f8269afb5abf0220560889752ec2d240bb93b908be81103783a09f2693327a7544e315997edd9d8c012103d7f9aed41d36c4f168c1a0e0c2b88e473db7364dc929442bdcebce83a9efd6d3feffffff02a05ad417000000001976a914f4c9eb2921b3b1d60fbd91427d8e10479763498488ac00000000000000005b010403a0252601284c5060606040523415600e57600080fd5b603580601b6000396000f3006060604052600080fd00a165627a7a7230582080f56e7215a3ec57420aa547eb6cb315f0b7ce974c1ec26c0fabf48c2c9518d40029c162070000

...
{
  "value": 0.00000000,
  "n": 1,
  "scriptPubKey": {
    "asm": "4 2500000 40 60606040523415600e57600080fd5b603580601b6000396000f3006060604052600080fd00a165627a7a7230582080f56e7215a3ec57420aa547eb6cb315f0b7ce974c1ec26c0fabf48c2c9518d40029 OP_CREATE",
    "hex": "010403a0252601284c5060606040523415600e57600080fd5b603580601b6000396000f3006060604052600080fd00a165627a7a7230582080f56e7215a3ec57420aa547eb6cb315f0b7ce974c1ec26c0fabf48c2c9518d40029c1",
    "type": "create"
  }
}
...
```

`OP_CREATE` is QTUM's new BTC script operation added to create a smart contract

```
4
2500000
40
60606040523415600e57600080fd5b603580601b6000396000f3006060604052600080fd00a165627a7a7230582080f56e7215a3ec57420aa547eb6cb315f0b7ce974c1ec26c0fabf48c2c9518d40029
OP_CREATE
```

* 4 is the version of the VM
* 2500000 is the gas limit
* 40 is the gas price
* contract bytecode
