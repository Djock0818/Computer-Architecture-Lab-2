# Computer-Architecture-Lab-2

Testbench:
`timescale 1ns/1ps
module Lab2_RD_testbench();

reg clock, reset, I;
    wire F;
    wire [2:0] S;

    Lab2_RD uut (.I(I), .clock(clock), .reset(reset), .F(F), .S(S));

    initial
        clock = 1'b0;
    always begin
        #5 clock = (clock == 0)? 1:0;
    end

    initial begin
         reset = 1'b0;
        I = 1'b0;
        #14 I = 1'b1;
        #10 I = 1'b0;
        #10 I = 1'b0;
        #10 I = 1'b1;
        #10 I = 1'b0;
        #10 I = 1'b0;
        #10 I = 1'b1;
        #10 I = 1'b0;
        #10 I = 1'b0;
        #10 I = 1'b1;
        #10 I = 1'b0;
        #10 I = 1'b0;
        #10 I = 1'b0;
        #10 I = 1'b1;
        #10 I = 1'b0;

          
    end

    initial begin
        #1000 $stop;
    end

endmodule

Source Code:

module Lab2_RD(I,clock,reset,F,S);
  input clock, reset, I;
    output reg F;
    output reg [2:0] S;

    parameter
        S0=3'b000,
        S1=3'b001,
        S2=3'b010,
        S3=3'b011,
        S4=3'b100;


    reg [2:0] CS,NS;

    always @(posedge clock)
    begin
        if(reset==1)
            CS <= S0;
        else
            CS <= NS; 
    end

    always @(CS,I)
    begin
        case(CS)
        S0:begin
        NS = (I==1)? S1:S0;
        end

        S1:begin
