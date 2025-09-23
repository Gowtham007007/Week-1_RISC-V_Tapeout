<div align="center">

![Timing](https://img.shields.io/badge/Timing-Libraries-blue?style=for-the-badge)
![Synthesis](https://img.shields.io/badge/Yosys-Synthesis-green?style=for-the-badge)
![Flip-Flop](https://img.shields.io/badge/Flip--Flop-Coding-orange?style=for-the-badge)
![Icarus-Verilog](https://img.shields.io/badge/Icarus--Verilog-Simulation-lightgrey?style=for-the-badge)

</div>

# 🌟 Welcome to Day 2 of the RTL Workshop!  

## 🕒 Topic: Timing Libraries, Synthesis Approaches & Flip-Flop Coding  

👋 **Hello Learner!**  
We’re excited to have you back on **Day 2** of this RTL journey 🚀.  
Today, we dive deeper into RTL design, focusing on **timing libraries**, **synthesis styles**, and **efficient flip-flop coding techniques**.  

By the end of this session, you will:  
✅ Understand the role of `.lib` timing libraries in digital design  
✅ Compare **Hierarchical vs Flat Synthesis** with clarity  
✅ Learn efficient RTL styles for **Flip-Flop implementation**  
✅ Simulate and synthesize designs with **Icarus Verilog** and **Yosys**  

---

## 📂 Contents

- ⚡ **[Timing Libraries](#timing-libraries)**
  - 📘 [SKY130 PDK Overview](#sky130-pdk-overview)
  - 🔍 [Decoding tt_025C_1v80 in the SKY130 PDK](#decoding-tt_025c_1v80-in-the-sky130-pdk)
  - 📝 [Opening and Exploring the .lib File](#opening-and-exploring-the-lib-file)

- 🛠 **[Hierarchical vs. Flattened Synthesis](#hierarchical-vs-flattened-synthesis)**
  - 🏗 [Hierarchical Synthesis](#hierarchical-synthesis)
  - 🧩 [Flattened Synthesis](#flattened-synthesis)
  - ⚖️ [Key Differences](#key-differences)

- 🔹 **[Flip-Flop Coding Styles](#flip-flop-coding-styles)**
  - ⏱ [Asynchronous Reset D Flip-Flop](#asynchronous-reset-d-flip-flop)
  - 🔴 [Asynchronous Set D Flip-Flop](#asynchronous-set-d-flip-flop)
  - ⏹ [Synchronous Reset D Flip-Flop](#synchronous-reset-d-flip-flop)

- 🖥 **[Simulation and Synthesis Workflow](#simulation-and-synthesis-workflow)**
  - 💻 [Icarus Verilog Simulation](#icarus-verilog-simulation)
  - ⚡ [Synthesis with Yosys](#synthesis-with-yosys)

---


## Timing Libraries

### SKY130 PDK Overview

The **SKY130 PDK** is an open-source Process Design Kit based on **SkyWater 130nm CMOS technology**, providing essential models for IC design, including timing, power, and process variation data.

---

### Decoding `tt_025C_1v80` in the SKY130 PDK

| Field | Meaning |
|-------|---------|
| **tt** | Typical process corner |
| **025C** | Temperature = 25°C |
| **1v80** | Core voltage = 1.8V |

> ⚡ **Tip:** This helps identify which process, voltage, and temperature conditions the library models.

---
### Opening and Exploring the .lib File

To open the sky130_fd_sc_hd__tt_025C_1v80.lib file:

1. **Install a text editor:**
   ```shell
   sudo apt install gedit
   ```
2. **Open the file:**
   ```shell
   gedit sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
 <img src="Images/libfile.jpeg" alt="Library file" width="70%"/> 


---

## Hierarchical vs. Flattened Synthesis

### Hierarchical Synthesis

- **Definition**: Retains the module hierarchy as defined in RTL, synthesizing modules separately.
- **How it Works**: Tools like Yosys process each module independently, using commands such as `hierarchy` to analyze and set up the design structure.

**Advantages:**
- Faster synthesis time for large designs.
- Improved debugging and analysis due to maintained module boundaries.
- Modular approach, aiding integration with other tools.

**Disadvantages:**
- Cross-module optimizations are limited.
- Reporting can require additional configuration.

**Example:**

<img src="Images/hierarchical_netlist.jpeg" alt="Hierarchical Netlist" width="70%"/>


---

### Flattened Synthesis

- **Definition**: Merges all modules into a single flat netlist, eliminating hierarchy.
- **How it Works**: The `flatten` command in Yosys collapses the hierarchy, allowing whole-design optimizations.

**Advantages:**
- Enables aggressive, cross-module optimizations.
- Results in a unified netlist, sometimes simplifying downstream processes.

**Disadvantages:**
- Longer runtime for large designs.
- Loss of hierarchy complicates debugging and reporting.
- Can increase memory usage and netlist complexity.

**Example:**


<img src="Images/flattened.jpeg" alt="Flattened Netlist" width="70%"/>

> **Important:** Hierarchical synthesis maintains sub-modules in the design, while flattening produces a netlist from the ground up.


## Multiple_Modulde_Netlist : 

 **Open the Generated Netlist :**
   ```shell
   write_verilog -noattr multiple_modules_hier.v
   ```
<img src="Images/multiple_module_netlist.jpeg" alt="Multiple Module Netlist" width="70%"/>

---

### Key Differences

| Aspect                | Hierarchical Synthesis             | Flattened Synthesis           |
|-----------------------|------------------------------------|------------------------------|
| Hierarchy             | Preserved                          | Collapsed                    |
| Optimization Scope    | Module-level only                  | Whole-design                 |
| Runtime               | Faster for large designs           | Slower for large designs     |
| Debugging             | Easier (traces to RTL)             | Harder                       |
| Output Complexity     | Modular structure                  | Single, complex netlist      |
| Use Case              | Modularity, analysis, reporting    | Maximum optimization         |

---

## Flip-Flop Coding Styles

Flip-flops are fundamental sequential elements in digital design, used to store binary data. Below are efficient coding styles for different reset/set behaviors.

### Asynchronous Reset D Flip-Flop

```verilog
module dff_asyncres (input clk, input async_reset, input d, output reg q);
  always @ (posedge clk, posedge async_reset)
    if (async_reset)
      q <= 1'b0;
    else
      q <= d;
endmodule
```
- **Asynchronous reset**: Overrides clock, setting q to 0 immediately.
- **Edge-triggered**: Captures d on rising clock edge if reset is low.

### Asynchronous Set D Flip-Flop

```verilog
module dff_async_set (input clk, input async_set, input d, output reg q);
  always @ (posedge clk, posedge async_set)
    if (async_set)
      q <= 1'b1;
    else
      q <= d;
endmodule
```
- **Asynchronous set**: Overrides clock, setting q to 1 immediately.

### Synchronous Reset D Flip-Flop

```verilog
module dff_syncres (input clk, input async_reset, input sync_reset, input d, output reg q);
  always @ (posedge clk)
    if (sync_reset)
      q <= 1'b0;
    else
      q <= d;
endmodule
```
- **Synchronous reset**: Takes effect only on the clock edge.

---

## Simulation and Synthesis Workflow

### Icarus Verilog Simulation

1. **Compile:**
   ```shell
   iverilog dff_asyncres.v tb_dff_asyncres.v
   ```
2. **Run:**
   ```shell
   ./a.out
   ```
3. **View Waveform:**
   ```shell
   gtkwave tb_dff_asyncres.vcd
   ```

<img src="Images/dff_asyncres.jpeg" alt="Asynch - Reset" width="70%"/>


### Synthesis with Yosys

1. Start Yosys:
   ```shell
   yosys
   ```
2. Read Liberty library:
   ```shell
   read_liberty -lib /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
3. Read Verilog code:
   ```shell
   read_verilog /path/to/dff_asyncres.v
   ```
4. Synthesize:
   ```shell
   synth -top dff_asyncres
   ```
5. Map flip-flops:
   ```shell
   dfflibmap -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
6. Technology mapping:
   ```shell
   abc -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```
7. Visualize the gate-level netlist:
   ```shell
   show
   ```

<img src="Images/gate_level_netlist.jpeg" alt="Gate Level Netlist" width="70%"/>

8. Similar Examples:
   
   i) Asynchronous Set D Flip-Flop :
   
   
   <img src="Images/dff_async_set.jpeg" alt="Asynch - Set" width="70%"/>
   
   ii) Synchronous Reset D Flip-Flop :
   
   
   <img src="Images/dff_syncres.jpeg" alt="Synch - Reset" width="70%"/>

   

# Multiple by 8 and its Netlist Generation : 

# 7️ Viewing the Generated Netlist

Once you synthesize your design (e.g., an 8-bit multiplier) using **Yosys**, you can export the netlist:

```shell
write_verilog -noattr mul_by_8_netlist.v

```

```verilog
module mul_by_8 (input [7:0] a, input [7:0] b, output [15:0] y);
  wire _0_, _1_, _2_, _3_, _4_, _5_;

  // Example internal connections (auto-generated)
  assign _0_ = a[0] & b[0];
  assign _1_ = a[1] & b[0];
  assign _2_ = a[0] & b[1];
  assign _3_ = _1_ ^ _2_;
  assign y[0] = _0_;
  assign y[1] = _3_;
  // ...
endmodule
```
 Netlist Generated : 

<img src="Images/multiple8.jpeg" alt="Library file" width="70%"/>


---
# Summary
This overview provides you with practical insights into timing libraries, synthesis strategies, and reliable coding practices for flip-flops. Continue experimenting with these concepts to deepen your understanding of RTL design and synthesis.
