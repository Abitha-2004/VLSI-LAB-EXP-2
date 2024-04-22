SIMULATION AND IMPLEMENTATION OF  COMBINATIONAL LOGIC CIRCUITS

AIM: 
 To simulate and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using vivado 2023.1.

APPARATUS REQUIRED:
vivado 2023.1

PROCEDURE:
 1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

**LOGIC DIAGRAM**

ENCODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/3cd1f95e-7531-4cad-9154-fdd397ac439e)


DECODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/45a5e6cf-bbe0-4fd5-ac84-e5ad4477483b)


MULTIPLEXER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/427f75b2-8e67-44b9-ac45-a66651787436)


DEMULTIPLEXER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/1c45a7fc-08ac-4f76-87f2-c084e7150557)


MAGNITUDE COMPARATOR

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/b2fe7a05-6bf7-4dcb-8f5d-28abbf7ea8c2)


  
VERILOG CODE
ENCODDER:
~~~
module encoder8to3(a0,a1,a2,d0,d1,d2,d3,d4,d5,d6,d7);
input d0,d1,d2,d3,d4,d5,d6,d7;
output a0,a1,a2;
or g1(a0,d1,d3,d5,d7);
or g2 (a1,d2,d3,d6,d7);
or g3(a2,d4,d5,d6,d7);
endmodule
~~~
OUTPUT:
![image](https://github.com/Abitha-2004/VLSI-LAB-EXP-2/assets/161303006/a8f7992e-77f2-4db7-ab3f-8ad3d26fb64d)
![image](https://github.com/Abitha-2004/VLSI-LAB-EXP-2/assets/161303006/9126d413-2224-4f8d-b670-88c0914e5046)
DECODER:
~~~
module decoder_struct(
   input [2:0] a,
  output [7:0] d
   );
wire x,y,z;
not g1(z,a[0]);
not g2(y,a[1]);
not g3(x,a[2]);
and g4(d[0],x,y,z);
and g5(d[1],x,y,a[0]);
and g6(d[2],x,a[1],z);
and g7(d[3],x,a[1],a[0]);
and g8(d[4],a[2],y,z);
and g9(d[5],a[2],y,a[0]);
and g10(d[6],a[2],a[1],z);
and g11(d[7],a[2],a[1],a[0]);
endmodule
~~~
OUTPUT:
![image](https://github.com/Abitha-2004/VLSI-LAB-EXP-2/assets/161303006/46cd29c7-73e7-40c0-9a75-623f6c4cce90)



MULTIPLEXER:
~~~
module mux_8to1(in,sel,out);
input [7:0] in; input [2:0] sel;
output reg out;
always @(*)
begin 
case(sel)
3'b000: out = in[0];
3'b001: out = in[1];
3'b010: out = in[2];
3'b011: out = in[3];
3'b100: out = in[4];
3'b101: out = in[5];
3'b110: out = in[6];
3'b111: out = in[7];
default:out = 1'bx;
endcase
end
endmodule
~~~
OUTPUT:
![image](https://github.com/Abitha-2004/VLSI-LAB-EXP-2/assets/161303006/7d1dc202-ab3f-4ccd-9921-3e75e2ab9b4b)
![image](https://github.com/Abitha-2004/VLSI-LAB-EXP-2/assets/161303006/466b79c5-ee93-4fe5-9533-419e5e546c5d)
DEMULTIPLEXER:
~~~
module demultiplexer1to8(y,s,a);
output reg[7:0]y;
input[2:0]s;
input a;

always@(*)
begin 
y=0;
case(s)
3'd0:y[0]=a;
3'd1:y[1]=a;
3'd2:y[2]=a;
3'd3:y[3]=a;
3'd4:y[4]=a;
3'd5:y[5]=a;
3'd6:y[6]=a;
3'd7:y[7]=a;
endcase
end
endmodule
~~~
OUTPUT:
![image](https://github.com/Abitha-2004/VLSI-LAB-EXP-2/assets/161303006/182b4140-779f-41e8-b4d6-07f69ffd3c51)
![image](https://github.com/Abitha-2004/VLSI-LAB-EXP-2/assets/161303006/1f2c1e2d-ab9c-43f0-9b2a-1cf990b4dc06)
MAGNITUDECOMPARATOR:
~~~
module comparator(a,b,eq,It,gt);
input[3:0]a,b;
output reg eq,It,gt;
always@(a,b)
begin
if(a==b)
begin
eq=1'b1;
It=1'b0;
gt=1'b0;
end 
else if(a>b)
begin
eq=1'b0;
It=1'b0;
gt=1'b1;
end
else
begin
eq=1'b0;
It=1'b1;
gt=1'b0;
end
end 
endmodule
~~~
OUTPUT:
![image](https://github.com/Abitha-2004/VLSI-LAB-EXP-2/assets/161303006/623cdbcb-1540-4da7-9b02-efc4265bc58b)
![image](https://github.com/Abitha-2004/VLSI-LAB-EXP-2/assets/161303006/f25e78d2-9f54-4778-8fe7-bc839059114a)

















OUTPUT WAVEFORM
 <<< PASTE YOUR OUTPUT WAVEFORM >>>

RESULT


