### Counting

**`git`** obsesses over SHA1s, which are forty-hex-digit strings, such as
```e69de29bb2d1d6434b8b29ae775ad8c2e48c5391` that name objects.

#### Quiz 1

How many different SHA1s are there? That is, how big is the space of possible objects?

- In hex?
- In binary?
- In decimal, approximately? (2^10 ~ 10^3)

#### Quiz 2

What are good ways to say how big this is?

- How big is a Mole (the number, not the animal)? What is the definition of a gross?
- How many stars are there?
- How many grains of sand did Archimedes decide it would take to fill the universe?
- What good analogy can you find to describe the number of SHA1s?

#### Quiz 3

When you're doing things with an object, **`git`** will let you get away with abbreviating SHA1s.
instead of typing
```git cat-file -p e69de29bb2d1d6434b8b29ae775ad8c2e48c5391```
you can type
```git cat-file -p e69d```

- How many would you have to create before you knew you had a four-hex-digit, hash collision --
before some two had the same four-hex-digit abbreviation?
- How many different objects would you have to create
to be guaranteed you had two different ones with the SHA1 abbreviation e69d?
- Although there are 367 possible birthdays, once you get 23 people in a room,
the probability that two people in the room have the same birthday --
that is, have a "birthday collision" -- goes over 50%.
Why?
- How many objects do you need before the probabilty of a 7-hex-digit, hash collision goes over 50%?
How safe are 7-hex-digit abbreviations?
- How many objects do you need before the probability of a SHA1 collision goes over 50%?
Over 1%?
- What's the connection between hash collisions and bitcoins?
