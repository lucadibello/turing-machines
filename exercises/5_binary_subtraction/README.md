# Problem description

In this exercise, we are asked to design a Multi-tape Turing Machine
(MTM) that is able to compute the subtraction of two given binary
numbers. The machine should halt in an accepting state when the result
of the subtraction is found, and in a rejecting state if it detects a
syntax error in the input string or if the result would be negative.

I identified two main approaches to solve this problem:

1. **Simple subtraction**: The machine computes the subtraction of the
   two numbers by subtracting one digit at the time, starting from the
   least significant bit (LSB) and moving to the most significant one
   (MSB). This approach requires to implement a mechanism to handle the
   borrow operation to perform the subtraction $0 - 1$.

2. **Two's complement**: This other approach is based on the two's
   complement representation, allowing to perform the subtraction of
   two numbers by adding the two's complement of the second number to
   the first one. Learn more
   [<https://en.wikipedia.org/wiki/Two%27s_complement>](here).

For simplicity, I decided to implement the first approach, as it is more
intuitive and requires less computational resources. The machine uses
three tapes: the first contains the first number, the second contains
the second number, and the third contains the result of the subtraction.

The algorithm has been implemented in the file `exercise3.txt` and can
be tested using the simulator at
<http://turingmachinesimulator.com/shared/lspvihlogm>.

The Turing Machine described in this exercise has been tested with
success the following input strings:

- `101-100`, result: `001`, final state: `halt-accept`

- `1000-111`, result: `0001`, final state: `halt-accept`

- `1000-1`, result: `0111`, final state: `halt-accept`

- `11-1101`, final state: `halt-reject`

- `-101`, final state: `halt-reject`

- `11-`, final state: `halt-reject`
