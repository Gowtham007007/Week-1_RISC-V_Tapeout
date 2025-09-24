# ⚡️ Gate-Level Simulation (GLS)

Gate-Level Simulation (**GLS**) is a **critical verification step** in the VLSI design flow where the **synthesized gate-level netlist** of a digital circuit is simulated.  
It ensures that what you designed at RTL truly works at the gate level, **with real delays and test structures** ✅  

---

## ❓ What is GLS?
GLS is the process of simulating a **post-synthesis netlist** (a circuit represented as logic gates) instead of high-level RTL.  
It helps to validate the following aspects:

- 🧩 **Functional correctness** – Does the netlist behave exactly like the RTL?  
- ⏱ **Timing behavior** – Does it meet timing constraints (setup/hold)?  
- 🔋 **Power estimates** – Switching activity and power can be observed.  
- 🧪 **DFT structures** – Scan chains and test logic work correctly.  

> ⚠️ GLS is slower than RTL simulation but much more **realistic** and **trustworthy**.

---

## 💡 Why Perform GLS?
- ✅ **Synthesis Validation** → Ensures synthesis tools correctly map RTL → gates.  
- ⏳ **Timing Verification** → Detects violations using **SDF (Standard Delay Format)** back-annotation.  
- 🧬 **Testability Checks** → Verifies scan chains and DFT features.  
- 🚀 **Confidence before tape-out** → Reduces risk of silicon failure.  

---

## 🕐 When is GLS Performed?
GLS is usually done at **two critical points**:
1. **After Synthesis** – Verify RTL → Gate translation.  
2. **Before Physical Design (P&R)** – Catch timing/test issues early.  

---

## 🧭 Types of GLS
| Type             | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| **Functional GLS** | 🔹 Logic-only simulation (zero or unit delays). Fast but ignores real timing. |
| **Timing GLS**     | 🔹 Uses SDF annotated delays. Checks setup/hold, glitches, and real-world timing. |

---

## ⏳ Delay Annotation
GLS often uses **SDF Back-Annotation** to model **real delays** from synthesis or P&R:
- **Without annotation** → Ideal behavior, unrealistic.  
- **With SDF annotation** → Realistic timing behavior (net delays, cell delays, setup/hold).  

> 💎 This step bridges the gap between **ideal RTL sim** and **silicon reality**.

---


# 🧪 Lab Experiment

## 🔹Ternary Operator MUX

In this lab, we design a **2:1 Multiplexer** using the **ternary operator** in Verilog.  
The multiplexer selects one of two inputs (`i0`, `i1`) based on the control signal (`sel`) and drives it to the output (`y`).  

### 📜 Verilog Code
```verilog
// 2:1 MUX using Ternary Operator
module ternary_operator_mux (
  input  i0, 
  input  i1, 
  input  sel, 
  output y
);
  assign y = sel ? i1 : i0;
endmodule
```
---
## Waveform of RTL Code Simulation :

![Ternary Operator Waveform ](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/ternary_wave.png)

---

## Netlist of RTL Code :
## Synthesis Using Yosys

Synthesize the above MUX using Yosys.  
_Follow the standard Yosys synthesis flow._

![Netlist](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/ternary_net.png)

---

## Netlist Code:
```shell
  write_verilog -noattr ternary_operator_mux_net.v
```

![Netlist](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/ternary_net_code.png)

---


## Waveform of Netlist Simulation :
## Gate-Level Simulation (GLS) of MUX

Run GLS for the synthesized MUX.  
Use this command (adjust paths as needed):

```shell
iverilog /path/to/primitives.v /path/to/sky130_fd_sc_hd.v ternary_operator_mux.v testbench.v
```

![Ternary Operator Waveform ](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/ternary_net_wave.png)

---


---

## ⚠️ Synthesis vs Simulation Mismatch

A **synthesis-simulation mismatch** occurs when the **simulation results of RTL (pre-synthesis)** do **not match** the **gate-level netlist (post-synthesis)** or actual hardware behavior.  

This is a critical issue in VLSI design because it can cause functional failures after tape-out! 🚨  

---

### 🔍 Common Causes of Mismatch

| Cause                           | Description                                                                 | Emoji |
|---------------------------------|-----------------------------------------------------------------------------|-------|
| **Non-synthesizable constructs** | Use of `#delays`, `initial` blocks, `real` numbers, or unsupported RTL.   | ⛔️   |
| **Incomplete / Ambiguous RTL**   | Missing `else` clauses, incomplete sensitivity lists, or undefined behavior. | ❓   |
| **Tool interpretation differences** | Different simulators or synthesis tools may handle ambiguous RTL differently. | 🛠️   |
| **Incorrect assumptions**        | Timing or resource assumptions not reflected in RTL or netlist.           | ⚡️   |

---

### 💡 Key Points to Avoid Mismatch

- ✅ Always write **synthesizable RTL** – avoid unsupported constructs.  
- ✅ Use **complete and unambiguous coding** – cover all branches, define all signals.  
- ✅ Verify **sensitivity lists** in combinational logic carefully.  
- ✅ Run **post-synthesis simulation** to catch mismatches early.  
- ✅ Compare **RTL simulation vs Gate-level simulation** waveforms systematically.  

> 💎 **Pro Tip:** A small mismatch in RTL vs netlist can lead to large functional failures on silicon!  

---

### 🔧 Quick Checklist for Designers

- [ ] No `#delay` or `initial` blocks in synthesizable code  
- [ ] Every `if` has an `else`  
- [ ] All combinational blocks have full sensitivity lists  
- [ ] Test both RTL and synthesized netlist  
- [ ] Annotate timing with SDF for timing GLS  

---




