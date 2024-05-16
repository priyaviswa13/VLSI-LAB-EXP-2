# SIMULATION AND IMPLEMENTATION OF COMBINATIONAL LOGIC CIRCUITS

# AIM: 
 To simulate ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using VIVADO 2023.1.

# APPARATUS REQUIRED:
  VIVADO 2023.1

# PROCEDURE:
```
STEP:1  Open Vivado: Launch Xilinx Vivado software on your computer.
STEP:2  Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".   
STEP:3  Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.                     
STEP:4  Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from 
        the file browser.
STEP:5  Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).                       
STEP:6  Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.             
STEP:7  Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.
STEP:8  Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window. 
STEP:9  View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.
```
# LOGIC DIAGRAM

# ENCODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/3cd1f95e-7531-4cad-9154-fdd397ac439e)

```
code:

module encoder_8_to_3(a0,a1,a2,d7,d6,d5,d4,d3,d2,d1,d0);
input d7,d6,d5,d4,d3,d2,d1,d0;
output a0,a1,a2;
or g1(a0,d1,d3,d5,d7);
or g2(a1,d2,d3,d6,d7);
or g3(a2,d4,d5,d6,d7);
endmodule
```

# OUTPUT:
![320416709-b2cb2f7d-c92a-47ec-a900-19bd3b3b0da3](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/166889783/8ea86d5a-3408-474d-b849-5f8ff8b18043)

# DECODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/45a5e6cf-bbe0-4fd5-ac84-e5ad4477483b)

```
CODE:
module decoder(input [2:0] a,output [7:0] d );
assign d[0]=(~a[2])&(~a[1])&(~a[0]);
assign d[1]=(~a[2])&(~a[1])&(a[0]);
assign d[2]=(~a[2])&(a[1])&(~a[0]);
assign d[3]=(~a[2])&(a[1])&(a[0]);
assign d[4]=(a[2])&(~a[1])&(~a[0]);
assign d[5]=(a[2])&(~a[1])&(a[0]);
assign d[6]=(a[2])&(a[1])&(~a[0]);
assign d[7]=(a[2])&(a[1])&(a[0]);
endmodule
```

# OUTPUT:
![320416856-6e158ab1-eca6-450b-b59e-a212e33a3e43](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/166889783/0e9b458f-9102-4f3b-8e35-0a6baf036f43)

# MULTIPLEXER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/427f75b2-8e67-44b9-ac45-a66651787436)

```
CODE:
module mux(a,s,y);
input [7:0]a;
input [2:0]s;
output y;
reg y;
always@({s ,a})
   begin
      case(s)
         3'b000: y=a[0];
         3'b001: y=a[1];
         3'b010: y=a[2];
         3'b011: y=a[3];
         3'b100: y=a[4];
         3'b101: y=a[5];
         3'b110: y=a[6];
         3'b111: y=a[7];
      endcase
   end
endmodule
```

# OUTPUT:
![320417225-766970e9-975e-478f-8ab1-8c5df2c24ad9](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/166889783/40d1035e-bcec-464c-a932-0f9c1b2886de)

# DEMULTIPLEXER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/1c45a7fc-08ac-4f76-87f2-c084e7150557)

```
CODE:

module demux(din,s,d);
input din;
input[2:0]s;
output [7:0]d;
assign d[0]=(din&~s [2]&~s[1]&~s[0]);
assign d[1]=(din&~s[2]&~s[1]&s[0]);
assign d[2]=(din&~s[2]&s[1]&~s[0]);
assign d[3]=(din&~s[2]&s[1]&s[0]);
assign d[4]=(din&s[2]&~s[1]&~s[0]);
assign d[5]=(din&s[2]&~s[1]&s[0]);
assign d[6]=(din&s[2]&s[1]&~s[0]);
assign d[7]=(din&s[2]&s[1]&s[0]);
endmodule
```

# OUTPUT:
![320417434-be30677f-15b5-4fc7-b9ec-3ec305974ccc](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/166889783/9d3917bd-6f98-41f1-bb03-3f6cae43e7e0)

# MAGNITUDE COMPARATOR

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/b2fe7a05-6bf7-4dcb-8f5d-28abbf7ea8c2)

```
CODE:

module comparator(a,b,eq,lt,gt);
input [3:0] a,b;
output reg eq,lt,gt;
always @(a,b)
begin
 if (a==b)
 begin
  eq = 1'b1;
  lt = 1'b0;
  gt = 1'b0;
 end
 else if (a>b)
 begin
  eq = 1'b0;
  lt = 1'b0;
  gt = 1'b1;
 end
 else
 begin
  eq = 1'b0;
  lt = 1'b1;
  gt = 1'b0;
 end
end 
endmodule
```

# OUTPUT:
![320417984-3b0a314f-3c1d-4e68-8284-020d02ebb8ef](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/166889783/ce94fb4f-7c5a-4c05-8696-8705a48579da)

# RESULT:
Simulation and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using Xilinx ISE is verified.


