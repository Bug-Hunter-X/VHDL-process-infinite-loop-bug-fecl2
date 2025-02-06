# VHDL Process Infinite Loop Bug

This repository demonstrates a common error in VHDL: an unintended infinite loop caused by an incomplete sensitivity list in a process.

## Bug Description

The `bad_process` entity uses a process with only the clock signal (`clk`) in its sensitivity list.  This means that the process only executes when the clock changes. However, the output value `data_out` is assigned inside the process.  This assignment doesn't change the sensitivity list, so the process will continuously execute at every clock cycle, leading to a potential infinite loop during simulation, or unexpected and unwanted behavior in hardware.

## Solution

The `good_process` entity demonstrates the correct approach.  The sensitivity list now includes `data_in`, ensuring that the process executes whenever the input data changes, regardless of the clock.  This way, `data_out` will update only when new input is available, and not at every clock pulse.

## How to reproduce

1. Compile both files using a VHDL simulator (e.g., ModelSim, GHDL).
2. Simulate the `bad_process` entity. Observe the continuous execution of the process at every clock edge, potentially leading to a simulation error.
3. Simulate the `good_process` entity to see the correct behavior. 