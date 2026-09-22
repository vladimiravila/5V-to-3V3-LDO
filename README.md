# 5 V to 3.3 V LDO Power Supply

Altium Designer implementation of a 5 V to 3.3 V linear regulator supply using the TI TPS79301-EP adjustable LDO.

## Overview

* **Input:** 5 V
* **Output:** 3.3 V
* **Maximum expected load:** 100 mA
* **Regulator:** TI TPS79301-EP
* **PCB:** 2-layer design with bottom-layer GND plane
* **Connectors:** 2-pin through-hole headers

## Schematic Design

The output voltage is set using the regulator's feedback network:

* R1 = 51 kΩ
* R2 = 30.1 kΩ
* CFF = 15 pF

Using the TPS79301-EP feedback equation:

$$
V_{OUT}=V_{REF}\left(1+\frac{R_1}{R_2}\right)
$$

with \(V_{REF}\approx1.2246\text{ V}\):

$$
V_{OUT}=1.2246\left(1+\frac{51}{30.1}\right)\approx3.30\text{ V}
$$

The remaining capacitors are:

* C1 = 1 µF input capacitor
* C2 = 2.2 µF output capacitor
* C3 = 10 nF BYPASS capacitor

## Power Dissipation

At the maximum expected load of 100 mA, the approximate regulator power dissipation is:

$$
P=(V_{IN}-V_{OUT})I_{OUT}
$$

$$
P=(5-3.3)(0.1)=0.17\text{ W}
$$

## PCB Design

The PCB layout was designed with component placement based on the regulator's input, output, bypass, and feedback connections.

Key layout considerations included:

* Input and output capacitors placed close to the regulator
* Short feedback connections
* Dedicated bottom-layer GND plane
* Through-hole input and output connectors
* Components selected with manufacturability and hand-assembly considerations in mind

## Verification

The completed PCB passed Altium Designer's Design Rule Check with:

**0 warnings and 0 rule violations**

Gerber and drill files were also generated for manufacturing.

A manufacturer-provided encrypted PSpice model was investigated for simulation, but regulator SPICE simulation was not completed. Therefore, no simulated regulator performance is claimed.

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
```
