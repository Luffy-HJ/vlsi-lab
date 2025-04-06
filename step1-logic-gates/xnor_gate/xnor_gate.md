# 🔘 XNOR Gate Lab

This lab demonstrates how to implement a simple 2-input OR gate in Verilog, test it using a testbench, and observe the waveform using GTKWave.

---

## 📄 Verilog Design

### `xnor_gate.v`

```verilog
// xnor_gate.v
// 2-input XNOR gate module

module xnor_gate(
    input A,      // First input
    input B,      // Second input
    output Y      // Output = ~(A ^ B)
);

    assign Y = ~(A ^ B);  // Perform bitwise XNOR operation

endmodule
```

---

## 🧪 Testbench

### `xnor_gate_tb.v`

```verilog
// xnor_gate_tb.v
// Testbench for 2-input XNOR gate

`timescale 1ns / 1ps

module xnor_gate_tb;

    // Declare testbench signals
    reg A;
    reg B;
    wire Y;

    // Instantiate the design under test (DUT)
    xnor_gate dut (
        .A(A),
        .B(B),
        .Y(Y)
    );

    // Apply test stimulus
    initial begin
        $dumpfile("xnor_gate.vcd");     // Output VCD file
        $dumpvars(0, xnor_gate_tb);     // Dump all variables

        A = 0; B = 0; #10;
        A = 0; B = 1; #10;
        A = 1; B = 0; #10;
        A = 1; B = 1; #10;

        $finish;
    end

endmodule
```

---

## ⚙️ Simulation Commands

```bash
# Compile the Verilog source and testbench into an executable
iverilog -o xnor_gate.vvp xnor_gate.v xnor_gate_tb.v

# Run the simulation using the compiled file
vvp xnor_gate.vvp

# Launch GTKWave to view the waveform from the generated VCD file
gtkwave xnor_gate.vcd
```

---

## 📷 Simulation Result

![XNOR gate waveform](xnor_wave.png)
