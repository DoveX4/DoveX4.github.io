---
date: 2025-03-16
draft: false
title: Note of Communication System | Chapter 0 Background and Preview
categories:
  - 通信原理
tags:
  - SNR
  - 通信网络
  - Shannon定理
---
# 1 The communication process
- **3 basic elements** to every communication system: ***transmitter***, ***channel***, and ***receiver***.![](attachments/0.1.1.png)
	- transmitter: message signal to transmitted signal
	- channel: the physical medium connecting the transmitter and receiver
	- receiver: received signal to original message signal

- **2 basic modes** of communication: ***broadcasting*** and ***point-to-point communication***
	- broadcasting: single transmitter to multiple receivers, unidirectional
	- point-to-point communication: single transmitter to single receiver, bidirectional (which requires the use of a transmitter and a receiver at each end of the link)
	- Remember the underlying communication process in any communication systems is ***statistical*** in nature
# 2 Primary communication resources
- **2 primary resources** employed in a communication system: ***transmitted power*** and ***channel bandwidth***, and so we may classify communication channels as *power limited* or *band limited*
	- transmitted power: the average power of the transmitted signal
	- channel band width: the band of frequencies allocated for the transmission of the message signal
		- When the spectrum of a message signal extends down to 0 or low frequencies, from a practical perspective, we define the bandwidth of the signal as that upper frequency. The spectral content of the signal above it is negligible and therefore unnecessary for transmitting information.
- A quantitative way to account for the effect of noise is to introduce ***signal-to-noise ratio (SNR)***$$\mathrm{SNR}(\mathrm{dB})=10\lg\frac{\mathrm{Average~signal~power}}{\mathrm{Average~noise~power}}$$
# 3 Sources of information
- **4 important sources of information**: ***speech***, ***music***, ***pictures***, and ***computer data***
	- Speech and Music: Notice the sound signal is bipolar
- *A signal* is defined as a single-valued function of *time* which is the independent variable
# 4 Communication networks
![](attachments/0.4.1.png)
- In this book, we rarely care about this part, so skip this section for just one figure.
# 5 Communication channels
- We may distinguish **2 basic groups** of communication channels: channels based on ***guided propagation*** and channels based on ***free propagation***.
	- guided propagation: telephone channels, coaxial cables, and optical fibers
		- In telecommunications, ***insertion loss*** is the loss of signal power resulting from the insertion of a device in a transmission line or optical fiber and is usually expressed in decibels. It is defined as $$\mathrm{insertion~loss}(\mathrm{dB})=10\lg(\frac{P_0}{P_L})$$in which $P_L$ refers to the power delivered to a load from a source via the channel, and $P_0$ refers to the power delivered to the same load **when it is connected directly** to the source
	- free propagation: wireless broadcast channels, mobile radio channels, and satellite channels
# 6 Modulation process
***Modulation*** is the process that the transmitter modifies the message signal into a form suitable for transmission over the channel. The classification of modulation types is as follows.
- Continuous-wave modulation (CW): often uses a sinusoidal wave as the carrier
	- Amplitude modulation (AM)
	- Angle modulation
		- Frequency modulation (FM)
		- Phase modulation (PM)
- Pulse modulation
	- Analog pulse modulation (corresponding to CW)
		- Pulse-amplitude modulation (PAM)
		- Pulse-duration modulation (PDM)
		- Pulse-position modulation (PPM)
	- Pulse-code modulation (PCM) (the digital form of pulse modulation)
Among all the different modulation schemes, PCM has emerged as the preferred method of modulation for the transmission of analog message signals for its robustness, flexibility, common integration format, and security.

In using the method of modulation, we are able to combining several message signals for their simultaneous transmission over the same channel, which is called ***multiplexing***. The 3 commonly used methods of multiplexing are as follows.
- Frequency-division multiplexing (FDM)
- Time-division multiplexing (TDM)
- Code-division multiplexing (CDM)
# 7 Analog and digital types of communication
This figure has described the case of digital communication system clearly.
![](attachments/0.7.1.png)
Different from the relatively superficial changes to the message signal in analog communication, digital communication endeavors to find a finite set of waveforms closely matched to the characteristics of the channel and decreasing the channel impairments.
# 8 Shannon's information capacity theorem
The ***information capacity theorem*** is $$C=B\log_2 (1+\mathrm{SNR})$$where $C$ (bit/s) is the information capacity of the channel, namely the maximum rate at which information can be transmitted across the channel **without error**, $B$ is the channel bandwidth, $\mathrm{SNR}$ is not in decibels here.

On this basis, we may use the ratio $$\eta=\frac{R}{C}$$as a measure of the efficiency of the digital communication system, where $R$ is the actual  signaling rate.
