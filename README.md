# 5 V to 3.3 V LDO Power Supply

An Altium Designer implementation of a 5 V to 3.3 V linear regulator power supply using the Texas Instruments TPS79301-EP adjustable low-dropout (LDO) regulator.

## Overview

| Parameter | Specification |
| :--- | :--- |
| **Input Voltage ($V_{IN}$)** | 5.0 V |
| **Output Voltage ($V_{OUT}$)** | 3.3 V |
| **Max Expected Load ($I_{OUT}$)** | 100 mA |
| **Regulator IC** | TI TPS79301-EP |
| **PCB Stackup** | 2-layer design with bottom-layer GND plane |
| **Connectors** | 2-pin through-hole headers |

## Schematic Design

The output voltage is set via the regulator's feedback network:

* **$R_1$:** $51\text{ k}\Omega$
* **$R_2$:** $30.1\text{ k}\Omega$
* **$C_{FF}$:** $15\text{ pF}$ (Feed-forward capacitor)

### Output Equation

The TPS79301-EP feedback voltage equation is:

$$V_{OUT} = V_{REF} \times \left(1 + \frac{R_1}{R_2}\right)$$

Given $V_{REF} \approx 1.2246\text{ V}$:

$$V_{OUT} = 1.2246\text{ V} \times \left(1 + \frac{51\text{ k}\Omega}{30.1\text{ k}\Omega}\right) \approx 3.30\text{ V}$$

### Decoupling & Bypass Capacitors

* **$C_1$:** $1\text{ }\mu\text{F}$ Input capacitor
* **$C_2$:** $2.2\text{ }\mu\text{F}$ Output capacitor
* **$C_3$:** $10\text{ nF}$ Noise BYPASS capacitor

## Power Dissipation

At the maximum load of $100\text{ mA}$, approximate power dissipation ($P_D$) is calculated as:

$$P_D = (V_{IN} - V_{OUT}) \times I_{OUT}$$

$$P_D = (5\text{ V} - 3.3\text{ V}) \times 0.1\text{ A} = 0.17\text{ W}$$

## PCB Design

Component layout prioritizes signal integrity and low noise around the regulator's critical pins:

* Input and output capacitors placed as close as possible to IC pins.
* Minimized feedback loop traces to reduce noise pickup.
* Continuous bottom-layer Ground plane.
* Through-hole headers selected for secure physical connections.
* Standardized component selection for easy hand assembly and manufacturing.

## Verification

The completed design successfully passed Altium Designer's Design Rule Check (DRC):

* **0 Warnings / 0 Rule Violations**

Manufacturing outputs (Gerber and N.C. Drill files) have been generated.

> **Note on Simulation:** An encrypted PSpice model from the manufacturer was evaluated; however, complete SPICE transient/AC simulations were not conducted. Consequently, no simulated efficiency or ripple metrics are claimed.

## Repository Structure

```text
5V-to-3V3-LDO/
├── Altium/
│   ├── 5V_to_3V3_LDO.PrjPcb
│   ├── 5V_to_3V3_LDO.SchDoc
│   └── 5V_to_3V3_LDO.PcbDoc
├── Manufacturing/
│   └── Gerbers/
└── Documentation/
    └── Schematic and PCB documentation