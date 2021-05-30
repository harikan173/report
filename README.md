# report
# RTLDesignusingVerilogwithSKY130Technology
![sky](https://user-images.githubusercontent.com/84865915/120062155-4e7a9200-c07e-11eb-9a57-7c6520750a72.JPG)
  This repository contains all the information studied and created during the [RTLDesignusingVerilogwithSKY130Technology](https://www.vlsisystemdesign.com/rtl-design-using-verilog-with-sky130-technology/) workshop. Workshop intends to teach the verilog coding guidelines that results in predictable logic in Silicon. it is important to note that every verilog code is not synthesizable and even if it is , it may result in different logic depending on the coding styles used. The course details all these aspects of the Verilog HDL with theory and backed with lot of practical examples. Workshop introduces to the digital logic design using Verilog HDL . Validating the functionality of the design using Functional Simulation. Writing Test Benches to validate the functionality of the RTL design . Logic synthesis of the Functional RTL Code. Gate Level Simulation of the Synthesized Netlist.
Workshop Day wise Content :
# Table of Contents  
- [Day 1 - Introduction to Verilog RTL design and Synthesis](#day-1---introduction-to-verilog-rtl-design-and-synthesis)
    - [Introduction to open-source simulator iverilog](#introduction-to-open-source-simulator-iverilog)
    
    - [Labs using iverilog and gtkwave](#labs-using-iverilog-and-gtkwave)
    - [introduction to Yosys and Logic synthesis](#introduction-to-yosys-and-logic-synthesis)
    - [Labs using Yosys and Sky130 PDKs](#labs-using-yosys-and-sky130-pdks)
- [Day 2 - Timing libs hierarchical vs flat synthesis and efficient flop coding styles](#day-2---timing-libs-hierarchical-vs-flat-synthesis-and-efficient-flop-coding-styles)
    - [Introduction to timing libs](#introduction-to-timing-libs)
    - [Hierarchical vs Flat Synthesis](#hierarchical-vs-flat-synthesis)
    - [Various Flop Coding Styles and optimization](#various-flop-coding-styles-and-optimization)
- [Day 3 - Combinational and sequential optmizations](#day-3---combinational-and-sequential-optmizations)
    - [Introduction to optimizations](#introduction-to-optimizations)
    - [Combinational logic optimizations](#combinational-logic-optimizations)
    - [Sequential logic optimizations](#sequential-logic-optimizations)
    - [Sequential optimzations for unused outputsDesign](#sequential-optimzations-for-unused-outputsdesign)
- [Day 4 - GLS blocking vs non-blocking and Synthesis-Simulation mismatch](#day-4---gls-blocking-vs-non-blocking-and-synthesis-simulation-mismatch)
    - [GLS Synthesis Simulation mismatch and Blocking non blocking statements](#gls-synthesis-simulation-mismatch-and-blocking-non-blocking-statements)
    - [Labs on GLS and Synthesis-Simulation Mismatch](#labs-on-gls-and-synthesis-simulation-mismatch)
    - [Labs on synth-sim mismatch for blocking statement](#labs-on-synth-sim-mismatch-for-blocking-statement)
- [Day 5 - Optimization in synthesis](#day-5---optimization-in-synthesis)
    - [If Case constructs](#if-case-constructs)
    
    - [for loop and for generate](#for-loop-and-for-generate)
    - [Labs on for loop and for generate](#labs-on-for-loop-and-for-generate)
  - [References](#references)
  - [Acknowledgement](#acknowledgement)

# Day 1 - Introduction to Verilog RTL design and Synthesis
## Introduction to open-source simulator iverilog
Tool used for simulation is Icarus verilog and for all the inputs we need to generate the stimulus and for all the outputs we need to observe the stimulus.
For synthesis, the compiler generates netlists in the desired format and the synthesizer tool used is yosys.
simulator is used for checking the design,where as the RTL design is the implementation of specifications.
To check whether our design is obeying the required specifications or not we use Test bench
- 1.For compiling the design file(s) and testbench file we use the command as:
 iverilog design_file_name.v testbench_file_name.v
- 2.After comiling a file with the name and extension a.out will be generated. And this file is executed using the command
 vvp a.out
- 3.This will generate a file with the extension .vcd, for this file name can be given by the user in the testbench.
- 4.And finally to see the waveform or to veiw the vsd file we use another tool called gtkwave using the coomand(vcd stands for value change dump format)
gtkwave filename.vcd
- Below screenshot shows us the different verilog files that we were created for the workshop

![Screenshot (329)](https://user-images.githubusercontent.com/84865915/120038539-12fdaa80-c021-11eb-84d4-afe4ced417ab.png)
- now we are shows Command to execute is "./a.out" shows vcd(value change dump) file been generated successfully the command to invoke gtkwave using vcd file
![Screenshot (330)](https://user-images.githubusercontent.com/84865915/120038553-18f38b80-c021-11eb-9a89-558900965b2a.png)

![Screenshot (331)](https://user-images.githubusercontent.com/84865915/120038588-23158a00-c021-11eb-97d1-5bd3e59dd590.png)
## Labs using iverilog and gtkwave
When the design and the test bench are given to the iverilog simulator then it will going to generate vsd file to veiw that vcd file we must use gtkwave
eg:now we are going to take a 2 by 1 mux 
- Below figure is showing the entire simulated output of 2 by 1 mux
![Screenshot (332)](https://user-images.githubusercontent.com/84865915/120038612-290b6b00-c021-11eb-89ca-78753d4a8c39.png)
- we will get the below figure when we choose sel=1 then output y follows i1 signal
![Screenshot (334)](https://user-images.githubusercontent.com/84865915/120038670-3b85a480-c021-11eb-9891-36d5c2db2fcd.png)
- when we choose sel=0 then output y follows i0 signal
![Screenshot (335)](https://user-images.githubusercontent.com/84865915/120038678-3fb1c200-c021-11eb-8758-8e5acd1195de.png)
![Screenshot (337)](https://user-images.githubusercontent.com/84865915/120039481-95d33500-c022-11eb-993e-cb1aff9a7035.png)

## introduction to Yosys and Logic synthesis
### Typical synthesis flow
![c3](https://user-images.githubusercontent.com/84865915/120080505-ea37ec80-c0d6-11eb-97e0-27e78aaf2d21.JPG)

# Labs using Yosys and Sky130 PDKs

The following commands and steps are followed for performing the synthesis using yosys synthesizer

- 1.read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib using the command read standard cells library into the yosys 
and the sky130_fd_sc_hd__tt_025C_1v80.lib is standard cell library which is from skywatertechnology

- 2.next we have to read verilog files into the yosys using the command
read_verilog filename.v

- 3.next we have to perform synthesis using the command 
synth -top module_name

 - 4. next we have to map to standard cells using the following command
abc -liberty sky130_fd_sc_hd__tt_025C_1v80.lib

### Invoking yosys
![y1](https://user-images.githubusercontent.com/84865915/120070163-13d91f80-c0a7-11eb-88ba-bac83ce57935.JPG)

### Yosys terminal
after invoking yosys we must read the data from the yosys
![y2](https://user-images.githubusercontent.com/84865915/120070180-19cf0080-c0a7-11eb-9eae-de53324f8781.JPG)
### Read liberty file
this step tells us what is the module that we are going to synthesize
![y2](https://user-images.githubusercontent.com/84865915/120070180-19cf0080-c0a7-11eb-9eae-de53324f8781.JPG)
### Read verilog file
![y3](https://user-images.githubusercontent.com/84865915/120070199-218ea500-c0a7-11eb-852f-e8374c8eda84.JPG)
### Run synthesis
![y4](https://user-images.githubusercontent.com/84865915/120070218-26ebef80-c0a7-11eb-98f5-1575864bc049.JPG)

### Standard cell netlist generation command
abc command is used to convert our RTL file into gates and what gates it has to link that gates specified in the library
![y5](https://user-images.githubusercontent.com/84865915/120070228-2a7f7680-c0a7-11eb-900c-8166ab6670dc.JPG)
we require different flavours of the cells like:
1.slow
2. medium
3. fast
different flavours of cells are present in the satandard cell library because speed of logic circuit is determined by the combinational delay in the logic circuit
![k1](https://user-images.githubusercontent.com/84865915/120070836-07a29180-c0aa-11eb-88e9-a0ef1d600153.JPG)
- when the delays of the combinational circuit are less then it cause minimum clock period ,maximum clock speed and therefore it reults in the **BETTER PERFORMANCE**
therefore we require **FASTER CELLS TO GET SMALL COMBINATIONAL DELAY**
- but to not to miss the data we must gaurantee a minimum delay,so inorder to ensure that no hold issues at the capture flop we need the **SLOWER CELLS**
- if we choose wider transistors then lower will be the delay and it occupies **MORE AREA AND POWER**
![y6](https://user-images.githubusercontent.com/84865915/120070240-2e12fd80-c0a7-11eb-8b72-5caa7bb8b18f.JPG)

### show command
the show command will show the graphical version of logic it has realized
![y7](https://user-images.githubusercontent.com/84865915/120070252-3408de80-c0a7-11eb-8fba-c8517c2151d4.JPG)


# Day 2 - Timing libs hierarchical vs flat synthesis and efficient flop coding styles
## Introduction to timing libs

Below sceen shot shows how the .lib looks and what it contains,in sky 130 the 130 indicates it is 130 nm technology and .lib also shows the operating conditions process, voltage and temperature.
 
 
![image](https://user-images.githubusercontent.com/84865915/120032386-bc3fa300-c017-11eb-8f04-a0395981e326.png)
![image](https://user-images.githubusercontent.com/84865915/120032504-e98c5100-c017-11eb-9a32-3b6ab9c6d5ac.png)


.lib also has the information about the different features of the cells
For each cell it gives the information about the 
- 1.leakage power
- 2.delay
- 3.area
- 4.input capacitance
- 5.power associated
- 6.timing information and etc..
## Hierarchical vs Flat Synthesis
Here we have taken AND gate as one module and OR gate as another module both were instantiated under multiple module.
- Eg:
```
  module sub_module2 (input a, input b,output);
                      Assign y=a | b;
     endmodule
module sub_module1 (input a, input b,output);
                      Assign y=a & b;
     endmodule
module multiple_module (input a, input b, input c ,output y);
                      wire net1;
                      sub_module1 u1(.a(a),.b(b),.y(net1));
                      sub_module2 u2(.a(net1),.b(c),.y(y));
     endmodule 
```

Here we are going to synthesize the top level multiple module,we can also synthesize sub modules and also connect their nere netlists also but this can be done  mainly in 2 cases:
- 1.If we have same module instatiated many times then instead of synthesizing many times we have to synthesize it one time and replicate that netlist those many times.
- 2.If we have massive design then instead of giving massive design to the tool we will give portion by portion and stich all the netlist to get best possible netlist at the top level this is called **DIVIDE AND CONQUER** approach.:

![image](https://user-images.githubusercontent.com/84865915/120032652-235d5780-c018-11eb-97cf-957112f34996.png)


 
After flattening heirarchies are not preserved

 
![image](https://user-images.githubusercontent.com/84865915/120032704-33753700-c018-11eb-95cb-d212bfbfd50e.png)

Without flattening heirarchies are preserved and we have seen U1 and U2
But when we flatten we can see entire structure which contains both AND and OR gates as shown in below screen shot

![image](https://user-images.githubusercontent.com/84865915/120033453-33296b80-c019-11eb-94d0-65baa08ec320.png)

## Various Flop Coding Styles and optimization
- **Usage of FLOPS:**
In the circuit if we have more combinational circuits then outputs will become more and more glitiching, so we want an element to store that value ,that element is called as a FLOP.
We must initialize the flipflop with some vaue otherwise combinational circuit will store garbage value so we are using RESET/SET pins.
- 1]asynchronous reset:irrespective of clock if reset is one then output goes to zero.

![image](https://user-images.githubusercontent.com/84865915/120033515-463c3b80-c019-11eb-9fcd-e5ecc7afa446.png)

 
- 2]asynchronous set:irrespective of clock if set is one then output goes to one.

![image](https://user-images.githubusercontent.com/84865915/120033535-50f6d080-c019-11eb-91fa-aecaeac9cc37.png)

 
- 3]synchronous reset:Synchronous means, the output not set/reset as soon as the reset/set pin is asserted. Instead, it waits for the next clock edge. Synchronous set/reset are always added to the datapath. ie they add extra logic to the input of the flop.Even though reset is one until and unless we come across posedge of clock then only output changes. 

![image](https://user-images.githubusercontent.com/84865915/120033566-5b18cf00-c019-11eb-8ead-aad2589b7b68.png)
 

- 4]When Both synchronous and asynchronous reset are used
 
![image](https://user-images.githubusercontent.com/84865915/120033605-64a23700-c019-11eb-97dd-7f4f7e8e7d5d.png)



### NETLIST of asynchronous reset:
Netlist obtained after using yosys synthesizer

 
![image](https://user-images.githubusercontent.com/84865915/120033636-7552ad00-c019-11eb-9c52-f609ca50b4b1.png)


### NETLIST of asynchronous set:


 
![image](https://user-images.githubusercontent.com/84865915/120033658-7daae800-c019-11eb-97bc-6193f5182726.png)


### NETLIST of synchronous reset:

 
![image](https://user-images.githubusercontent.com/84865915/120033684-8c919a80-c019-11eb-9202-057a68ae717f.png)


### NETLIST of synchronous reset and asynchronous reset:

 
![image](https://user-images.githubusercontent.com/84865915/120033710-96b39900-c019-11eb-921f-f38326647c94.png)
### why the senthesizer is generating net list using NAND gate instead of using OR gate?
the synthesizer is inferring NAND and inverters to get OR gate because the direct cmos implementation of or gate contains stacked PMOS it has many disadvantages so we go for stacked nmos using nand gate

![pmos](https://user-images.githubusercontent.com/84865915/120104985-ae536480-c174-11eb-9ccc-d2df6846dfac.JPG)


1. consequently normal delay of NAND is less than normal delay of NOR gate.

In other words we can say that NAND gate is faster than NOR gate for same inputs.

2. For the same delay NAND gate require less area than NOR gate.

3. For the same area NAND gate is superior to NOR gates in switching characteristics because of higher mobility of electrons as compared to holes.

4. For equal fan-in, noise margin of NAND gate is better than NOR gate.


### Optimizations:
Eg:module mul2 (input [2:0] a, output [3:0] y);
                      Assign y =a*2;
endmodule

 
![image](https://user-images.githubusercontent.com/84865915/120033741-a337f180-c019-11eb-93a2-a7fa1310c957.png)

 
![image](https://user-images.githubusercontent.com/84865915/120033773-af23b380-c019-11eb-940b-14aea86ffd65.png)


Below screenshot it is showing during synthesis no cells are inferred

 
 
![image](https://user-images.githubusercontent.com/84865915/120034305-80f2a380-c01a-11eb-9ada-e1aae3ae8875.png)



![image](https://user-images.githubusercontent.com/84865915/120034324-8819b180-c01a-11eb-8106-5150f9358b07.png)
# Day 3 - Combinational and sequential optmizations
## Introduction to optimizations
It is used inorder to get most optimized design in terms of :
- 1.area
- 2.power
## Combinational logic optimizations
Techniques used for combinational logic optimization are:
- 1.constant propagation:In this technique, constant inputs to the logic are propagate to the output which results in a minimized expression implementing the same logic. For example consider the case y=((ab)+c)' when b is tied to 0.
- 2.Boolean logic optimization
![Screenshot (407)](https://user-images.githubusercontent.com/84865915/120074776-15611280-c0bc-11eb-9c5b-b96dcca8cbd2.png)
 
In the below screenshot even though reset went low but q is waiting for the next raising edge,after it come across the next raising edge the only q is going to one,therefore the operation of q depends on the edge of the clock ,so the circuit will infer a flop 
 ![Screenshot (408)](https://user-images.githubusercontent.com/84865915/120074778-1abe5d00-c0bc-11eb-8872-1649a672c913.png)
By seeing the statistics we can clearly see that it is inferring a flipflop under dff_const1
![Screenshot (410)](https://user-images.githubusercontent.com/84865915/120074826-578a5400-c0bc-11eb-96cc-455f00af7a1a.png)
 
Synthesis report for above simulation
Actually we are expecting active high reset but tool is inferring the active low reset with an inverter
![Screenshot (411)](https://user-images.githubusercontent.com/84865915/120074830-5ce79e80-c0bc-11eb-842d-ce1096c6db63.png)
 
In the below screenshot output is always one irrespective of clock,reset and set 

![Screenshot (409)](https://user-images.githubusercontent.com/84865915/120074781-1eea7a80-c0bc-11eb-846b-c86774769116.png)
We already seen under dff_const1 it inferred flipflop but under dff_const2 it inferred ,it has inferred zero cells,zero memories it inferred only wires
 
![Screenshot (412)](https://user-images.githubusercontent.com/84865915/120074832-6113bc00-c0bc-11eb-8a2e-4d7f393fb45b.png)
- Below figure shows the different files available for the checing of combinational logic optimizations.

![fa](https://user-images.githubusercontent.com/84865915/120102339-21a2a980-c168-11eb-94a8-3bac0c1acb21.JPG)
- from the above files Here we will be taking first file opt_check module where we have assign y= a?b:0, which is a mux so at a=1, y will take b's values, but at a=0, y will take 0 as its value.
![oc](https://user-images.githubusercontent.com/84865915/120102113-24e96580-c167-11eb-876f-2deff0ed4960.JPG)
- **testbench**
![oct](https://user-images.githubusercontent.com/84865915/120102118-287cec80-c167-11eb-900a-60f1b586259b.JPG)
- Below figure is showing the number of cells available in the netlist

![gp1](https://user-images.githubusercontent.com/84865915/120102362-37b06a00-c168-11eb-85b6-54af8e1ab07d.JPG)
- netlist of the opt_check
![gp2](https://user-images.githubusercontent.com/84865915/120102365-3b43f100-c168-11eb-888a-50dd277f172d.JPG)
- Here we will be taking second file opt_check2 module where we have assign y= a?1;b, which is a mux so at a=1, y will take 1, but at a=0, y will take b's value.
![oc2](https://user-images.githubusercontent.com/84865915/120102125-2d41a080-c167-11eb-8a18-9910c5d8bbe4.JPG)
- **testbench**
![oc2t](https://user-images.githubusercontent.com/84865915/120102126-30d52780-c167-11eb-961b-d18cbf574f89.JPG)
- Below figure is showing the number of cells available in the netlist

![gp3](https://user-images.githubusercontent.com/84865915/120102369-3ed77800-c168-11eb-9131-e450e3b2a671.JPG)
- netlist of the opt_check2
![gp4](https://user-images.githubusercontent.com/84865915/120102371-426aff00-c168-11eb-981e-eba4e65afa97.JPG)

## Sequential logic optimizations
1.sequential constant propagation
2.state optimization
3.Retiming
4.sequential logic cloning:Used when we are doing physical logic synthesis
- Eg:if in a floor plan if the cells are sitting far away from each other then their will be large routing between them
As our q is always one irrespective of clock,reset ,so there is no requirement of any flop,therefore we can see in the netlist there is no connection with the clock and reset.therefore this is called as **Sequential optimization**

![Screenshot (413)](https://user-images.githubusercontent.com/84865915/120074842-65d87000-c0bc-11eb-9439-cd7dfd17e08f.png)
 
- Eg:3 if there are two flops,both having the same clock and same reset
 ![Screenshot (414)](https://user-images.githubusercontent.com/84865915/120074849-6c66e780-c0bc-11eb-88fb-db5aff29dc92.png)
![Screenshot (415)](https://user-images.githubusercontent.com/84865915/120074859-71c43200-c0bc-11eb-8079-8117a9d0ed90.png)
## Sequential optimzations for unused outputsDesign
eg:
```
  module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[0];

always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end

endmodule 
```
- **test bench**
```
   `timescale 1ns / 1ps
module tb_counter_opt;
	// Inputs
	reg clk, reset   ;
	// Output
	wire q;

        // Instantiate the Unit Under Test (UUT)
	counter_opt uut (
		.clk(clk),
		.reset(reset),
		.q(q)
	);

	initial begin
	$dumpfile("tb_counter_opt.vcd");
	$dumpvars(0,tb_counter_opt);
	// Initialize Inputs
	clk = 0;
	reset = 1;
	#3000 $finish;
	end

always #10 clk = ~clk;
always #1547 reset=~reset;
endmodule

```
![cast](https://user-images.githubusercontent.com/84865915/120101690-e8b50580-c164-11eb-927d-67ce71aecc7e.JPG)
![cast1](https://user-images.githubusercontent.com/84865915/120101692-ebaff600-c164-11eb-991d-1ed9bc20c473.JPG)



# Day 4 - GLS blocking vs non-blocking and Synthesis-Simulation mismatch
### what is GLS?
- It stands for **Gate Level Simulation**.
- Running the Test Bench With Netlist as design under Test.
- Netlist is logically same as the RTL Code.
- GLS is used to Verify the LOgical Correctness of the design after synthesis and it also used for Ensuring the Timing of design is met,For this GLS needs to be run with delay     annotation. 
### GLS using iverilog
- When we give the Netlist,Gate Level Verilog Models and Testbench to the iverilog.the Netlist has all the standard cell instantiated and the meaning of standard cell is conveyed to the iverilog by **Gate Level Verilog Models** and After that the iverilog will produce vcd file using which we can generate Waveform using GTKwave.
# GLS Synthesis Simulation mismatch and Blocking non blocking statements
### Synthesis-Simulation Mismatch
Suppose we have a Netlist of:
- and u_and(.a(a),.b(b))
- or u_or (.a(a),.b(b))
- Gate level Verilog Models can be 
1.Timing Aware:
- for Timing Aware we will validate functionality as well as timing both
2.Functional aware
- forFunctional aware we will validate functionality
### **missing sensitivity list**:
- simulator works based on ACTIVITY that means if there is change in input then only there is a change in the output
 - //**eg-2 by 1 mux**:
```
  module mux(
input i0,input i1
input sel,
output reg y
);
always @ (sel)
begin
   if (sel)
            y = i1;
   else 
            y = i0;
            
end
endmodule
```
//
-**here always block is getting evaluated only when the select is changing even though there is changes in i0 and i1**
- always block is not sensitive to changes in the i1 this is what we called as **missing element in the sensitivity list**
- so to overcome that we must use always(*) 
- therefore the output changes for any of the input changes its code is given as below

```
 module mux(
input i0,input i1
input sel,
output reg y
);
always @ (*)
begin
   if (sel)
            y = i1;
   else 
            y = i0;
            
end
endmodule  
```
### Blocking and Non Blocking Statements
- Inside always block
- 1.If we are using '=' to make assignments
- 2.Executes the Statement in the order it is written,So the first statement is evaluated before the second statement.
- 3.If we are using '<=' to make assignments ,executes all the RHS when always block is enteredand assigns to LHS it is parallel level of execution
### Caveats with Blocking Statements
- **eg:shift register using blocking assignments**
```
 module code (input clk,input reset,
input d,
output reg q);
always @ (posedge clk,posedge reset)
begin
if(reset)
begin
        q0 = 1'b0;
        q = 1'b0;
end
else
        q = q0;
        q0 = d;
        
end
endmodule  
```
- In this case q0 is assigned to q and then d gets assigned to q0.So we get 2 values,so it will have 2 flops in the netlist.
- **eg:**
```
  module code (input clk,input reset,
input d,
output reg q);
always @ (posedge clk,posedge reset)
begin
if(reset)
begin
        q0 = 1'b0;
        q = 1'b0;
end
else
        q0 = d;
        q = q0;
                
end
endmodule 
```

- In this case q0 is assigned d the q0 gets assigned to q ,So it is as if q is getting the value of d which means it only has 1 flop
### eg:shift register using non blocking assignments
```
module code (input clk,input reset,
input d,
output reg q);
always @ (posedge clk,posedge reset)
begin
if(reset)
begin
        q0 <= 1'b0;
        q <= 1'b0;
end
else
        q0 <= d;
        q <= q0;
                
end
endmodule
```

- In the non-blocking assignments the order doesnt matter,therefore irrespective of order we will get two flops over here
- therefore **always use NON BLOCKING to write SEQUENTIAL CIRCUITS**
### eg:to understand Synthesis-Simulation Mismatch
- **(a+b)c**
![56](https://user-images.githubusercontent.com/84865915/120095315-eb9efe80-c142-11eb-906b-2f4aa4ded22c.JPG)
```
  module code (input a,b,c
output reg y);
reg q0;
always @ (*)
begin
        y = q0 & c;
        q0 = a|b ;
        
end 
endmodule 
```

- here we assigning the value of y with q0 and with c first and then assign q0 as a or b , So we see that q0 value is the old q0 value and is not updated.
When we simulate old q0 value will mimic a delay or flop but when we synthesis there will not be a flop.
- **when we change the order**
 ```
   module code (input a,b,c
output reg y);
reg q0;
always @ (*)
begin
        q0 = a|b ;
        y = q0 & c;
        
        
end 
endmodule
```
In this case there will not be any delay as the q0 is updated first then used.When we simulate it will work as the given circuit and In both cases above when we synthesis we get the desired circuit but in first case the simulation result differ with synthesis results.
Because of these kind of issues it becomes very important to run GLS on the Netlist and match with the expected output and see if there are no Synthesis Simulation Mismatches.
# Labs on GLS and Synthesis-Simulation Mismatch
To Run GLS we need
- Netlist
- Verilog Models
- Testbench
- the above three are given to the iverilog then it is dump into the vcd file and generate the gtkwave
### eg:2 by 1 mux using ternary operator
```
module ternary_operator_mux (input i0 , input i1 , input sel , output y);
	assign y = sel?i1:i0;
	endmodule   
```

![ter](https://user-images.githubusercontent.com/84865915/120097394-d8ddf700-c14d-11eb-87de-2cfbbd9e2527.JPG)


![Screenshot (446)](https://user-images.githubusercontent.com/84865915/120097520-82bd8380-c14e-11eb-9304-e548c26e5ffc.png)
- In the above picture we can clearly see that one mux is inferred

![Screenshot (448)](https://user-images.githubusercontent.com/84865915/120097728-cbc20780-c14f-11eb-8ab1-5f60399bc4aa.png)

### invoke GLS
![gls](https://user-images.githubusercontent.com/84865915/120098398-55270900-c153-11eb-9442-3782294da23f.JPG)
- By seeing those _6,_7,_8 we can say that it is **gls**
![gls2](https://user-images.githubusercontent.com/84865915/120098401-58ba9000-c153-11eb-97fa-9807c6d60745.JPG)
- eg:bad_mux
```
 module bad_mux (input i0 , input i1 , input sel , output reg y);
always @ (sel)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule  
```

**testbench**

`timescale 1ns / 1ps
module tb_bad_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	bad_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_bad_mux.vcd");
	$dumpvars(0,tb_bad_mux);
	// Initialize Inputs
	sel = 1'b0;
	i0 = 1'b0;
	i1 = 1'b0;
	#300 $finish;
	end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule

![bad](https://user-images.githubusercontent.com/84865915/120098663-d632d000-c154-11eb-8120-772c8372db5c.JPG)
simulation shows that there is no activity of select,simulation also showing as if the Mux is acting like a flop 

**synthesis report**

![badmux](https://user-images.githubusercontent.com/84865915/120098854-e1d2c680-c155-11eb-9050-05ad6c6e867b.JPG)
- the above figure shows the number of standard cell statistics of bad_mux
- And now we are going to invoke the gls
![gls](https://user-images.githubusercontent.com/84865915/120098872-f7e08700-c155-11eb-882a-b48f979f9b69.JPG)
- we can say that we invoke GLS by seeing those _6,_7,_8
![gls3](https://user-images.githubusercontent.com/84865915/120098874-fc0ca480-c155-11eb-8e56-5f24402e298a.JPG)
- **In the RTL simulation when the sel=0 the activity of i0 is not reflecting on the output this is called as synthesis simulation mismatch**
- **in the GLS simulation when sel=0 the output is following the i0**
- **therfore the synthesis and simulation mismatch is overcomed by invoking GLS**
 ## Labs on synth-sim mismatch for blocking statement
### eg:synthesis and simulation explanation using blocking code
```
  module blocking_caveat (input a , input b , input  c, output reg d); 
reg x;
always @ (*)
begin
	d = x & c;
	x = a | b;
end
endmodule 
```

**test bench**

`timescale 1ns / 1ps
module tb_blocking_caveat;
	// Inputs
	reg a,b,c   ;
	// Output
	wire d;

        // Instantiate the Unit Under Test (UUT)
	blocking_caveat uut (
		.a(a),
		.b(b),
		.c(c),
		.d(d)
	);

	initial begin
	$dumpfile("tb_blocking_caveat.vcd");
	$dumpvars(0,tb_blocking_caveat);
	// Initialize Inputs
	a = 0;
	b = 0;
	c = 0;
	#3000 $finish;
	end

always #10 a = ~a;
always #100 c =~c;
always #50 b = ~b;
endmodule

- Now because of the blocking statement first d will be assigned (x and c) then x = a or b will be executed and by the time the statement for d is getting evaluated we have the previous value of x ,So when we simulate it , it will look as if x is a flopped output.
- ![gls5](https://user-images.githubusercontent.com/84865915/120099540-a0441a80-c159-11eb-80c8-40224d39d2f6.JPG)
### synthesis report
the below figure shows the standard cells statistics
![block](https://user-images.githubusercontent.com/84865915/120099643-46902000-c15a-11eb-9505-42d1a4134047.JPG)
the below figure shows the veiw of the netlist
![block1](https://user-images.githubusercontent.com/84865915/120099650-4b54d400-c15a-11eb-8d55-563e52e24ef9.JPG)
### invoking of gls
![gls](https://user-images.githubusercontent.com/84865915/120099658-54de3c00-c15a-11eb-9d1f-b8183e2a74cf.JPG)
- In the below figure We can clearly see that the value of d = 0 for the same case where a = 0,b = 0 and c = 1,This is Synthesis Simulation Mismatch caused by Blocking statement,therefore we must be careful while using blocking statements for the sequential circuits.
![gls6](https://user-images.githubusercontent.com/84865915/120099665-5c054a00-c15a-11eb-8c50-59eacfd9dc57.JPG)

# Day 5 - Optimization in synthesis
## If Case constructs
if is used to create priority logic in terms of hardware
**Behavioral statements**
- IF-ELSE statement
- CASE statement
- Loop statement
- These behavioral statements can also be used in a clocked process
behavioral modeling
**if else**
- •Conditions are evaluated in order from top to bottom
•Prioritization
- •The first condition, that is true, causes the corresponding sequence of statements to be executed.
- •If all conditions are false, then the sequence of statements associated with the “else” clause is evaluated.
![c1](https://user-images.githubusercontent.com/84865915/120080200-692c2580-c0d5-11eb-9abf-2ce3528be51f.JPG)
eg:
![c2](https://user-images.githubusercontent.com/84865915/120080383-45b5aa80-c0d6-11eb-8b0a-a33a6fb1e893.JPG)
 ## If Case constructs
   ### eg:1-incomplete if
    this example tells us when we write a incomplete if statement then dlatch is inferred , whenver i0 is present i1 is seen on y
    ```
```
    ```
    module incomp_if (input i0 , input i1 , input i2 , output reg y);
always @ (*)
begin
	if(i0)
		y <= i1;
end
endmodule 
```
  
### test bench
`timescale 1ns / 1ps
module tb_incomp_if;
	//input
	reg i0,i1,i2;
	// Output
	wire y;

        // Instantiate the Unit Under Test (UUT)
	incomp_if uut (
		.i0(i0),
		.i1(i1),
		.i2(i2),
		.y(y)
	);

	initial begin
	$dumpfile("tb_incomp_if.vcd");
	$dumpvars(0,tb_incomp_if);
	// Initialize Inputs
	i0 = 1'b0;
	i1 = 1'b0;
	i2 = 1'b0;
	
	#3000 $finish;
	end

always #317 i0 = ~i0;
always #37 i1 = ~i1;
always #57 i2 = ~i2;

endmodule
```
```
### simulated output
whenever i0 is going low the output y is latching on to either one or zero permanently and there is no change in y whenever i0 is low but when i0 signal is high the output follows i1 signal therfore we can say that as a latching action.
![Screenshot (421)](https://user-images.githubusercontent.com/84865915/120088584-ce047180-c10f-11eb-99ac-f0b93df716c4.png)
### synthesis report
if we write a incomplete if statement then clearly in the statistics we can see that D LATCH is inferred, as our main aim is to code a mux but here the tool is inferring a latch

![Screenshot (422)](https://user-images.githubusercontent.com/84865915/120088587-d492e900-c10f-11eb-8ccb-ab20137f6ff8.png)
therefore in the synthesiszed netlist we can see that dlatch is inferred with i0 as enable.
![Screenshot (423)](https://user-images.githubusercontent.com/84865915/120088589-d8267000-c10f-11eb-87f3-62b70fc5869f.png)
### eg:2
```
  module incomp_if2 (input i0 , input i1 , input i2 , input i3, output reg y);
always @ (*)
begin
	if(i0)
		y <= i1;
	else if (i2)
		y <= i3;

end
endmodule 
```


### test bench
`timescale 1ns / 1ps
module tb_incomp_if2;
	//input
	reg i0,i1,i2,i3;
	// Output
	wire y;

        // Instantiate the Unit Under Test (UUT)
	incomp_if2 uut (
		.i0(i0),
		.i1(i1),
		.i2(i2),
		.i3(i3),
		.y(y)
	);

	initial begin
	$dumpfile("tb_incomp_if2.vcd");
	$dumpvars(0,tb_incomp_if2);
	// Initialize Inputs
	i0 = 1'b0;
	i1 = 1'b0;
	i2 = 1'b0;
	i3 = 1'b0;
	
	#3000 $finish;
	end

always #317 i0 = ~i0;
always #37 i1 = ~i1;
always #157 i2 = ~i2;
always #67 i3 = ~i3;

endmodule

### simulate output
whenever io or i1 is true, then the output of the combinational logic which is the function of i0,i1,i2,i3 is going to be seen at the output

![Screenshot (424)](https://user-images.githubusercontent.com/84865915/120089035-36555200-c114-11eb-899c-a0dbcfa02369.png)

whenever i0 is high output is following i1 and when i0 is low it follows i2 and when  i0 and i2 both are low then output is constant,and when i0 is low and i2 is high then output is following i3
### synthesis report
 clearly in the statistics we can see that D LATCH is inferred, as our main aim is to code a mux but here the tool is inferring a latch

![Screenshot (425)](https://user-images.githubusercontent.com/84865915/120089038-3ce3c980-c114-11eb-8697-6266b366c102.png)
in the synthsized netlist we can see that i0 and i2 are given to or gate and that output is acting as the enable of the latch,when both i0 and i2 are not there then the actual latching action happens and whenever io or i1 is true, then the output of the combinational logic which is the function of i0,i1,i2,i3 is going to be seen at the output

![Screenshot (427)](https://user-images.githubusercontent.com/84865915/120089041-410fe700-c114-11eb-8236-ccd58dc8285b.png)
### eg:3- incomplete case
```

    module incomp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
	case(sel)
		2'b00 : y = i0;
		2'b01 : y = i1;
	endcase
end
endmodule   
```


### test bench

`timescale 1ns / 1ps
module tb_incomp_case;
	//input
	reg i0,i1,i2;
	reg [1:0] sel;
	// Output
	wire y;
	//TB_SIGNALS
        reg clk,reset;	

        // Instantiate the Unit Under Test (UUT)
	incomp_case uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.i2(i2),
		.y(y)
	);

	initial begin
	$dumpfile("tb_incomp_case.vcd");
	$dumpvars(0,tb_incomp_case);
	// Initialize Inputs
	i0 = 1'b0;
	i1 = 1'b0;
	i2 = 1'b0;
	clk = 1'b0;
	reset = 1'b0; #1;
	reset = 1'b1; #10;
	reset = 1'b0; 

	
	#5000 $finish;
	end

always #317 i0 = ~i0;
always #600 clk = ~clk;
always #37 i1 = ~i1;
always #57 i2 = ~i2;


always @(posedge clk , posedge reset)
begin
if(reset)
	sel <= 2'b00;
else
	sel <= sel + 1;
end
endmodule
### simulated output:
![Screenshot (428)](https://user-images.githubusercontent.com/84865915/120090146-ccda4100-c11d-11eb-9c66-e6289be51674.png)
when -
- sel=0 then y is following i0
-  sel=1 then y is following i1
-  sel==10 or 11 then output is latching on to the previous output value 
### synthesis report:
 clearly in the statistics we can see that D LATCH is inferred, as our main aim is to code a mux but here the tool is inferring a latch

![Screenshot (429)](https://user-images.githubusercontent.com/84865915/120090148-d368b880-c11d-11eb-99fd-7250d25218ac.png)

    - sel = 00 then i0 is seen at the output
    - sel=  01 then i1 is seen at the output
    - sel= 10 or 11 nothing is specified and default statement also not coded so it is going to be latched,therfore in the netlist we can see that output is driven by the latch
![Screenshot (430)](https://user-images.githubusercontent.com/84865915/120090150-d6fc3f80-c11d-11eb-9c41-efe3bdda36ea.png)

### eg:4- complete case
```
 module comp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
always @ (*)
begin
	case(sel)
		2'b00 : y = i0;
		2'b01 : y = i1;
		default : y = i2;
	endcase
end
endmodule  
```

### test bench:

`timescale 1ns / 1ps
module tb_comp_case;
	//input
	reg i0,i1,i2;
	reg [1:0] sel;
	// Output
	wire y;
	//TB_SIGNALS
        reg clk,reset;	

        // Instantiate the Unit Under Test (UUT)
	comp_case uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.i2(i2),
		.y(y)
	);

	initial begin
	$dumpfile("tb_comp_case.vcd");
	$dumpvars(0,tb_comp_case);
	// Initialize Inputs
	i0 = 1'b0;
	i1 = 1'b0;
	i2 = 1'b0;
	clk = 1'b0;
	reset = 1'b0; #1;
	reset = 1'b1; #10;
	reset = 1'b0; 

	
	#5000 $finish;
	end

always #317 i0 = ~i0;
always #600 clk = ~clk;
always #37 i1 = ~i1;
always #57 i2 = ~i2;

always @(posedge clk , posedge reset)
begin
if(reset)
	sel <= 2'b00;
else
	sel <= sel + 1;
end
endmodule

### simulated output
![Screenshot (431)](https://user-images.githubusercontent.com/84865915/120090673-f39a7680-c121-11eb-90cc-df38e55c37a5.png)


- when sel=00 then y will follow i0
- when sel=01 then y will follow i1
- when sel=10 or 11  then output is going to follow our default condition that it should follow i2 so no latch will be inferred over here
### synthesized output
![Screenshot (432)](https://user-images.githubusercontent.com/84865915/120090677-f85f2a80-c121-11eb-84e6-8702c49269ea.png)
As we are using the default condition in our program so no lataches will be inferred 
 clearly in the statistics we can see that no latch is inferred
![Screenshot (433)](https://user-images.githubusercontent.com/84865915/120090682-fbf2b180-c121-11eb-9e8b-6a0695de1637.png)

### eg:5 partial case
```
 module partial_case_assign (input i0 , input i1 , input i2 , input [1:0] sel, output reg y , output reg x);
always @ (*)
begin
	case(sel)
		2'b00 : begin
			y = i0;
			x = i2;
			end
		2'b01 : y = i1;
		default : begin
		           x = i1;
			   y = i2;
			  end
	endcase
end
endmodule  
```

### test bench

`timescale 1ns / 1ps
module tb_partial_case_assign.v;
	//input
	reg i0,i1,i2,sel;
	// Output
	wire x,y;
	//TB_SIGNALS
        reg clk,reset;	

        // Instantiate the Unit Under Test (UUT)
	partial_case_assign.v uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.i2(i2),
		.i3(i3),
		.x(x),
		.y(y)
	);

	initial begin
	$dumpfile("tb_partial_case_assign.v.vcd");
	$dumpvars(0,tb_partial_case_assign.v);
	// Initialize Inputs
	i0 = 1'b0;
	i1 = 1'b0;
	i2 = 1'b0;
	clk = 1'b0;
	reset = 1'b0; #1;
	reset = 1'b1; #10;
	reset = 1'b0; 

	
	#5000 $finish;
	end

always #317 i0 = ~i0;
always #600 clk = ~clk;
always #37 i1 = ~i1;
always #57 i2 = ~i2;


always @(posedge clk , posedge reset)
begin
if(reset)
	sel <= 2'b00;
else
	sel <= sel + 1;
end
endmodule

### synthesized report
![Screenshot (434)](https://user-images.githubusercontent.com/84865915/120090979-64429280-c124-11eb-8123-ee616af15281.png)
when
- sel=00 then y follows i0
- sel=01 nothing is mentioned so latch is inferred
- sel=10 or 11 given a default condition that it should follow i1 
- therefore we can see only one latch in the statistics 
- so in the path of y there is no latch inferred but in the path of x latch is inferred
![Screenshot (435)](https://user-images.githubusercontent.com/84865915/120090986-6a387380-c124-11eb-9d8b-67554a1ae5dc.png)

### eg:bad_case
```
 module bad_case (input i0 , input i1, input i2, input i3 , input [1:0] sel, output reg y);
always @(*)
begin
	case(sel)
		2'b00: y = i0;
		2'b01: y = i1;
		2'b10: y = i2;
		2'b1?: y = i3;
		//2'b11: y = i3;
	endcase
end

endmodule  
```

### test bench
`timescale 1ns / 1ps
module tb_bad_case;
	// TB_SIGNALS
	reg clk, reset   ;
	//input
	reg i0,i1,i2,i3;
	reg [1:0] sel;
	// Output
	wire y;

        // Instantiate the Unit Under Test (UUT)
	bad_case uut (
		.i0(i0),
		.i1(i1),
		.i2(i2),
		.i3(i3),
		.sel(sel),
		.y(y)
	);

	initial begin
	$dumpfile("tb_bad_case.vcd");
	$dumpvars(0,tb_bad_case);
	// Initialize Inputs
	clk = 0;
	i0 = 1'b0;
	i1 = 1'b0;
	i2 = 1'b0;
	i3 = 1'b0 ;
	reset = 1'b0; #1;
	reset = 1'b1; #10;
	reset = 1'b0; 
	
	#3000 $finish;
	end

always #200 clk = ~clk;
always #17 i0 = ~i0;
always #37 i1 = ~i1;
always #57 i2 = ~i2;
always #97 i3 = ~i3;

always @ (posedge clk , posedge reset)
begin
	if(reset)
		sel <= 2'b00;
	else
		sel <= sel + 1;
end
endmodule
### simulated output
![Screenshot (436)](https://user-images.githubusercontent.com/84865915/120091590-28aac700-c12a-11eb-803f-58906f9bc116.png)
- when sel=00 then y will follow i0
- when sel=01 then y will follow i1
- when sel=10 then y will follow i2
- when sel=1? that means when sel=11 or 10 in both cases output follows i3,therefore it causes **SYNTHESIS AND SIMULATION MISMATCHES**
- therefore when sel=11 we can see in the simulation it is latching to a value of one it is neither following i2 or i3 because of the confusion
- In the below simulated output there is no latching action is happening and the tool is not getting confused,because we must ensure that there should not be any overlapping cases while writing the RTL code all gates must be mutually exclusive inorder to avoid the confusion during simulation
![Screenshot (439)](https://user-images.githubusercontent.com/84865915/120091610-598afc00-c12a-11eb-8c77-317d3c546a36.png)
### sythesized report
![Screenshot (437)](https://user-images.githubusercontent.com/84865915/120091603-4aa44980-c12a-11eb-93bb-e66c020e0eb5.png)
here no latches will be inferred because all the cases are present since there are no missing cases
![Screenshot (438)](https://user-images.githubusercontent.com/84865915/120091607-50019400-c12a-11eb-95c9-4aeefff51a63.png)
## for loop and for generate
Loop statements include 
- forever
-  repeat
-  while
-  and for
![loop](https://user-images.githubusercontent.com/84865915/120091729-7c69e000-c12b-11eb-80c7-01ccc7eb9ff5.JPG)
- **for loop must be used inside the always block**
- for loop is used for **evaluating the expressions**
- for loop is just used for writing a very big hardware
- for loop is not used for instantiating the hardware
- advantage of **for loop** over **case** is number of lines of the code will be reduced.
- **generate for loop must be used outside the always block**
- generate for loop is used for **instantiating the hardware**

## Labs on for loop and for generate
### eg:mux_generate
- Here i_int is a bus
```
 module mux_generate (input i0 , input i1, input i2 , input i3 , input [1:0] sel  , output reg y);
wire [3:0] i_int;
assign i_int = {i3,i2,i1,i0};
integer k;
always @ (*)
begin
for(k = 0; k < 4; k=k+1) begin
	if(k == sel)
		y = i_int[k];
end
end
endmodule  
```

### simulated output:

![Screenshot (440)](https://user-images.githubusercontent.com/84865915/120092816-ae7f4000-c133-11eb-8b3c-2c1ba35a5c99.png)
when
- sel=00 then y follows i0
- sel=01 then y follows i1
- sel=10 then y follows i2
- sel=11 then y follows i3
### eg:demux_generate
```
  module demux_generate (output o0 , output o1, output o2 , output o3, output o4, output o5, output o6 , output o7 , input [2:0] sel  , input i);
reg [7:0]y_int;
assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
integer k;
always @ (*)
begin
y_int = 8'b0;
for(k = 0; k < 8; k++) begin
	if(k == sel)
		y_int[k] = i;
end
end
endmodule 
```


### simulate output
for 1 by 4 demux we have four outputs ,only one of the output signal is going to follow our input signal remaining all are zeros



![Screenshot (441)](https://user-images.githubusercontent.com/84865915/120092819-b2ab5d80-c133-11eb-9c89-a800547f4156.png)


### eg:ripple carry adder
adding the two 8 bit numbers
**RULE FOR ADDITION**
- if we add two N bit numbers then the result is going to be N+1 bits
- if we add one n bit and one m bit number then the result is going to be MAX(m,n)+1 bit
### eg:ripple carry adder

```
   module rca (input [7:0] num1 , input [7:0] num2 , output [8:0] sum);
wire [7:0] int_sum;
wire [7:0]int_co;

genvar i;
generate
	for (i = 1 ; i < 8; i=i+1) begin
		fa u_fa_1 (.a(num1[i]),.b(num2[i]),.c(int_co[i-1]),.co(int_co[i]),.sum(int_sum[i]));
	end

endgenerate
fa u_fa_0 (.a(num1[0]),.b(num2[0]),.c(1'b0),.co(int_co[0]),.sum(int_sum[0]));


assign sum[7:0] = int_sum;
assign sum[8] = int_co[7];
endmodule
module fa (input a , input b , input c, output co , output sum);
	assign {co,sum}  = a + b + c ;
endmodule 

```
 

### simulated output:

![Screenshot (442)](https://user-images.githubusercontent.com/84865915/120093324-197e4600-c137-11eb-910a-5ace7ec72d64.png)
### sythesized output:
![Screenshot (444)](https://user-images.githubusercontent.com/84865915/120093427-d83a6600-c137-11eb-946b-e2f684d5e802.png)
![Screenshot (445)](https://user-images.githubusercontent.com/84865915/120093410-ade8a880-c137-11eb-96ed-366aaa85c493.png)

# acknowledgement
- Kunal Gosh, Co-Founder (VSD Corp. Pvt Ltd)
- Shon Taware, Teaching Assistant (VSD Corp. Pvt Ltd)
# references
  
- [https://www.vlsisystemdesign.com/rtl-design-using-verilog-with-sky130-technology/](https://www.vlsisystemdesign.com/rtl-design-using-verilog-with-sky130-technology/)
- [https://skywater-pdk.readthedocs.io/en/latest/](https://skywater-pdk.readthedocs.io/en/latest/)
- [http://www.clifford.at/yosys/](http://www.clifford.at/yosys/)
   

 
