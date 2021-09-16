# 16X4_Ram_Memory_Using_verilog_HDL
module raminfr (clk, en, we, a, di, do);
input clk;
input en;
input we;
input [4:0] a;
input [3:0] di;
output [3:0] do;
reg [3:0] ram [15:0];
reg [4:0] read_a;

always @(posedge clk) begin
if (en)
begin
if (we)
ram[a] &lt;= di;
read_a &lt;= a;
end
end
assign do = ram[read_a];
endmodule

//testbench

module tb_RAM16X4;

// Inputs
reg clk;
reg en;
reg we;
reg [4:0] a;
reg [3:0] di;

// Outputs
wire [3:0] do;

// Instantiate the Unit Under Test (UUT)
raminfr uut (
.clk(clk),
.en(en),
.we(we),
.a(a),
.di(di),
.do(do)
);

initial begin
// Initialize Inputs
clk = 0;
en = 0;
we = 0;
a = 0;
di = 0;

// Wait 100 ns for global reset to finish
#10;clk = 1;
en = 1;
we = 1;
a = 1;
di = 1;

end

endmodule
