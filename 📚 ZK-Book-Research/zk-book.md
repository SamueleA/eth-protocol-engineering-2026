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
(P4 = Q4 ∧ P3 = Q3 ∧ P2 = Q2 ∧ P1 > Q1)

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