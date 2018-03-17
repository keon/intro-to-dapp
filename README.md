# DApp with Ethereum and Solidity Tutorial

## Table of Contents

* Blockchain
* What is DApp?
* How does Ethereum work?
* Smart Contracts
* Voting App
* Truffle

## Developing Blockchain Software

What is blockchain and what is it good for?

Blockchains record state and history. State is modified by transactions.
Everyone eventually agrees on the transactions.
It can be used to transfer tokens.

Assets are owned by identities.
Identities are public keys.
Authority is proven by digital signatures.
Transactions are signed.
Integrity of the blockchain is protected by secure hashes.
- we can communicate a secure hash and then follow a secure hash chain to find a history of the blockchain.


So its just a database?
* Database store information
* Have transacitons which change the State

So is a blockchain just a databse?
Not quite, blockchain prevents the double spending problem.
If I have $10, I should not be able to spend it twice or give it to multiple people.

The usual solution to this is to have a central authority such as banks.
Banks prevent double spending by reconciling against a ledger.
Which means that they have a record somewhere that how much everybody has and checks out if the transaction is good.
Can also be done with secure hardware. Ultimately, you need a central authority.

The breakthrough came with Bitcoin, the first blockchain.

It was literally a chain of blocks.
Each block contains the hash of the previous block.
Transactions transfer a native token.

It has what we call a UTXO model. It gets kind of technical but it is important to understand.
UTXO stands for Unspent transaction output. In other words, it is basically a bitcoin that was sent to someone but not yet been spent. So every payment creates a UTXO. If I send you a bitcoin, I create a UTXO that you have the private key to claim for that bitcoin. We assume that the network agrees on the UTXOs.
Network state is a set of valid UTXOs.
Payments create new UTXOs.
We assume the network agrees on the set of UTXOs.

Bitcoin meets all the requirements of a currency.

* Scarce
* Fungible - units look the same. There is no bad $10 or a good $10
* Divisible
* Durable
* Transferable

Bitcoin solves the double spending problem with mining.


Bitcoin is a currency and a payment system at the same time.
Payment system provides ultimate grounding.
System regulates introduction of new currency. Supply is ultimately fixed.
Rules are notionally set in stone (bitcoin supply).
They can be changed by social consensus.
The past can be rewritten
Mining uses a lot of power to secure transaction.

## Challenges

Public blockchains must be fortresses

Code is Public
Vulnerabilities are painful
This makes development much slower, maybe 10X
Public APIs.
If someone finds a bug, he can profit off of it by hacking 70 mil.
Plus, because the blockchain can be accessed all over the world and identification is difficult, there is very low chance of getting caught for the hacking.
So there is a huge incentive for the person not to report the bug like any other open source project but to exploit it.

Even if it corrupts the blockchain it has to make everyone on the blockchain to agree to rewind the hacking.

It is like trying to protect a PC from being hacked by its own user.
Unlike the traditional problem of protecting the PC from the outside of the network,
it becomes a lot harder since the user has more control.

Resource Management
* we have to keep up with the Network
* we have to respond to remote queries
* We have to respond to local queries
* We have to cache



## What is DApp?

## Solidity

High level language for Ethereum contracts.
It looks a lot like JavaScript with types. Like so:

```
contract Math {
  function multiply(uint v) returns (uint) {
    return v * 13;
  }
}
```

The code is compiled through the Ethereum Virtual Machine (EVM).
Once deployed to the EVM, code is completely isolated and cannot reach outside of the EVM.

Reason for that isolation is that it has to be completely deterministic.
That is why you cannot generate random numbers easily inside of the EVM.
Contracts are really easy to write but it is hard to make sure they are secure.


```
contract Wallet {
  function withdraw(uint amount) public {
    // Check they have a sufficient balance
    if (balances[msg.sender] >= amount){
      // Send them the funds
      msg.sender.send(amount);
      // Deduct the funds from their account
      balances[msg.sender] -= amount;
    }
  }
}
```

Look at the code above. This will let somebody completely drain this contract of the funds.
This is actually what happened to the Dao.
What actually happens here is that `msg.sender.send(amount);` can execute code on the address that it is sending to.
Since the account balance is only deducted on the next line, the contract can be call `withdraw` method multiple times.
This will execute the line again and again until it runs out of gas.
If it can get through a hundred loops, it will withdraw a hundred times than the amount it was supposed to.

```
contract Wallet {
  function balance() public returns (uint) {
    // this can be called by any other
    // contract or directly
  }

  function transferBalance() internal {
    // This can only be called from within
    // the other functions of this contract
  }
}
```

Public functions are callable by anybody.
Internal functions are only callable from inside the contract.

One of the interesting things that are happening right now
is that some standards are beginning to emerge for how we write contracts.

ERC20 Standard is the standard interface of contract that tokens should implement.

If you go to Etherscan (a very popular Ethereum blockchain explorer),
they have a search feature for ERC20 tokens. If any contract implements ERC20
standard, you can search for tokens within that contract. Because it is the standard,
it will provide with functionalities you need such as checking balance, deposit, withdraw, etc.

You can even make a decentralized exchange like EtherEx.
and You don't have to worry about the exchange going to bankrupt like Mt.Gox.


Solidity is about 2 years old. Since then, communities made a lot of tools.
Popular editing tools such as Atom, Sublime, Visual Studio, Vim already provide solidity compatibility.




## References

### Videos

*[Solidity for Dummies by Hudson Jameson @ Ethereum Foundation](https://www.youtube.com/watch?v=kx_TgcWgbkw)
*[Developing Blockchain Software by David Schwarts @ Ripple](https://www.youtube.com/watch?v=RRP65VvIgGg)
