# PUT IT TO TEST

##### LESSON 1: Making the Zombie Factory  (REVISION NOTES)
> Chapter 1: Lesson Overview



> Chapter 2: Contract

```
To start creating our Zombie army, let's create a base contract called ZombieFactory.

    In the box to the right, make it so our contract uses solidity version 0.4.25.

    Create an empty contract called ZombieFactory.

When you're finished, click "check answer" below. If you get stuck, you can click "hint".
```

> Chapter 3: State Variables & Integers

```
Our Zombie DNA is going to be determined by a 16-digit number.

Declare a uint named dnaDigits, and set it equal to 16.
```

> Chapter 4: Math Operations

```
To make sure our Zombie's DNA is only 16 characters, let's make another uint equal to 10^16. That way we can later use the modulus operator % to shorten an integer to 16 digits.

    Create a uint named dnaModulus, and set it equal to 10 to the power of dnaDigits.

```

> Chapter 5: Structs

```
In our app, we're going to want to create some zombies! And zombies will have multiple properties, so this is a perfect use case for a struct.

    Create a struct named Zombie.

    Our Zombie struct will have 2 properties: name (a string), and dna (a uint).

```

> Chapter 6: Arrays

```
We're going to want to store an army of zombies in our app. And we're going to want to show off all our zombies to other apps, so we'll want it to be public.

    Create a public array of Zombie structs, and name it zombies.

```

> Chapter 7: Function Declarations

```
In our app, we're going to need to be able to create some zombies. Let's create a function for that.

    Create a function named createZombie. It should take two parameters: __name_ (a string), and __dna_ (a uint).

Leave the body empty for now — we'll fill it in later.
```

> Chapter 8: Working With Structs and Arrays

```
Let's make our createZombie function do something!

    Fill in the function body so it creates a new Zombie, and adds it to the zombies array. The name and dna for the new Zombie should come from the function arguments.
    Let's do it in one line of code to keep things clean.

```

> Chapter 9: Private / Public Functions
```
Our contract's createZombie function is currently public by default — this means anyone could call it and create a new Zombie in our contract! Let's make it private.

    Modify createZombie so it's a private function. Don't forget the naming convention!

```

> Chapter 10: More on Functions

```
We're going to want a helper function that generates a random DNA number from a string.

    Create a private function called _generateRandomDna. It will take one parameter named _str (a string), and return a uint.

    This function will view some of our contract's variables but not modify them, so mark it as view.

    The function body should be empty at this point — we'll fill it in later.

```

> Chapter 11: Keccak256 and Typecasting

```
Let's fill in the body of our _generateRandomDna function! Here's what it should do:

    The first line of code should take the keccak256 hash of abi.encodePacked(_str) to generate a pseudo-random hexidecimal, typecast it as a uint, and finally store the result in a uint called rand.

    We want our DNA to only be 16 digits long (remember our dnaModulus?). So the second line of code should return the above value modulus (%) dnaModulus.

```

> Chapter 12: Putting It Together

```


    Create a public function named createRandomZombie. It will take one parameter named _name (a string). (Note: Declare this function public just as you declared previous functions private)

    The first line of the function should run the _generateRandomDna function on _name, and store it in a uint named randDna.

    The second line should run the _createZombie function and pass it _name and randDna.

    The solution should be 4 lines of code (including the closing } of the function).

```

> Chapter 13

```
We want an event to let our front-end know every time a new zombie was created, so the app can display it.

    Declare an event called NewZombie. It should pass zombieId (a uint), name (a string), and dna (a uint).

    Modify the _createZombie function to fire the NewZombie event after adding the new Zombie to our zombies array.

    You're going to need the zombie's id. array.push() returns a uint of the new length of the array - and since the first item in an array has index 0, array.push() - 1 will be the index of the zombie we just added. Store the result of zombies.push() - 1 in a uint called id, so you can use this in the NewZombie event in the next line.

```

##### LESSON 2: Zombies Attack Their Victims 

> Chapter 2: Mappings and Addresses   
```
To store zombie ownership, we're going to use two mappings: one that keeps track of the address that owns a zombie, and another that keeps track of how many zombies an owner has.

    Create a mapping called zombieToOwner. The key will be a uint (we'll store and look up the zombie based on its id) and the value an address. Let's make this mapping public.

    Create a mapping called ownerZombieCount, where the key is an address and the value a uint.

``` 

> Chapter 3: Msg.sender
```
Let's update our _createZombie method from lesson 1 to assign ownership of the zombie to whoever called the function.

    First, after we get back the new zombie's id, let's update our zombieToOwner mapping to store msg.sender under that id.

    Second, let's increase ownerZombieCount for this msg.sender.

In Solidity, you can increase a uint with ++, just like in javascript:

uint number = 0;
number++;
// `number` is now `1`

Your final answer for this chapter should be 2 lines of code.
```

> Chapter 4: Require
```
In our zombie game, we don't want the user to be able to create unlimited zombies in their army by repeatedly calling createRandomZombie — it would make the game not very fun.

Let's use require to make sure this function only gets executed one time per user, when they create their first zombie.

    Put a require statement at the beginning of createRandomZombie. The function should check to make sure ownerZombieCount[msg.sender] is equal to 0, and throw an error otherwise.

    Note: In Solidity, it doesn't matter which term you put first — both orders are equivalent. However, since our answer checker is really basic, it will only accept one answer as correct — it's expecting ownerZombieCount[msg.sender] to come first.

```

> Chapter 5: Inheritance
```
In the next chapters, we're going to be implementing the functionality for our zombies to feed and multiply. Let's put this logic into its own contract that inherits all the methods from ZombieFactory.

    Make a contract called ZombieFeeding below ZombieFactory. This contract should inherit from our ZombieFactory contract.

```

> Chapter 6: Import
```
Now that we've set up a multi-file structure, we need to use import to read the contents of the other file:

    Import zombiefactory.sol into our new file, zombiefeeding.sol.

```

> Chapter 7: Storage vs Memory