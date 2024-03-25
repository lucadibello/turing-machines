# Problem description

In this exercise we are asked to design a Multi-tape Turing Machine
(MTM) that is able to compute the division of two given binary numbers.
The machine should halt in an accepting state when the result of the
division is found, and in a rejecting state if it detects a syntax error
in the input string or if the result would be a non-integer number.

The input format is `<dividend>/<divisor>`, where both the dividend and
the divisor are represented in binary form, and the symbol `/` is used
to separate them (just like in mathematical notation).

Also in this problem, I identified two approaches to solve the problem:

1. **Long division**: The machine computes the division of the two
    binary numbers just as we would do by hand, by performing the long
    division algorithm. This approach requires to implement a mechanism
    to align the divisor with the dividend, to perform the subtraction
    of the two numbers and to handle the quotient computation. It is
    also important to shift the quotient to ensure that the result is
    correct.

2. **2's complement division**: This other approach is based on the
    two's complement representation of binary numbers, allowing us to
    detect whether the result of a subtraction is negative or positive.
    This approach in fact subtracts the two's complement of the divisor
    from the dividend, and then checks if the result is negative or
    positive. If it is negative, the machine will halt in a rejecting
    state, otherwise it will continue the division process and count the
    number of iterations to compute the quotient.

For the sake of simplicity, I decided to implement the first approach,
as (at first) seemed to be more intuitive and simpler to implement. The
machine uses 4 tapes: the first contains the dividend, the second
contains the divisor, and the third contains the result of the
subtraction (performed at each iteration of the algorithm). To conclude,
the remaining tape is used to store the result of the division (only
quotient as the remainder is not requested in the exercise).

To go into detail, the algorithm encompasses the following phases:

1. The machine starts by moving the divisor to the second tape (the
    first tape already stores the dividend). Then, it will align the MSB
    (most significant bit) of the divisor with the MSB of the dividend.

2. Next, the machine will identify the first bit of the dividend that
    is greater than the divisor, computing in the meantime the quotient
    of the division until that point. The quotient is stored in the
    fourth tape.

3. After having identified a subset of the dividend that is greater
    than the divisor, the machine will perform the subtraction of the
    two numbers, storing the result in the third tape.

4. The machine will now swap the dividend with the result of the
    subtraction, in order to continue recursively the division process
    until the dividend is less than the divisor. In this case, the
    machine will halt in an accepting state, as the division has been
    completed.

5. If the machine detects that the dividend is less than the divisor,
    it will halt in a rejecting state, as the division cannot be
    completed using only integer numbers (without the remainder).

This task was harder than expected as, at first, I thought that the long
division algorithm implementation was trivial. However, I encountered
some difficulties in managing the tape movements and the correct
alignment of the quotient with the dividend during multiple iterations
of the algorithm. After some troubleshooting, I was able to design a
working algorithm and test it successfully with the following input
strings:

- `101/100`, result: `1`, final state: `halt-accept`

- `1000/101`, result: `1`, final state: `halt-accept`

- `1000/10`, result: `100`, final state: `halt-accept`

- `10101/11`, result: `111`, final state: `halt-accept`

Unfortunately, the simulator does not allow me to share the link to the
machine directly, but the machine can be loaded by pasting the content
of the file `solution.txt` in the web interface at
<http://turingmachinesimulator.com/>.
