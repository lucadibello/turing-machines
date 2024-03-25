# Problem description

In this exercise, we are asked to design a Single-tape Turing Machine
(STM) that is able to calculate the remainder of the division of two
given numbers. The designed STM presents all the steps of the division
process and halts in an accepting state when the remainder is found. On
the other hand, the machine halts in a rejecting state as soon as it
detects a syntax error in the input string.

The input format is `<dividend>#<divisor>`, where both the dividend and
the divisor are represented by a series of $1$s, and the symbol `#` is
used to separate them.

Here is a high level description of the algorithm, encompassing the main
steps and ideas behind the design:

1. The machine stats on the first symbol of the input string, which is
   the divided. As soon as the head of the machine reads the symbol
   \"$1$\", it marks it with a special symbol `X` to indicate that it
   has been processed. Then, the machine moves to divisor part of the
   input string and looks for another $1$ to match with the first one
   and marks it with the same special symbol `X`. The machine in fact
   computes the division using multiple symbol subtractions.

2. After each iteration of the algorithm, the machine always checks for
   the presence of special symbol patterns around the divider of the
   input string:

   1. `1#1`: In this case, both the dividend and the divisor have not
      been completely processed, so the machine continues the
      subtraction process.

   2. `1#X`: If the machine encounters a $1$ on the left side of `#`
      and a `X` on the right side, this means that the dividend is
      too big to be processed in a single iteration. In this case, the
      algorithm enters a \"_reset state_\" where it changes back all
      the `X` symbols of the divisor $1$ and removing all the `X`
      symbols from the dividend as they have been already processed in
      the previous iteration.

      The reset allows to restart the division, but with a smaller
      divided. For example, if we compute the operation $5 \mod 3$,
      this particular rule allows to restart the division from an
      equivalent but simplified modulo operation $2 \mod 3$. Here is
      an example of the reset process:

      - `11111#111` $\rightarrow$ `X1111#11X`
        $\rightarrow \hdots \rightarrow$
        `XXX1`[`1#X`]{style="color: red"}`XX` $\rightarrow$
        **reset** $\rightarrow$ `11#111` = $2 \mod 3$

   3. `X#X`: This indicates that the division process has been
      completed without any remainder. The machine will clear the tape
      and halt in an accepting state.

   4. `X#1`: If there is no more dividend to process, this means that
      the division process has been completed with some remainder left
      (the divisor is bigger than the divided, in fact the machine was
      not able to find enough $1$s in the left part of the input
      string). The machine will clear the right part of the tape and
      will convert all the remaining `X` symbols of the divisor to
      $1$s to represent the remainder. Then, the machine halts in an
      accepting state.

3. The algorithm iterates until one of the above string patterns is
   found, and the machine halts in the corresponding state.

4. All invalid characters have been handled by the machine, and as soon
   as it encounters a character in an illegal position, the machine
   halts in a rejecting state named `halt-reject`.

As the previous exercise, the algorithm has been implemented in the file
`solution.txt` and can be tested using the simulator at
<http://turingmachinesimulator.com/shared/gcjmttgery>.

The aim of the designed algorithm is to compute the modulo operation
with the smallest number of iterations to minimize the time complexity
of the algorithm. For this reason, the code is quite complex and may be
difficult to understand. For this reason, I have also included detailed
comments in the code to help the reader understand the logic behind the
algorithm.

The Turing Machine described in this exercise has been tested with
success the following input strings:

- `#1`, result: _empty_, final state: `halt-accept`

- `1111#11`, result: _empty_, final state: `halt-accept`

- `11111#111`, result: `11`, final state: `halt-accept`

- `1111111111#111`, result: `1`, final state: `halt-accept`

- `#111#`, final state: `halt-reject`

- `111#`, final state: `halt-reject`

- `1111#111#`, final state: `halt-reject`
