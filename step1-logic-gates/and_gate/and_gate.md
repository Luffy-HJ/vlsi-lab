# 🔘 AND Gate Lab

This lab demonstrates how to implement a simple 2-input AND gate in Verilog, test it using a testbench, and observe the waveform using GTKWave.

---

## 📄 Verilog Design

### `and_gate.v`

```verilog
// and_gate.v
// 2-input AND gate module

module and_gate(
    input A,      // First input
    input B,      // Second input
    output Y      // Output = A AND B
);

    assign Y = A & B;  // Perform bitwise AND operation

endmodule
```

---

## 🧪 Testbench

### `and_gate_tb.v`

```verilog
// and_gate_tb.v
// Testbench for 2-input AND gate

`timescale 1ns / 1ps

module and_gate_tb;

    // Declare testbench signals
    reg A;
    reg B;
    wire Y;

    // Instantiate the design under test (DUT)
    and_gate dut (
        .A(A),
        .B(B),
        .Y(Y)
    );

    // Apply test stimulus
    initial begin
        $dumpfile("and_gate.vcd");  // Output VCD file
        $dumpvars(0, and_gate_tb);  // Dump all variables

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
iverilog -o and_gate.vvp and_gate.v and_gate_tb.v

# Run the simulation using the compiled file
vvp and_gate.vvp

# Launch GTKWave to view the waveform from the generated VCD file
gtkwave and_gate.vcd
```

---

## 📷 Simulation Result

![AND gate waveform](and_wave.png)

## 🗺️ Netlist Visualization

![AND gate netlist](and_gate_netlist.png)
