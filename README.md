# Memristor-Model

SPICE models and testbenches for **Diffusive Memristor** and **Drift Memristor**.

## Overview

This repository provides reusable core model netlists and ready-to-run test circuits:

- Diffusive memristor core model with optional cycle-to-cycle stochastic variation
- Drift memristor core model based on coupled internal state variables
- Single-pulse and multi-pulse testbenches for current/voltage excitation
- Example bipolar pulse testbench for drift memristor

The files are written in SPICE netlist format (`.cir`) and have only been tested in `LTspice`.

## Repository Structure

- `Diffusive_model_core.cir`: core equations for the diffusive memristor
- `Drift_model_core.cir`: core equations for the drift memristor
- `test_diffusive_current_single_pulse.cir`: diffusive model, single current pulse
- `test_diffusive_current_multi_pulse.cir`: diffusive model, multiple current pulses
- `test_diffusive_voltage_single_pulse.cir`: diffusive model, single voltage pulse
- `test_diffusive_voltage_multi_pulse.cir`: diffusive model, multiple voltage pulses
- `Test bipolar.cir`: drift model, bipolar repeating pulse stimulus
- `LICENSE`: MIT license

## Requirements

- A SPICE simulator supporting behavioral sources and `.func` expressions
- Validated environment: `LTspice`

## Quick Start

Open any testbench in `LTspice` and click **Run**.

Each testbench already includes:

- `.include` of the corresponding core model file
- stimulus source definition (`PULSE`)
- transient simulation command (`.tran`)
- saved variables for waveform plotting (`.save`, `.plot`, `.probe`)

## How to Tune Parameters

All tunable parameters are declared in the testbench `.cir` files (not hardcoded in the core model include files).

### Diffusive Memristor

In `test_diffusive_*.cir`, you can tune:

- device/kinetic parameters: `alpha`, `lamda`, `Ron`, `Roff`, `mu`, `beta`, `gamma1`, `gamma2`, `eta`
- noise/stochastic controls: `dt`, `kappa`, `m`, `eps`
- pulse shape and timing: `Iamp` or `Vamp`, `tdelay`, `trise`, `tfall`, `ton`, `tperiod`, `cycles`

### Drift Memristor

In `Test bipolar.cir`, you can tune:

- model parameters: `n`, `m`, `h0`, `hmax`, `h1`, `h2`, `h_lambda`, `s0`, `alpha`, `beta`, `sigma`, `eta`, `theta`, `Ron`, `Roff`, `cc`
- read/write/reset waveform parameters: `vread`, `vset`, `vreset`, `tdelay`, `tedge`, `ton`, `ttotal`, `cycles`

## Typical Workflow

1. Select a testbench file.
2. Adjust `.param` values for your target device behavior.
3. Run transient simulation.
4. Inspect saved states/currents (`V(f)`, `V(r)`, `V(h)`, `V(s)`, `I(BIMx)`, `I(BIx)`, etc.).
5. Iterate parameters until measured and simulated responses align.

## Notes

- The core files are intended to be included by testbenches; keep model equations in core files and experiment settings in test files.
- Some tests use long transient times (seconds scale) and may take longer to simulate depending on timestep and simulator settings.

## References

[1] T. Wang et al., "A faithful and compact diffusive memristor model," IEEE Trans. Circuits Syst. Artif. Intell., vol. 1, no. 2, pp. 141-148, Dec. 2024, doi:10.1109/TCASAI.2024.3484370.

[2] R. Zhao et al., "A spiking artificial neuron based on one diffusive memristor, one transistor and one resistor," Nat. Electron., vol. 8, pp. 1211-1221, 2025, doi:10.1038/s41928-025-01488-x.

[3] Y. Zhuo et al., "A dynamical compact model of diffusive and drift memristors for neuromorphic computing," Adv. Electron. Mater., vol. 8, no. 8, 2022, doi:10.1002/aelm.202270040.

## License

This project is licensed under the MIT License. See `LICENSE` for details.
