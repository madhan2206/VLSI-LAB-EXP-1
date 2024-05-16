# VLSI-LAB-EXPERIMENTS
**AIM:**

 To simulate and synthesis Logic Gates,Adders and Subtractor using Xilinx ISE.

**APPARATUS REQUIRED:**

 Vivado 2023.1

**PROCEDURE:**

STEP:1 Start the Xilinx navigator, Select and Name the New project. 

STEP:2 Select the device family, device, package and speed. 

STEP:3 Select new source in the New Project and select Verilog Module as the Source type. 

STEP:4 Type the File Name and Click Next and then finish button. Type the code and save it. 

STEP:5 Select the Behavioral Simulation in the Source Window and click the check syntax. 

STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table. 

STEP:7 Select the Implementation in the Sources Window and select the required file in the Processes Window. 
STEP:8 Select Check Syntax from the Synthesize XST Process. Double Click in the Floorplan Area/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 

STEP:9 In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu. 

STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here. 

STEP:11 Load the Bit file into the SPARTAN 6 FPGA STEP:11 On the board, by giving required input, the LEDs starts to glow light, indicating the output.

Logic Diagram :


Logic Gates:
![324424600-6c0fefc1-5e35-4e2a-a7e6-a43307c59025](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/4b3a9252-f1c3-42bf-8ff3-91d9f3b60d32)

Half Adder:
![324424861-d2824b19-c614-4450-8e48-4ca53009ba06](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/1b02adc7-3969-4626-95b8-ddb7c150a04c)


Full adder:
![324424945-356a5336-2ab6-47d4-82d9-e8c33a3e6a8d](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/5a9051e0-6ef4-4920-9997-109e7e531db1)



Half Subtractor:
![324425023-87d90f41-33f6-46dd-818e-9dd509484811](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/8127a851-f4c4-4b9c-b55a-5f1048b4fa80)




Full Subtractor:
![324425057-3c7cfc11-e688-43f8-a535-baf265887eaa](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/cf998e90-c92a-4584-a01b-ed1a1a9a3f59)






8 Bit Ripple Carry Adder:

![324425205-55e24d85-0a84-41dc-8696-fca8777a0b81](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/9d1ae261-63e7-4264-82db-8fc86fd7d8f9)







VERILOG CODE:

# Full Adder:
```
module fulladder (sum, cout, a,b,c);
input a,b,c;
output sum, cout;
wire w1,w2,w3,w4,w5;
xor x1(w1,a,b);
xor x2(sum,w1,c);
and al(w2,a,b);
and a2(w3,b,c);
and a3(w4,a,c);
or o1(w5,w2,w3); or o2(cout,w5,w4);
endmodule
```
# Full Subractor:
```
module full_subtractor(a, b, c,D, Bout);
input a, b, c;
output D, Bout;
assign D = a^b^c;
assign Bout = (~a & b) | (~(a^ b) & c);
endmodule
```
# Half Adder:
```
module half_adder(a,b,sum,carry);
input a,b;
output sum,carry;
or(sum,a,b);
and(carry,a,b);
endmodule
```
# Half Subractor:
```
module half_subtractor(D,Bo,A,B);
input A,B;
output D,Bo;
assign D=A^B;
assign Bo=(~A)&B;
endmodule
```
# Logic Gates:
```
module logicgates(a,b,andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate);
input a,b;
output andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate;
and(andgate,a,b);
or(orgate,a,b);
xor(xorgate,a,b);
nand(nandgate,a,b);  
nor(norgate,a,b);
xnor(xnorgate,a,b);
not(notgate,a);
endmodule
```
# Ripple Carry Adder 4Bit:
```
module rippe_adder(S, Cout, X, Y,Cin);
 input [3:0] X, Y;// Two 4-bit inputs
 input Cin;
 output [3:0] S;
 output Cout;
 wire w1, w2, w3;fulladder u1(S[0], w1,X[0], Y[0], Cin);
 fulladder u2(S[1], w2,X[1], Y[1], w1);
 fulladder u3(S[2], w3,X[2], Y[2], w2);
 fulladder u4(S[3], Cout,X[3], Y[3], w3);
endmodule
module fulladder(S, Co, X, Y, Ci);
  input X, Y, Ci;
  output S, Co;  
  wire w1,w2,w3;  
  xor G1(w1, X, Y); 
  xor G2(S, w1, Ci);
  and G3(w2, w1, Ci);
  and G4(w3, X, Y);
  or G5(Co, w2, w3);
endmodule
```
# Ripple Carry Adder 8bit
```
module fulladder(a,b,c,sum,carry);
input a,b,c;
output sum,carry;
wire w1,w2,w3;
xor(w1,a,b);
xor(sum,w1,c);
and(w2,w1,c);
and(w3,a,b);
or(carry,w2,w3);
endmodule

module rca_8bit(a,b,cin,s,cout);
input [7:0]a,b;
input cin;
output [7:0]s;
output cout;
wire [7:1]w;
fulladder f1(a[0], b[0], cin, s[0], w[1]);
fulladder f2(a[1], b[1], w[1], s[1], w[2]);
fulladder f3(a[2], b[2], w[2], s[2], w[3]);
fulladder f4(a[3], b[3], w[3], s[3], w[4]);
fulladder f5(a[4], b[4], w[4], s[4], w[5]);
fulladder f6(a[5], b[5], w[5], s[5], w[6]);
fulladder f7(a[6], b[6], w[6], s[6], w[7]);
fulladder f8(a[7], b[7], w[7], s[7], cout);
endmodule
```

OUTPUT:

# Full Adder:
![324426983-9da87612-f76f-4a55-87b7-e64c072769a3](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/8b00a1aa-6bac-4742-a00c-83bd5e7d7121)
<img width="632" alt="324427193-dd32baf4-0a88-482a-8eba-eb74ee91efb0" src="https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/f0d74361-5cfe-4782-a191-df087f47c6a5">

# Full Subractor:
![324427465-9698c902-c33c-4c23-9cbd-b4e399c2a447](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/bafae282-c753-4a9d-beef-3dab1af83e5c)
<img width="490" alt="324427507-200430eb-dbdd-4eda-91f5-883510da1b13" src="https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/72be47f4-15f1-49eb-9eb3-9b1538f6041e">


# Half Adder:
![324427690-3cbf9482-03a9-4b53-a03a-f49f7cafe3ef](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/f7aadef6-bc4b-4180-a592-f5ef99d86b6a)

![324427730-2892f94d-0821-4ecd-8566-50061df0bd6d](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/8e6946f0-9e31-4041-8459-9331e961f587)



# Half Subractor:

![324427923-3c3fcd36-7ac7-425e-abc3-1230d561b14f](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/a03fc4c0-cd2f-4a2c-8b58-93243bdb873b)

<img width="488" alt="324428000-447e0d86-694c-47e2-b866-92984326abe2" src="https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/5ad6e59f-eeab-4cf8-98b7-1c580b2186f9">


# Logic Gates:
![324428312-8385c1de-dc92-4170-be5c-af45ab89229f](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/82a941b3-6fb9-4b51-b66f-75ad6453da06)
<img width="556" alt="324428398-02755fc3-9927-4ad6-b151-ca97679df7e7" src="https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/545551f2-108b-462c-a8a9-588f99fc6f36">


# Ripple Carry Adder 4bit:

![324428627-8e4ad7f6-481a-4da9-a74b-920fb131775e](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/fc000514-4cf8-4ca0-b578-c9e97293ff03)

<img width="632" alt="324428849-904f020e-63c9-451c-813e-84d7d64f3f20" src="https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/171f34fa-c9e9-43f1-9c82-e378be7220b1">



# Ripple Carry Adder 8bit:
![324428956-f6b997df-af3c-488a-b7b9-57e91deb6d96](https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/d12eaf16-3add-4ea0-9fcc-3a43dd458247)
<img width="631" alt="324429019-0827ac48-940f-4c8f-982d-75be689e746a" src="https://github.com/madhan2206/VLSI-LAB-EXP-1/assets/170016170/8c23962c-0b31-46fd-a65e-cea78a4f67fe">


RESULT:Thus the simulation and synthesis Logic Gates,Adders and Subtractor using VIVADO 2023.2 has been verified.

