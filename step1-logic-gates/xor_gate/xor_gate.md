# 🔘 XOR Gate Lab

This lab demonstrates how to implement a simple 2-input XOR gate in Verilog, test it using a testbench, and observe the waveform using GTKWave.

---

## 📄 Verilog Design

### `xor_gate.v`

```verilog
// xor_gate.v
// 2-input XOR gate module

module xor_gate(
    input A,      // First input
    input B,      // Second input
    output Y      // Output = A XOR B
);

    assign Y = A ^ B;  // Perform bitwise XOR operation

endmodule
```

---

## 🧪 Testbenh

### `xor_gate_tb.v`

```verilog
// xor_gate_tb.v
// Testbench for 2-input XOR gate

`timescale 1ns / 1ps

module xor_gate_tb;

    // Declare testbench signals
    reg A;
    reg B;
    wire Y;

    // Instantiate the design under test (DUT)
    xor_gate dut (
        .A(A),
        .B(B),
        .Y(Y)
    );

    // Apply test stimulus
    initial begin
        $dumpfile("xor_gate.vcd");  // Output VCD file
        $dumpvars(0, xor_gate_tb);  // Dump all variables

        A = 0; B = 0; #10;
        A = 0; B = 1; #10;
        A = 1; B = 0; #10;
        A = 1; B = 1; #10;

        $finish;
    end

endmodule
```

---

## ⚙️ Simulation on Commands

```bash
# Compile the Verilog source and testbench into an executable
iverilog -o xor_gate.vvp xor_gate.v xor_gate_tb.v

# Run the simulation using the compiled file
vvp xor_gate.vvp

# Launch GTKWave to view the waveform from the generated VCD file
gtkwave xor_gate.vcd
```

---

## 📷 Simulation Result

![OR gate waveform](or_wave.png)
