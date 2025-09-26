<div align="center">

  # 🎉✨ **Welcome to Day 4: GLS & Verilog Adventures** ✨🎉 
  
  <a href="#"><img src="https://img.shields.io/badge/GLS-Simulation-purple?style=for-the-badge" alt="GLS"></a>
  <a href="#"><img src="https://img.shields.io/badge/Labs-HandsOn-green?style=for-the-badge" alt="Labs"></a>
  <a href="#"><img src="https://img.shields.io/badge/Verilog-Coding-red?style=for-the-badge" alt="Verilog"></a>
  <a href="#"><img src="https://img.shields.io/badge/Synthesis-Verification-blue?style=for-the-badge" alt="Synthesis"></a>


  ##  "From RTL to Gates – Making Your Designs Real!" 💡💻
</div>




## 🔹 What’s in this Workshop?

This session focuses on bridging the gap between **RTL design** and **actual gate-level behavior**.  
We’ll explore:

- ⚡️ **Gate-Level Simulation (GLS)** – Validate your post-synthesis netlist for **function, timing, and testability**.  
- 🔀 **Synthesis vs Simulation Mismatch** – Understand why RTL may behave differently from synthesized netlists and how to avoid it.  
- 🛠️ **Blocking vs Non-Blocking Assignments** – Learn correct coding practices for combinational & sequential logic.  
- 🧪 **Hands-on Labs** – Build, simulate, synthesize, and correct modules like **2:1 MUX & Blocking Caveat**.  

---

## 🏆 Why This is Important?

- Prevent **silicon bugs** before tape-out ⚠️💣  
- Master **robust RTL coding practices** 📝✅  
- Gain confidence in **post-synthesis verification** ⏱️💪  
- Prepare for **real-world ASIC/FPGA design workflows** 🛠️🚀  

---


# 🗂️ Day 4: Table of Contents 🛠️💡

| Section | Topics | Link |
|---------|--------|------|
| 1️⃣ Gate-Level Simulation (GLS) ⚡️ | ❓ What is GLS? <br> 💡 Why Perform GLS? <br> 🕐 When is GLS Performed? <br> 🧭 Types of GLS <br> ⏳ Delay Annotation | [🚀 Dive In](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/tree/main/Day_4#%EF%B8%8F-gate-level-simulation) |
| 2️⃣ Lab Experiment 🧪 | 🔹 Ternary Operator MUX <br> 📜 Verilog Code <br> 🖥️ Waveform of RTL Code Simulation <br> 📝 Netlist of RTL Code <br> 💻 Netlist Code <br> ⏱️ Waveform of Netlist Simulation | [Click Here](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/tree/main/Day_4#-lab-experiment) |
| 3️⃣ Synthesis vs Simulation Mismatch 🔀 | 🔍 Common Causes of Mismatch <br> 💡 Key Points to Avoid Mismatch <br> ⚡️ Causes of S-S Mismatch <br> 🔧 Quick Checklist for Designers | [Click Here](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/tree/main/Day_4#%EF%B8%8F-synthesis-vs-simulation-mismatch) |
| 4️⃣ Bad MUX Example 🧩💥 | ❌ Problematic Code <br> ✅ Corrected Version <br> 🖥️ Waveform of RTL Simulation <br> 💻 Netlist Code <br> ⏱️ Netlist Simulation | [Click Here](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/tree/main/Day_4#-bad-mux-example-common-pitfalls-) |
| 5️⃣ Blocking vs Non-Blocking Assignments 🛠️🔄 | 📝 Blocking Statements (`=`) <br> ⏱️ Non-Blocking Statements (`<=`) <br> 🆚 Comparison Table | [Click Here](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/tree/main/Day_4#%EF%B8%8F-blocking-vs-non-blocking-assignments-in-verilog-%EF%B8%8F) |
| 6️⃣ Lab: Blocking Assignment Caveat 🛠️ | ❌ Problematic Code <br> ✅ Corrected Order <br> 💻 Synthesis of Module <br> ⏱️ GLS Synthesis on Netlist | [Click Here](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/tree/main/Day_4#%EF%B8%8F-lab--blocking-assignment-caveat-%EF%B8%8F) |
| 7️⃣ Day 4 Summary 🧩💡 | Quick Recap of GLS, S-S Mismatch, Assignments & Labs | [Click Here](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/tree/main/Day_4#-day-4-summary-gate-level-simulation--verilog-assignments-%EF%B8%8F) |
| 8️⃣ Conclusion 🏁 | Key Takeaways & Learnings | [Click Here](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/tree/main/Day_4#-conclusion) |
| 9️⃣ References 📚 | Books, Tutorials & Docs Used | [Click Here](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/tree/main/Day_4#-references) |

---

### ***🚀 Let's Dive In! 🌟***
---


#  ⚡️ Gate Level Simulation

Gate-Level Simulation (**GLS**) is a **critical verification step** in the VLSI design flow where the **synthesized gate-level netlist** of a digital circuit is simulated.  
It ensures that what you designed at RTL truly works at the gate level, **with real delays and test structures** ✅  

---

## ❓ What is GLS ?
GLS is the process of simulating a **post-synthesis netlist** (a circuit represented as logic gates) instead of high-level RTL.  
It helps to validate the following aspects:

- 🧩 **Functional correctness** – Does the netlist behave exactly like the RTL?  
- ⏱ **Timing behavior** – Does it meet timing constraints (setup/hold)?  
- 🔋 **Power estimates** – Switching activity and power can be observed.  
- 🧪 **DFT structures** – Scan chains and test logic work correctly.  

> ⚠️ GLS is slower than RTL simulation but much more **realistic** and **trustworthy**.

---

![GLS](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/Screenshot%20(2).png)

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
### Waveform of RTL Code Simulation :

![Ternary Operator Waveform ](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/ternary_wave.png)

---

## Netlist of RTL Code :

### Synthesis Using Yosys

Synthesize the above MUX using Yosys.  
_Follow the standard Yosys synthesis flow._

![Netlist](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/ternary_net.png)

---

### Netlist Code:

```shell
  write_verilog -noattr ternary_operator_mux_net.v
```

![Netlist](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/ternary_net_code.png)

---


## Waveform of Netlist Simulation :

### Gate-Level Simulation (GLS) of MUX

Run GLS for the synthesized MUX.  
Use this command (adjust paths as needed):

```shell
iverilog /path/to/primitives.v /path/to/sky130_fd_sc_hd.v ternary_operator_mux.v testbench.v
```

![Ternary Operator Waveform ](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/ternary_net_wave.png)

---


# ⚡️🔀 Synthesis vs Simulation Mismatch


A **synthesis-simulation mismatch** occurs when the **simulation results of RTL (pre-synthesis)** do **not match** the **gate-level netlist (post-synthesis)** or actual hardware behavior.  

This is a critical issue in VLSI design because it can cause **functional failures after tape-out**! 🚨💣  

---

## 🔍 Common Causes of Mismatch 🕵️‍♂️

| Cause                           | Description                                                                 |
|---------------------------------|-----------------------------------------------------------------------------|
| **Non-synthesizable constructs** | Use of `#delays`, `initial` blocks, `real` numbers, or unsupported RTL.⛔️💀|
| **Incomplete / Ambiguous RTL**   | Missing `else` clauses, incomplete sensitivity lists, or undefined behavior.❓🌀|
| **Tool interpretation differences** | Different simulators or synthesis tools may handle ambiguous RTL differently.🛠️⚖️|
| **Incorrect assumptions**        | Timing or resource assumptions not reflected in RTL or netlist.⚡️⚠️|



## 💡 Key Points to Avoid Mismatch 🌟✨

- ✅ **Always write synthesizable RTL** – avoid unsupported constructs. 📝  
- ✅ **Use complete and unambiguous coding** – cover all branches, define all signals. ✅🔧  
- ✅ **Verify sensitivity lists** in combinational logic carefully. 🧐  
- ✅ **Run post-synthesis simulation** to catch mismatches early. ⏱️  
- ✅ **Compare RTL vs Gate-level waveforms** systematically. 📊🔍

  ---

## ⚡️ Causes of Synthesis–Simulation (S-S) Mismatch 🧩💥

Synthesis–Simulation mismatches often occur due to subtle coding issues in RTL. Understanding the causes helps **avoid functional surprises**! 🚨

| Cause | Description |
|-------|-------------|
| **Missing Sensitivity List** | Combinational blocks without proper sensitivity lists can behave differently in simulation vs synthesized hardware.🕵️‍♂️⚡️|
| **Blocking vs Non-blocking Assignment** | Incorrect use of `=` (blocking) vs `<=` (non-blocking) in sequential logic may create mismatches in timing and ordering.🔀⏱️|
| **Non-standard Verilog Coding** | Using non-synthesizable constructs, initial blocks, or non-standard RTL may simulate correctly but fail after synthesis.❌🛠️|

Tips for Avoiding S-S Mismatch

- ✅ Always include **full sensitivity lists** in combinational logic (`always @(*)`).  
- ✅ Use **blocking assignments (`=`) for combinational**, **non-blocking (`<=`) for sequential** logic.  
- ✅ Stick to **standard synthesizable Verilog constructs**.  
- ✅ Perform **post-synthesis simulation** to catch mismatches early.
  

> 🔍 **Pro Insight:** Even small mismatches can lead to **major functional failures on silicon**! ⚡️💣  

---


<details>
<summary>💡 Fun Tip / Pro Insight 🌈</summary>

> A **tiny mismatch** in RTL vs netlist can lead to **huge silicon failures**! 🚀💥  
> Always simulate **both functional & timing GLS** before moving to physical design. 🛡️
</details>

---

## 🔧 Quick Checklist for Designers ✅🛠️

- [ ] No `#delay` or `initial` blocks in synthesizable code ⛔️  
- [ ] Every `if` has an `else` 📝  
- [ ] All combinational blocks have full sensitivity lists 🧐  
- [ ] Test **both RTL and synthesized netlist** ⚡️  
- [ ] Annotate timing with **SDF** for timing GLS ⏳  

---


# 🌟 Bad MUX Example (Common Pitfalls) 🧩💥

Sometimes, **small RTL mistakes** lead to **synthesis–simulation mismatches**.  
Here’s an example **2:1 MUX** with intentional issues to demonstrate common pitfalls. 🚨

## 🔹 Problematic Code

```verilog
module bad_mux (
  input i0, 
  input i1, 
  input sel, 
  output reg y
);
  always @ (sel) begin
    if (sel)
      y <= i1;
    else 
      y <= i0;
  end
endmodule
```

<details> <summary>❗ Issues in this Code (click to expand)</summary>

  1. Incomplete sensitivity list – always @(sel) ignores i0 and i1, which may cause mismatches in simulation. ⚡️

  2. Non-blocking assignment in combinational logic – Using <= in combinational blocks is not recommended; should use blocking assignment =. 🔀

</details>

## ✅ Corrected Version of MUX 🔧

```verilog
always @ (*) begin
  if (sel)
    y = i1;
  else
    y = i0;
end
```
## Waveform of RTL Code Simulation of Bad Mux :

- This shows the **behavior of the original RTL MUX**.  
- Output `y` is computed based on **ideal combinational logic**.  
- No real gate delays are considered here. ⚡️  

**Observations:**  
- Logic appears correct in all test cases. ✅  
- Immediate update of output based on `sel` input.  
- Helps verify functional correctness of RTL before synthesis.
  
![bad_mux](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/bad_mux_wave.png)

---

## Netlist Code Generated for Bad Mux :

- This waveform shows **post-synthesis behavior** of the Bad MUX.  
- Realistic **gate delays** from synthesis tools are included (SDF annotated). ⏱️  
- Output `y` may **not match the RTL simulation** due to issues like:  
  - Missing sensitivity list 🕵️‍♂️  
  - Wrong blocking vs non-blocking assignment 🔄  

### **Observations:**  

- Timing differences may appear in waveform. ⚠️  
- Some outputs may lag or be incorrect in edge cases.  
- Highlights **why synthesis-simulation mismatch occurs**.
  
![bad_mux](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/bad_mux_net_code.png)

---

## Netlist Simulation of Bad Mux :

Perform GLS on the `bad_mux`.  
Expect simulation mismatches or warnings due to above issues.

![bad_mux](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/bad_mux_net_wave.png)

---

### **Note:** 🔀 There is a difference between the **RTL simulation** and the **gate-level netlist simulation** due to synthesis-Simulation Mismatch issues.

---

# ⚡️ Blocking vs. Non-Blocking Assignments in Verilog 🛠️🔄

Verilog offers **two types of procedural assignments** that behave differently depending on **combinational vs sequential logic**. ⚡️

---

## 3.1 Blocking Statements (`=`) 📝

- **Syntax:** `=`  
- **Execution:** Sequential, executes **immediately** ⏩  
- **Suitable for:** **Combinational logic** (`always @(*)`)
  
### 🔹**Example:**  

```verilog
always @(*) 
  y = a & b;
```

## 3.2 Non-Blocking Statements (`<=`) ⏱️

- **Syntax:** `<=`  
- **Execution:** Scheduled, executes **concurrently** at the end of the time step 🔄  
- **Suitable for:** **Sequential logic** (`always @(posedge clk)`) 🛠️
  
### 🔹**Example:**  

```verilog
always @(posedge clk) 
  q <= d;
```

---

## 3.3 Comparison Table 🆚⚡️

| **Blocking (`=`)** 📝                        | **Non-Blocking (`<=`)** ⏱️                 |
|---------------------------------------------|--------------------------------------------|
| Uses `=` operator                           | Uses `<=` operator                         |
| Sequential, **immediate execution** ⏩       | Concurrent, **scheduled at end of timestep** 🔄 |
| Updates happen instantly in code order ⚡️   | Updates applied after time step ⏳          |
| For **combinational logic**, temp variables 🔹 | For **sequential logic**, registers/flip-flops 🛡️ |
| Infers **combinational logic (gates)** 🧩    | Infers **sequential logic (flip-flops)** 🔧 |

> 💡 **Pro Tip:** Choosing the correct assignment type prevents **simulation vs synthesis mismatches** and ensures correct hardware behavior! 💥

---


# 🛠️ Lab : Blocking Assignment Caveat 🛠️

Sometimes, **blocking assignments (`=`)** can produce unexpected results if the **order of assignments** is not carefully handled. 🧩  

## 🔹 Problematic Code
```verilog
module blocking_caveat (
  input a, 
  input b, 
  input c, 
  output reg d
);
  reg x;
  always @ (*) begin
    d = x & c;
    x = a | b;
  end
endmodule
```

## What’s wrong ❓

- The order of assignments causes `d` to use the old value of `x`—not the newly computed value.
- **Best Practice:** Assign intermediate variables before using them.

## **Corrected order:**

```verilog
always @ (*) begin
  x = a | b;
  d = x & c;
end
```

![blocking](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/blocking_wave.png)

---

## Synthesis of the Blocking Caveat Module

Synthesize the corrected version of the module and observe the results.

![blocking](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/blocking_net.png)

---

## GLS Synthesis on the Netlist of Blocking Caveat Module

```shell
iverilog /path/to/primitives.v /path/to/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
```

![blocking](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_4/Images/blocking_net_wave.png)

---


# 📌 Day 4 Summary: Gate-Level Simulation & Verilog Assignments 🛠️🧩

Here’s a **quick recap** of what we learned today:  

- **🖥️ Gate-Level Simulation (GLS):**  
  Validates **post-synthesis netlist** for:  
  ✅ Functional correctness  
  ⏱️ Timing behavior  
  🧩 Testability (scan chains, DFT)  

- **🔀 Synthesis vs Simulation Mismatch:**  
  Occurs when **RTL sim ≠ Netlist sim** due to:  
  🕵️‍♂️ Missing sensitivity lists  
  🔄 Blocking vs Non-Blocking assignment issues  
  ❌ Non-standard/ambiguous Verilog  

- **📝 Blocking vs Non-Blocking Assignments:**  
  `=` → Blocking, **combinational logic** ⚡️  
  `<=` → Non-blocking, **sequential logic** ⏱️  

- **🛠️ Labs Covered:**  
  1️⃣ **Bad MUX Demo:** Shows S-S mismatch ⚡  
  2️⃣ **Corrected MUX:** Proper sensitivity & assignments ✅  
  3️⃣ **Blocking Assignment Caveat:** Correct order for reliable results 🔧  

- **🔍 Simulation Observations:**  
  - RTL waveform 🖥️ → ideal, immediate output  
  - Netlist waveform 🔧 → realistic delays, may mismatch ⚠️  

> 💡 **Key Takeaway:** Correct **RTL coding + assignment usage + GLS** ensures your hardware behaves as intended 🛡️💥  

---

# 🏁 Conclusion

Today’s session focused on **Gate-Level Simulation, RTL coding practices, and synthesis verification**.  

- ✅ **GLS** ensures your **post-synthesis netlist** works as intended.  
- 🔀 Understanding **synthesis vs simulation mismatches** helps catch subtle RTL errors early.  
- 📝 **Blocking vs Non-Blocking assignments** are crucial for **combinational and sequential logic**.  
- 🛠️ Labs demonstrated **common pitfalls** (Bad MUX, Blocking caveats) and how to **correct them**.  

> 💡 **Takeaway:** Careful RTL design, correct assignment usage, and thorough GLS **prevent hardware bugs and mismatches**, saving time during physical design and tape-out. 🛡️💥  

---

# 📚 References

1. **M. Mano, "Digital Design," 6th Edition, Pearson.**  
2. **R. Brown, "FPGA Prototyping By Verilog Examples," 1st Edition, Wiley.**  
3. **S. Palnitkar, "Verilog HDL: A Guide to Digital Design and Synthesis," 2nd Edition, Prentice Hall.**  
4. **ASIC World Tutorials:** [https://www.asic-world.com/verilog/index.html](https://www.asic-world.com/verilog/index.html)  
5. **Xilinx Documentation – Verilog Coding Guidelines:** [https://www.xilinx.com/support/documentation](https://www.xilinx.com/support/documentation)  
6. **Yosys Open-Source Synthesis Manual:** [http://www.clifford.at/yosys/](http://www.clifford.at/yosys/)  

---














