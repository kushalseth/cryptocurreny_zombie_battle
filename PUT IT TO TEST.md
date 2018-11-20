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

```
It's time to give our zombies the ability to feed and multiply!

When a zombie feeds on some other lifeform, its DNA will combine with the other lifeform's DNA to create a new zombie.

    Create a function called feedAndMultiply. It will take two parameters: _zombieId (a uint) and _targetDna (also a uint). This function should be public.

    We don't want to let someone else feed using our zombie! So first, let's make sure we own this zombie. Add a require statement to make sure msg.sender is equal to this zombie's owner (similar to how we did in the createRandomZombie function).


    We're going to need to get this zombie's DNA. So the next thing our function should do is declare a local Zombie named myZombie (which will be a storage pointer). Set this variable to be equal to index _zombieId in our zombies array.

```

> Chapter 8: Zombie DNA

```


    First we need to make sure that _targetDna isn't longer than 16 digits. To do this, we can set _targetDna equal to _targetDna % dnaModulus to only take the last 16 digits.

    Next our function should declare a uint named newDna, and set it equal to the average of myZombie's DNA and _targetDna (as in the example above).

        Note: You can access the properties of myZombie using myZombie.name and myZombie.dna

    Once we have the new DNA, let's call _createZombie. You can look at the zombiefactory.sol tab if you forget which parameters this function needs to call it. Note that it requires a name, so let's set our new zombie's name to "NoName" for now — we can write a function to change zombies' names later.

```

> Chapter 9: More on Function Visibility

```
Change _createZombie() from private to internal so our other contract can access it.
```

> Chapter 10: What Do Zombies Eat?

```
Now that we know what this function looks like, we can use it to create an interface:

    Define an interface called KittyInterface. Remember, this looks just like creating a new contract — we use the contract keyword.

    Inside the interface, define the function getKitty (which should be a copy/paste of the function above, but with a semi-colon after the returns statement, instead of everything inside the curly braces.

```

> Chapter 11: Using an Interface

```
I've saved the address of the CryptoKitties contract in the code for you, under a variable named ckAddress. In the next line, create a KittyInterface named kittyContract, and initialize it with ckAddress — just like we did with numberContract above.
```

> Chapter 12: Handling Multiple Return Values

```
Time to interact with the CryptoKitties contract!

Let's make a function that gets the kitty genes from the contract:

    Make a function called feedOnKitty. It will take 2 uint parameters, _zombieId and _kittyId, and should be a public function.

    The function should first declare a uint named kittyDna.

        Note: In our KittyInterface, genes is a uint256 — but if you remember back to lesson 1, uint is an alias for uint256 — they're the same thing.

    The function should then call the kittyContract.getKitty function with _kittyId and store genes in kittyDna. Remember — getKitty returns a ton of variables. (10 to be exact — I'm nice, I counted them for you!). But all we care about is the last one, genes. Count your commas carefully!

    Finally, the function should call feedAndMultiply, and pass it both _zombieId and kittyDna.

```

> Chapter 13: Bonus: Kitty Genes

```
Let's implement cat genes in our zombie code.

    First, let's change the function definition for feedAndMultiply so it takes a 3rd argument: a string named _species

    Next, after we calculate the new zombie's DNA, let's add an if statement comparing the keccak256 hashes of _species and the string "kitty". We can't directly pass strings to keccak256. Instead, we will pass abi.encodePacked(_species) as an argument on the left side and abi.encodePacked("kitty") as an argument on the right side.

    Inside the if statement, we want to replace the last 2 digits of DNA with 99. One way to do this is using the logic: newDna = newDna - newDna % 100 + 99;.

        Explanation: Assume newDna is 334455. Then newDna % 100 is 55, so newDna - newDna % 100 is 334400. Finally add 99 to get 334499.

    Lastly, we need to change the function call inside feedOnKitty. When it calls feedAndMultiply, add the parameter "kitty" to the end.

```

> Chapter 14: Wrapping It Up



##### LESSON 3: Advanced Solidity Concepts (REVISION NOTES)

> Chapter 1: Immutability of Contracts

```
Let's update our code from Lesson 2 to be able to change the CryptoKitties contract address.

    Delete the line of code where we hard-coded ckAddress.

    Change the line where we created kittyContract to just declare the variable — i.e. don't set it equal to anything.

    Create a function called setKittyContractAddress. It will take one argument, _address (an address), and it should be an external function.

    Inside the function, add one line of code that sets kittyContract equal to KittyInterface(_address).

```

> Chapter 2: Ownable Contracts

```
We've gone ahead and copied the code of the Ownable contract into a new file, ownable.sol. Let's go ahead and make ZombieFactory inherit from it.

    Modify our code to import the contents of ownable.sol. If you don't remember how to do this take a look at zombiefeeding.sol.

    Modify the ZombieFactory contract to inherit from Ownable. Again, you can take a look at zombiefeeding.sol if you don't remember how this is done.

```

> Chapter 3: onlyOwner Function Modifier

```
add onlyOwner to setKittyContractAddress
```

> Chapter 4: Gas

```
In this lesson, we're going to add 2 new features to our zombies: level and readyTime — the latter will be used to implement a cooldown timer to limit how often a zombie can feed.

So let's jump back to zombiefactory.sol.

    Add two more properties to our Zombie struct: level (a uint32), and readyTime (also a uint32). We want to pack these data types together, so let's put them at the end of the struct.

32 bits is more than enough to hold the zombie's level and timestamp, so this will save us some gas costs by packing the data more tightly than using a regular uint (256-bits).
```

> Chapter 5: Time Units

```
Let's add a cooldown time to our DApp, and make it so zombies have to wait 1 day after attacking or feeding to attack again.

    Declare a uint called cooldownTime, and set it equal to 1 days. (Forgive the poor grammar — if you set it equal to "1 day", it won't compile!)

    Since we added a level and readyTime to our Zombie struct in the previous chapter, we need to update _createZombie() to use the correct number of arguments when we create a new Zombie struct.

    Update the zombies.push line of code to add 2 more arguments: 1 (for level), and uint32(now + cooldownTime) (for readyTime).

    Note: The uint32(...) is necessary because now returns a uint256 by default. So we need to explicitly convert it to a uint32.

now + cooldownTime will equal the current unix timestamp (in seconds) plus the number of seconds in 1 day — which will equal the unix timestamp 1 day from now. Later we can compare to see if this zombie's readyTime is greater than now to see if enough time has passed to use the zombie again.

We'll implement the functionality to limit actions based on readyTime in the next chapter.
```

> Chapter 6: Zombie Cooldowns

```
Put it to the test

    Start by defining a _triggerCooldown function. It will take 1 argument, _zombie, a Zombie storage pointer. The function should be internal.

    The function body should set _zombie.readyTime to uint32(now + cooldownTime).

    Next, create a function called _isReady. This function will also take a Zombie storage argument named _zombie. It will be an internal view function, and return a bool.

    The function body should return (_zombie.readyTime <= now), which will evaluate to either true or false. This function will tell us if enough time has passed since the last time the zombie fed.

```

> Chapter 7: Public Functions & Security

```


    Currently feedAndMultiply is a public function. Let's make it internal so that the contract is more secure. We don't want users to be able to call this function with any DNA they want.

    Let's make feedAndMultiply take our cooldownTime into account. First, after we look up myZombie, let's add a require statement that checks _isReady() and passes myZombie to it. This way the user can only execute this function if a zombie's cooldown time is over.

    At the end of the function let's call _triggerCooldown(myZombie) so that feeding triggers the zombie's cooldown time.

```

> Chapter 8:

```


    In ZombieHelper, create a modifier called aboveLevel. It will take 2 arguments, _level (a uint) and _zombieId (also a uint).

    The body should check to make sure zombies[_zombieId].level is greater than or equal to _level.

    Remember to have the last line of the modifier call the rest of the function with _;.

```

> Chapter 9: Zombie Modifiers

```


    Create a function called changeName. It will take 2 arguments: _zombieId (a uint), and _newName (a string), and make it external. It should have the aboveLevel modifier, and should pass in 2 for the _level parameter. (Don't forget to also pass the _zombieId).

    In this function, first we need to verify that msg.sender is equal to zombieToOwner[_zombieId]. Use a require statement.

    Then the function should set zombies[_zombieId].name equal to _newName.

    Create another function named changeDna below changeName. Its definition and contents will be almost identical to changeName, except its second argument will be _newDna (a uint), and it should pass in 20 for the _level parameter on aboveLevel. And of course, it should set the zombie's dna to _newDna instead of setting the zombie's name.

```

> Chapter 10: Saving Gas With 'View' Functions

```
We're going to implement a function that will return a user's entire zombie army. We can later call this function from web3.js if we want to display a user profile page with their entire army.

This function's logic is a bit complicated so it will take a few chapters to implement.

    Create a new function named getZombiesByOwner. It will take one argument, an address named _owner.

    Let's make it an external view function, so we can call it from web3.js without needing any gas.

    The function should return a uint[] (an array of uint).

Leave the function body empty for now, we'll fill it in in the next chapter.
```

> Chapter 11: Storage is Expensive

```
In our getZombiesByOwner function, we want to return a uint[] array with all the zombies a particular user owns.

    Declare a uint[] memory variable called result

    Set it equal to a new uint array. The length of the array should be however many zombies this _owner owns, which we can look up from our mapping with: ownerZombieCount[_owner].

    At the end of the function return result. It's just an empty array right now, but in the next chapter we'll fill it in.

```

> Chapter 12: For Loops

```
Let's finish our getZombiesByOwner function by writing a for loop that iterates through all the zombies in our DApp, compares their owner to see if we have a match, and pushes them to our result array before returning it.

    Declare a uint called counter and set it equal to 0. We'll use this variable to keep track of the index in our result array.

    Declare a for loop that starts from uint i = 0 and goes up through i < zombies.length. This will iterate over every zombie in our array.

    Inside the for loop, make an if statement that checks if zombieToOwner[i] is equal to _owner. This will compare the two addresses to see if we have a match.

    Inside the if statement:
        Add the zombie's ID to our result array by setting result[counter] equal to i.
        Increment counter by 1 (see the for loop example above).

That's it — the function will now return all the zombies owned by _owner without spending any gas.
```

> Chapter 13:

```
```

> Chapter 14:

```
```

##### LESSON 4:  Zombie Battle System (REVISION NOTES)  
> Chapter 1: Payable

```
Let's create a payable function in our zombie game.

Let's say our game has a feature where users can pay ETH to level up their zombies. The ETH will get stored in the contract, which you own — this a simple example of how you could make money on your games!

    Define a uint named levelUpFee, and set it equal to 0.001 ether.

    Create a function named levelUp. It will take one parameter, _zombieId, a uint. It should be external and payable.

    The function should first require that msg.value is equal to levelUpFee.

    It should then increment this zombie's level: zombies[_zombieId].level++.

```

> Chapter 2: Withdraws


```


    Create a withdraw function in our contract, which should be identical to the GetPaid example above.

    The price of Ether has gone up over 10x in the past year. So while 0.001 ether is about $1 at the time of this writing, if it goes up 10x again, 0.001 ETH will be $10 and our game will be a lot more expensive.

    So it's a good idea to create a function that allows us as the owner of the contract to set the levelUpFee.

    a. Create a function called setLevelUpFee that takes one argument, uint _fee, is external, and uses the modifier onlyOwner.

    b. The function should set levelUpFee equal to _fee.

```

> Chapter 3: Zombie Battles

```
Let's review creating a new contract. Repetition leads to mastery!

If you can't remember the syntax for doing these, check zombiehelper.sol for the syntax — but try to do it without peeking first to test your knowledge.

    Declare at the top of the file that we're using Solidity version ^0.4.25.

    import from zombiehelper.sol.

    Declare a new contract called ZombieAttack that inherits from ZombieHelper. Leave the contract body empty for now.

```

> Chapter 4: Random Numbers

```
Let's implement a random number function we can use to determine the outcome of our battles, even if it isn't totally secure from attack.

    Give our contract a uint called randNonce, and set it equal to 0.

    Create a function called randMod (random-modulus). It will be an internal function that takes a uint named _modulus, and returns a uint.

    The function should first increment randNonce (using the syntax randNonce++).

    Finally, it should (in one line of code) calculate the uint typecast of the keccak256 hash of abi.encodePacked(now,msg.sender,randNonce) — and return that value % _modulus. (Whew! That was a mouthful. If you didn't follow that, just take a look at the example above where we generated a random number — the logic is very similar).

```

> Chapter 5: Zombie Fightin'

```


    Give our contract a uint variable called attackVictoryProbability, and set it equal to 70.

    Create a function called attack. It will take two parameters: _zombieId (a uint) and _targetId (also a uint). It should be an external function.

Leave the function body empty for now
```

> Chapter 6: Refactoring Common Logic

```
We're back to zombiefeeding.sol, since this is the first place we used that logic. Let's refactor it into its own modifier.

    Create a modifier called ownerOf. It will take 1 argument, _zombieId (a uint).

    The body should require that msg.sender is equal to zombieToOwner[_zombieId], then continue with the function. You can refer to zombiehelper.sol if you don't remember the syntax for a modifier.

    Change the function definition of feedAndMultiply such that it uses the modifier ownerOf.

    Now that we're using a modifier, you can remove the line require(msg.sender == zombieToOwner[_zombieId]);

```

> Chapter 7: More Refactoring

```
```

> Chapter 8:  Back to Attack!

```


    Add the ownerOf modifier to attack to make sure the caller owns _zombieId.

    The first thing our function should do is get a storage pointer to both zombies so we can more easily interact with them:

    a. Declare a Zombie storage named myZombie, and set it equal to zombies[_zombieId].

    b. Declare a Zombie storage named enemyZombie, and set it equal to zombies[_targetId].

    We're going to use a random number between 0 and 99 to determine the outcome of our battle. So declare a uint named rand, and set it equal to the result of the randMod function with 100 as an argument.

```

> Chapter 9:  Zombie Wins and Losses

```


    Modify our Zombie struct to have 2 more properties:

    a. winCount, a uint16

    b. lossCount, also a uint16

        Note: Remember, since we can pack uints inside structs, we want to use the smallest uints we can get away with. A uint8 is too small, since 2^8 = 256 — if our zombies attacked once per day, they could overflow this within a year. But 2^16 is 65536 — so unless a user wins or loses every day for 179 years straight, we should be safe here.

    Now that we have new properties on our Zombie struct, we need to change our function definition in _createZombie().

    Change the zombie creation definition so it creates each new zombie with 0 wins and 0 losses.

```

> Chapter 10: Zombie Victory 😄

```


    Create an if statement that checks if rand is less than or equal to attackVictoryProbability.

    If this condition is true, our zombie wins! So:

    a. Increment myZombie's winCount.

    b. Increment myZombie's level. (Level up!!!!!!!)

    c. Increment enemyZombie's lossCount. (Loser!!!!!! 😫 😫 😫)

    d. Run the feedAndMultiply function. Check zombiefeeding.sol to see the syntax for calling it. For the 3rd argument (_species), pass the string "zombie". (It doesn't actually do anything at the moment, but later we could add extra functionality for spawning zombie-based zombies if we wanted to).

```

> Chapter 11: Zombie Loss 

```
```

> Chapter 12: Wrapping It Up

```
```

> Chapter 13:

```
```

> Chapter 14:

```
```



##### LESSON 5:  ERC721 & Crypto-Collectibles (REVISION NOTES)  	
> Chapter 1:

```
Putting it to the Test

We're going to dive into the ERC721 implementation in the next chapter. But first, let's set up our file structure for this lesson.

We're going to store all the ERC721 logic in a contract called ZombieOwnership.

    Declare our pragma version at the top of the file (check previous lessons' files for the syntax).

    This file should import from zombieattack.sol.

    Declare a new contract, ZombieOwnership, that inherits from ZombieAttack. Leave the body of the contract empty for now.

```

> Chapter 2: ERC721 Standard, Multiple Inheritance


```
impoert erc721
```

> Chapter 3: balanceOf & ownerOf

```
I'll leave it to you to figure out how to implement these 2 functions.

Each function should simply be 1 line of code, a return statement. Take a look at our code from previous lessons to see where we're storing this data. If you can't figure it out, you can hit the "show me the answer" button for some help.

    Implement balanceOf to return the number of zombies _owner has.

    Implement ownerOf to return the address of whoever owns the zombie with ID _tokenId.

```

> Chapter 4:

```
```

> Chapter 5:

```
```

> Chapter 6:

```
```

> Chapter 7:

```
```

> Chapter 8:

```
```

> Chapter 9:

```
```

> Chapter 10:

```
```

> Chapter 11:

```
```

> Chapter 12:

```
```

> Chapter 13:

```
```

> Chapter 14:

```
```





##### LESSON 6:  App Front-ends & Web3.js (REVISION NOTES)  (REVISION NOTES)  	
> Chapter 1:

```
```

> Chapter 2:


```
```

> Chapter 3:

```
```

> Chapter 4:

```
```

> Chapter 5:

```
```

> Chapter 6:

```
```

> Chapter 7:

```
```

> Chapter 8:

```
```

> Chapter 9:

```
```

> Chapter 10:

```
```

> Chapter 11:

```
```

> Chapter 12:

```
```

> Chapter 13:

```
```

> Chapter 14:

```
```


