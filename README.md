# Circuit-Design-for-PLL-from-scratch-to-post-layout-simulation Design using SKY130nm-Technology
2 day workshop 31st July to 1st August

Here we have to learn to how we design a basic PLL circuit from scratch to post layout simulation.

PLL Specification

Technology - SKywater 130nm


Supply Voltage    - 1.8V


Process Corner    - TT


Temperature       - room temperature


Input Frequency(Fmin)   - 5Mhz, Fmax - 12.5Mhz


Multiplier -8x


Duty Cycle =50%


Jitter < 20ns



Overview 

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

Day 1 : PLL Theory and setup tools for simulation 
PLL Theory
Why PLL?
To get precise clock signal without frequency or phase noise.A PLL is a feedback system that compares the output phase with the input phase.
The comparison is performed by a "phase comparator".To arrive the concept of phase locking, let us consider the problem of aligning the output phase of VCO with the phase of a
reference clock.

Basic block diagram of PLL

![image](https://user-images.githubusercontent.com/67455761/127779269-1ab34b4f-a3df-48b1-90e8-58d3c3325e24.png)

PLL have five blocks

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



















Frequency Divider Circuit

![image](https://user-images.githubusercontent.com/67455761/127774410-63873540-d18c-4df7-bcd3-3c99e8342243.png)

Charge Pump Output

![image](https://user-images.githubusercontent.com/67455761/127776158-1fde4ddc-f5f6-4931-8546-be3689f09fbd.png)

Voltage Control Oscillator simultator Output

![image](https://user-images.githubusercontent.com/67455761/127776206-67bc2a17-cde5-4ab2-ad36-7f0ef047573a.png)

PFD simulator Output

![image](https://user-images.githubusercontent.com/67455761/127776406-b6cd0291-2ced-4c37-b707-3086fb1307e8.png)

PLL simulator OutPut
![image](https://user-images.githubusercontent.com/67455761/127777450-6f04f7f5-2298-4924-80e3-ce7c0f318064.png)


Layout
1) PFD layout

![image](https://user-images.githubusercontent.com/67455761/127777573-ceed4a21-5c29-4b60-9ce8-bb4e2accf2b5.png)

2)PFD layout

![image](https://user-images.githubusercontent.com/67455761/127777596-04855662-6ff3-49f8-a0ae-ff70ae753a8d.png)

3)Charge Pump layout

![image](https://user-images.githubusercontent.com/67455761/127777653-15f16b37-e166-46d4-8040-d5877c8614d6.png)

4)VCO layout

![image](https://user-images.githubusercontent.com/67455761/127777696-aaf96813-83cc-49ca-bb21-924416574191.png)


5)PFD Post layout simulation

![image](https://user-images.githubusercontent.com/67455761/127777907-abb55fac-1427-47ae-8f1b-f1ce4673dbcf.png)


























































