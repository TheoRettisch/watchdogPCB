# Hand-built SPICE testbenches — dhw watchdog

Run with ngspice in batch mode; each writes a `.out` file with the key results.

| File | Verifies | Result |
|------|----------|--------|
| `tb_monostable_timeout.cir` | IC1 R6/C1 watchdog timeout = 90 ms; stays armed at 20 Hz; drops out 90 ms after heartbeat loss | PASS (sim fall = 89.9 ms) |
| `tb_gate_driver.cir` | Q1 P-MOS high-side fail-off: Vsg, Z1 clamp margin, AMP_REM on/off | PASS (Vsg 10.9 V on / 0 V off) |
| `tb_opto_led_drive.cir` | LTV-817 input LED drive current vs 3.0–3.6 V GPIO | ~3.1 mA (low side — see findings) |

```
ngspice -b tb_monostable_timeout.cir && cat tb_monostable_timeout.out
ngspice -b tb_gate_driver.cir         && cat tb_gate_driver.out
ngspice -b tb_opto_led_drive.cir      && cat tb_opto_led_drive.out
```

Full write-up: `../../docs/spice-simulation-findings.md`.
Component values, trust levels, and topology notes are documented in the header
comment of each `.cir` file.
