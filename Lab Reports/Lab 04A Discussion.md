1. Compare the results of steps 1, 2, and 3. Are they different? If so, how? 

We got the same answers for all three steps.

2.  What components do we need to implement this algorithm in hardware?

We need a priority encoder, a barrel shifter, a comparator, and an adder. We also need a resistor to store values from previous iterations.

3. If a is a negative value, would the algorithm still work? If not, what do we need to change?

Represent the numbers in sign and magnitude, find the modulo of the magnitude, add the sign at the end, and then add `n` if our remainder is negative.