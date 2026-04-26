# RTL-to-GDS Implementation of User Project Wrapper

## PHASE 1 — Analyze the Top-Level Wrapper

The “https://github.com/vsdip/vsdsquadron-soc/blob/add-vsdsquadron-soc-folders/caravel/verilog/rtl/__user_project_wrapper.v” file is used for this week. 

### About __user_project_wrapper.v:
- The user_project_wrapper is not standalone and instantiates multiple lower-level modules. 
- **Dependency tree of the wrapper:**
  + user_project_wrapper instantiates 3 lower level modules.
  + The following are the three modules instantiated in the user_project_wrapper:
    * user_project_la_example
    * user_project_gpio_example
    * debug_regs
- **List of all RTL files used in the design:**
  + __user_project_wrapper.v
  + __user_project_la_example.v
  + __user_project_gpio_example.v
  + debug_regs.v
- **Explanation of the module hierarchy:**
  + The user_project_wrapper is the main module used in this design
  + This module instantiates 3 other modules. The 3 modules include user_project_la_example, user_project_gpio_example and debug_regs
  + user_project_la_example is instantiated as **"la_testing"**, user_project_gpio_example is instantiated as **"gpio_testing"** and debug_regs is instantiated as **"debug"**
  + Both user_project_la_example and user_project_gpio_example modules will be instantiated only if **LA_TESTING** and **GPIO_TESTING** are included because both the modules are instantiated inside the **`ifdef** directive
  + But debug_regs will be instantiated always as it is not included inside the `ifdef directive

--- 
## PHASE 2 — Prepare the ORFS Design Environment

The ORFS design environment was set-up to work with the user_project_wrapper. For this, a new directory is created with the name "user_project_wrapper". The config.mk and constraint.sdc files are kept under the Week_4/orfs/flow/designs/sky130hd/user_project_wrapper folder. All the verilog files which includes the __user_project_wrapper.v and the other lower level modules (__user_project_la_example.v, __user_project_gpio_example.v and debug_regs.v) instantiated in the user_project_wrapper are kept under the Week_4/orfs/flow/designs/src/user_project_wrapper/rtl folder. The defs.v is also included in the same folder.

#### Directory Created:
![Directory](Screenshots/Directory.png)
#### Config file used:
![Config file](Screenshots/Config_file.png)
#### Integration of RTL files into the flow:
The VERILOG_FILES variable used in the config.mk file includes all the verilog files available in the rtl folder. 
Both the modules(user_project_la_example, user_project_gpio_example) are instantiated inside the **`ifdef** directive, so in order to include these modules **GPI0_TESTING** and **LA_TESTING** are set to **1** in the defs.v file whereas the debug_regs will be instantiated always.
![defs.v](Screenshots/defs_file.png)

---
## PHASE 3 — Apply 100 MHz Clock Constraint

#### Constraint file used:
A 100 MHz clock corresponds to a 10 ns clock period. So, here the period is set to 10.0 ns.
![Constraint file](Screenshots/constraint.png)
#### Identification of the clock port:
The clock port used in the user_project_wrapper is **wb_clk_i**, which is denoted in the below image.
![Clock port in user_project_wrapper](Screenshots/clk_port_1.png)
The below image denotes the usage of the clock port in the lower level modules
![Clock port in lower level modules](Screenshots/clk_port_2.png)
#### Recognization of the constraint in the flow:
Once synthesis was done using the same constraint for this project, a file named **"clock period.txt"** was generated under the results folder. This file contains a single value denoting the clock period set for this flow. Here, the file contains the value **"10.0"**, which provides the confirmation that the constraint was recognized during the flow.
![Clock Period.txt](Screenshots/clk_port_confirmation.png)

---
## PHASE 4 — Run the RTL-to-GDS Flow

The full OpenROAD flow includes Synthesis, Floorplanning, Placement, Clock Tree Synthesis, Routing, Fill Insertion, Final database generation and Final GDS generation stages. All the stages are executed successfully for the user_project_wrapper project.

#### 1️⃣ Synthesis:
The below images denote the report generated post synthesis
![Synthesis report_1](Screenshots/Synthesis_report_1.png)
![Synthesis report_2](Screenshots/Synthesis_report_2.png)

#### 2️⃣ Floorplan:
The below images represent the successful execution of floorplan for the user_project_wrapper
![Floorplan execution start](Screenshots/Floorplan_execution_start.png)
![Floorplan execution end ](Screenshots/Floorplan_execution_end.png)

#### 3️⃣ Placement:
The below images represent the successful execution of placement for the user_project_wrapper
![Placement execution start](Screenshots/Placement_execution_start.png)
![Placement execution end](Screenshots/Placement_execution_end.png)

#### 4️⃣ Clock Tree Synthesis:
The below images represent the successful execution of CTS for the user_project_wrapper
![CTS execution start](Screenshots/CTS_execution_start.png)
![CTS execution end](Screenshots/CTS_execution_end.png)

#### 5️⃣ Routing:
The below images represent the successful execution of routing for the user_project_wrapper
![Routing execution start](Screenshots/Routing_execution_start.png)
![Routing execution end](Screenshots/Routing_execution_end.png)

#### 6️⃣ Fill insertion:
**"Fill insertion"** is triggered automatically when the **"make finish"** command was given.
![Fill insertion execution](Screenshots/Fill_insertion.png)
The files generated post Fill insertion under the logs folder are denoted in the below image.
![Fill insertion logs](Screenshots/Fill_insertion_logs.png)
The results generated post Fill insertion under the results folder are denoted in the below image.
![Fill insertion results](Screenshots/Fill_insertion_results.png)

#### 7️⃣ Final GDS generation:
The below images represent the final GDS generated using the KLayout tool
![GDS 1](Screenshots/final_GDS.png)
![GDS 2](Screenshots/klayout.png)

#### 8️⃣ Final timing report:
The below images denote the timing report generated after the completion of the full OpenROAD flow for user_project_wrapper
![Timing report_1](Screenshots/Timing_report_1.png)
![Timing report_2](Screenshots/Timing_report_2.png)

---
## PHASE 5 — Generate Outputs for Gate-Level Verification Preparation

The key outputs generated in the flow are:
#### 1️⃣ Synthesized netlist:
- **Purpose** - Logic representation after synthesis
- **Stage where the output generated** - Post synthesis
- The below images represent the gate level verilog file generated post synthesis.
![Post synthesis 1](Screenshots/Post_synthesis_1.png)
![Post synthesis 2](Screenshots/Post_synthesis_2.png)

#### 2️⃣ Final netlist:
- **Purpose** - Netlist after physical implementation
- **Stage where the output generated** - Post final execution
- The below images represent the verilog structural netlist file generated post final execution.
![Final netlist 1](Screenshots/Final_netlist_1.png)
![Final netlist 2](Screenshots/Final_netlist_2.png)

#### 3️⃣ Routed database:
- **Purpose** - Physical design database
- **Stage where the output generated** - Post routing 
- The below image denotes the binary database file(.odb) generated post routing stage.
![Routed Database](Screenshots/Routed_Database.png)

#### 4️⃣ Final filled database:
- **Purpose** - Required for downstream verification
- **Stage where the output generated** - Post final execution
- The below image denotes the complete physical binary database file(.odb) generated post final execution.
![Physical Database](Screenshots/Physical_Database.png)

#### 5️⃣ GDSII:
- **Purpose** - Final layout
- **Stage where the output generated** - Post final execution
- The below images represent the final GDS generated post final execution
![GDS file](Screenshots/GDS_file.png)
![GDS 1](Screenshots/final_GDS.png)
![GDS 2](Screenshots/klayout.png)

#### 6️⃣ Timing report:
- **Purpose** - Setup and hold timing results
- **Stage where the output generated** - Post final execution
- The below images denote the final timing report generated post final execution
![Timing report_1](Screenshots/Timing_report_1.png)
![Timing setup and hold](Screenshots/Timing_report_setup_hold.png)
![Timing report_2](Screenshots/Timing_report_2.png)

---
## PHASE 6 — Debugging and Issue Resolution

**Issue :** "ERROR:Unimplemented compiler directive or undefined macro MPRJ IO PADS" while executing the command `make synth`
![Issue - 1](Screenshots/Issue_1.png)

**Resolving steps:** The following steps are followed to overcome the issue
- The SYNTH_DEFINES variable defined in the config.mk file is removed
![Config file issue](Screenshots/config_file_issue.png)
- A separate file named **"defs.v"** is created under the "rtl" folder.
![defs.v](Screenshots/defs_file.png)
![rtl files](Screenshots/rtl_files.png)
- A small change in the __user_project_wrapper.v file is added to include the defs.v file
![change in user_project_wrapper](Screenshots/change_in_user_project_wrapper.png)

**Result:** Synthesis step is executed successfully post adding the defs.v file under the rtl folder and including the same in the __user_project_wrapper.v file
![Synthesis 1](Screenshots/Synthesis_1.png)
![Synthesis 2](Screenshots/Synthesis_2.png)

--- 
