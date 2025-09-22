# 🚀 RTL Design And Synthesis Workshop Using Sky130

![Status](https://img.shields.io/badge/Status-Active-brightgreen)
![Contributions](https://img.shields.io/badge/Contributions-Welcome-blue)

> Hands-on learning series on **Verilog RTL Design, Simulation, Synthesis, and Optimization**  
> Using open-source SKY130 PDK and Icarus Verilog / GTKWave tools.

---

## 📌 Table of Contents

- [About This Workshop](#about-this-workshop)
- [Prerequisites](#prerequisites)
- [Workshop Structure](#workshop-structure)
- [Progress Tracker](#progress-tracker)
- [Design Flow](#design-flow)
- [Learning Outcomes](#learning-outcomes)
- [Author & Mentor](#author--mentor)
- [License](#license)

---

## About This Workshop

This workshop is intended for students, hobbyists, and engineers who want to learn about:

- Verilog RTL design and simulation  
- Using Icarus Verilog and GTKWave for waveform analysis  
- Logic synthesis using **Yosys** and the **SKY130 open-source PDK**  
- Key digital design concepts: testbenches, timing libraries, D flip-flop coding styles, and optimization  

> 💡 **Pro Tip:** Separate testbenches from RTL modules for clarity and reusability.  
> ⚠️ **Warning:** Avoid implicit latches to prevent synthesis issues.

---

## Prerequisites

- Basic understanding of digital logic (gates, flip-flops, multiplexers, etc.)  
- Familiarity with Linux shell commands  
- Linux environment (or WSL on Windows/macOS)  
- Tools: `git`, `iverilog`, `gtkwave`, `yosys`, text editor (VS Code recommended)

---

## Workshop Structure

The workshop is organized by day, each with its own folder and README:

| Day | Topic | Tools | Output |
|-----|-------|-------|--------|
| 📘 Day 1 | Verilog RTL Basics | `iverilog`, `gtkwave` | ✅ Waveform |
| ⚡ Day 2 | Timing Libraries & Flip-Flops | `yosys` | 📊 Netlist |
| 🧩 Day 3 | Combinational & Sequential Optimization | `yosys`, `abc` | 🔧 Optimized Circuit |
| 🔒 Day 4 | Gate-Level Simulation (GLS) | `iverilog`, `gtkwave` | 🛠 Verification |
| 🏁 Day 5 | Advanced Synthesis & Optimization | SKY130 | 🚀 Final Report |

> Each day’s README includes:
> - Step-by-step practical labs  
> - Code examples  
> - Screenshots or waveform images  
> - Tips & best practices

---

## Progress Tracker

- [x] Day 1 - Verilog RTL Design ✅  
- [x] Day 2 - Timing Libraries & Flip-Flops ✅  
- [ ] Day 3 - Combinational & Sequential Optimization ⏳  
- [ ] Day 4 - GLS & Synthesis-Simulation Mismatch ❌  
- [ ] Day 5 - Final Optimization 🏁

---

##  Design Flow

The RTL design workflow follows these steps:

1. **Verilog RTL Code** – Write your RTL modules.  
2. **Simulation with Icarus Verilog** – Verify functionality using testbenches.  
3. **Synthesis using Yosys** – Convert RTL into gate-level netlist.  
4. **Netlist Generation** – Produce the circuit representation for verification.  
5. **Gate-Level Simulation (GLS)** – Validate synthesized design.  
6. **Optimized Design** – Apply optimizations for area, power, and performance.

---

##  Learning Outcomes

By completing this workshop, participants will be able to:

- 🔹 Understand RTL coding practices and design methodology  
- 🔹 Simulate designs using **Icarus Verilog + GTKWave**  
- 🔹 Perform synthesis using **Yosys + SKY130 PDK**  
- 🔹 Debug synthesis-simulation mismatches  
- 🔹 Optimize designs for **power, performance, and area (PPA)**  

> 💡 **Pro Tip:** Always separate testbenches from design code for clarity.  

---

##  Author & Mentor

| Name | Role | Profile |
|------|------|---------|
| ✍️ Gowtham | Author | ![Author Badge](https://img.shields.io/badge/author-Gowtham-blue) |
| 🧑‍🏫 Kunal Ghosh | Mentor | [LinkedIn](https://www.linkedin.com/in/kunal-ghosh-vlsisystemdesign-com-28084836/) |

---

##  License

This project is licensed under the **Attribution 4.0 International (CC BY 4.0)** License.  


