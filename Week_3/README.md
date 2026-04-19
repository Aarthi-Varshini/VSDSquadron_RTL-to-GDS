# Block-Level Verification of VSDSquadron SoC

## PHASE 1 — Standalone Block Verification 

The “https://github.com/vsdip/vsdsquadron-soc" repository was cloned and navigated to the standalone verification tests directory("tests-standalone")

![Cloning and Navigation to standalone](Screenshots/Cloning_Navigation_to_standalone.png)

### Task 1 — Run SPI Master Test :

Navigated to "spi_master" and executed the "make" command. Post executing the "make" command, faced the below errors.

![Error 1](Screenshots/error_1.png)
![Error 2](Screenshots/error_2.png)
![Error 3](Screenshots/error_3.png)

The errors were overcomed by following the below steps:

**Step 1:** "gcc-riscv64-unknown-elf" was installed
![Installation](Screenshots/Installation.png)
**Step 2:** Changes made in the Makefile
![Changes in Makefile](Screenshots/changes_makefile.png)
**Step 3:** The "sky130_sram_2kbyte_1rw1r_32x512_8.v" file's location was changed from /home/aarthi/RTL_GDS/Week_3/vsdsquadron-soc/caravel_mgmt_soc_litex/verilog/cvc-pdk/sky130_sram_2kbyte_1rw1r_32x512_8.v to /home/aarthi/RTL_GDS/Week_3/vsdsquadron-soc/caravel_mgmt_soc_litex/verilog/dv/vip/sky130_sram_2kbyte_1rw1r_32x512_8.v

After making the above changes, spi_master executed properly
![spi_master execution](Screenshots/spi_master_execution.png)

---

### Task 2 — Understand the Verification Flow :

1. What commands are executed when **"make"** is invoked?

    When "make" command was invoked, the Makefile will be triggered, which in turn triggers the “all” command . This command requires “.vcd” file to execute which requires a ".vvp" file(which will be available post the simulation) . So, the “C code” will be compiled to get a RISC-V executable, which in turn will be converted to a ".hex" file. 

2. How the simulation environment is created?

    Environment setup is done using environmental variables. For the standalone tests, the Config variable is set to standalone[ **CONFIG = standalone**]. The CPU, PDK and project paths were set-up

3. How Verilog sources are compiled?

    The .hex file along with the other Verilog files will be compiled using **“iverilog”**. The other verilog files include the testbench(“test_name_tb.v”) and the files from include.rtl.standalone. Post compilation a ".vvp" file will be generated

4. How the simulator is invoked?

    The simulator will be invoked via the “vvp” command. The generated ".vvp file" will be simulated which in turn generates a ".vcd" file. The ".vcd" file records every "flip" of a signal for later viewing.

5. How pass/fail status is determined?

    The test status is determined based on the logic present in the testbench file.

## Verification flow for "spi_master" test
![spi_master block diagram](Diagrams/spi_master_blockdiagram.png)

---

## PHASE 2 — Run ALL Standalone Tests

Tests-Standalone block contains GPIO Mgmt, mem, uart, timer, irq, debug and spi_master tests. 
![Standalone tests](Screenshots/Standalonetests.png)
These tests are executed by repeating the below steps for all the tests in the block

**Execution Steps:**

**Step 1:** Navigate to the test directory using the command `cd test_name`

**Step 2:** Do the changes in the Makefile

**Step 3:** Execute these commands sequentially
`make clean`
`make` 

**Step 4:** Observe the result

### Execution of Standalone Tests
**1. gpio_mgmt** 

Changes made in makefile:
![Changes in Makefile gpio_mgmt](Screenshots/changes_makefile_gpio_mgmt.png)

Execution:
![Execution gpio_mgmt](Screenshots/gpio_mgmt_execution.png)

## Verification flow for "gpio_mgmt" test
![gpio_mgmt block diagram](Diagrams/gpio_mgmt_blockdiagram.png)

**2. mem** 

Changes made in makefile:
![Changes in Makefile mem](Screenshots/changes_makefile_mem.png)

Execution:
![Execution mem](Screenshots/mem_execution.png)

## Verification flow for "mem" test
![mem block diagram](Diagrams/mem_blockdiagram.png)

**3. uart**

Changes made in makefile:
![Changes in Makefile uart](Screenshots/changes_makefile_uart.png)

Execution:
![Execution uart](Screenshots/uart_execution.png)

## Verification flow for "uart" test
![uart block diagram](Diagrams/uart_blockdiagram.png)

**4. timer**

Changes made in makefile:
![Changes in Makefile timer](Screenshots/changes_makefile_timer.png)

Execution:
![Execution timer](Screenshots/timer_execution.png)

## Verification flow for "timer" test
![timer block diagram](Diagrams/timer_blockdiagram.png)

**5. irq**

Changes made in makefile:
![Changes in Makefile irq](Screenshots/changes_makefile_irq.png)

Execution:
![Execution irq](Screenshots/irq_execution.png)

## Verification flow for "irq" test
![irq block diagram](Diagrams/irq_blockdiagram.png)

**6. debug**

Changes made in makefile:
![Changes in Makefile debug](Screenshots/changes_makefile_debug.png)

Execution:
![Execution debug](Screenshots/debug_execution.png)

## Verification flow for "debug" test
![debug block diagram](Diagrams/debug_blockdiagram.png)

---

## PHASE 3 — Caravel Integrated Tests 

Navigated to the caravel tests directory("tests-caravel")

![Navigation to caravel](Screenshots/Navigation_to_caravel.png)

To setup the caravel environment the "https://github.com/efabless/caravel_user_project" repository was cloned and `make setup` command was executed

### Task - Run All Caravel Tests :

These tests are executed by repeating the below steps for all the tests in the block

**Execution Steps:**

**Step 1:** Navigate to the test directory using the command `cd test_name`

**Step 2:** Do the changes in the Makefile

**Step 3:** Execute these commands sequentially
`make clean`
`make` 

**Step 4:** Observe the result

### Execution of Caravel Tests

**1. user_pass_thru** 

Changes made in makefile:
![Changes in Makefile user_pass_thru](Screenshots/changes_makefile_user_pass_thru.png)

Execution:
![Execution user_pass_thru](Screenshots/user_pass_thru_execution.png)

**2. uart** 

Changes made in makefile:
![Changes in Makefile uart caravel](Screenshots/changes_makefile_uart_c.png)

Execution:
![Execution uart caravel](Screenshots/uart_execution_c.png)

**3. sysctrl** 

Changes made in makefile:
![Changes in Makefile sysctrl](Screenshots/changes_makefile_sysctrl.png)

Execution:
![Execution sysctrl](Screenshots/sysctrl_execution.png)

**4. sram_exec** 

Changes made in makefile:
![Changes in Makefile sram_exec](Screenshots/changes_makefile_sram_exec.png)

Execution:
![Execution sram_exec](Screenshots/sram_exec_execution.png)

**5. spi_master** 

Changes made in makefile:
![Changes in Makefile spi_master caravel](Screenshots/changes_makefile_spi_master_c.png)

Execution:
![Execution spi_master caravel](Screenshots/spi_master_execution_c.png)

**6. pullupdown** 

Changes made in makefile:
![Changes in Makefile pullupdown](Screenshots/changes_makefile_pullupdown.png)

Execution:
![Execution pullupdown](Screenshots/pullupdown_execution.png)

**7. pll** 

Changes made in makefile:
![Changes in Makefile pll](Screenshots/changes_makefile_pll.png)

Execution:
![Execution pll](Screenshots/pll_execution.png)

**8. pass_thru_fix** 

Changes made in makefile:
![Changes in Makefile pass_thru_fix](Screenshots/changes_makefile_pass_thru_fix.png)

Execution:
![Execution pass_thru_fix](Screenshots/pass_thru_fix_execution.png)

**9. mem** 

Changes made in makefile:
![Changes in Makefile mem caravel](Screenshots/changes_makefile_mem_c.png)

Execution:
![Execution mem caravel](Screenshots/mem_execution_c.png)

**10. hkspi_power** 

Changes made in makefile:
![Changes in Makefile hkspi_power](Screenshots/changes_makefile_hkspi_power.png)

Execution:
![Execution hkspi_power](Screenshots/hkspi_power_execution.png)

**11. gpio_mgmt** 

Changes made in makefile:
![Changes in Makefile gpio_mgmt caravel](Screenshots/changes_makefile_gpio_mgmt_c.png)

Execution:
![Execution gpio_mgmt caravel](Screenshots/gpio_mgmt_execution_c.png)

**12. hkspi** 

Changes made in makefile:
![Changes in Makefile hkspi](Screenshots/changes_makefile_hkspi.png)

Execution:
![Execution hkspi](Screenshots/hkspi_execution.png)

---

## PHASE 4 — Verification Flow Understanding

1. What happens when **"make"** is executed?

    When "make" command was invoked, the Makefile will be triggered, which in turn triggers the “all” command . This command requires “.vcd” file to execute which requires a ".vvp" file(which will be available post the simulation) . So, the “C code” will be compiled to get a RISC-V executable, which in turn will be converted to a ".hex" file. 

2. How the Makefile invokes the simulator?

    The simulator will be invoked via the “vvp” command in the makefile. The generated ".vvp file" will be simulated which in turn generates a ".vcd" file. The ".vcd" file records every "flip" of a signal for later viewing.

3. What files are compiled?

    The .hex file along with the other Verilog files will be compiled using **“iverilog”**. The other verilog files include the testbench(“test_name_tb.v”) and the files from include.rtl.caravel. Post compilation a ".vvp" file will be generated

4. How the testbench interacts with the design?

    The testbench file contains the “caravel uut” which is the Design Under Test(DUT). 
    The testbench provides the power(VDD and GND), master clock it. Once the “caravel uut” line was faced by the compiler, the DUT will be instantiated. 

5. How pass/fail status is determined?

    The test status is determined based on the logic present in the testbench file.

## Verification flow for "user_pass_thru" test
![user_pass_thru caravel block diagram](Diagrams/user_pass_thru_blockdiagram_c.png)

## Verification flow for "uart" test
![uart caravel block diagram](Diagrams/uart_blockdiagram_c.png)

## Verification flow for "sysctrl" test
![sysctrl caravel block diagram](Diagrams/sysctrl_blockdiagram_c.png)

## Verification flow for "sram_exec" test
![sram_exec caravel block diagram](Diagrams/sram_exec_blockdiagram_c.png)

## Verification flow for "spi_master" test
![spi_master caravel block diagram](Diagrams/spi_master_blockdiagram_c.png)

## Verification flow for "pullupdown" test
![pullupdown caravel block diagram](Diagrams/pullupdown_blockdiagram_c.png)

## Verification flow for "pll" test
![pll caravel block diagram](Diagrams/pll_blockdiagram_c.png)

## Verification flow for "pass_thru_fix" test
![pass_thru_fix caravel block diagram](Diagrams/pass_thru_fix_blockdiagram_c.png)

## Verification flow for "mem" test
![mem caravel block diagram](Diagrams/mem_blockdiagram_c.png)

## Verification flow for "hkspi_power" test
![hkspi_power caravel block diagram](Diagrams/hkspi_power_blockdiagram_c.png)

## Verification flow for "gpio_mgmt" test
![gpio_mgmt caravel block diagram](Diagrams/gpio_mgmt_blockdiagram_c.png)

## Verification flow for "hkspi" test
![hkspi caravel block diagram](Diagrams/hkspi_blockdiagram_c.png)
---

## PHASE 5 — Documentation

The Week_3 folder contains the README.md, Standalone_results.md, Caravel_results.md, Diagrams folder and Screenshots folder

**1. README.md :**
This file contains the Execution steps of all the standalone and caravel tests. It also includes the Block diagrams and the explanation for the verification flow

**2. Standalone_results.md :**
This file contains the results and the result table of the standalone tests

**3. Caravel_results.md :**
This file contains the results and the result table of the caravel tests

**4. Diagrams folder :**
This folder contains the block diagrams of the all tests mentioned in the README.md file

**5. Screenshots folder :**
This folder contains all the images used in README.md, Standalone_results.md and Caravel_results.md files




