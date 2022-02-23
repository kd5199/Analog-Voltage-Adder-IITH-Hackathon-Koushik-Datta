
# Analog Voltage Adder Circuit using Op amp in 28nm technology

In this project I have designed a analog voltage adder circuit using op amp in Synopsys Custom 
Compiler. The Op amp circuit used is a 2 state Miller Op amp circuit. 



## Content

- Abstract
- Reference Circuit Details
- Reference Circuit Diagram
- Reference Circuit Waveform
- Designed Circuit Details
- Designed Circuit Diagram
- Designed Circuit Netlist
- Designed Circuit Waveform
- Conclusion
- Acknowledgement
- Reference

### Abstract

In this paper a design of analog voltage adder circuit adder circuit using Op amp has been
shown. Besides, the circuit diagram, theoretical proof and estimated waveform has been shown.
The adder circuit is used in different signal processing application in communication
engineering.

### Reference Circuit Details


The adder circuit consists of an opamp. A negative feedback is provided in the circuit.
The nodal analysis on the circuit is shown below, considering virtual short concept.

![app screenshot](https://www.tutorialspoint.com/linear_integrated_circuits_applications/images/adder.jpg)

    Fig. Adder Circuit Diagram using Opamp

The theoretical calculation is shown below. If the in put is V1 and V2 then we are supposed
to get output of -(V1+V2).

![alt text](https://github.com/kd5199/Analog-Voltage-Adder-IITH-Hackathon-Koushik-Datta/blob/main/Calculation.png?raw=true)

The output will be in inverted form. It can be passed through a inverting amplifier with
unity gain, which will increase number of stages. The op amp itself has the following
circuit[2] at transistor level.	

![alt text](https://github.com/kd5199/Analog-Voltage-Adder-IITH-Hackathon-Koushik-Datta/blob/main/Miller%20Opamp.png?raw=true)

    Fig. Reference Miller op amp circuit 

### Reference Circuit Diagram

![alt text](https://github.com/kd5199/Analog-Voltage-Adder-IITH-Hackathon-Koushik-Datta/blob/main/Reference%20Circuit.png?raw=true)

    Fig. Reference circuit generated by Circuitlab.com 

### Reference Circuit Waveform

![alt text](https://github.com/kd5199/Analog-Voltage-Adder-IITH-Hackathon-Koushik-Datta/blob/main/Reference%20waveform.png?raw=true)

    Fig. Estimated Waveform

### Designed Circuit Details

First of all, a two stage miller opamp has been designed, which is shown below.

![alt text](https://github.com/kd5199/Analog-Voltage-Adder-IITH-Hackathon-Koushik-Datta/blob/main/Miller%20Opamp%20Designed.png?raw=true)

    Fig. Designed wo state miller op amp 


Practically the virtual ground concept isn’t dominant. Thats why the calculations that we
have done theoretically doesn't hold error free. The changes in the waveform show the same. 

It is estimated that the current through the inverting and non inverting terminal of the 
op amp as zero, but in simulation there is non zero value exist. 

Besided, in the circuit, Iref has 40uA current. Applied Vdd is 1.8V and Vss applied is -1.8V. In the complete circuit the Rf=R1=R2= 100K Ohm
and at the output the 1pF capacitor is used. For the input, two constant voltage sources
are used, one of 0.5V and other of 0.2V. The output was estimated at -0.7V. 
But the obtained output voltage is -0.67V.

![alt text](https://github.com/kd5199/Analog-Voltage-Adder-IITH-Hackathon-Koushik-Datta/blob/main/Symbol.png?raw=true)
    
    Fig. The created symbol for the two state miller op amp 


### Designed Circuit Diagram

![alt text](https://github.com/kd5199/Analog-Voltage-Adder-IITH-Hackathon-Koushik-Datta/blob/main/Complete%20Circuit.png?raw=true)

    Fig. Complete adder circuit 

### Designed Circuit Netlist


```
*  Generated for: PrimeSim
*  Design library name: cp_lib1
*  Design cell name: opamp_adder
*  Design view name: schematic
.lib 'saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Wed Feb 23 04:12:05 2022

.global gnd! vdd!
********************************************************************************
* Library          : cp_lib1
* Cell             : opamp_v1
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt opamp_v1 vdd vin_inv vin_non_inv vss out vt_bulk_n_gnd! vt_bulk_p_vdd!
xm11 net21 vin_non_inv net14 vt_bulk_p_vdd! p105 w=3u l=0.03u nf=1 m=1
xm12 net26 vin_inv net14 vt_bulk_p_vdd! p105 w=3u l=0.03u nf=1 m=1
xm2 out net29 vdd vt_bulk_p_vdd! p105 w=0.4u l=0.03u nf=1 m=1
xm1 net14 net29 vdd vt_bulk_p_vdd! p105 w=0.4u l=0.03u nf=1 m=1
xm0 net29 net29 vdd vt_bulk_p_vdd! p105 w=0.4u l=0.03u nf=1 m=1
xm7 out net26 vss vt_bulk_n_gnd! n105 w=3.5u l=0.03u nf=1 m=1
xm6 net21 net21 vss vt_bulk_n_gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm5 net26 net21 vss vt_bulk_n_gnd! n105 w=0.1u l=0.03u nf=1 m=1
r8 net26 net28 r=0k
c9 net28 out c=1u
i10 net29 vss dc=40u
.ends opamp_v1

********************************************************************************
* Library          : cp_lib1
* Cell             : opamp_adder
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi0 net21 net6 gnd! net18 net10 gnd! vdd! opamp_v1
r3 net6 net10 r=100k
r2 net14 net6 r=100k
r1 net16 net6 r=100k
c4 net10 gnd! c=1p
v13 net21 gnd! dc=01.8
v12 gnd! net18 dc=01.8
v11 net16 gnd! dc=0.2
v10 net14 gnd! dc=0.5

.tran '0.1u' '10u' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(net10) v(net14) v(net16)
.temp 25
.option primesim_output=wdf
.option parhier = LOCAL
.end

```


### Designed Circuit Waveform

![alt text](https://github.com/kd5199/Analog-Voltage-Adder-IITH-Hackathon-Koushik-Datta/blob/main/Waveform1.png?raw=true)

    Fig. Ungrouped Waveform 

![alt text](https://github.com/kd5199/Analog-Voltage-Adder-IITH-Hackathon-Koushik-Datta/blob/main/Grouped%20waveform.png?raw=true)

    Fig. Grouped Waveform 

### Conclusion

The adder circuit has been designed and simulated successfully in 28nm technology using Synopsys Custom Compiler.
The out put is 0.3V greater than the estimated -7V. So an error of 4.2% is seen.

### Acknowledgement

    1. Kunal Ghosh, Co-Founder, VSD Corp. Pvt Ltd.
    2. Chinmay Panda, IIT Hyderabad

### Reference

    1. Arithmetic Circuits (https://www.tutorialspoint.com/linear_integrated_circuits_applications/linear_integrated_circuits_applications_arithmetic_circuits.htm)
    2. Optimal Design of a CMOS Op-Amp via Geometric Programming - Maria del Mar Hershenson et al.
    
