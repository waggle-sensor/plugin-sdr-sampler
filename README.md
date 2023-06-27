# Sage-Waggle Plugin for RTL-SDR 

The plugin-sdr-sampler consists of several Python scripts that work together to process data from an RTL-SDR (Software-Defined Radio) device. Let's describe each script and its variables:

1. detection.py:
 Variables are:
`Thresh` - The noise threshold that determines what anomalies are worth saving. Noise usually sits below .15 in amplitude. 
samp_rate - The sample rate of the program. Determines how fast data is processed and recorded. 
`Location` - determines the location where the .wav file and .txt file are saved. Event.py and stall_gate.py also contain file paths that may need to be updated to match this one.
`freq` - this is the center frequency that the SDR is recording. 

`detection.py` takes input data from and RTL-SDR. This data is then put down 2 paths: one on a several second delay and the other in real time. The one in real time's amplitude is monitored, whenever its amplitude excedes the threshhold value the program begins recording the delayed data stream. This will capture the moments leading up to and following the anomaly. This data is then stored in a .wav file containing only the important data.

2. epy_block_0_2_0_0_0.py:

Binary gate has 2 inputs. complex data and byte data. This gate only allows the complex data to flow through if the byte input is recieving 1s

3. epy_block_1_0_0_0.py:

`stall_gate` outputs 0 bytes until it recieves a signal of 1. No matter the legth of the 1 signal the gate outputs 1 for approximatly 10 seconds.

