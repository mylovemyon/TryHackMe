## John who?
Welcome  
John the Ripper is one of the most well known, well-loved and versatile hash cracking tools out there. It combines a fast cracking speed, with an extraordinary range of compatible hash types. This room will assume no previous knowledge, so we must first cover some basic terms and concepts before we move into practical hash cracking.
### What are Hashes?
A hash is a way of taking a piece of data of any length and  representing it in another form that is a fixed length. This masks the original value of the data. This is done by running the original data through a hashing algorithm. There are many popular hashing algorithms, such as MD4,MD5, SHA1 and NTLM. Lets try and show this with an example:  
If we take "polo", a string of 4 characters- and run it through an MD5 hashing algorithm, we end up with an output of: b53759f3ce692de7aff1b5779d3964da a standard 32 character MD5 hash.  
Likewise, if we take "polomints", a string of 9 characters- and run it through the same MD5 hashing algorithm, we end up with an output of: 584b6e4f4586e136bc280f27f9c64f3b another standard 32 character MD5 hash.

### What makes Hashes secure?
Hashing functions are designed as one-way functions. In other words, it is easy to calculate the hash value of a given input; however, it is a difficult problem to find the original input given the hash value. By "difficult", we mean that it is computationally infeasible. This has its roots in mathematics and P vs NP.  
In computer science, P and NP are two classes of problems that help us understand the efficiency of algorithms:  
- P (Polynomial Time): Class P covers the problems whose solution can be found in polynomial time. Consider sorting a list in increasing order. The longer the list, the longer it would take to sort; nonetheless, the increase in time is not exponential.  
- NP (Non-deterministic Polynomial Time): Problems in the class NP are those for which a given solution can be checked quickly, even though finding the solution itself might be hard. In fact, we don't know if there is a fast algorithm to find the solution in the first place.

While this is an extremely interesting mathematical concept that proves fundamental to computing and cryptography, it is completely outside the scope of this room. But abstractly it means that the algorithm to hash the value will be "P" and can therefore be calculated reasonably. However an un-hashing algorithm would be "NP" and intractable to solve- meaning that it cannot be computed in a reasonable time using standard computers.

### Where John Comes in...
Even though the algorithm itself is not feasibly reversible. That doesn't mean that cracking the hashes is impossible. If you have the hashed version of a password, for example- and you know the hashing algorithm- you can use that hashing algorithm to hash a large number of words, called a dictionary. You can then compare these hashes to the one you're trying to crack, to see if any of them match. If they do, you now know what word corresponds to that hash- you've cracked it!  
This process is called a dictionary attack and John the Ripper, or John as it's commonly shortened to, is a tool to allow you to conduct fast brute force attacks on a large array of different hash types.


###
