# EXP-3-Adder-sub
## Design and Verification of Half Adder and Half Subtractor
### Aim
To design and verify basic one-bit arithmetic circuits using Verilog HDL.
### Theory / Synopsis
A Half Adder adds two single-bit binary numbers, A and B, and produces a Sum and a Carry output. A Half Subtractor subtracts one single-bit binary number B from another A, producing a Difference and a Borrow output. Both circuits are purely combinational and form the basic building blocks of larger arithmetic units such as Full Adders and Full Subtractors.
Boolean Functions
Half Adder:
•	Sum = A ⊕ B
•	Carry = A . B
Half Subtractor:
•	Difference = A ⊕ B
•	Borrow = A' . B

### Files to be Created
File name	Purpose
half_add_sub.v	Arithmetic-circuit RTL
half_add_sub_tb.v	Stimulus and VCD generation

### Verilog Program
```
module half_add(
	input wire a,
	input wire b,
	output wire sum,carry
);
	assign sum= a^b;
	assign carry= a&b;
endmodule
module half_sub(
	input wire a,
	input wire b,
	output wire diff,bor
);
	assign diff= a^b;
	assign bor= (~a)&b;
endmodule

```
### Testbench Program
```
module tb;
    reg a,b;
    wire sum, carry;
    wire diff, bor;
 
    // Instantiate the Half Adder
    half_add uut1 (
        .a(a),
        .b(b),
        .sum(sum),
        .carry(carry)
    );
 
    // Instantiate the Half Subtractor
    half_sub uut2 (
        .a(a),
        .b(b),
        .diff(diff),
        .bor(bor)
    );
 
    initial begin
        // ---- VCD dump setup ----
        $dumpfile("half.vcd");   // name of the VCD file to be generated
        $dumpvars(0, tb);                // dump all signals in this testbench hierarchy
 
        // ---- Apply all 4 input combinations ----
        $monitor("Time=%0t A=%b B=%b | Sum=%b Carry=%b | Diff=%b Borrow=%b",
                   $time, a, b, sum, carry, diff, bor);
        a = 0; b = 0; #10;
        a = 0; b = 1; #10;
        a = 1; b = 0; #10;
        a = 1; b = 1; #10;
 
        #10 $finish;
    end
endmodule<img width="1535" height="228" alt="Screenshot 2026-10-29 103634" src="https://github.com/user-attachments/assets/30d860d7-ed30-435d-ad63-2ef510fc3d46" />

```

### Truth Table
<img width="1533" height="178" alt="Screenshot 2026-10-29 103839" src="https://github.com/user-attachments/assets/1e289553-db34-4976-88a6-4a2e604f62db" />


### Simulation Procedure

STEP 1 – Open Terminal
Open a terminal in the experiment folder.

STEP 2 – Load Synopsys Environment
source /synopsys/start.sh

STEP 3 – Compile Using VCS
vcs half_add_sub.v half_add_sub_tb.v -full64
If compilation is successful, VCS generates the simulation executable:
simv

STEP 4 – Run Simulation
./simv
The terminal displays the input combinations and corresponding outputs Sum, Carry, Diff, and Borrow.
A VCD waveform file is also generated:
half_add_sub.vcd

STEP 5 – Open DVE
dve -full64
Other option
dve -full64 &
A DVE environment will open.

DVE Waveform Verification
In DVE:
•	Open the testbench hierarchy.
•	Locate the signals:
o	A
o	B
o	Sum
o	Carry
o	Diff
o	Borrow
•	Add the signals to the waveform window.
•	Run/inspect the waveform.

•	Verify that Sum = 1 whenever A and B are different (A⊕B), and Carry = 1 only when A=1 AND B=1.

•	Verify that Diff = 1 whenever A and B are different (same XOR pattern as Sum), and Borrow = 1 only when A=0 AND B=1.

•	Confirm that Carry and Borrow never both go high for the same input pair, since they represent different (AND vs A'B) conditions.

The waveform should agree with the truth table.

### Expected Result

The Half Adder and Half Subtractor were realized using Verilog HDL:

•	Sum = A⊕B, Carry = A.B
•	Diff = A⊕B, Borrow = A'.B

The design was compiled and simulated using Synopsys VCS, and the functionality was verified using DVE waveform analysis, matching the expected truth table.

### Output

<img width="1535" height="228" alt="Screenshot 2026-10-29 103634" src="https://github.com/user-attachments/assets/30d860d7-ed30-435d-ad63-2ef510fc3d46" />

<img width="1527" height="267" alt="Screenshot 2026-10-29 103805" src="https://github.com/user-attachments/assets/0d881b4e-9fc5-4396-8918-72e4138d9f07" />

### Result

Thus, the Half Adder and Half Subtractor were designed, implemented using Verilog HDL, successfully simulated using Synopsys VCS, and verified using Synopsys DVE.





