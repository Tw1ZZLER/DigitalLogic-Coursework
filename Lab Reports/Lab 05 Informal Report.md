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



## Part C - Implementing Logic Gates

## Part D - More on Logic Gates

## Part E - Novel Gate Representation Activity