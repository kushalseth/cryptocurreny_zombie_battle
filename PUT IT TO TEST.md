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
