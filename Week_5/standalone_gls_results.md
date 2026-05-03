# Gate-Level Simulation (GLS) for Full Block Verification

## PHASE 3 — Run GLS for Standalone Tests

### Execution results:

#### 1️⃣ gpio_mgmt - Passed

![gpio_mgmt result](Screenshots/gpio_mgmt_result.png)

#### 2️⃣ mem - Passed

![mem result](Screenshots/mem_result.png)

#### 3️⃣ uart - Passed

![uart result](Screenshots/uart_result.png)

#### 4️⃣ timer - Failed

![timer result](Screenshots/timer_result.png)

#### 5️⃣ irq - Failed

![irq result](Screenshots/irq_result.png)

#### 6️⃣ debug - Failed

![debug result](Screenshots/debug_result.png)

#### 7️⃣ spi_master - Passed

![spi_master result](Screenshots/spi_master_result.png)

### Standalone GLS Result Table 

| Test | RTL Status(Week-3)| GLS Status|
| -------- | -------- | --------|
| gpio_mgmt	| PASS	| PASS |
| mem	| PASS | PASS |
| uart	| PASS | PASS |
| timer	| FAIL | FAIL |
| irq	| FAIL | FAIL |
| debug	| FAIL | FAIL |
| spi_master	| PASS | PASS |

### Inference
GLS verification results successfully align with the previously established RTL verification outcomes.