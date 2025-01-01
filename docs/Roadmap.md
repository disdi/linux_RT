---
title: Roadmap
---

Roadmap
=======

## CLIC Support in RISC-V Ecosystem 

Adding an extension to the RISC-V architecture involves several steps, from defining the specification to implementing and testing the extension. Here's a high-level roadmap for the process:

| Steps                             | Status           | Remark      |
|-----------------------------------|------------------|-------------|
| Define the Extension Specification|Already Implemented|[Specification](https://github.com/riscv/riscv-fast-interrupt) by RISC-V Community.|
| Proposal and Review               |Already Implemented|CLIC ratification status ticket [Jira](https://lf-riscv.atlassian.net/browse/RVS-1017).|
| Simulation Support                |Already Implemented|Already supported by [RISC-V ACT](https://lf-riscv.atlassian.net/browse/RVS-2506).|
| Emulator Support                  |Already Implemented|Initial patches in [QEMU](https://mail.gnu.org/archive/html/qemu-devel/2024-08/msg02791.html).|
| Hardware Implementation           |Not Implemented|No Vexriscv support. [Commercial](https://lf-riscv.atlassian.net/browse/RVS-2513) & [Opensource](https://github.com/pulp-platform/clic) reference.|
| Software Implementation           |Not Implemented|No Vexriscv support. [Opensource](https://github.com/pulp-platform/pulp-freertos/blob/master/drivers/clic.c) reference.|
| Compliance and Testing            |Not Implemented|No Vexriscv support. Reference [tests](https://github.com/pulp-platform/safety_island/tree/main/sw/tests/runtime_clic_basic).|
| Documentation and Release         |Not Implemented|No Vexriscv support.|


## CLIC Support in Vexriscv

### Milestone 1 - Hardware Modifications

- Implement the CLIC Interrupt Controller
    - Integrate CLIC with any simple RISC-V SOC.
        - Integrate reference CLIC Implementation to trigger RISC-V Core into Trap.
    - Integrate CLIC in Litex
        - Implement CLIC in SpinalHDL to trigger Vexriscv Core into Trap.

### Milestone 2 - Software Modifications

- RISC-V Bare Metal Software
    -  Interrupt Vector Implementation:
        - Update the trap vector initialization code to handle interrupts from CLIC.
        - Modify Interrupt vector table to switch to CLIC as interrupt controller.
        - Write Interrupt Controller Driver to interface with the new interrupt controller.
        - Modify interrupt service routines (ISRs) to acknowledge and service interrupts from CLIC.
    - Verify CLIC interrupts work on bare-metal application booting on RISC-V Core.

### Milestone 3 - Software Modifications

- RISC-V Linux Software
    -  Device Tree (DT): Update the device tree to include entries for the new interrupt controller.
    -  Interrupt Controller Driver: Write Linux driver to interface with the new interrupt controller.
     - Verify CLIC interrupts work on Risc-V Core in Litex booting Linux.

### Milestone 4 - Verification and Testing

- Simulation: Run simulations to verify the integration of CLIC interrupt controller with the RISC-V core. Check that interrupts are correctly triggered, handled, and acknowledged.
- Hardware Testing: Once simulations are successful, perform hardware testing to ensure the entire system with Litex framework to ensure working correctly in a real-world scenario.