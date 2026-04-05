# SIMULATION OF FREQUENCY DIVISION MULTIPLEXING (FDM) AND DEMULTIPLEXING USING SCILAB
### AIM:

To write a PYTHON program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.

---

### EQUIPMENTS Needed

Computer with COLAB

---
### ALGORITHM

Define six different frequencies to generate six sine wave signals.

Generate the time vector to represent time samples.

Compute six sine signals for each frequency over the time vector.

Frequency Division Multiplexing: sum all six sine signals to make one multiplexed signal.

Frequency Division Demultiplexing: for each frequency, multiply the multiplexed signal by a sine wave of that frequency (mixing), then apply a lowpass filter to extract the baseband (original) signal.

Plot original signals, multiplexed signal, and demultiplexed signals for verification.


---
### PROGRAM

```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import firwin, lfilter

# Time and sampling
t = np.linspace(0, 1, 1000)
fs = 1000  

# Frequencies
freqs = [4, 8, 12, 16, 20, 24]

# Generate signals
signals = np.zeros((6, len(t)))
for i in range(6):
    signals[i, :] = np.sin(2 * np.pi * freqs[i] * t)

# FDM signal (sum of all signals)
fdm_signal = np.sum(signals, axis=0)

# Low-pass filter design (FIR)
order = 50
cutoff_freq = 8 / (fs / 2)  # normalized cutoff
h = firwin(order + 1, cutoff_freq)

# Demultiplexing
demux_signals = np.zeros((6, len(t)))
for i in range(6):
    mixed = fdm_signal * np.sin(2 * np.pi * freqs[i] * t)
    demux_signals[i, :] = lfilter(h, 1.0, mixed)

# Plot original signals
plt.figure(1)
for i in range(6):
    plt.subplot(3, 2, i+1)
    plt.plot(t, signals[i, :])
    plt.title(f'Original Signal f={freqs[i]} Hz')
plt.tight_layout()

# Plot FDM signal
plt.figure(2)
plt.plot(t, fdm_signal)
plt.title('FDM Signal')

# Plot demultiplexed signals
plt.figure(3)
for i in range(6):
    plt.subplot(3, 2, i+1)
    plt.plot(t, demux_signals[i, :])
    plt.title(f'Demultiplexed Signal f={freqs[i]} Hz')
plt.tight_layout()

plt.show()

```


---
### GRAPH:

<img width="1915" height="901" alt="image" src="https://github.com/user-attachments/assets/2d1568ef-ed4a-4499-828f-d4928e1800a7" />
<img width="1648" height="804" alt="image" src="https://github.com/user-attachments/assets/7c8ea91b-075f-48fa-a5f4-1a206c26613b" />
<img width="1919" height="909" alt="image" src="https://github.com/user-attachments/assets/38da7fb9-924a-42eb-a5c6-2555e11b7aa5" />

---

### TABULATION:
<img width="948" height="1280" alt="image" src="https://github.com/user-attachments/assets/b86619a3-7d07-42f4-8c0d-8657c39cd4be" />
<img width="997" height="1164" alt="image" src="https://github.com/user-attachments/assets/04ac7e48-3402-443a-8375-98b45463830b" />


---

### RESULTS:

The program successfully simulates FDM and demultiplexing for multiple frequency signals with filtering to recover original signals accurately in PYTHON
