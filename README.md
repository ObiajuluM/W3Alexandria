# Alexandria

## Decentralized literary infrastructure for the distributed metaverse.

A set of contract built to integrate literary infrastructure in the metaverse.

This set of contracts are built to emulate books and a library for storing literary data on-chain.

Written in vyper for low cost and security


Decentralized literary infrastructure for the distributed metaverse

### Abstract:
The Metaverse is an upcoming technology that requires infrastructure to be at the stages of web2.

Current metaverse is still under development and needs a functioning literary infrastructure to emulate the likes of wikipedia.

I propose a unique mechanism of contracts that will emulate physical literary infrastructure on-chain and will be used to create an interconnected decentralized library of digital knowledge that can be accessed from the metaverse.

##### Technicals:
Currently there are 3 approaches of using this idea to publish books, the first which i am currently working on.

All code instances are written in vyper and the first approach is currently live on polygon testnet.

1. `Book Contract -> Library Contract`

2. `Chapter Contract -> Book Contract -> Library Contract`

3. `Offchain Storage [IPFS] -> Library Contract`

## Usages
### Your are to understand that is a single approach to what is possible with this idea
   #### * It can be modified to publish daily, weekly or monthly content such as blogposts, articles stories etc. (currently a work in progress)
   #### * It can be used to publish uncensorable and unmodifiable literary works. (WIP)


#### 1. Book Contract -> Library Contract
   This approach involves a contract A and contract B that will be refernced from now on as Book Contract -BC- and Library Contract -LC- respectively.

   The book contract is used to store chapters represented as structs in a Book hashmap of `uint256 -> chapter`.

   The contract can only be modified by the author defined upon deployment. Modification in the sense of adding, removing chapters and funds transfer.

   Ether can be deposited to the contract as it is labeled payable to incentivize the author. A log of all the funds deposited to the contract is kept for future refernce

   *Advantages:*
   
        1. The author is directly incentivized
        
        2. This method provides distributed easily accessed and uncensorable data
        
    
   *Disdavantages:*
   
        1. The contract will increase in size as the book increases which isnt good.
        
              fixes: create multiple contracts per book
              

   The -BC- contract contains the following data types:
   
   
        -Author-
        Type: public(address)
        The writer of the book

        -Title-
        Type: public(String[256])
        The title of the book

        -License-
        Type: public(String[256])
        Licensing rights of the book

        -Chapters-
        Type: public(uint256)
        Number of chapters in the book

        -Book-
        Type: public(HashMap[uint256, Chapter])
        Hashmap of uint256 and chapter struct that represents a book

        -AllTimeValue-
        Type: public(uint256)
        Sum of all ether sent to this contract

        -Chapter-
        Type: struct
            ispresent: bool
            name: String[256]
            chapterid: uint256
            content: String[1000000] *can be modified
        Chapter struct

        -AddedChapter-
        Type: event
            Author: indexed(address)
            Chapter_id: indexed(uint256)
            Name: String[256]
        Event fired upon chapter addition 

        -RemovedChapter-
        Type: event
            Author: indexed(address)
            Chapter_id: indexed(uint256)
            Name: String[256]
        Event fired upon chapter removal 

        -Deposit-
        Type: event
            sender: indexed(address)
            amount: indexed(uint256)
        Event fired upon deposit

        -Withdrawal-
        Type: event
            sender: indexed(address)
            receiver: indexed(address)
            amount: indexed(uint256)
        Event fired upon withdrawal

        -addchapter-
        Type: method
        params
            _chapter: uint256
            _name: String[256]
            _content: String[1000000]
        returns
            bool
        Method to create a new chapter and add it to the book HashMap

        -removechapter-
        Type: method
        params
            _chapter: uint256
        returns
            bool
        Method to reomve an exsting chapter from the book HashMap

        -transfer-
        Type: method
        params
            _amount: uint256
            _to: address
        returns

        Method to withdraw ether from the contract

        -balanceof-
        Type: method
        params

        returns
            uint256
        Method to return the balance of the book contract


This is under development constructive critism is highly encouraged

Other approaches are under construction
