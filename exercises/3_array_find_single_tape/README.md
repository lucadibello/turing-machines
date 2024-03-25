# Problem description

In this exercise we are asked to design a Single-tape Turing Machine
(STM) that is able to decide whether a given binary number is present in
a given list of binary numbers. The STM should halt in an accepting
state if the number is present in the list, and in a rejecting state
otherwise.

To perform this task, I have designed the following STM algorithm:

1. Initially, the head of the machine is positioned at the beginning of
   the input string (the first symbol of the entire string).

2. The machine starts by finding the last available symbol of the
   binary number to look for by moving the head to the right until it
   finds the symbol that divides the query input string from the array
   of numbers (symbol \"$|$\") and moves back until it finds an
   unprocessed symbol (last $0$ or $1$ in the query binary number).

3. Now, it marks the current symbol with a special element that allows
   the machine to roll back changes made to the query input string if
   we need to restart the search from the beginning. Zeros will be
   encoded as `A` and ones as `B`.

4. The machine now explores the array elements, looking for an element
   that has the same symbol as what has been found in the previous
   point. To do this, the machine will move to the right until it finds
   the symbol that divides array elements (symbol \"`#`\") and then
   moves back until it finds an unprocessed symbol (last $0$ or $1$ in
   the array element). The matched symbol of the array element is
   marked as `A` or `B` as well.

5. If we encounter a symbol that is different from the one marked in
   the input string, this means that this element is not what we are we
   looking for, so we write a special symbol `Y` to mark that this
   element has already been processed and must not be considered again
   during next iterations of the algorithm. Then, the machine moves
   back to the starting position and resets the input query string to
   allow a fresh start.

6. We then continue iteratively this process, but we must consider that
   as soon as we find the symbol Y in the array, we must skip to the
   next element and continue the search from there as we know that this
   element does not match the query input string.

7. When the machine marks as \"matched\" all symbols of a certain array
   element, it moves back to the starting position to verify if also
   the query input string has been processed. If this is the case, the
   machine halts in an accepting state, otherwise, it goes back to the
   element that resulted \"processed\", we add the special symbol `Y`
   to mark it as processed, and we reset the query input string to
   allow again fresh start.

This machine has been implemented in the file `solution.txt` and can be
tested using the simulator at <https://turingmachinesimulator.com/>.
Somehow the simulator does not allow me to share the link to the machine
directly, but the machine can be loaded by pasting the content of the
file `solution.txt` in the web interface.

The algorithm has been tested with success the following input strings:

- `1|1#101#1101`, final state: `halt-accept`

- `1001|100#1001#0#1111`, final state: `halt-accept`

- `0|0`, final state: `halt-accept`\

- `0|1#101#1101`, final state: `halt-reject`

- `1011|100#1001#0#1111`, final state: `halt-reject`

- `1|0`, final state: `halt-reject`

- `111|`, final state: `halt-reject`
