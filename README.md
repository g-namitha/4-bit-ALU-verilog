# 4-bit-ALU using verilog
Project Overview  

This project implements a 4-bit Arithmetic Logic Unit (ALU) using Verilog HDL. The ALU performs multiple arithmetic and logical operations based on control signals and is verified using a simulation testbench.

The design is suitable for FPGA simulation in Xilinx Vivado.

## Features  
The ALU supports the following operations:

Select (S2 S1 S0)	Operation  
000	Addition (A + B)  
001	Subtraction (A − B)  
010	AND  
011	OR  
100	XOR  
101	NOT A  
110	Increment A  
111	Decrement A
## Tools Used
- Verilog HDL
- Xilinx Vivado

## How to Run
1. Clone repository  
2. Open project in Vivado  
3. Run Behavioral Simulation  
4. Observe waveform outputs  
 ## ALU Verilog Code
   
```verilog
module alu_4bit(
input [3:0] A,
input [3:0] B,
input [2:0] S,
output reg [3:0] Result
);

always @(*) begin
case(S)

3'b000: Result = A + B;
3'b001: Result = A - B;
3'b010: Result = A & B;
3'b011: Result = A | B;
3'b100: Result = A ^ B;
3'b101: Result = ~A;
3'b110: Result = A + 1;
3'b111: Result = A - 1;

endcase
end

endmodule
```
## Testbench code (alu_tb.v)

```verilog
`timescale 1ns/1ps

module alu_tb;

reg [3:0] A;
reg [3:0] B;
reg [2:0] S;
wire [3:0] Result;

/* Instantiate ALU module */

alu_4bit DUT (
    .A(A),
    .B(B),
    .S(S),
    .Result(Result)
);

/* Test procedure */

initial
begin

$display("------------------------------------------------------");
$display("Time\t A\t B\t S\t Result\t Operation");
$display("------------------------------------------------------");

/* Test Case 1 : Addition */

A = 4'b0101; 
B = 4'b0011; 
S = 3'b000; 
#10;
$display("%0t\t%b\t%b\t%b\t%b\t ADD", $time, A, B, S, Result);

/* Test Case 2 : Subtraction */

A = 4'b0101; 
B = 4'b0011; 
S = 3'b001; 
#10;
$display("%0t\t%b\t%b\t%b\t%b\t SUB", $time, A, B, S, Result);

/* Test Case 3 : AND */

A = 4'b1010; 
B = 4'b1100; 
S = 3'b010; 
#10;
$display("%0t\t%b\t%b\t%b\t%b\t AND", $time, A, B, S, Result);

/* Test Case 4 : OR */

A = 4'b1010; 
B = 4'b1100; 
S = 3'b011; 
#10;
$display("%0t\t%b\t%b\t%b\t%b\t OR", $time, A, B, S, Result);

/* Test Case 5 : XOR */

A = 4'b1010; 
B = 4'b1100; 
S = 3'b100; 
#10;
$display("%0t\t%b\t%b\t%b\t%b\t XOR", $time, A, B, S, Result);

/* Test Case 6 : NOT A */

A = 4'b0101; 
B = 4'b0000; 
S = 3'b101; 
#10;
$display("%0t\t%b\t%b\t%b\t%b\t NOT", $time, A, B, S, Result);

/* Test Case 7 : Increment */

A = 4'b0101; 
B = 4'b0000; 
S = 3'b110; 
#10;
$display("%0t\t%b\t%b\t%b\t%b\t INC", $time, A, B, S, Result);

/* Test Case 8 : Decrement */

A = 4'b0101; 
B = 4'b0000; 
S = 3'b111; 
#10;
$display("%0t\t%b\t%b\t%b\t%b\t DEC", $time, A, B, S, Result);

/* Additional random test cases */

A = 4'b1111; 
B = 4'b0001; 
S = 3'b000; 
#10;
$display("%0t\t%b\t%b\t%b\t%b\t ADD", $time, A, B, S, Result);

A = 4'b1000; 
B = 4'b0010; 
S = 3'b001; 
#10;
$display("%0t\t%b\t%b\t%b\t%b\t SUB", $time, A, B, S, Result);

$display("------------------------------------------------------");

$finish;

end

endmodule
```
