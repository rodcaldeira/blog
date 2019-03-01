---
layout: default
title:  "Ownership!"
excerpt: "It's mine and I can prove it!"
date:   2019-02-27 16:01:56 -0300
isSmartContract: true
categories: smartcontract
---

### MY PRECIOUSSSSS

Hello,

Everybody have an special object in their life. A collectible, a gift from someone special, an heritage or just an object that they have an attachment. I'll assume that the phrase above is true, just as motive for the effort that will be done in this post.


Let's go! I have a book with a dedication from my father, this book is **very important** for mim and I hope that nothing bad happens to it. But, life happens and... I can forget it in a bus, or have my backpack stole, lend to someone careless. Well, I'm not here to talk about every single tragic choice for my beloved book.


The point is, it is precious to me and I want to have a way to prove that its belongs to me. May had happen some tragic ending to it and in some years I bump into the same book, with all the details and with the dedication from my father. Obviously I will be realized, after all my book will be my again! However, it can be that it is in a shelf in a second-hand bookshop. I could not get out of there with the book claiming: "It's mine! There is even a dedication from my father... I would never sell it, are you insane?".


We can kind of solve this with a simple Smart Contract of ownership inside the [Ethereum Blockchain](ethereum-url). Why use blockchain instead of a notary's officer? In my case, because I'm in Brazil, to do a register in a notary's office you have to face an endless line and pay a fortune - ok, just a couple of bucks, but still a lot!


So now my goal is to create a Smart Contract that I can deploy in the Blockchain wich proves my ownership over the book. A small phrase, but not so simple to do, here is the ordered list of what we need to do:


1. Define the contract (!)
2. Do the sourcecode of the Smart Contract
3. Compile and test the SC
4. Use the SC (deploy it on the [Ethereum](ethereum-url) Blockchain)


### Define the contract


The contract I want is well defined: register in the blockchain that the book **belongs to me**. Nothing more, for now. To prove the ownership of anything, I need two informations, the owner and the thing, right? To facilitate understanding I'll assume that the thing - my book - have some kind of numeric unique identifier, any kind of sequence of numbers that represent the book.


I'll use two variables: the first one to store the **owner** and the second one to store de **identifier**. I need one more information - or definition. Who will deploy the Smart Contract in the Blockchain Network? In the case of this specific Smart Contract the owner of the book will deploy the contract.


Normally at some point between the definition and the coding of any program (mobile, web or desktop) the developers will define too what languages will be used. In this case, I'm targeting the Smart Contract itself, not trying to create a new Blockchain, an dApp to use it nor any kind of interface for it... so I'll use the official language (I think I can call it official) of Ethereum Smart Contracts. It's the [Solidity](solidity-url).


### Coding the Smart Contract

As said above, the language is the [Solidity](solidity-url). I'll use the version 0.5.4 - the latest at the moment I'm writing this post. This is a pertinent information, since we can have some breaking changes in the languages (semantic and sintax). Ok, enough talking, let's code!

~~~
    pragma solidity ^0.5.4;

    contract Ownership {
        address public owner; // owner of the contract - In this case onwer of the book too.
        uint public identifier; // numeric unique identifier

        constructor (uint id) public {
            owner = msg.sender;
            identifier = id;
        }
    }
~~~
{: .language-javascript}

Yep. That's it. There is a lot to do so you can deploy this sourcecode in the network, but in line of code for now is just that - you couldn't expect much more of the contract definition. Still, I believe that is worth it to explain the code beyond the comments (the text after // in lines 4 and 5).


The first line I define what version of [Solidity](solidity-url) I'm using - so it can compile and behave like I need it. This is not part of the contract at all.


Between the lines 3 and 11 the contract is defined! Inside the contract in the first two lines (4 and 5) its declared the variables required to register my expected informations. Actually this variables in this case can be called as constants, since will not be possible to change it values after the deployment of the Smart Contract(!).


In the line 7 we have the method the will build the contract in the Blockchain Network when invoked, it called constructor. As you can see we have some information inside the parentheses:

 `constructor (uint id) public {`

This are called parameters, and you can understand this way: to call the constructor of this Smart Contract I need to pass by parameter an unsigned integer number (unsigned integer are all numbers non negative and integer). This parameter is our unique numeric identifier defined in the contract to identify the book. At line 9 the contract stores the information passed by parameter in the variable defined to store our identifier.


At line 8, as you can see the owner receives and value `msg.sender`. This `msg` is a special object of the language that works as holder of some information, the sender value stores the sender of the message (current call to the contract). You can read as, the guy who is calling to the constructor method - in this case: **me**. I'm identified by an address(!) in the Blockchain Network, and it's that address that is stored in the owner variable.


### Compiling, testing and deploying

The code is done! For compile, test and deploy I'll use the [remix](remix-url) an powerfull opensource tool. Actually I used the remix to write the code down too.


Since it's a simple contract that I have no intention to deploy in the real Ethereum Blockchain(!) (it cost ethers to deploy contracts), I did the deploy in a local test network - also included in the remix tool. Works like a charm!


Well, that's it for this post. I believe you saw some "(!)" here and there, this are some points that probably will be explained in details in the future, but by now I didn't want to lose the track of the main goal here: develop a Smart Contract to register something precious to me in the Blockchain. But here goes a brief explanation:

(!) **Define the contract** - this is the most import stage of any kind of codification. In this moment you define what you want: the information stored, the behavior in each kind of interaction, who can use the contract, how can they use the contract... From this definition, the developer will translate it all to machine language. And since the Smart Contract are immutable you need it to be really careful in this process.

(!) **Not possible to change it values after the deployment of the Smart Contract** - as my first definition: I want to register in the Blockchain that **I'm** the owner of the book. Anywhere in this post you can read "Maybe I can write the wrong identifier" nor "Maybe I'll give this book to my son someday". So the contract work as expected, but between us, isn't much useful this way... We can fix it, but will do in other moment.

(!) **address** - Inside the Ethereum Blockchain there is this concept of address, that works as identifier of contracts and accounts. You need an account to interact with contracts or others persons, so an account can be your own reference inside there.

PS.: I really have the book with a dedication from my father <3.

Regards,
Rodrigo

[ethereum-url]: https://ethereum.org/
[solidity-url]: https://solidity.readthedocs.io/
[remix-url]: http://remix.ethereum.org
