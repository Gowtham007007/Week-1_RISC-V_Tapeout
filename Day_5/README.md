# 🏁 Day 5: Advanced Synthesis & Optimization

<div align="center">

![SKY130](https://img.shields.io/badge/PDK-SKY130-blue?style=for-the-badge&logo=opensourceinitiative)
![Yosys](https://img.shields.io/badge/Tool-Yosys-green?style=for-the-badge&logo=gnu)
![Icarus](https://img.shields.io/badge/Simulator-Icarus_Verilog-orange?style=for-the-badge)
![GTKWave](https://img.shields.io/badge/Waveform-GTKWave-lightgrey?style=for-the-badge)
![Final](https://img.shields.io/badge/Status-Final_Day-red?style=for-the-badge)

</div>

---

# 🎯 Block 1: Inferred Latches – Hidden Hazards in RTL Design

🎯 **Learning Objective**

Understand how incomplete conditional statements in Verilog can unintentionally create **inferred latches**, and learn best practices to avoid them.

🧩 **Key Focus Areas**

- ⚡ Proper use of if–else statements
- 🧮 Complete case statements
- ❗ Problems caused by missing assignments
- 🔧 Techniques to avoid latch inference

---

💡 **1. If – Else Statements in Verilog**

If – else statements control conditional execution inside procedural blocks such as **always**, **initial**, **tasks**, or **functions**.

Syntax example

if (condition) begin

// Code executes if condition is true

end else begin

// Code executes if condition is false

end

✨ Notes

- ✅ **condition**: Must evaluate to true (non-zero) or false (zero).
- ✅ **begin ... end**: Group multiple statements. Can be skipped for a single statement.
- 🟢 **else** is optional but recommended for clarity.

🔀 **Nested If–Else Example**

```verilog
if (condition1) begin

// Executes when condition1 is true

end else if (condition2) begin

// Executes when condition2 is true

end else begin

// Executes when neither condition is true

end
```

---

💡 **2. Inferred Latches**

⚠️ An **inferred latch** occurs when a variable inside a combinational always block is **not assigned in every possible path**.

This forces the synthesis tool to create storage (a latch) so that the signal holds its previous value—often **not intended** by the designer.

Example of a latch being inferred :

```verilog
module ex (

input wire a, b, sel,

output reg y

);

always @(a, b, sel) begin

if (sel == 1'b1)

y = a; // ❌ No 'else' → y is undefined when sel = 0

end

endmodule
```

Problem :

- When **sel** is 0, `y` is never updated.
- The tool infers a latch to preserve the old value of `y`.
- Latches can create **timing hazards** and **unpredictable behavior**.

---

✅ **Best Practices to Avoid Latch Inference**

1️⃣ **Provide a Default Assignment**

Assign a safe value to the variable at the start of the block.

2️⃣ **Always Use Else or Default in Case**

Cover all possibilities explicitly.

Corrected Example using case

```verilog
module ex (

input wire a, b, sel,

output reg y

);

always @(a, b, sel) begin

case (sel)

1'b1 : y = a;

default : y = 1'b0; // ✅ Ensures y is always assigned

endcase

end

endmodule
```

---

🚀 **Takeaway**

By ensuring every signal inside a combinational block is assigned in **all possible paths**, you eliminate unintended latches, improving design reliability and synthesis quality.


## 🎓 **Lab 1: Incomplete If Statement**

---

🔍 **Objective:**

Understand how incomplete `if` statements can lead to **inferred latches** and unpredictable behavior in RTL synthesis.

---

💻 **Module Example:**
```verilog
module incomp_if (input i0, input i1, input i2, output reg y);

always @(*) begin

if (i0)

y <= i1; // ❌ No else branch: y retains previous value when i0 == 0

end

endmodule
```

---

![If](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_5/Images/ifwave.png)

⚠️ **Observation:**

- When `i0` is `0`, the output `y` is **not assigned**, so the synthesis tool infers a latch to store its previous value.
- This can lead to **functional mismatches** and **timing hazards** in your design.
- Hence a D-Latch is Inferred

---
![If](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_5/Images/ifnet.png)


✅ **Best Practice:**

- Always include an `else` branch to cover all conditions.
- Alternatively, assign a **default value** at the beginning of the block:

```verilog
always @(*) begin
    y = 1'b0; // Default assignment
    if (i0)
        y <= i1;
end

```

## Nested Incomplete If : 
### Verilog Code :
![If2](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_5/Images/if2code.png)

### Waveform Generated on Simulation of the above RTL Code :
![If2](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_5/Images/if2wave.png)

---

⚠️ **Observation:**

- When `i0` is `1`, the output `y` is  assigned to `i1`, and  When `i2` is `1`, the output `y` is  assigned to `i3`so the synthesis tool infers a latch to store value when both are zero.
- This can lead to **functional mismatches** and **timing hazards** in your design.
- Hence a D-Latch is Inferred
- Hence the Netlist will be :

### Netlist Generated :
![If2](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_5/Images/if2net.png)
  


💡 **Pro Tip:**

Even in small combinational modules, **never leave branches incomplete**. This practice ensures RTL remains purely combinational and avoids inferred latches.





# 🎯 **Block 2: Problems in Case Statements – Incomplete and Wildcard Usage**

---

🔍 **Objective:**

Learn how incomplete or improperly used `case` statements in Verilog can lead to **inferred latches**, unpredictable behavior, and synthesis warnings.

---
💻 ** Problematic Module Example:**

```verilog
    module incomp_case(input i0 , input i1 , input i2 , input[1:0] sel , output reg y);
    always @(*) begin
        case(sel)
            2'b00 : y = i0;
            2'b01 : y = i1;
        endcase
    end
    endmodule
```
## Waveform Generated for the RTL Code Simulation :
![case](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_5/Images/casewave.png)

⚠️ Problem Description:

Only sel = 2'b00 and sel = 2'b01 are assigned values.

For sel = 2'b10 or 2'b11, y is not assigned, causing synthesis tools to infer a latch to hold the previous value.

This can lead to unintended memory behavior, functional mismatches, and timing hazards.

## Netlist Generated for the RTL Code :
![case](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_5/Images/casenet.png)


✅ Solution – Add a Default Case:
```verilog
always @(*) begin
    case(sel)
        2'b00: y = i0;
        2'b01: y = i1;
        2'b10: y = i2;
        2'b11: y = 1'b0;      // Explicit assignment
        default: y = 1'b0;    // Safe catch-all
    endcase
end
```


## 💻 ** Overlapping Problematic Module Example:**

```verilog
module bad_case (

input i0, input i1, input i2, input i3,

input [1:0] sel,

output reg y

);

always @(*) begin

case(sel)

2'b00: y = i0;

2'b01: y = i1;

2'b10: y = i2;

2'b1?: y = i3; // ❌ Wildcard usage; sel == 2'b11 is ambiguous

endcase

end

endmodule
```
### Waveform Generated on Simulation of the above RTL Code :
![If2](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_5/Images/badcasewave.png)

---

⚠️ **Observation:**

- Using a **wildcard (`?`)** can unintentionally leave **some input combinations uncovered**.
- For example, `2'b1?` covers `10` and `11`, but if not handled carefully, synthesis tools may still infer **latches** for other unassigned cases.
- Incomplete coverage in `case` statements is a **common source of unintended storage elements** in combinational logic.
- 

🖼 Demo Images:

Generated Netlist:
![Netlist](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_5/Images/badcasenet.png)

Netlist Simulation Result:
![Simulation](https://github.com/Gowtham007007/Week-1_RISC-V_Tapeout/blob/main/Day_5/Images/bcnwave.png)

⚠️ Observation: The simulation shows unexpected retention of previous values when the input does not match explicit cases. This confirms the latch inference issue.

✅ Solution – Complete Coverage:
```verilog

always @(*) begin
    case(sel)
        2'b00: y = i0;
        2'b01: y = i1;
        2'b10: y = i2;
        2'b11: y = i3;     // Explicitly assign all combinations
        default: y = 1'b0; // Safe catch-all
    endcase
end
```


💡 Best Practices:

Avoid ambiguous wildcards unless fully intentional.

Always include a default: case to handle all unmatched inputs.

Verify with simulation and synthesis reports to catch any inferred latches early.

✨ Pro Tip:

Covering all cases prevents glitches, ensures combinational behavior, and improves RTL reliability for downstream synthesis and layout.




