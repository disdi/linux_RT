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

This milestone focuses on the hardware modifications needed for integrating the CLIC with the Vexriscv core.

#### 1.1 Top-Level Integration to Litex SOC
- [ ] Create CLIC module instance in SoC top-level
- [ ] Connect clock and reset signals
- [ ] Define and connect interrupt input signals from peripherals
- [ ] Connect Vexriscv-to-CLIC configuration interface

#### 1.2 Memory Map Implementation
- [ ] Define CLIC memory map (base address and regions)
- [ ] Implement address decoder for CLIC registers
- [ ] Connect to system bus (TileLink/AHB/AXI)
- [ ] Map CLIC vector table in memory

#### 1.3 Register Implementation
- [ ] Implement CLIC control registers
- [ ] Implement per-interrupt configuration registers
- [ ] Implement interrupt pending/enable registers
- [ ] Implement level/priority registers

#### 1.4 Interrupt Logic
- [ ] Implement interrupt priority resolution
- [ ] Implement level-based preemption logic
- [ ] Implement selective hardware vectoring
- [ ] Implement interrupt completion logic

#### 1.5 Vector Table
- [ ] Implement vector table storage
- [ ] Implement vector table lookup logic
- [ ] Connect vector addresses to Vexriscv core


### Milestone 2 - Baremetal Software Modifications

This milestone addresses the necessary software changes for supporting CLIC on baremetal systems.

#### 2.1 Startup Handling
- [ ] Update bootup code
- [ ] Modify linker scripts
- [ ] Create vector table setup functions
- [ ] Update system initialization functions

#### 2.2 Configuration
- [ ] Define interrupt priority levels
- [ ] Configure interrupt modes (vectored/non-vectored)
- [ ] Setup privilege levels
- [ ] Configure preemption thresholds

#### 2.3 Interrupt Handlers
- [ ] Create default interrupt handler
- [ ] Implement vectored interrupt handlers
- [ ] Setup interrupt entry/exit code
- [ ] Implement interrupt nesting support

#### 2.4 Driver Development
- [ ] Create CLIC initialization function
- [ ] Implement interrupt enable/disable functions
- [ ] Implement interrupt priority setting functions
- [ ] Create vector table setup functions

#### 2.5 Software Development Kit(SDK) update
- [ ] Add CLIC support to build system
- [ ] Add CLIC debugging support

### Milestone 3 - Linux Software Modifications

This milestone focuses on the necessary software changes needed for CLIC in Linux.

#### 3.1 Linux Kernel Configuration
- [ ] Update the device tree to include entries for the new interrupt controller.
- [ ] Update kernel configuration options to include support for the new interrupt controller.

#### 3.2 Linux Interrupt Controller Driver
- [ ] Write Linux driver to interface with the new interrupt controller.
- [ ] Add support for interrupt prioritization and preemption.
- [ ] Ensure compatibility with existing Linux kernel interrupt handling mechanisms.
    
#### 3.3 Linux Startup Code
- [ ] Initialize CLIC interrupts on RISC-V core booting Linux.
- [ ] Ensure proper initialization of interrupt vectors.
- [ ] Update the kernel boot parameters to recognize the new interrupt controller.

### Milestone 4 - Verification and Testing

This milestone involves thorough verification and testing of the CLIC integration.

#### 4.1 Compliance Testing
- [ ] Verify RISC-V CLIC specification compliance
- [ ] Test privilege level handling
- [ ] Verify CSR functionality
- [ ] Check timing requirements

#### 4.2 System Validation
- [ ] Validate system stability
- [ ] Test corner cases
- [ ] Verify error handling
- [ ] Validate power modes

#### 4.3 Performance Analysis
- [ ] Measure interrupt latency
- [ ] Analyze resource utilization
- [ ] Profile interrupt handling
- [ ] Document performance metrics