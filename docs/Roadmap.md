---
title: Roadmap
---

Roadmap
=======

## CLIC Support in RISC-V Ecosystem 

Adding an extension to the RISC-V architecture involves several steps, from defining the specification to implementing and testing the extension. Here's a high-level roadmap for the process:

| Steps                             | Status           | Remark      |
|-----------------------------------|------------------|-------------|
| Define the Extension Specification|Already Implemented|[Specification](https://github.com/riscv/riscv-fast-interrupt) by RISC-V Community|
| Proposal and Review               |Already Implemented|CLIC ratification status is now tracked using [Jira](https://lf-riscv.atlassian.net/browse/RVS-1017)|
| Toolchain Support                 |Already Implemented|Already supported by [GCC](https://lf-riscv.atlassian.net/browse/RVS-2508)|
| Hardware Implementation           |Not Implemented|No support in Vexriscv. [Commercial implementation](https://lf-riscv.atlassian.net/browse/RVS-2513). [Opensource implementation](https://github.com/pulp-platform/clic)|
| Software Implementation           |Not Implemented|No support in Vexriscv. Reference implementation in [QEMU](https://mail.gnu.org/archive/html/qemu-devel/2024-08/msg02791.html)|
| Compliance and Testing            |Not Implemented|No support in Vexriscv. Reference tests in [Safety Island](https://github.com/pulp-platform/safety_island/tree/main/sw/tests)|
| Documentation and Release         |Not Implemented|No support in Vexriscv.|


## CLIC Support in Vexriscv

### Milestone 1 - Hardware Modifications

- Integrate the Interrupt 
    - Select the CLIC Interrupt Controller: first step is to integrate CLIC it with Vexriscv core.
- Modify the Vexriscv Core
    - Interface Design: Ensure the CLIC interrupt controller's interface is compatible with Vexriscv core's interrupt handling mechanism. This typically involves connections for interrupt request lines and acknowledge signals.

### Milestone 2 - Software Modifications

- RISC-V Machine (M-Mode) & Supervisor (S-Mode) Software
    -  Trap Vector Initialization: Update the trap vector initialization code to handle interrupts from the new interrupt controller.
    -  Interrupt Handling Code: Modify the interrupt service routines (ISRs) to acknowledge and service interrupts from the new controller.
    -  Device Tree (DT): Update the device tree to include entries for the new interrupt controller.
    -  Interrupt Controller Driver: Write or modify an existing driver to interface with the new interrupt controller.  

### Milestone 3 - Verification and Testing

- Simulation: Run simulations to verify the integration of CLIC interrupt controller with the RISC-V core. Check that interrupts are correctly triggered, handled, and acknowledged.
- Hardware Testing: Once simulations are successful, perform hardware testing to ensure the entire system with Litex framework to ensure working correctly in a real-world scenario.