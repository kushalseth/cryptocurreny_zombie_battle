# CryptoZombies
> **Purpose of this Repository is to check and revise what I have learned in CrypotoZombies tutorials. Also to remember the important syntaxes. Thanks Loom Network for such an amazing Learning Process.**

- Learn to Code Ethereum DApps By Building Your Own Game: https://cryptozombies.io 
- CryptoZombies is an interactive code school that teaches you to write smart contracts in Solidity through building your own crypto-collectables game.

# Loom Network Release 1.0
- This release had omly top 6 lessons of **Solidity Path: Beginner to Intermediate Smart Contracts**

# Loom Network Release 2.0

#### **1. Solidity Path: Beginner to Intermediate Smart Contracts**
##### LESSON 1: Making the Zombie Factory  (REVISION NOTES)
- Chapter 1: Lesson Overview

- Chapter 2: Contract 
    - A **contract** is the fundamental building block of Ethereum applications — all variables and functions belong to a contract, and this will be the starting point of all your projects.

- Chapter 3: State Variables & Integers
    - **State variables** are permanently stored in contract storage. This means they're written to the Ethereum blockchain. Think of them like writing to a DB.
    - **Note:** In Solidity, uint is actually an alias for uint256
```
contract Example {
  // This will be stored permanently in the blockchain
  uint myUnsignedInteger = 100;
}
```
- Chapter 4: Math Operations
    - Power Operator: **
```
var test = 5 ** 10; // 5 power 10;
```
- Chapter 5: Structs
    - Structs allow you to create more complicated data types that have multiple properties. 
```
struct Person {
  uint age;
  string name;
}
```
- Chapter 6: Arrays
    - There are two types of arrays in Solidity: fixed arrays and dynamic arrays:
```
// Array with a fixed length of 2 elements:
uint[2] fixedArray;

// a dynamic Array - has no fixed size, can keep growing:
uint[] dynamicArray;

Person[] people; // dynamic Array for struct, we can keep adding to it
```
- Chapter 7: Function Declarations
    - **Note:** It's convention (but not required) to start function parameter variable names with an underscore
 
- Chapter 8: Working With Structs and Arrays
```
// create a New Person:
Person satoshi = Person(172, "Satoshi");

// Add that person to the Array:
people.push(satoshi);

// In one line
people.push(Person(172, "Satoshi"));
```
- Chapter 9: Private / Public Functions
    - **Notes:** In Solidity, functions are public by default. 
    -  It's good practice to mark your functions as private by default, and then only make public the functions you want to expose to the world.
    -  Private functions This means only other functions within our contract will be able to call this function and add to the numbers array.
    - **Note:** it's convention to start private function names with an underscore.
    
- Chapter 10: More on Functions
    - Return Values:
    - **Function modifiers:**
        - So in this case we could declare it as a **view function**, meaning it's only viewing the data but not modifying it: 
        - Solidity also contains **pure functions**, which means you're not even accessing any data in the app. This function doesn't even read from the state of the app — its return value depends only on its function parameters. So in this case we would declare the function as pure.
```
// Return Values example:
string greeting = "What's up dog";

function sayHello() public returns (string) {
  return greeting;
}

// View function Example:
function sayHello() public view returns (string) { }

// pure function Example: 
function _multiply(uint a, uint b) private pure returns (uint) {
  return a * b;
}

```
- Chapter 11: Keccak256 and Typecasting
    - Ethereum has the hash function keccak256 built in, which is a version of SHA3. A hash function basically maps an input into a random 256-bit hexidecimal number. A slight change in the input will cause a large change in the hash.
    
- Chapter 12: Putting It Together
- Chapter 13: Events
    - **Events** are a way for your contract to communicate that something happened on the blockchain to your app front-end, which can be 'listening' for certain events and take action when they happen.

```
// declare the event
event IntegersAdded(uint x, uint y, uint result);

function add(uint _x, uint _y) public {
  uint result = _x + _y;
  // fire an event to let the app know the function was called:
  emit IntegersAdded(_x, _y, result);
  return result;
}

// Your app front-end could then listen for the event.
YourContract.IntegersAdded(function(error, result) { 
  // do something with result
}

```

##### LESSON 2: Zombies Attack Their Victims  (REVISION NOTES)  

- Chapter 1: Lesson 2 Overview
- Chapter 2: Mappings and Addresses:
    - Let's make our game multi-player by giving the zombies in our database an owner.
    - So we can use it as a unique ID for ownership of our zombies.
    - Mappings are another way of storing organized data in Solidity.
```
// For a financial app, storing a uint that holds the user's account balance:
mapping (address => uint) public accountBalance;
// Or could be used to store / lookup usernames based on userId
mapping (uint => string) userIdToName;
```
- Chapter 3: Chapter 3: Msg.sender
    - Now that we have our mappings to keep track of who owns a zombie, we'll want to update the _createZombie method to use them.
    - msg.sender: In Solidity, there are certain global variables that are available to all functions. One of these is msg.sender, which refers to the address of the person (or smart contract) who called the current function.
```
//Example:
mapping (address => uint) favoriteNumber;

function setMyNumber(uint _myNumber) public {
  // Update our `favoriteNumber` mapping to store `_myNumber` under `msg.sender`
  favoriteNumber[msg.sender] = _myNumber;
  // ^ The syntax for storing data in a mapping is just like with arrays
}

function whatIsMyNumber() public view returns (uint) {
  // Retrieve the value stored in the sender's address
  // Will be `0` if the sender hasn't called `setMyNumber` yet
  return favoriteNumber[msg.sender];
}
```     
- Chapter 4: Require
    - In lesson 1, we made it so users can create new zombies by calling createRandomZombie and entering a name. However, if users could keep calling this function to create unlimited zombies in their army, the game wouldn't be very fun.
    - Let's make it so each player can only call this function once. That way new players will call it when they first start the game in order to create the initial zombie in their army.
    - How can we make it so this function can only be called once per player?

```
function sayHiToVitalik(string _name) public returns (string) {
  // Compares if _name equals "Vitalik". Throws an error and exits if not true.
  // (Side note: Solidity doesn't have native string comparison, so we
  // compare their keccak256 hashes to see if the strings are equal)
  require(keccak256(_name) == keccak256("Vitalik"));
  // If it's true, proceed with the function:
  return "Hi!";
}
```
     
- Chapter 5: Inheritance
    - Our game code is getting quite long. Rather than making one extremely long contract, sometimes it makes sense to split your code logic across multiple contracts to organize the code.
    - One feature of Solidity that makes this more manageable is contract inheritance: 

```
// BabyDoge inherits from Doge. That means if you compile and deploy BabyDoge, it will have access to both catchphrase() and anotherCatchphrase() (and any other public functions we may define on Doge).

contract Doge {
  function catchphrase() public returns (string) {
    return "So Wow CryptoDoge";
  }
}

contract BabyDoge is Doge {
  function anotherCatchphrase() public returns (string) {
    return "Such Moon BabyDoge";
  }
}
```
- Chapter 6: Import
    - When you have multiple files and you want to import one file into another, Solidity uses the import keyword:
```
// So if we had a file named someothercontract.sol in the same directory as this contract (that's what the ./ means), it would get imported by the compiler.

import "./someothercontract.sol";
contract newContract is SomeOtherContract {

}
```
- Chapter 7: Storage vs Memory
    - In Solidity, there are two places you can store variables — in storage and in memory.
    - **Storage** refers to variables stored permanently on the blockchain. 
    - **Memory** variables are temporary, and are erased between external function calls to your contract. Think of it like your computer's hard disk vs RAM.
    - Most of the time you don't need to use these keywords because Solidity handles them by default. 
        - **State variables** (variables declared outside of functions) are by default storage and written permanently to the blockchain, 
        - while **variables declared inside functions** are memory and will disappear when the function call ends.
```
contract SandwichFactory {
  struct Sandwich {
    string name;
    string status;
  }

  Sandwich[] sandwiches;

  function eatSandwich(uint _index) public {
    // Sandwich mySandwich = sandwiches[_index];

    // ^ Seems pretty straightforward, but solidity will give you a warning
    // telling you that you should explicitly declare `storage` or `memory` here.

    // So instead, you should declare with the `storage` keyword, like:
    Sandwich storage mySandwich = sandwiches[_index];
    // ...in which case `mySandwich` is a pointer to `sandwiches[_index]`
    // in storage, and...
    mySandwich.status = "Eaten!";
    // ...this will permanently change `sandwiches[_index]` on the blockchain.

    // If you just want a copy, you can use `memory`:
    Sandwich memory anotherSandwich = sandwiches[_index + 1];
    // ...in which case `anotherSandwich` will simply be a copy of the 
    // data in memory, and...
    anotherSandwich.status = "Eaten!";
    // ...will just modify the temporary variable and have no effect 
    // on `sandwiches[_index + 1]`. But you can do this:
    sandwiches[_index + 1] = anotherSandwich;
    // ...if you want to copy the changes back into blockchain storage.
  }
}
```
- Chapter 8: Zombie DNA

- Chapter 9: More on Function Visibility
    - Internal and External
        - **Internal** is the same as private, except that it's also accessible to contracts that inherit from this contract.  
        - **External** is similar to public, except that these functions can ONLY be called outside the contract — they can't be called by other functions inside that contract. 
    
- Chapter 10: What Do Zombies Eat?
    - **Interacting with other contracts** For our contract to talk to another contract on the blockchain that we don't own, first we need to define an interface.
```
Let's look at a simple example. Say there was a contract on the blockchain that looked like this:

contract LuckyNumber {
  mapping(address => uint) numbers;

  function setNum(uint _num) public {
    numbers[msg.sender] = _num;
  }

  function getNum(address _myAddress) public view returns (uint) {
    return numbers[_myAddress];
  }
}

// Now let's say we had an external contract that wanted to read the data in this contract using the getNum function.

// First we'd have to define an interface of the LuckyNumber contract:

contract NumberInterface {
  function getNum(address _myAddress) public view returns (uint);
}

```
- Chapter 11: Using an Interface
```
// Continuing our previous example with NumberInterface, once we've defined the interface as:

contract NumberInterface {
  function getNum(address _myAddress) public view returns (uint);
}

contract MyContract {
  address NumberInterfaceAddress = 0xab38... 
  // ^ The address of the FavoriteNumber contract on Ethereum
  NumberInterface numberContract = NumberInterface(NumberInterfaceAddress);
  // Now `numberContract` is pointing to the other contract

  function someFunction() public {
    // Now we can call `getNum` from that contract:
    uint num = numberContract.getNum(msg.sender);
    // ...and do something with `num` here
  }
}

```
- Chapter 12: Handling Multiple Return Values
```
function multipleReturns() internal returns(uint a, uint b, uint c) {
  return (1, 2, 3);
}

function processMultipleReturns() external {
  uint a;
  uint b;
  uint c;
  // This is how you do multiple assignment:
  (a, b, c) = multipleReturns();
}

// Or if we only cared about one of the values:
function getLastReturnValue() external {
  uint c;
  // We can just leave the other fields blank:
  (,,c) = multipleReturns();
}
```
- Chapter 13: Bonus: Kitty Genes

- Chapter 14: Wrapping It Up
```
Javascript Implementation
var abi = /* abi generated by the compiler */
var ZombieFeedingContract = web3.eth.contract(abi)
var contractAddress = /* our contract address on Ethereum after deploying */
var ZombieFeeding = ZombieFeedingContract.at(contractAddress)

// Assuming we have our zombie's ID and the kitty ID we want to attack
let zombieId = 1;
let kittyId = 1;

// To get the CryptoKitty's image, we need to query their web API. This
// information isn't stored on the blockchain, just their webserver.
// If everything was stored on a blockchain, we wouldn't have to worry
// about the server going down, them changing their API, or the company 
// blocking us from loading their assets if they don't like our zombie game ;)
let apiUrl = "https://api.cryptokitties.co/kitties/" + kittyId
$.get(apiUrl, function(data) {
  let imgUrl = data.image_url
  // do something to display the image
})

// When the user clicks on a kitty:
$(".kittyImage").click(function(e) {
  // Call our contract's `feedOnKitty` method
  ZombieFeeding.feedOnKitty(zombieId, kittyId)
})

// Listen for a NewZombie event from our contract so we can display it:
ZombieFactory.NewZombie(function(error, result) {
  if (error) return
  // This function will display the zombie, like in lesson 1:
  generateZombie(result.zombieId, result.name, result.dna)
})
```

##### LESSON 3: Advanced Solidity Concepts (REVISION NOTES)

- Chapter 1: Immutability of Contracts
    - To start with, after you deploy a contract to Ethereum, it’s immutable, which means that it can never be modified or updated again.
    - The initial code you deploy to a contract is there to stay, permanently, on the blockchain. This is one reason security is such a huge concern in Solidity. If there's a flaw in your contract code, there's no way for you to patch it later. You would have to tell your users to start using a different smart contract address that has the fix.
    - The code is law. 
    - It often makes sense to have functions that will allow you to update key portions of the DApp.
    
- Chapter 2: Ownable Contracts
    -  one common practice that has emerged is to make contracts Ownable — meaning they have an owner (you) who has special privileges.
    -  **OpenZeppelin's Ownable contract:**
        - **Constructors:**
        - **function Modifiers:** modifier onlyOwner(). Modifiers are kind of half-functions that are used to modify other functions, usually to check some requirements prior to execution. In this case, onlyOwner can be used to limit access so only the owner of the contract can run this function. 
        - **indexed keyword:** don't worry about this one, we don't need it yet.
    - So the Ownable contract basically does the following:
        - When a contract is created, its constructor sets the owner to msg.sender (the person who deployed it)
        - It adds an onlyOwner modifier, which can restrict access to certain functions to only the owner
        - It allows you to transfer the contract to a new owner

- Chapter 3: onlyOwner Function Modifier
    - **Function Modifiers:** A function modifier looks just like a function, but uses the keyword modifier instead of the keyword function. And it can't be called directly like a function can — instead we can attach the modifier's name at the end of a function definition to change that function's behavior.
    - Then when it hits the _; statement in onlyOwner, it goes back and executes the code inside function
    
- Chapter 4: Gas
    - In Solidity, your users have to pay every time they execute a function on your DApp using a currency called gas. Users buy gas with Ether (the currency on Ethereum), so your users have to spend ETH in order to execute functions on your DApp. 
    - How much gas is required to execute a function depends on how complex that function's logic is. Each individual operation has a gas cost based roughly on how much computing resources will be required to perform that operation (e.g. writing to storage is much more expensive than adding two integers). The total gas cost of your function is the sum of the gas costs of all its individual operations.
    - Because running functions costs real money for your users, code optimization is much more important in Ethereum than in other programming languages. If your code is sloppy, your users are going to have to pay a premium to execute your functions — and this could add up to millions of dollars in unnecessary fees across thousands of users.
    
    - **Why is gas necessary?** 
        - Ethereum is like a big, slow, but extremely secure computer. When you execute a function, every single node on the network needs to run that same function to verify its output — thousands of nodes verifying every function execution is what makes Ethereum decentralized, and its data immutable and censorship-resistant. 
        - The creators of Ethereum wanted to make sure someone couldn't clog up the network with an infinite loop, or hog all the network resources with really intensive computations. So they made it so transactions aren't free, and users have to pay for computation time as well as storage.
        - **Struct packing to save gas:** 
            - In Lesson 1, we mentioned that there are other types of uints: uint8, uint16, uint32, etc. Normally there's no benefit to using these sub-types because Solidity reserves 256 bits of storage regardless of the uint size. For example, using uint8 instead of uint (uint256) won't save you any gas. 
            - But there's an **exception to this: inside structs.** If you have multiple uints inside a struct, using a smaller-sized uint when possible will allow Solidity to pack these variables together to take up less storage. For example:
            - For this reason, **inside a struct you'll want to use the smallest integer sub-types** you can get away with.
            
- Chapter 5: Time Units
    - The **level property** is pretty self-explanatory. Later on, when we create a battle system, zombies who win more battles will level up over time and get access to more abilities.
    - The **readyTime property** requires a bit more explanation. The goal is to add a "cooldown period", an amount of time a zombie has to wait after feeding or attacking before it's allowed to feed / attack again. Without this, the zombie could attack and multiply 1,000 times per day, which would make the game way too easy. 
    
    - **Time units:** The variable now will return the current unix timestamp of the latest block (the number of seconds that have passed since January 1st 1970). The unix time as I write this is 1515527488.
        - Solidity also contains the time units seconds, minutes, hours, days, weeks and years.
        - Note: The uint32(...) is necessary because now returns a uint256 by default. So we need to explicitly convert it to a uint32.

```
uint lastUpdated;

// Set `lastUpdated` to `now`
function updateTimestamp() public {
  lastUpdated = now;
}

// Will return `true` if 5 minutes have passed since `updateTimestamp` was 
// called, `false` if 5 minutes have not passed
function fiveMinutesHavePassed() public view returns (bool) {
  return (now >= (lastUpdated + 5 minutes));
}
```
        
- Chapter 6: Zombie Cooldowns
    - Now that we have a readyTime property on our Zombie struct, let's jump to zombiefeeding.sol and implement a cooldown timer.
    - We're going to modify our feedAndMultiply such that: Feeding triggers a zombie's cooldown, and Zombies can't feed on kitties until their cooldown period has passed. This will make it so zombies can't just feed on unlimited kitties and multiply all day. In the future when we add battle functionality, we'll make it so attacking other zombies also relies on the cooldown. First, we're going to define some helper functions that let us set and check a zombie's readyTime. 
    - **Passing structs as arguments:** You can pass a storage pointer to a struct as an argument to a private or internal function.
```
function _doStuff(Zombie storage _zombie) internal {
  // do stuff with _zombie
}
```
    
- Chapter 7: Public Functions & Security

- Chapter 8:     
    - **Function modifiers with arguments** 
```
// A mapping to store a user's age:
mapping (uint => uint) public age;

// Modifier that requires this user to be older than a certain age:
modifier olderThan(uint _age, uint _userId) {
  require(age[_userId] >= _age);
  _;
}

// Must be older than 16 to drive a car (in the US, at least).
// We can call the `olderThan` modifier with arguments like so:
function driveCar(uint _userId) public olderThan(16, _userId) {
  // Some function logic
}
```
- Chapter 9: Zombie Modifiers

- Chapter 10: Saving Gas With 'View' Functions
    - Awesome! Now we have some special abilities for higher-level zombies, to give our owners an incentive to level them up. We can add more of these later if we want to.
    - Let's add one more function: our DApp needs a method to view a user's entire zombie army — let's call it getZombiesByOwner.
    - This function will only need to read data from the blockchain, so we can make it a view function. Which brings us to an important topic when talking about gas optimization:
    - **View functions don't cost gas**
        - view functions don't cost any gas when they're called externally by a user.
        - Note: If a view function is called internally from another function in the same contract that is not a view function, it will still cost gas. This is because the other function creates a transaction on Ethereum, and will still need to be verified from every node. So view functions are only free when they're called externally.

- Chapter 11: Storage is Expensive
    - One of the more expensive operations in Solidity is using storage — particularly writes.
        - This is because every time you write or change a piece of data, it’s written permanently to the blockchain. Forever! Thousands of nodes across the world need to store that data on their hard drives, and this amount of data keeps growing over time as the blockchain grows. So there's a cost to doing that.
        - In order to keep costs down, you want to avoid writing data to storage except when absolutely necessary. Sometimes this involves seemingly inefficient programming logic — like rebuilding an array in memory every time a function is called instead of simply saving that array in a variable for quick lookups.
        - In most programming languages, looping over large data sets is expensive. But in Solidity, this is way cheaper than using storage if it's in an external view function, since view functions don't cost your users any gas. (And gas costs your users real money!).
        - **Declaring arrays in memory:**
            - You can use the memory keyword with arrays to create a new array inside a function without needing to write anything to storage. The array will only exist until the end of the function call, and this is a lot cheaper gas-wise than updating an array in storage — free if it's a view function called externally.
            - 
- Chapter 12: For Loops
    - In the previous chapter, we mentioned that sometimes you'll want to use a for loop to build the contents of an array in a function rather than simply saving that array to storage.
    - Let's look at why. 

```
// For our getZombiesByOwner function, a naive implementation would be to store a mapping of owners to zombie armies in the ZombieFactory contract:

mapping (address => uint[]) public ownerToZombies

// Then every time we create a new zombie, we would simply use ownerToZombies[owner].push(zombieId) to add it to that owner's zombies array. And getZombiesByOwner would be a very straightforward function:

function getZombiesByOwner(address _owner) external view returns (uint[]) {
  return ownerToZombies[_owner];
}
```

> The problem with above approach:
> This approach is tempting for its simplicity. But let's look at what happens if we later add a function to transfer a zombie from one owner to another (which we'll definitely want to add in a later lesson!).
> That transfer function would need to:
> 1  Push the zombie to the new owner's ownerToZombies array,
> 2  Remove the zombie from the old owner's ownerToZombies array,
> 3  Shift every zombie in the older owner's array up one place to fill the hole, and then Reduce the array length by 1.
> Step 3 would be extremely expensive gas-wise, since we'd have to do a write for every zombie whose position we shifted. If an owner has 20 zombies and trades away the first one, we would have to do 19 writes to maintain the order of the array.

> Since writing to storage is one of the most expensive operations in Solidity, every call to this transfer function would be extremely expensive gas-wise. And worse, it would cost a different amount of gas each time it's called, depending on how many zombies the user has in their army and the index of the zombie being traded. So the user wouldn't know how much gas to send.

>    Note: Of course, we could just move the last zombie in the array to fill the missing slot and reduce the array length by one. But then we would change the ordering of our zombie army every time we made a trade.

> Since view functions don't cost gas when called externally, we can simply use a for-loop in getZombiesByOwner to iterate the entire zombies array and build an array of the zombies that belong to this specific owner. Then our transfer function will be much cheaper, since we don't need to reorder any arrays in storage, and somewhat counter-intuitively this approach is cheaper overall.

```
Using for loops
function getEvens() pure external returns(uint[]) {
  uint[] memory evens = new uint[](5);
  // Keep track of the index in the new array:
  uint counter = 0;
  // Iterate 1 through 10 with a for loop:
  for (uint i = 1; i <= 10; i++) {
    // If `i` is even...
    if (i % 2 == 0) {
      // Add it to our array
      evens[counter] = i;
      // Increment counter to the next empty index in `evens`:
      counter++;
    }
  }
  return evens;
}
```

- Chapter 13:
- Chapter 14:
 
##### LESSON 4:  Zombie Battle System (REVISION NOTES)  
- Chapter 1:
- Chapter 2:
- Chapter 3:
- Chapter 4:
- Chapter 5:
- Chapter 6:
- Chapter 7:
- Chapter 8:
- Chapter 9:
- Chapter 10:
- Chapter 11:
- Chapter 12:
- Chapter 13:
- Chapter 14:
- 

##### LESSON 5:  ERC721 & Crypto-Collectibles (REVISION NOTES)  
- Chapter 1:
- Chapter 2:
- Chapter 3:
- Chapter 4:
- Chapter 5:
- Chapter 6:
- Chapter 7:
- Chapter 8:
- Chapter 9:
- Chapter 10:
- Chapter 11:
- Chapter 12:
- Chapter 13:
- Chapter 14:
- 

##### LESSON 6: App Front-ends & Web3.js (REVISION NOTES)  
- Chapter 1:
- Chapter 2:
- Chapter 3:
- Chapter 4:
- Chapter 5:
- Chapter 6:
- Chapter 7:
- Chapter 8:
- Chapter 9:
- Chapter 10:
- Chapter 11:
- Chapter 12:
- Chapter 13:
- Chapter 14:

#### **2. Hands-on Path: Make and Deploy a Custom Game Mode**


#### **3. Plasma Path: Learn how to use PlasmaCash**









