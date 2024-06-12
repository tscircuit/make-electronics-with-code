# Make Electronics with Code

> A curated list of software packages that allow you to make electronics with code

Please PR to this repo if you find a new package!

# Overview

## PCB Design / EDA

* [tscircuit](#tscircuit) - Open-source EDA package for schematic and PCB design using React and Typescript
* [atopile](#atopile) - Open-source python-like language and toolchain to describe electronic circuit boards with code
* [jitX](#jitx) - Mature project with custom language. Custom licensing

## Simulation

* [ngspice](#ngspice) - SPICE simulator for electric and electronic circuits
* [PySpice](#pyspice) - Simulate electronic circuits using Python and the Ngspice / Xyce simulators

# Packages

## tscircuit

[Website](https://tscircuit.com) &middot; [Github](https://github.com/tscircuit/tscircuit) &middot; [Quick start](https://docs.tscircuit.com/quickstart)

* MIT-licensed open-source (permissive)
* React/Typescript Language

Example code:

```tsx
const Circuit = () => (
  <board width="10mm" height="10mm">
    <resistor
      name="R1"
      resistance="10ohm"
      footprint="0805"
    />
    <bug
      name="B1"
      port_arrangement={{ left_size: 3, right_size: 3 }}
      footprint="sot236"
      port_labels={{
        1: "PWR",
        2: "NC",
        3: "RG",
        4: "D0",
        5: "D1",
        6: "GND",
      }}
    />
    <ground name="GND" />
    <trace from=".B1 > .D0" to=".R1 > .left" />
    <trace from=".R1 > .right" to=".GND" />
  </board>
)
```


## atopile

[Website](https://atopile.io) &middot; [Github](https://github.com/atopile/atopile) &middot; [Quick Start](https://atopile.io/getting-started/)

* Apache 2 open-source (permissive)
* Python-like language (`ato`)
* VS-code extension

Example code:

```python
from "generics/resistors.ato" import Resistor

module VoltageDivider:
    signal top
    signal out
    signal bottom

    r_top = new Resistor
    r_top.footprint = "R0402"
    r_top.value = 100kohm +/- 10%

    r_bottom = new Resistor
    r_bottom.footprint = "R0402"
    r_bottom.value = 200kohm +/- 10%

    top ~ r_top.p1; r_top.p2 ~ out
    out ~ r_bottom.p1; r_bottom.p2 ~ bottom
```



## jitX

[Website](https://www.jitx.com/)

* Custom licensing (CERN Open Hardware License V2 or paid)
* Mature

Example code:

```
; create a coin cell battery
val battery-capacity = 90.0 ;set the capacity of battery, in mAh
inst battery : ocdb/components/q-n-j/CR2032-BS-6-1/component(battery-capacity); create a battery with the specified capacity
net (POWER battery.power.vdd); connect positive of battery to the POWER net
net (GND battery.power.gnd); connect negative of battery to the GND net
val battery-y = board-height / 3.5; programmatically calculate an x and y position of the battery based on the board-shape
val battery-x = board-width / -7.0; 
place(battery) at loc(battery-x, battery-y, 90.0) on Top; place the battery on the top of the board at the calculated position
```

## ngspice

[Website](https://ngspice.sourceforge.io/) &middot; [SourceForge](https://sourceforge.net/projects/ngspice/) &middot; [Quick Start](https://ngspice.sourceforge.io/ngspice-tutorial.html)

* BSD-3-Clause license

Example code:
![image](https://github.com/tscircuit/make-electronics-with-code/assets/1910070/bdedca55-7cb5-48c7-a594-9f63532855cb)

## PySpice

[Website](https://pypi.org/project/PySpice/) &middot; [Github](https://github.com/PySpice-org/PySpice)

* GPLv3 Open-source

Example code:

```python
class ParallelResistor2(SubCircuit):
    __nodes__ = ('n1', 'n2')
    def __init__(self, name, R1=1@u_Ω, R2=2@u_Ω):
        SubCircuit.__init__(self, name, *self.__nodes__)
        self.R(1, 'n1', 'n2', R1)
        self.R(2, 'n1', 'n2', R2)

circuit = Circuit('Test')
circuit.subcircuit(ParallelResistor2('pr1', R2=2@u_Ω))
circuit.X('1', 'pr1', 1, circuit.gnd)
circuit.subcircuit(ParallelResistor2('pr2', R2=3@u_Ω))
circuit.X('2', 'pr2', 1, circuit.gnd)
```


