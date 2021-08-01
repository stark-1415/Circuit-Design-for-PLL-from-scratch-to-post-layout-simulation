# Circuit-Design-for-PLL-from-scratch-to-post-layout-simulation Design using SKY130nm-Technology
2 day workshop 31st July to 1st August

Here we have to learn to how we design a basic PLL circuit from scratch to post layout simulation.

# PLL Specification

Technology - SKywater 130nm


Supply Voltage    - 1.8V


Process Corner    - TT


Temperature       - room temperature


Input Frequency(Fmin)   - 5Mhz, Fmax - 12.5Mhz


Multiplier -8x


Duty Cycle =50%


Jitter < 20ns



# Overview 

Day 1:    PLL Theory and setup tools for simulation

content:  

1) PLL theory
2) Tool setup
3) Development Flow
4) Introduction to PDK,simulation tools

Day 2:  PLL Circuit Design and Pre and Post simulation 

5)  PLL component circuit design 
6)  PLL component circuit simulate
7)  Layout Design
8)  Pre layout simulation
9)  Parasitic Extraction
10) Post layout simulation
11) Tapeout

## Day 1 : PLL Theory and setup tools for simulation 
# PLL Theory
Why PLL?


To get precise clock signal without frequency or phase noise.A PLL is a feedback system that compares the output phase with the input phase.
The comparison is performed by a "phase comparator".To arrive the concept of phase locking, let us consider the problem of aligning the output phase of VCO with the phase of a
reference clock.

# Basic block diagram of PLL

![image](https://user-images.githubusercontent.com/67455761/127779269-1ab34b4f-a3df-48b1-90e8-58d3c3325e24.png)

### PLL have five blocks

1) Phase Frequency Detector (PFD)

The phase difference between the input signal with frequency fin and the feedback (output) signal with frequency fout is proportional to the DC voltage produced by the phase detector. In this case, a phase detector is nothing more than a comparator. It generates a dc voltage by comparing the two frequency components delivered into its input. A phase detector is a multiplier that generates two frequency components.


Basic block diagram of PLL is

![image](https://user-images.githubusercontent.com/67455761/127779625-5cdc1f15-3d73-4fa8-aa9e-b30aa5d8de7c.png)

2) Charge Pump

Charge pump circuit gives a constant current. The amplitude of the current always remains same.The polarity changes which depend on the value of the UP and DOWN signal.
Traditional circuit has  non-ideal effects, such as leakage current, current mismatch.


![image](https://user-images.githubusercontent.com/67455761/127780632-a8530c67-4bc7-4205-adeb-a28406fc0558.png)

3) Low Pass Filter(LPF)

The output of the phase detector is supplied to a low pass filter that removes from the output of the comparator the high frequency component and noise. The output of the phase detector is the sum and difference frequency of two input signals. Because the total of two frequencies (i.e., fi + fo) is a high-frequency component, the LPF filters it out. The difference (i.e., fi – fo) is a low-frequency component that the filter passes through. After that, the low-frequency dc voltage signal is sent into a dc amplifier, which boosts the signal level. After that, the VCO receives the enhanced signal.


4) Voltage Controlled Oscillator (VCO)


PLLs are continually adjusted to match (lock on) a phase and frequency of an input signal using a voltage-controlled oscillator (VCO) tuned by a unique half-conductive diode known as a varactor. The LPF output serves as a VCO control signal. The DC signal is produced by the VCO and its amplitude is proportional to the LPF output amplitude. In this case the VCO output frequency modification is done till the input signal frequency is equivalent.

![image](https://user-images.githubusercontent.com/67455761/127781254-a8b88f6e-232e-4dab-b726-c96bd209a736.png)

5) Frequency Divider


When the frequency difference of each input is 0, which shows a consistent phase difference, the loop is locked.
If the two signals are shifted by 180, the output voltage must be at the highest. The output voltage generated will be zero in the absence of an input signal to allow the VCO to function at a fixed frequency. This frequency is referred to as the oscillator's operating frequency.


![image](https://user-images.githubusercontent.com/67455761/127781380-948db5ff-926e-482e-8c41-67f2a448e923.png)





## Some Important term in Phase Locked Loop

1) Lock Range 

The Frequency range the PLL is able to follow input frequency variations once locked.


2) Capture Range

The Frequency range the PLL is able to lock-in when starting from an unlocked condition.

3) Settling time

 The time with in which the PLL is able to lock-in form an unlocked condition
 
 
 
##  Day 1 LAB Setup : 
  
  In this workshop we use two simulation tools:
  1) Ng-spice - for Circuit design and Simulation
  2) Magic    - for Layout Design and parasitic Extraction
  
  
 Installation Process Setup
 1) Ng-spice we write code in unix system
 
  sudo apt-get install ngspice
  
  after installation we have to fetch SKYWATER 130nm PDK technology file.
  
 2) Install the magic tool
 
   We use  the git  clone  and install the magic file.Then we need compile it, which requires installing the prerequisites from opendesigncircuit.com. Then we execute the command ./configure. The command we execute. We next execute the sudo make install command.
   
   Then we should install the sky130nm technology information that Magic requires for layout design.
   
   
   ## Day 2  PLL Circuit and  Layout Simulation
   
     We have to design the single block of PLL and simulate the circuit in ngspice.
     
 
### Individual block and result of PLL Design

##### 1) Frequency Divider Circuit
    
    wave form of the FD show here:
    
![image](https://user-images.githubusercontent.com/67455761/127774410-63873540-d18c-4df7-bcd3-3c99e8342243.png)

<b>Red:</b> Clock 1 <br>
<b>Blue:</b> Clock 2 <br>
<b>Orange:</b> Up Signal <br>
<b>Green:</b> Down Signal


#### 2) Charge Pump 

#### CP response when "UP" signal is high:

![image](https://user-images.githubusercontent.com/67455761/127776158-1fde4ddc-f5f6-4931-8546-be3689f09fbd.png)

<b>Red:</b> Charge pump output voltage <br>

#### 3) Voltage Control Oscillator simultator Output

#### VCO waveform is as shown below:

![image](https://user-images.githubusercontent.com/67455761/127776206-67bc2a17-cde5-4ab2-ad36-7f0ef047573a.png)

<b>Red:</b> Control Voltage <br>
<b>Blue:</b> Output Clock <br>

###  4) Frequency Divider 

#### The Frequency Divider waveform is as shown below:

![image](https://user-images.githubusercontent.com/67455761/127776406-b6cd0291-2ced-4c37-b707-3086fb1307e8.png)

<b>Red:</b> Output Clock <br>
<b>Blue:</b> Input Clock <br>

### 5) PLL

#### The PLL waveform is as shown below: 

![image](https://user-images.githubusercontent.com/67455761/127777450-6f04f7f5-2298-4924-80e3-ce7c0f318064.png)

<b>Red:</b> Reference Clock <br>
<b>Blue:</b> Output Clock Divided by 8 <br>
<b>Yellow:</b> Down Signal <br>
<b>Brown:</b> Up Signal <br>
<b>Pink (top) :</b>Charge pump output <br>


###  Layout Design For PLL

In layout, these are the following different colour codes for different components used in layout: 

1. p-diffusion - plane orange colour

2. n-diffusion - plane green colour

3. polysilicon - plane red

4. n-well - dotted  lines

5. metal1 layer - purple

6. local interconnect layer - blue

To connect two transistors, we use interconnect layer. To connect two metal layers, we use the contact/via.

### 1) FD layout
 PFD layout show below 
 
 
![image](https://user-images.githubusercontent.com/67455761/127777573-ceed4a21-5c29-4b60-9ce8-bb4e2accf2b5.png)

### 2) PFD layout

![image](https://user-images.githubusercontent.com/67455761/127777596-04855662-6ff3-49f8-a0ae-ff70ae753a8d.png)

### 3)Charge Pump layout

![image](https://user-images.githubusercontent.com/67455761/127777653-15f16b37-e166-46d4-8040-d5877c8614d6.png)

### 4)VCO layout

![image](https://user-images.githubusercontent.com/67455761/127777696-aaf96813-83cc-49ca-bb21-924416574191.png)


### 5)PFD Post layout simulation

![image](https://user-images.githubusercontent.com/67455761/127777907-abb55fac-1427-47ae-8f1b-f1ce4673dbcf.png)



### About Tapeout

Tapeout refers to the process of sending our design to the fab once it has been prepared with all of the additional assistance we need. First, we must link our silicon wafer to the outside world. We utilise I/O pads for this.

Then we should have designs for any type of serial communication, such as I2C, UART, and other peripherals. Memory must also be included, which takes up a lot of space. Mechanisms for testing should also be included. 

Taking care of all of this gets complex, therefore we need select a driver to enable our IP to fulfil the required standards for fabrication.

# Acknowledgement

1. I would like to thank Mr. Kunal Ghosh, co-founder [VSD](https://www.vlsisystemdesign.com/), for providing me with this wonderful 2-day workshop.

2. I would like to thank Ms. Lakshmi S, for guiding throughout the workshop about how to design PLL.


