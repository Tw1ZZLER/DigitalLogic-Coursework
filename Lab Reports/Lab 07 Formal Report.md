
# ECCS 1721
## Lab 07 - Priority Encoders
- Lab Conducted: 2024-03-05
- Lab Group Members:
	- Corbin Hibler
	- Dylan Hughes
### Introduction
- In this lab, we practiced creating logic gate diagrams from K-Maps of multiplexers and priority encoders. We worked more on solving the Two High-Bit challenge, from labs 5 and 6. We also tested gate-based 8:3 priority encoders, multiplexer-based 8:3 priority encoders, and two-level 16:4 priority encoders, on our field-programmable gate array (FPGA) development board.

### Procedure
#### Part A 
1. First, we downloaded the 7A-handout from Canvas.
2. The first goal of the lab was to understand the implementation of gates and how we can substitute them with each other to make the process use less transistors
3. We considered solutions to the given K-Maps, by evaluating their sum-of-product and product-of-sum boolean expressions.
4. Then, we drew the hardware implementations of both of these equations, with 2-input `AND` and `OR` gates.
5. Afterwards, we instead used `NAND` and `NOT` gates for the sum-of-product hardware, and `NOR` and `NOT` gates for the product-of-sum hardware, and used the following procedure:
	1. We took our previously made `AND/OR` gate implementations and counted our transistors (6 per `AND`/`OR` gate).
	2. Applied the Double Bubble rule to all internal wires. This keeps the function of the circuit the same while changing it's implementation.
	3. Circled all the `NAND` or `NOR` gates we created using this technique.
	4. Counted all the transistors and calculated the total transistors saved.
		  - 4 Ts per `NAND`/`NOR`, and 2 Ts per `NOT` gate.
	5. Determined the critical path by finding the longest sequence of gates and inverters between the input wires and output wires.
6. We drew the gate implementations of this hardware, as seen in the appendix in the rDrawn Gate Implementations section.
#### Part B
- We created a new Vivado project and imported `lab07b.vhd` and `lab07b.xdc` files from Canvas.
- We generated bitstream and uploaded to our FPGA board, to test our gate-based 8:3 priority encoder on the board.
- We tested the switches on the board and took 3 photos of our results with 3 different inputs, as seen in Figures 1, 2, and 3.
- We reviewed the elaborated design with the instructor and took a photo of the schematic, as seen in Figure 4.
- We also took a photo of our look-up table usage, as seen in Figure 5.
#### Part C
- We created a new Vivado project and imported `lab07c.vhd` and `lab07c.xdc` files from Canvas.
- We generated bitstream and uploaded to our FPGA board, to test our MUX-based 8:3 priority encoder on the board.
- The MUX-based priority encoder gave us the same results as the gate-based priority encoder.
- We took photos of our schematic after we reviewed it with the instructor, as seen in Figure 6. 
- We also took a photo of our look-up table usage, as seen in Figure 7.
#### Part D
 - We created a new Vivado project and imported `lab07d.vhd`, `priority_encoder_4.vhd`, and `lab07d.xdc` files from Canvas.
 - We reviewed with the instructor the elaborated design schematic of our 16:4 priority encoder, and took a screenshot and annotated each important part. This can be viewed in Figure 11.
 - We also noted the resource utilization of the FPGA board by our hardware, including look-up tables and flip-flops, which can be viewed in Figure 12.
 - We generated bitstream and uploaded to our FPGA board, to test the two-level 16:4 priority encoder.
 - We tested 3 different inputs of the 16:4 priority encoder, as seen in Figures 8, 9 and 10. The inputs we tested were `0000010000000000`, `0000011111111111`, and `0000000000001001`, which yielded the results `9`, `A`, and `3` respectively.
 - We then verified that our hardware generated the correct outputs. We evaluated the truth table ourselves and produced our own outputs, and then compared them to the ones received by the FPGA board.

### Results
![[Pasted image 20240305163941.png]]
<div style="text-align: center">Figure 1: Gate-Based 8:3 Priority Encoder (Input: 10000000)</div>

![[Pasted image 20240305163949.png]]
<div style="text-align: center">Figure 2: Gate-Based 8:3 Priority Encoder  (Input: 00011111)</div>

![[Pasted image 20240305163955.png]]
<div style="text-align: center">Figure 3: Gate-Based 8:3 Priority Encoder (Input: 00011011)</div>

![[Pasted image 20240305162156.png]]
<div style="text-align: center">Figure 4: Schematic of Gate-based 8:3 Priority Encoder</div>

![[Pasted image 20240305162242.png]]
<div style="text-align: center">Figure 5: LUT Usage of Gate-based 8:3 Priority Encoder</div>

![[Pasted image 20240305164909.png]]
<div style="text-align: center">Figure 6: Schematic of MUX-based 8:3 Priority Encoder</div>

![[Pasted image 20240305165417.png]]
<div style="text-align: center">Figure 7: LUT Usage of MUX-based 8:3 Priority Encoder</div>

![[Pasted image 20240305171317.png]]
<div style="text-align: center">Figure 8: Two-Level 16:4 Priority Encoder (Input: 0000010000000000)</div>

![[Pasted image 20240305173014.png]]
<div style="text-align: center">Figure 9: Two-Level 16:4 Priority Encoder (Input: 0000011111111111)</div>


![[Pasted image 20240305173021.png]]
<div style="text-align: center">Figure 10: Two-Level 16:4 Priority Encoder (Input: 0000000000001001)</div>

![[Pasted image 20240305172917.png]]
<div style="text-align: center">Figure 11: Annotated Schematic of 16:4 Priority Encoder</div>

![[Pasted image 20240305173516.png]]
<div style="text-align: center">Figure 12: LUT Usage of 16:4 Priority Encoder</div>

### Discussion/Analysis
#### Part A
- We learned how we can easily reduce the numbers of transistors and increase the speed of our hardware by using the Double Bubble rule.
- We saw how to convert hardware implementation from `AND` / `OR` gates into `NAND` / `NOR` / `NOT` gates, and it showed us that being stingy is always a good thing the realm of digital logic.
#### Part B
- We learned that we can edit the constraints (`.xdc`) file in Vivado to change how the switches behave.
- The constraints file we downloaded makes the 8 rightmost switches the input bits, where the rightmost switch is the least significant bit, and the leftmost bit is the most significant bit.
	- In addition, the leftmost switch on the board is reserved for the valid bit, which told us that we have a valid input. It is off when there are no switches inputted.
	- We saw how these constraints are implemented in the schematic shown in Figure 4.
	- We also saw how the constraint file affects the number of LUTs and FFs, as seen in Figure 5.
- The valid bit is necessary to verify that we have any input versus no input. We saw the importance of this validity bit in the truth table shown in the `07B-handout`. We saw this valid bit in action in Figures 1-3 and 8-10 in the LED all the way at the left. 
#### Part C
- Figure 6 shows the schematic for implementing a priority encoder using multiplexers instead of gates, and makes the process much, much easier.
	- The LATCH at the very right of Figure 6 was a mistake, and should not have been there. 
- The functionality of the the MUX-based priority encoder is the exact same as the gate-based priority encoder.
- Gate-based priority encoders are cheaper in terms of LUTs, as we can see from Figures 5 and 7. Gate-based uses 1 more LUT than MUX-based.
#### Part D
- In Figure 11, we can see the 4 input OR gates on the left that are our friends. These are an important part of the two-level structure of this priority encoder, which helps mitigate the exponential growth of priority encoders when they get more and more inputs.
- Figure 12 shows the LUT and FF usage of the 16:4 priority encoder. We can compare it to Figure 7 and see it uses 17 more LUTs, which is significantly more resources.
- One-level hardware can easily become massive without being divided and split up into multiple parts. Since priority encoders get exponentially larger, we can think of the levels of hardware as making the hardware logarithmically smaller.
- For a 64:6 two-level priority encoder, the coarse encoder would be a 32:5 priority encoder and the fine encoder would be a 16:4 priority encoder.  For a 32:5 two-level priority encoder, the coarse encoder would be a 16:4 priority encoder and the fine encoder would be a 8:3 priority encoder. 
- A four-level hardware structure instead of the two-level hardware structure show in this lab could be used to mitigate the exponential growth of priority encoders four-fold. As discussed earlier, the levels of hardware can reduce our hardware logarithmically, up to a certain point. I think 8-level could introduce problems that cause it to be more complex. A four-level would likely be a good middle ground.
### Conclusion
We covered deriving boolean equations from truth tables and K-Maps and transforming boolean equations to both Sum of Product and Product of Sum with `NAND` / `NOR` gates. Afterwards, in Part B, we worked more with Vivado and VHDL and practicing using the FPGA board for development and testing. We saw implementations of priority encoders in Vivado, including a gate-based 8:3 priority encoder, a multiplexer-based 8:3 priority encoder, and a two-level 16:4 priority encoder.

### Attachments / Appendix
#### Drawn Gate Implementations
![[IMG_20240326_220626667.jpg]]
![[IMG_20240326_220600965.jpg]]
![[20240327_001943.jpg]]

#### Gate Implementation Analysis
5. How many transistors do your AND / OR implementations from Step 3 cost? Do the SoP and PoS implementations differ in cost?

- AND/OR SoP contained 66Ts
- AND/OR PoS contained 66Ts
- They did not differ in cost.

6. How many transistors does your NAND / NOR implementations from Step 4 cost? Are they different from their corresponding implementations from Step 3? Are the different from each other? If so, by how many transistors?

- NAND/NOR SoP contained 52Ts
- NAND/NOR PoS contained 56Ts		
- Both NAND / NOR contained less transistors than their counterparts but the NAND / NOR SoP contained the least with 14 less transistors than its counterpart. 


7. How long are the critical paths from your NAND / NOR implementations from Step 4? Are the critical paths from the NAND and NOR implementations different? If so, by how much?

  - NAND/NOR SoP critical path was 6 gates long
  - NAND/NOR PoS critical path was also 6 gates long
  - They did not differ in length.

9. Which method (sum-of-product or product-of-sum) resulted in a more efficient hardware implementation from the perspective of complexity/power (number of transistors) and speed (critical path)? Why?

- Both SoP and PoS had the same optimal critical path length of 6 Tg in NAND/NOR format.  However, the NAND/NOR SoP had the least transistors with 52 Ts.

			
