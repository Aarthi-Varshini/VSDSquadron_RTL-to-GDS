# Toolchain Mastery and ORFS Execution (Cloud to Local)

## PHASE 1 — ORFS Execution in GitHub Codespaces
### Task 1.1 — Repository Setup :

The “ https://github.com/vsdip/vsd-scl180-orfs” repository was forked and GitHub Codespace was launched. The devcontainer was build successfully.

![Successful devcontainer build](Screenshots/Successful_devcontainer_build.png)

![Tools and versions](Screenshots/Tools_and_versions.png)
---
### Task 1.2 — Run Sky130 Testcase in Cloud :

The execution of the provided design file in the repository was completed successfully by making a change in the make file. In the make file, DESIGN_CONFIG = ./designs/scl180fs120/gcd/config.mk was commented and DESIGN_CONFIG = ./designs/sky130hd/gcd/config.mk was uncommented, as a result DESIGN_CONFIG = ./designs/sky130hd/gcd/config.mk ran successfully.

![Changes in makefile](Screenshots/Changes_in_makefile.png)

The total runtime for this file is **2 mins 51 seconds**. The following image denotes the total runtime and the flow execution.

![Total runtime](Screenshots/Total_runtime.png)

#### 1️⃣ Synthesis:
The below images denote the cell count and chip area post synthesis

![Post synthesis cell count](Screenshots/Post_synthesis_cell_count.png)
![Post synthesis chip area](Screenshots/Post_synthesis_chip_area.png)

#### 2️⃣ Floorplan:
The below images represent the log snippet of the floorplan

![Floorplan log snippet](Screenshots/Floorplan_log_snippet_1.png)
![Floorplan log snippet](Screenshots/Floorplan_log_snippet_2.png)

#### 3️⃣ Placement:
The below images represent the reports generated post placement
##### Global placement:
![Global placement](Screenshots/global_placement_1.png)
![Global placement](Screenshots/global_placement_2.png)

##### Detailed placement:
![Detailed placement](Screenshots/detailed_placement_1.png)
![Detailed placement](Screenshots/detailed_placement_2.png)

##### Resizer placement:
![Resizer placement](Screenshots/resizer_placement_1.png)
![Resizer placement](Screenshots/resizer_placement_2.png)

#### 4️⃣ CTS:
The below images represent the log snippet of the CTS

![CTS log snippet](Screenshots/CTS_log_snippet_1.png)
![CTS log snippet](Screenshots/CTS_log_snippet_2.png)

#### 5️⃣ Routing:
The below images represent the report generated post routing

![Routing](Screenshots/routing_1.png)
![Routing](Screenshots/routing_2.png)

#### 6️⃣ Final GDS generation:
The below images represent the GDS generated using the KLayout tool

![GDS](Screenshots/GDS_command.png)
![GDS](Screenshots/GDS_generation.png)

#### 7️⃣ Final timing report:
The below image displays the TNS and WNS values of this design

![Timing_report](Screenshots/Timing_report.png)
---
## PHASE 2 — Toolchain Understanding (Devcontainer Deep Dive)

### Task 2.1 — Toolchain Mapping :
| S.No | Tool | Installed from | Purpose in Flow | Stage Used |
| :--- | :--- | :--- | :--- | :--- |
| 1 | OpenROAD | https://vsd-labs.sgp1.cdn.digitaloceanspaces.com/vsd-labs/openroad-linux-x64.tar.gz | Automated physical design implementation | Automated PnR |
| 2 | Yosys | https://github.com/YosysHQ/oss-cad-suite-build/releases/download/2025-10-31/oss-cad-suite-linux-x64-20251031.tgz | Logical Equivalence Check(LEC) | Synthesis |
| 3 | TritonCTS | https://vsd-labs.sgp1.cdn.digitaloceanspaces.com/vsd-labs/openroad-linux-x64.tar.gz | Distribute the clock signal | CTS |
| 4 | FastRoute | https://vsd-labs.sgp1.cdn.digitaloceanspaces.com/vsd-labs/openroad-linux-x64.tar.gz| Plan the paths for all signal wires to avoid congestion | Routing |
| 5 | OpenSTA | https://vsd-labs.sgp1.cdn.digitaloceanspaces.com/vsd-labs/openroad-linux-x64.tar.gz| Static Timing Analysis(STA) | In all stages for verification |
| 6 | KLayout | https://www.klayout.org/downloads/Ubuntu-22/klayout_0.29.0-1_amd64.deb| GDSII Viewing & Editing | GDS |
| 7 | Python | Ubuntu (APT) | Automation & Scripting | All Stages |
| 8 | Make | Ubuntu (APT) | Automation of build steps | All Stages |
| 9 | Git | Ubuntu (APT) | Version Control | All Stages |

---
### Task 2.2 – Flow Architecture Explanation:

ORFS automates the entire RTL-to-GDS. It includes synthesis, floorplan, placement, clock tree synthesis, routing, PDN and GDS stages using OpenROAD tools. For the flow to execute, changes are made in the Makefiles. It orchestrate the flow by defining the targets tracking the dependencies. It ensures that the stages are executed in the correct order. The synthesis ends when the RTL is converted into a gate level netlist mapped to a specific technology library. Once synthesis ends, the physical design begins. Here, the netlist is imported into the OpenROAD and it starts the execution of physical implementation from floorplan proceeding to placement and routing. Timing is checked using STA in all stages of the flow such as post-synthesis, post-placement, post-CTS and post-routing. OpenSTA is used to verify Setup and Hold timing constraints. Once the physical design stage completed, the GDS generated. KLayout tool is used for viewing or editing the generated GDS file. It represents the final layout which is sent for fabrication.

--- 
## PHASE 3 — Local Installation (Self-Owned Environment)
### Task 3.1 — Install ORFS Locally :

ORFS was installed locally by cloning the “ https://github.com/vsdip/vsd-scl180-orfs” repository

![Local Terminal](Screenshots/Indication_of_local_terminal.png)
---
### Task 3.2 – Install official OpenROAD:
“https://openroad.readthedocs.io/en/latest/user/Build.html# ” documentation is used for installing the official OpenROAD 

#### 1️⃣ Cloning the repository:
![Cloning openroad repository](Screenshots/Cloning_openroad_repository.png)

#### 2️⃣ Installing dependencies:
![Dependency Installation](Screenshots/Dependency_Installation_1.png)
![Dependency Installation](Screenshots/Dependency_Installation_2.png)

#### 3️⃣ Building

##### While compiling faced the below error:
```
Building CXX object CMakeFiles/cmTC_9f093.dir/src.cxx.o
/usr/bin/g++ -DHAVE_CXX_STD_FORMAT  -std=c++20 -std=c++20 -o CMakeFiles/cmTC_9f093.dir/src.cxx.o -c /home/aarthi/RTL_GDS/OpenROAD/build/CMakeFiles/CMakeTmp/src.cxx
/home/aarthi/RTL_GDS/OpenROAD/build/CMakeFiles/CMakeTmp/src.cxx:2:10: fatal error: format: No such file or directory
    2 | #include <format>
      |          ^~~~~~~~
compilation terminated.
gmake[1]: *** [CMakeFiles/cmTC_9f093.dir/build.make:78: CMakeFiles/cmTC_9f093.dir/src.cxx.o] Error 1
```

The error occurred while compiling latest openROAD source in ubuntu 22.04 with g++ version 11.
The compilation was successful when using g++ version 13 (installed seperately).

![Build](Screenshots/Build_1.png)
![Build](Screenshots/Build_2.png)

#### Version output:
![Openroad local version](Screenshots/Openroad_local_version.png)
---
## PHASE 4 — Re-Run RTL-to-GDS Locally

As mentioned while executing the file in cloud, the same changes are done in the makefile.

![Local makefile](Screenshots/Local_makefile.png)

The total runtime for this file is **4 mins 15 seconds**. The following image denotes the total runtime and the flow execution.

![Local Total runtime](Screenshots/Local_Total_runtime.png)

#### 1️⃣ Synthesis:
The below images denotes the cell count and chip area post synthesis

![Local Post synthesis cell count](Screenshots/Local_Post_synthesis_cell_count.png)
![Local Post synthesis chip area](Screenshots/Local_Post_synthesis_chip_area.png)

#### 2️⃣ Floorplan:
The below images represent the log snippet of the floorplan

![Local Floorplan log snippet](Screenshots/Local_Floorplan_log_snippet_1.png)
![Local Floorplan log snippet](Screenshots/Local_Floorplan_log_snippet_2.png)

#### 3️⃣ Placement:
The below images represent the reports generated post placement
##### Global placement:
![Local Global placement](Screenshots/Local_global_placement_1.png)
![Local Global placement](Screenshots/Local_global_placement_2.png)

##### Detailed placement:
![Local Detailed placement](Screenshots/Local_detailed_placement_1.png)
![Local Detailed placement](Screenshots/Local_detailed_placement_2.png)

##### Resizer placement:
![Local Resizer placement](Screenshots/Local_resizer_placement_1.png)
![Local Resizer placement](Screenshots/Local_resizer_placement_2.png)

#### 4️⃣ CTS:
The below images represent the log snippet of the CTS

![Local CTS log snippet](Screenshots/Local_CTS_log_snippet_1.png)
![Local CTS log snippet](Screenshots/Local_CTS_log_snippet_2.png)

#### 5️⃣ Routing:
The below images represent the report generated post routing

![Local Routing](Screenshots/Local_routing_1.png)
![Local Routing](Screenshots/Local_routing_2.png)

#### 6️⃣ Final GDS generation:
The below image represents the GDS generated using the KLayout tool

![Local GDS](Screenshots/Local_GDS_generation.png)

#### 7️⃣ Final timing report:
The below image displays the TNS and WNS values of this design

![Local Timing report](Screenshots/Local_Timing_report.png)

#### Comparsion between cloud and local execution:
| Metric | Cloud| Local |
| -------- | -------- | -------- |
| Runtime	| 2 mins 51 seconds	| 4 mins 15 seconds| 
| WNS	| -2.19	| -2.25|
| TNS	|-92.21	|-99.05|
| GDS Generated	|Yes	|Yes|

Able to notice a minor difference in the metrics 

---
## PHASE 5 — Debugging and Unix Literacy

#### Navigating to directories using "cd" command 
![navigating directories](Screenshots/navigating_directories.png)

#### Inspecting Makefiles
![Changes in makefile](Screenshots/Changes_in_makefile.png)
![Local makefile](Screenshots/Local_makefile.png)

#### Searching logs 
![Searching logs](Screenshots/Searching_logs_1.png)

#### Filtering timing violations using "grep" command
![grep command](Screenshots/grep_command.png)
--- 

