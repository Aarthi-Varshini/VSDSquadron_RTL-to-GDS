## PHASE 2 — RTL-to-GDS Implementation

A 100 MHz clock corresponds to a 10 ns clock period. So, here the period is set to 10.0 ns in the constraint.sdc file
![clock constraint](Implementation/clock_constraint.png)

#### 1️⃣ Synthesis:
The below images denote the report generated post synthesis
![Synthesis report_1](Implementation/Synthesis_report_1.png)
![Synthesis report_2](Implementation/Synthesis_report_2.png)

#### 2️⃣ Floorplan:
The below images represent the generated floorplan report
![Floorplan report_1](Implementation/Floorplan_report_1.png)
![Floorplan report_2](Implementation/Floorplan_report_2.png)

#### 3️⃣ Placement:
The below images represent the generated global placement report, detailed placement report and resizer placement report

**Global placement report:**
![Global Placement report](Implementation/Global_Placement_report.png)

**Detailed placement report:**
![Detailed Placement report](Implementation/Detailed_Placement_report.png)

**Resizer placement report:**
![Resizer Placement report](Implementation/Resizer_Placement_report.png)

#### 4️⃣ Clock Tree Synthesis:
The below images represent the log of CTS
![CTS log 1](Implementation/CTS_log_1.png)
![CTS log 2](Implementation/CTS_log_2.png)

#### 5️⃣ Routing:
The below images represent the successful execution of routing for the design_pll project
![Routing execution start](Implementation/Routing_execution_start.png)
![Routing execution end](Implementation/Routing_execution_end.png)

#### 6️⃣ Final GDS generation:
The below images represent the final GDS generated using the KLayout tool
![GDS 1](Implementation/final_GDS.png)
![GDS 2](Implementation/klayout.png)

---
## PHASE 3 — Generate Implementation Outputs
#### 1️⃣ Synthesized netlist:
- **Description** - Post-synthesis
- The below images represent the gate level verilog file generated post synthesis.
![Post synthesis 1](Implementation/Post_synthesis_1.png)
![Post synthesis 2](Implementation/Post_synthesis_2.png)

#### 2️⃣ Final netlist:
- **Description** - Post-routing
- The below images represent the verilog structural netlist file generated
![Final netlist 1](Implementation/Final_netlist_1.png)
![Final netlist 2](Implementation/Final_netlist_2.png)

#### 3️⃣ DEF/database:
- **Description** - Physical layout
- The below image denotes the DEF file generated post final execution
![DEF 1](Implementation/DEF_1.png)
![DEF 2](Implementation/DEF_2.png)

#### 4️⃣ Filled database:
- **Description** - For signoff readiness
- The below image denotes the complete physical binary database file(.odb)
![Physical Database](Implementation/Physical_Database.png)

#### 5️⃣ GDSII:
- **Description** - Final layout
- The below images represent the final GDS generated post final execution
![GDS file](Implementation/GDS_file.png)
![GDS 1](Implementation/final_GDS.png)
![GDS 2](Implementation/klayout.png)

#### 6️⃣ Timing report:
- **Description** - At target frequency
- The below images denote the final timing report generated post final execution
![Timing report_1](Implementation/Timing_report_1.png)
![Timing report_2](Implementation/Timing_report_2.png)

---
