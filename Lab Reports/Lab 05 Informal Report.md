## Part A - Truth Tables
- We learned how to create quick and easy truth tables by doing $2^n$ where $n$ is the number of inputs. We cut the selection of bits in half for each column. We also were told about the game Turing Complete which is a cool game about building computers yourself, and the opportunity for bonus points.
## Part B - Challenge
```vhdl
library IEEE;
  use IEEE.std_logic_1164.all;
  use IEEE.numeric_std.all;

entity lab05b is
  port
  (
    switches : in std_logic_vector(15 downto 0);
    leds     : out std_logic_vector(15 downto 0)
  );
end lab05b;

architecture behavioral of lab05b is

  signal input  : std_logic_vector(3 downto 0); -- input 4 bits
  signal output : std_logic; -- output 1 bit

begin

  input   <= switches(3 downto 0);
  leds(0) <= output;

  process (input)
  begin
    case (input) is
      when "0000" => output <= '0';
      when "0001" => output <= '0';
      when "0010" => output <= '0';
      when "0011" => output <= '1';
      when "0100" => output <= '0';
      when "0101" => output <= '1';
      when "0110" => output <= '1';
      when "0111" => output <= '1';
      when "1000" => output <= '0';
      when "1001" => output <= '1';
      when "1010" => output <= '1';
      when "1011" => output <= '1';
      when "1100" => output <= '1';
      when "1101" => output <= '1';
      when "1110" => output <= '1';
      when "1111" => output <= '1';
      when others => output <= '-';
    end case;
  end process;

end architecture behavioral;
```

![[05-fpgaboard-1.png]]
![[05-fpgaboard-2.png]]

## Part C - Implementing Logic Gates
```vhdl
library IEEE;
use IEEE.std_logic_1164.all;
use IEEE.numeric_std.all;

entity lab05c is
  port
  (
    switches : in std_logic_vector(15 downto 0);
    leds     : out std_logic_vector(15 downto 0)
  );
end lab05c;

architecture behavioral of lab05c is

  -- Leds:     | NOT |  X  | AND  |  X   | OR  |  X  |  X  | NAND  |   X   | NOR  |  X   |  X  | XOR  |  X   | XNOR  |   X   |
  -- Switches: | NOT |  X  | AND1 | AND2 | OR1 | OR2 |  X  | NAND1 | NAND2 | NOR1 | NOR2 |  X  | XOR1 | XOR2 | XNOR1 | XNOR2 |
  -- Index:    | 15  |  14 |  13  |  12  | 11  | 10  |  9  |   8   |   7   |  6   |  5   |  4  |  3   |  2   |   1   |   0   |

begin

  leds(15) <= not switches(15);

  leds(13) <= switches(13) and switches(12);
  leds(11) <= switches(11) or switches(10);

  leds(8) <= switches(8) nand switches(7);
  leds(6) <= switches(6) nor switches(5);

  leds(3) <= switches(3) xor switches(2);
  leds(1) <= switches(1) xnor switches(0);

end architecture behavioral;
```
![[05-fpgaboard-4.png]]
![[05-fpgaboard-5.png]]

## Part D - More on Logic Gates
- We went over seven logic gates and their boolean expressions, as well as schematic notations and VHDL. 
#### Through
$$O = A$$
```vhdl
output < = A;
```
#### NOT
$$O = \overline{A} $$
```vhdl
output < = not A;
```
#### AND
$$O = A\cdot B = AB $$
```vhdl
output < = A and B;
```
#### NAND
$$O = \overline{A\cdot B} = \overline{AB}$$
```vhdl
output < = A nand B;
```
#### OR
$$ O = A + B $$
```vhdl
output < = A or B;
```
#### NOR
$$ O = \overline{A + B} $$
```vhdl
output < = A nor B;
```
#### XOR
$$ O = A \oplus B = A \cdot \overline{B} +\overline{A} \cdot B$$
```vhdl
output < = A xor B;
```
#### XNOR
$$ O = \overline{A \oplus B} = \overline{A} \cdot \overline{B} + A \cdot B$$
```vhdl
output < = A xnor B;
```

## Part E - Novel Gate Representation Activity
![[05-logic-not.png]]
<p style="text-align: center">(a)</p>

![[05-logic-and.png]]
<p style="text-align: center">(b)</p>

![[05-logic-or.png]]
<p style="text-align: center">(c)</p>

![[05-logic-nand.png]]
<p style="text-align: center">(d)</p>

![[05-logic-nor.png]]
<p style="text-align: center">(e)</p>

![[05-logic-xor.png]]
<p style="text-align: center">(f)</p>

![[05-logic-xnor.png]]
<p style="text-align: center">(g)</p>
<p style="text-align: center">Figure 1: Play-Doh Logic gate symbols (a) NOT gate, (b) AND gate, (c) OR gate, (d) NAND gate, (e) NOR gate, (f) XOR gate, (g) XNOR gate.</p>

#### In-Depth Gate Analysis
- The gate we'll select for in-depth analysis is the OR gate. Our novel logic gate symbol is represented in figure 1c.
	- The accepted logic gate does not seem sensible. 
		- The curved arrow does not represent the OR operation to us. 
		- The convergence of the arrow into the line might incorrectly represent the AND operation to some.
	- The accepted logic gate is aesthetically pleasing.
		- We will admit that the curved arrow is more pretty to look at than our right bracket. However, this takes away from the function of the gate.
 - The form of our OR gate is in the shape of a right bracket. 
		- This converges the two lines into a single vertical line and that vertical line is passed out of the front. We feel this is a better representation of the OR operation than the curved arrow. 
		- The 90 degree angles also make it easier to draw and represent, as opposed to the curved arrow of the accepted design.
	- It is aesthetically pleasing because of our 90 degree angles and right bracket design. 
		- The two lines going inside of the bracket and then passing out as one line is nice to look at. This is in contrast the sharp edges of the accepted OR gate and oblong curvy shape.

#### Summary
- We examined the OR gate because out of the 3 main symbols for logic gates, it is the most confusing. The sharpness of the arrow does not indicate anything about how it's logic functions, and we thought we could do it better.
- The other novel gates include an angled bracket for the AND and NAND gates, and a vertical line to represent the inverter in the NOT, NAND, and XNOR gates. The XOR and XNOR gates feature a vertical line on the left of the angle brackets to close off the brackets into rectangles.
- I never really thought about how important having legible and functionally symbolic logic gate symbols was before this lab. I respect the work that engineers before me have put into designing the logic gate schematic system and their symbols.