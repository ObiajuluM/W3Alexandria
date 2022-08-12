# Alexandria


#### A project to decentralize and distribute literary infrastructure.

Approaches found here can be directly integrated with the metaverse or any existing dapp.

#### Project Alexandria will bring literary arts on-chain, make literary censorship impossible, directly reward the artist/ publisher, allow the first on-chain tokenization of literary art works

##### The set of contracts and code found here is a small piece of what can be made possible with this idea.

##### An on-chain book and library infrastructure.

Other possibilities I am working on while improving the existing ones are:

	1. Publication of daily, weekly, or monthly content such as blog posts, articles, stories, etc.

Yes, all these are possible, plus the fact that literary works published in this manner can be unmodifiable and are by default uncensorable with the aid of properly written smart contracts; this can also be used to directly incentivize the publisher/ artist.

I am currently working on 3 approaches to the managing of books and library infrastructure
1 and 2 are currently available on this SDK.

	1. Off-chain Storage [IPFS] -> Library Contract

	2. Book Contract -> Library Contract

	3. Chapter Contract -> Book Contract -> Library Contract


The Library contract is constant so I defined it first, you can reference it as you read through other sections.
A reference to all book contracts is stored in the library contract.

#### The Library Contract -LC- 
This will be deployed by the librarian, As the name implies it is a contract that stores information and a reference to a book.
The library name and a quote are set upon deployment.
A Library `hashmap` for storing a struct of books `Library: public(HashMap[uint256, Book])` the book struct is made up of:

	ispresent: bool - to check if the book is present in the library
   
	title: string - the title of the book
   
	bookaddr: uint256 - the address of the book
   
	author: address - the author of the book
   
An all-time value counter that stores the total amount of ether deposited to the contract and a quote about Alexandria

Events: `AddedBook`, `RemovedBook`, `Deposit`, `Transfer` - emit logs as the name implies.

Built-in Methods

`addbook`: to add a new book struct to the library `hashmap`.

`removebook`: to delete a book struct from the library `hashmap`.

`transfer`: to transfer out ether from the library contract.

`balanceof`: to get the balance of the library contract.

`transferposition`: to transfer the position of librarian 


private methods

`gettitle`: to get the title of the book.

`getauthor`: to get the author of the book.

----------------------------------------------------------------------------

#### 1. Off-chain Storage [IPFS] -> Library Contract

As the name implies an off-chain storage such as ipfs is used to store the content of the book and the reference hash is stored in the book contract which will be referred to as -BC-.

A book is uploaded to ipfs and the hash, author, title, license, and book format e.g .pdf, .epub is stored in the book contract.
An all-time value to log the total amount of ether deposited to the contract.

The author, title, license, ipfshash, and book format are defined upon contract creation.
The Book Contract -BC- will be deployed by the author of the book

All information stored in the contract will be used to build the book from the ipfs hash.

Events: `Deposit`, `Transfer` - emit logs as the name implies.


Built-in Methods

`transfer`: to transfer out ether from the book contract.

`balanceof`: to get the balance of the book contract.


-----------------------------------------------------------------------


#### 2. Book Contract -> Library Contract

As the name implies there is a book contract and a library contract which we will refer to as BC and LC respectively from now on.

The Book Contract -BC- will be deployed by the author of the book, the title, and the license set at that point.
It contains a count of all chapters in the book that is increased by +1 every time a new chapter is added and vice versa.
A book `hashmap` for storing a `struct` of chapters `Book: public(HashMap[uint256, Chapter])`.

The chapter struct is made up of:

	`ispresent: bool - to check if the chapter is present in the book
   
	`name: string` - the name of the chapter
   
	`chapterid: uint256` - the chapter id
   
	'content: String[1_000_000]` - the content of the chapter (scale to fit work)
   
An all-time value counter that stores the total amount of ether deposited to the contract.

Events: `AddedChapter`, `RemovedChapter`, `Deposit`, `Transfer` - emit logs as the name implies.


Built-in Methods

`addchapter`: to add a new chapter struct to the book `hashmap`.

`removechapter`: to delete a chapter struct from the book `hashmap`.

`transfer`: to transfer out ether from the book contract.

`balanceof`: to get the balance of the book contract.


-----------------------------------------------------------------------


#### 3. Chapter Contract -> Book Contract -> Library Contract

This approach has not yet been implemented in this version of the project.
It greatly copies the functionality of the above approach but each chapter is a different contract, their respective addresses are stored in the book contract.

Currently working on this 
