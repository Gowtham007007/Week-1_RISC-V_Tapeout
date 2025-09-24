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

<details>
<summary>📚 References</summary>

- [Synopsys: GLS Basics](https://www.synopsys.com/)  
- [ChipVerify: Gate-Level Simulation](https://www.chipverify.com/verilog/gate-level-simulation)  
- [VLSI Pro: GLS Flow](https://vlsipro.com/)  

</details>

---

👉 Next Section: [🔗 Add your next block here!](#)  

