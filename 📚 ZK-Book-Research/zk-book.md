# ZK book summaries

Summaries for the [zk book](https://rareskills.io/tutorials/zk-book) by Rareskills. These summaries are meant to help test my comprehension and improve my retension.

## Chapter 1: P VS NP and its application to zero knowledge proofs
part 1:
An algorithm is efficient, or easy to compute, if it run in O(n^c), where n is the size of the data and c is a constant. This is also called polynomial time. Polynomial time = efficient = easy to compute.

An algorithm is inefficient, or difficult to compute,  if it runs in O(c^n) where c is a constant and n is the size of the date. Exponential time = inefficient = difficult to compute

*P problems*
These problems are easy to solve and easy to verify.
Example: sorting a list.
Solving: Can be done in O(n log(n)) time with an algo such as mergesort.
Verifying: Done in O(n) as we go through the list.

Witness: proof that a problem has been solved. With the example above, this would be providing the sorted list.

*PSPACE problems*
These problems are both difficult to solve and difficult to verify.
Example: Finding the best move in chess.
Solving: Verify every possible chess move and the resulting board state.
Verifying: Doing the exact same work that has been done to solve it.

*NP Problems*
Problems that are easy to verify but difficult to solve.
Example: Solving a sudoky VS verifying that a sudoky solution is correct
Computing the 3 coloring of a map
Finding the assignment to a boolean formula.

If the set P = NP, then all problems that can be verified easily can be solved easily. Whether P = NP or not has not been proved yet, but most people believe P != NP and NP != PSPACE, that is to say that P is a subset of NP which is a subset of PSPACE.

If P=NP, then all encryption would break as we rely on the assymetry between solving and proving for encryption schemes.


part 2:
Verifying a P or NP problem can be done through an encoding of the problem in a boolean formula.

Boolean formula = boolean circuit.
Boolean formula are easy to verify (just plug in the true or false values of the variables), but difficult to prove(in other words NP, since the only way to solve is to try all the combinations of values).

P > Q
if P and Q are bits ( 0 or 1), the following boolean formula encodes the relationship
P∧¬Q

P = Q
encoded by this formulate
(P∧Q) ∨ ¬(P∨Q)

combining both, we can calculate P >= Q
(P∧¬Q)∧((P∧Q) ∨ ¬(P∨Q))

The above is just for a big but we can tell if a number (a sequence of bits) if greater than or equal to another number by iterating through each bit from Most significant to Least. If one of the bits is higher, then we know that the number is > the other. If it's equal all the way through, then the number is equal.

P >= Q, as 4-bit numbers could be encoded so (with number Q, representaed as bit sequence Q4-Q3-Q2-Q1)

(P4 > Q4) ∨
(P4 = Q4 ∧ P3 > Q3) ∨
(P4 = Q4 ∧ P3 = Q3 ∧ P2 > Q2) ∨
(P4 = Q4 ∧ P3 = Q3 ∧ P2 = Q2 ∧ P1 > Q1) ∨
(P4 = Q4 ∧ P3 = Q3 ∧ P2 = Q2 ∧ P1 = Q1) 

With the above, we can not construct a witness to verify whether a list if sorted. We compare each adjacent pair of indexed values and verify if the second is >= to the first. If yes, we move to the next number and make another check. We AND all of those checks and we have our boolean circuit.

3 color problem.

A similar problem is the 3 color problem. We can also construct a boolean circuit for this.

1. First we construct the boolean circuit specifying that each country can only be 1 color.
2. We construct the boolean circuit encoding the fact that each neighbor cannot be the same color.

The two examples above show how we can construct a boolean formula/boolean circuit which is exponential to solve but can be verified in polynomial time with a witness.


part 3:
The point of a ZK proof is to demonstrate that I have a witness without showing the witness.

All P and NP problems can be expressed in boolean circuits and thus we could provide a witness to it and thus began constructing a ZK scheme.

With a witness, we could verify that a computation has been performed without having to perform it ourselves.

For PSPACE problems, zk proofs don't work since we can't construct a boolean circuit allowing us to verify easily, thus zk proofs don't work with such problems (like finding the best move in chess).

## Chapter 2: Arithmetic Circuits for ZK
Boolean circuits tend to be verbose, including when testing arithmetic statements. Thus we use arithmetic circuits instead.

Like a boolean circuit, a circuit is satisfied by a witness if all the variables provided satisfy ALL the equations.

In circom (a programming language used in ZK), variable  = signals. Also,  `===` means equality.

*Interpreting arithmetic circuits*
`x(x-1) === 0` << restricts x to be either 0 or 1. 

Arithmetic circuits require less inpputs than boolean circutis

Arithmetic and boolean circuits are equivalent. Any arithmetic circuit can be converted into a boolean circuit.

*Example with arithmetic circuits*

3 color problem.

We first assign a number to each color. EG blue=1, red=2, yellow=3

Then, we restrict each state to only have 1 such number.

`0 = (1-x) * (2-x) * (3-x)`

Then, we model the fact that both status cannot be the same number so we excludes squares, such as 1, 4, 9.

`0 = (2 - xy) * (3 - xy) * (6 - xy)`

*Proving a list is sorted*
We have to be able to compate GTE(x1, x2). If we can have such as circuit, then we can simple compare each pair of numbers in the list.

First we convert numbes to binary. If 3 bits.

```
# the number must be 3 bits
v = b2² + b1² + b0

# each bit is either 0 or 1
0 = b0(b0 -1)
0 = b1(b1 -1)
0 = b2(b2 -1)
```

2^n = require n + 1 bit to represent
2^(n-1) = the "midoint", half the value above. Requires n bits. The MSB is 1 and all other bits are 0
2^n - 1 = the maximum number that can be represented with n bit... all the bits are 1.

```
0000
0001
0010
0011
0100
0101
0110
0111
1000  <<<<<<<< the midpoint AKA 2^(n-1)
1001
1010
1011
1100
1101
1110
1111
```

if we compute u-v with three bit and add the midpoint we can tell the if u >= v by looking at the MSB to see if it is 1 or 0.

midpoint + u-v >> if MSB === 1, u >= v, otherwise v < u

so for the GTE(x1, x2) function we must:
1. Constrain x1, x2 to be at most n-1 bits
2. Contains the bits to be 0 or 1.
3. do the same for the sum with the midpoint but for 4 bits.
4. look is the MSB of that sum is 1.

*how arithmetic circuit can model boolean circuits`*

Contraint number to 0 or 1.

`0 = u(u - 1)`

AND gate
`t = u*v`

NOT game
`t = 1 - u`

OR gate

`t = u + v - u*v`

Since all NP problems can be modelled as boolean circuits (the Cook-Levin Theorem), and all boolean circuits can be modelled with arithmetic circuits, it follows that all NP problems can be modelled as arithmetic.

Problems: