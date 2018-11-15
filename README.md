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
- sas

#### **2. Hands-on Path: Make and Deploy a Custom Game Mode**


#### **3. Plasma Path: Learn how to use PlasmaCash**





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
    
- sas

#### **2. Hands-on Path: Make and Deploy a Custom Game Mode**


#### **3. Plasma Path: Learn how to use PlasmaCash**





