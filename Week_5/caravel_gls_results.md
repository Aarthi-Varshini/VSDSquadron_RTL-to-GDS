# Gate-Level Simulation (GLS) for Full Block Verification

## PHASE 4 — Run GLS for Caravel Integrated Tests

### Execution results:

#### 1️⃣ mem - Passed

![mem caravel result](Screenshots/mem_result_c.png)

#### 2️⃣ pass_thru_fix - Passed

![pass_thru_fix result](Screenshots/pass_thru_fix_result.png)

#### 3️⃣ hkspi_power - Passed

![hkspi_power result](Screenshots/hkspi_power_result.png)

#### 4️⃣ hkspi - Passed

![hkspi result](Screenshots/hkspi_result.png)

#### 5️⃣ sysctrl - Failed

![sysctrl result](Screenshots/sysctrl_result.png)

#### 6️⃣ pll - Failed

![pll result](Screenshots/pll_result.png)

#### 7️⃣ pullupdown - Failed

![pullupdown result](Screenshots/pullupdown_result.png)

#### 8️⃣ uart - Failed

![uart caravel result](Screenshots/uart_result_c.png)

#### 9️⃣ sram_exec - Failed

![sram_exec result](Screenshots/sram_exec_result.png)

#### 🔟 spi_master - Failed

![spi_master caravel result](Screenshots/spi_master_result_c.png)

#### 1️⃣1️⃣ gpio_mgmt - Failed

![gpio_mgmt caravel result](Screenshots/gpio_mgmt_result_c.png)

#### 1️⃣2️⃣ user_pass_thru - Execution got stuck

![user_pass_thru result](Screenshots/user_pass_thru_result.png)

### Caravel GLS Result Table 

| Test | RTL Status(Week-3)| GLS Status|
| -------- | -------- | -------- |
| user_pass_thru | PASS | FAIL |
| uart	| PASS | FAIL |
| sysctrl | FAIL | FAIL |
| sram_exec	| PASS | FAIL |
| spi_master	| PASS | FAIL |
| pullupdown	| PASS | FAIL |
| pll	| FAIL | FAIL |
| pass_thru_fix	| PASS | PASS |
| mem	| PASS | PASS |
| hkspi_power	| PASS |PASS |
| gpio_mgmt	| PASS	| FAIL |
| hkspi	| PASS | PASS |

### Inference:
The Gate-Level Simulation (GLS) verification results demonstrate only a 50% correlation with the initial RTL verification outcomes.