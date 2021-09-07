## What is Ethereum ?

Ethereum is an open-source blockchain that along with providing cryptocurrency (similar to Bitcoin) , also allows developers to develop applications on the blockchain through **smart contracts.** Its native currency is - Ether. It was developed by Vitalik Buterin.


## What is a smart contract ?

According to Ethereum dev guide, "Smart contract is a program that runs on Ethereum blockchain. It is a collection of code (its functions) and data (its state) that resides at a specific address on the Ethereum blockchain."

Similar to a user account, smart contracts also have their own balance and can send transactions over the network. The only difference is, instead of a user managing them, they are deployed to the blockchain network and are self-managed in the sense that they run autonomously based on the logic inside them. 

Other users interact with the smart contracts by sending transactions that execute a function defined in the smart contract.


## Ethereum virtual machine & Gas

Allowing applications to run on blockchain through smart contracts has 2 main challenges:

1. **Infinite loops:**

    Applications could have logic involving a large number of loops, a bug that could have the applications run into infinite loops or a computationally heavy application. Such applications could slow down the the nodes they are running on significantly, consequently, slowing down the entire network. Since the applications once deployed to blockchain are nearly impossible to change, fixing such applications would be out of question. The applications cannot be deleted from the blockchain either. 

    Ethereum solved this challenge by introducing the concept of "gas". Ethereum dev guide defines **Gas** as "a unit that measures the amount of computational effort required to execute specific operations on Ethereum network". Eg: adding or subtracting two integers costs 3 gas units, checking balance requires 400 gas units, etc. Each gas unit costs a certain amount of gwei (10^-9 ether = nanoether) which continues to change depending on the market. This is called as the **gasPrice**. So the

     **total transaction fee = gasPrice * total gasUnits of the transaction**. 

    The reason why "gasPrice" was introduced instead of simply using ether was to avoid fluctuations in transaction fee as ether price fluctuates. So now, if ether price goes up, the gasPrice would go down to maintain the same transaction fee. However, an increase in network activity can increase the transaction fee since now there are more transactions in the mempool for the miners to choose from. Miners are incentivized to choose transactions that have a higher transaction fee to mine thereby increasing their profits.  It is similar to the demand-supply mechanism in general economics. You can find the average transaction fee in ethereum [here](https://ycharts.com/indicators/ethereum_average_transaction_fee).

    **Transaction fee (gas fee) is paid by the users initiating the transaction and not the contract developers.** 

    Defining a standard computational effort within Ethereum was great to calculate transaction but did help in solving the challenge of infinite loops by itself. What really solved the issue of infinitely running transactions or applications is what is called a **Gas limit.** Gas limit is the maximum amount of gas specified by the user that can be consumed for the transaction. ****For each transaction, the gas required to execute the transaction should be ≤ gas limit. If the gas needed exceeds the gas limit, the transaction is stopped and reverted. However, since the computational effort had already been put into executing the transaction thus far, the miners still get to keep the transaction fee. 

    Now, let's say a smart contract has a function which has a buggy code that results in infinite loop. A user creates a transaction to interact with the smart contract through that functionality. Without the gas limit, when the transaction is executed, the program would have ended up running infinitely. But with gas limit associated with the transaction, as soon as the total amount of computational effort hits the gas limit, the program stops executing and the transaction is reverted if it is not yet complete. This is how gas limit prevents issues that arise with infinite loops or computationally heavy applications. For smart contracts, the gas limit is usually higher than just transferring ethers since they require more computational work. You can check prices and buy gas at [ethgasstation.info](http://ethgasstation.info). 

    Gas limit also incentivizes developers to write computationally efficient and good code so the users interactions (transactions) with the applications don't run out of gas resulting in a bad experience.

    Detailed explanation on calculating cost of ethereum smart contract [here](https://hackernoon.com/ether-purchase-power-df40a38c5a2f). 

2. Since smart contract runs on every node in the blockchain, it is **easy to spread virus** through malicious code in smart contracts which generates a security threat for the the nodes on the blockchain.  To mitigate this threat, every node runs on a virtual machine called Ethereum virtual machine (EVM). EVM is completely isolated from the host so any code that runs inside the EVM has no access to network system, files, or other processes on the host which safeguards the host  from any modifications from ethereum applications.


## Smart contracts vs web applications

- Smart contracts are **immutable** - once deployed, the logic inside them cannot be changed. So the code should be thoroughly tested before deploying it. If there are any errors, etc - there is no way to fix them.
- Smart contracts maintain your **privacy** - In order to interact with web applications, you have to provide your identification such as username, email, etc. Smart contracts do not need any of your private information and therefore, helps to maintain your privacy and anonymity. You interact with them only through your public keys.
- Smart contracts are **inspectable by anybody** - Smart contracts are compiled into bytecode which is deployed to the blockchain. Since this bytecode is available on the blockchain which is available to everybody, all smart contracts in-effect are inspectable by anybody (bytecode available can be decompiled, but usually its not as legible as the source code). However, whether they are open-source or not depends on whether the developer of that contract has voluntarily published the underlying code on the blockchain. While for web-apps, whether they are open-source or private depends on the developer/organization that owns it.
- Designed for trust & scalability - Traditional apps are designed for performance whereas smart contracts are designed for trust and scalability

## Pros and cons of smart contracts:

**Pros:**

1. **Autonomy & speed** - no middle man required. Since smart contracts bypass bureaucratic processes and work based on algorithms instead, the overall transaction processing speed is increased considerably. Eg: Enables faster payment processing due to absence of intermediaries like banks
2. **Backup** - the smart contracts are duplicated on multiple nodes as part of blockchain 
3. **Safety** - smart contracts are encrypted and therefore have a higher level of security

**Cons:**

1. **Immutable** - Since they are immutable, if there are any errors or bugs in the smart contract, it is nearly impossible to fix it. 
2. Currently, no proper **legal regulations** are enforced for smart contracts regarding responsibilities, liabilities, agreements between the users, etc.
3. Does not support very **complex applications** - due to the high gas price associated with running complex applications (with high number of operations), smart contracts are limited in terms of what types of applications they can support. 
4. Interacting with smart contracts is **costly for a user** as well.  Since, all transactions on blockchain involve at least a  transaction fee for the user, this can act as a deterrant for the user to use or interact with your application.

## Resources:

1. [Ethereum dev guide](https://ethereum.org/en/developers/docs)
2. Reddit thread - [are all smart contracts open source](https://www.reddit.com/r/ethereum/comments/ewqo9q/are_all_smart_contracts_open_source_and/)
3. Blogs:
    - [https://blog.ionixxtech.com/dapps-vs-web-apps/](https://blog.ionixxtech.com/dapps-vs-web-apps/)
    - [https://corporatefinanceinstitute.com/resources/knowledge/deals/smart-contracts/](https://corporatefinanceinstitute.com/resources/knowledge/deals/smart-contracts/)
    - [https://knowtechie.com/advantages-and-disadvantages-of-using-smart-contracts-how-to-create-a-smart-contract/](https://knowtechie.com/advantages-and-disadvantages-of-using-smart-contracts-how-to-create-a-smart-contract/)
    - [https://coinmarketcap.com/alexandria/glossary/ethereum-virtual-machine-evm](https://coinmarketcap.com/alexandria/glossary/ethereum-virtual-machine-evm)
4. Udemy courses:
    1. [Blockchain A-Z](https://www.udemy.com/course/build-your-blockchain-az/)
    2. [Ethereum and solidity: A complete developer's guide](https://www.udemy.com/course/ethereum-and-solidity-the-complete-developers-guide/)
5. Youtube video - [What is gas?](https://www.youtube.com/watch?v=Yh8cHUB-KoU)
