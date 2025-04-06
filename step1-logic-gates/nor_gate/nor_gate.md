# 🔘 NOR Gate Lab

This lab demonstrates how to implement a simple 2-input NOR gate in Verilog, test it using a testbench, and observe the waveform using GTKWave.

---

## 📄 Verilog Design

### `nor_gate.v`

```verilog
// nor_gate.v
// 2-input NOR gate module

module nor_gate(
    input A,      // First input
    input B,      // Second input
    output Y      // Output = ~(A | B)
);

    assign Y = ~(A | B);  // Perform bitwise NOR operation

endmodule
```

---

## 🧪 Testbench

### `nor_gate_tb.v`

```verilog
// nor_gate_tb.v
// Testbench for 2-input NOR gate

`timescale 1ns / 1ps

module nor_gate_tb;

    // Declare testbench signals
    reg A;
    reg B;
    wire Y;

    // Instantiate the design under test (DUT)
    nor_gate dut (
        .A(A),
        .B(B),
        .Y(Y)
    );

    // Apply test stimulus
    initial begin
        $dumpfile("nor_gate.vcd");     // Output VCD file
        $dumpvars(0, nor_gate_tb);     // Dump all variables

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
iverilog -o nor_gate.vvp nor_gate.v nor_gate_tb.v

# Run the simulation using the compiled file
vvp nor_gate.vvp

# Launch GTKWave to view the waveform from the generated VCD file
gtkwave nor_gate.vcd
```

---

## 📷 Simulation Result

![NOR gate waveform](nor_wave.png)
