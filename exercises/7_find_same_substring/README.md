# Problem description

In this exercise, we are asked to design a Non-deterministic Turing
Machine (NTM) that is able to decide whether a given string that
represents a set of binary elements divided by a symbol `#`, if there
are two identical elements in the set. The machine should halt in an
accepting state if the two identical elements are found, and in a
rejecting state otherwise.

The input format is `<element1>##...#<elementN>`, where each element is
a number represented in binary form, and the symbol `#` is used to
separate them.

To solve this problem, I leveraged non-determinism to explore all
possible combination of elements in the input string. These are the main
steps of the algorithm:

1. The machine starts by moving the head to the right until it finds
   the dividing symbol `#` that separates the first element from the
   second one. At this point, the machine non-deterministically splits
   into two branches: one that will explore the rest of the input
   string looking for a match with the first element, and the other
   that will continue to the next element without effectively searching
   for a match. This allows the machine to explore all possible
   combinations of elements in the input string.

2. As soon the machine enters a search branch, it will change the
   diving symbol of the element from `#` to `^` in order to remember
   what element is being searched. The machine will then move to the
   right until it finds the next dividing symbol `#` and will compare
   the current element with the one that is being searched going back
   and forth between each symbol of the two elements. If the two
   elements match perfectly (no differences or unmatched symbols are
   found), the machine will halt in an accepting state, as the two
   elements are identical.

3. If the machine does not find a match, it will move back to the
   starting position and will continue to the next element of the input
   string. The machine will then repeat the process for each element in
   the input string, exploring all possible combinations of elements.

4. If no match, the machine will halt in a rejecting state, as no
   identical elements have been found in the input string.

The algorithm has been implemented in the file `solution.txt` and can
be tested using the non-deterministic Turing machine simulator:
<https://francoisschwarzentruber.github.io/turingmachinesimulator/>.

I have tested the machine with the following input strings:

- `11#10101#1101#11`, final state: `acc`

- `1010#1111#1#101#1111#1011`, final state: `acc`

- `1000#1000`, final state: `acc`

- `_`(empty string), final state: `rej`

- `#`, final state: `rej`

- `101`, final state: `rej`

- `11#1111`, final state: `rej`
