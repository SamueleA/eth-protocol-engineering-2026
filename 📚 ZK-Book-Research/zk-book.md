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


part 2: TODO

part 3: TODO