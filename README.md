# RTL-to-GDSII Implementation of 4-Bit Adder using Synopsys Tools and SAED32nm Technology

## Project Overview

This project demonstrates the complete ASIC RTL-to-GDSII flow of a 4-bit Ripple Carry Adder using Synopsys EDA tools and SAED32nm technology library.

### Tools Used

- Synopsys VCS
- Synopsys Design Compiler (DC)
- Synopsys IC Compiler II (ICC2)
- SAED32nm Standard Cell Library

---

## RTL Design

The RTL of the 4-bit adder was written in Verilog HDL.

### RTL Code

```
module adder (
    input a,
    input b,
    input cin,
    output sum,
    output cout
);

assign sum  = a ^ b ^ cin;
assign cout = (a & b) | (b & cin) | (a & cin);

endmodule

module adder_tb;

    reg  [3:0] a;
    reg  [3:0] b;
    reg        cin;

    wire [3:0] sum;
    wire       cout;

    // DUT Instantiation
    adder uut (
        .a(a),
        .b(b),
        .cin(cin),
        .sum(sum),
        .cout(cout)
    );

    // Dump waveform
    initial begin
        $dumpfile("adder.vcd");
        $dumpvars(0, adder_tb);
    end

    // Apply test vectors
    initial begin

        // Initialize signals
        a   = 4'b0000;
        b   = 4'b0000;
        cin = 1'b0;

        #10;

        // Test Case 1
        a   = 4'b0000;
        b   = 4'b0000;
        cin = 1'b0;

        #10;

        // Test Case 2
        a   = 4'b0011;
        b   = 4'b0101;
        cin = 1'b0;

        #10;

        // Test Case 3
        a   = 4'b0110;
        b   = 4'b0011;
        cin = 1'b1;

        #10;

        // Test Case 4
        a   = 4'b1111;
        b   = 4'b0001;
        cin = 1'b0;

        #10;

        // Test Case 5
        a   = 4'b1111;
        b   = 4'b1111;
        cin = 1'b1;

        #20;   // Hold last testcase for visibility

        $finish;
    end

endmodule
```
## RTL Simulation using Synopsys VCS

RTL verification was performed using Synopsys VCS and DVE waveform viewer.

### Compilation Command

```bash
vcs -full64 adder.v adder_tb.v
```

### Run Simulation

```bash
./simv
```

### Launch DVE

```bash
dve &
```

### RTL Waveform Result

<img width="1600" height="900" alt="WhatsApp Image 2026-07-14 at 3 14 57 PM" src="https://github.com/user-attachments/assets/9b8730e2-aa44-46a7-9f15-0d02e33bd321" />

Example:
- `a = 0000, b = 0000, cin = 0 → sum = 0000`
- `a = 0011, b = 0101, cin = 0 → sum = 1000`
- `a = 0110, b = 0011, cin = 1 → sum = 1010`
- `a = 1111, b = 0001, cin = 0 → sum = 0000, cout = 1`
- `a = 1111, b = 1111, cin = 1 → sum = 1111, cout = 1`

---

## Logic Synthesis using Synopsys Design Compiler

The RTL was synthesized using Synopsys Design Compiler using SAED32nm technology library.

### Technology Library

```text
saed32rvt_tt1p05v25c.db
```

### Design Compiler Flow

1. Analyze RTL
2. Elaborate Design
3. Link Libraries
4. Read Constraints
5. Compile Ultra
6. Generate Reports
7. Write Netlist

### Design Compiler Script

📌 **Paste Design Compiler screenshot here**

<!-- INSERT DESIGN COMPILER SCREENSHOT HERE -->

Generated files:

- Synthesized Netlist
- Area Report
- Timing Report
- Power Report
- QoR Report

---

## Floorplanning using ICC2

The synthesized netlist was imported into ICC2 for physical implementation.

Floorplanning includes:

- Core area definition
- Aspect ratio setup
- Utilization setup
- IO placement preparation

---

## Routing

Routing connects all placed standard cells using metal layers.

Routing stages include:

- Global Routing
- Detailed Routing
- Optimization
- DRC fixing

### Routing Result

<img width="1600" height="974" alt="WhatsApp Image 2026-07-14 at 3 11 20 PM" src="https://github.com/user-attachments/assets/a980d471-63cc-4144-a2fa-c76fea56f3fb" />

---

## Physical Verification

Physical verification ensures the design is manufacturable.

Verification performed:

- DRC
- LVS
- Connectivity Check
- Timing Verification

---

## GDSII Generation

The final layout database was exported as a GDSII file.

Generated file:

<img width="1600" height="972" alt="WhatsApp Image 2026-07-14 at 3 11 43 PM" src="https://github.com/user-attachments/assets/c0109ef3-1692-4798-963c-123de681f14f" />

```

### GDSII Export Result
<img width="1600" height="950" alt="WhatsApp Image 2026-07-14 at 3 12 11 PM" src="https://github.com/user-attachments/assets/02c07eeb-40ca-4212-9726-8968bcfaeb7a" />

---

## Project Directory Structure

```text
adder/
│
├── rtl/
│   ├── adder.v
│   └── adder_tb.v
│
├── constraints/
│   └── constraints.sdc
│
├── scripts/
│   └── script.tcl
│
├── reports/
│   ├── area.rpt
│   ├── timing.rpt
│   ├── power.rpt
│   └── qor.rpt
│
├── netlist/
│   └── adder_syn.v
│
├── outputs/
│   ├── adder.gds
│   ├── adder.def
│   └── adder_postroute.v
│
└── README.md
```

---

## Results Summary

| Parameter | Value |
|-----------|-------|
| Technology | SAED32nm |
| Design | 4-Bit Adder |
| Simulator | Synopsys VCS |
| Synthesis Tool | Design Compiler |
| Physical Design Tool | ICC2 |
| Output Format | GDSII |

---

## Author

**Sakthi Narayanan V**

M.E VLSI Design

Saveetha Engineering College

Chennai, India
