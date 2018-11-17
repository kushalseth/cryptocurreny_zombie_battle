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
Example:
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
    - Most of the time you don't need to use these keywords because Solidity handles them by default. **State variables** (variables declared outside of functions) are by default storage and written permanently to the blockchain, while **variables declared inside functions** are memory and will disappear when the function call ends.
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
- Chapter 8:
- Chapter 9:
- Chapter 10:



#### **2. Hands-on Path: Make and Deploy a Custom Game Mode**


#### **3. Plasma Path: Learn how to use PlasmaCash**


