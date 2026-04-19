# Block-Level Verification of VSDSquadron SoC

## Standalone Block Results

### spi_master - Passed

![spi_master result](Screenshots/spi_master_result.png)

### gpio_mgmt - Passed

![gpio_mgmt result](Screenshots/gpio_mgmt_result.png)

### mem - Passed

![mem result](Screenshots/mem_result.png)

### uart - Passed

![uart result](Screenshots/uart_result.png)

### timer - Failed

![timer result](Screenshots/timer_result.png)

### irq - Failed

![irq result](Screenshots/irq_result.png)

### debug - Failed

![debug result](Screenshots/debug_result.png)

### Standalone Test Result Table 

| tests-standalone | status(sky130) |
| -------- | -------- |
| gpio_mgmt	| PASS	| 
| mem	| PASS |
| uart	| PASS |
| timer	| FAIL |
| irq	| FAIL |
| debug	| FAIL |
| spi_master	| PASS |
