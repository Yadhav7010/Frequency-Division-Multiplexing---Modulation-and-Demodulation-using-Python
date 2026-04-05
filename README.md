# SIMULATION OF FREQUENCY DIVISION MULTIPLEXING (FDM) AND DEMULTIPLEXING USING SCILAB
### AIM:

To write a Scilab program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.

---

### EQUIPMENTS Needed

Computer with Scilab installed


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
t = linspace(0, 1, 1000);
fs = 1000; 

freqs = [4, 8, 12, 16, 20, 24];

signals = zeros(6, length(t));
for i = 1:6
    signals(i, :) = sin(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
    fdm_signal = fdm_signal + signals(i, :);
end

order = 50;
cutoff_freq = 8 / (fs/2); 
h = ffilt("lp", order, cutoff_freq);

demux_signals = zeros(6, length(t));
for i = 1:6
    mixed = fdm_signal .* sin(2 * %pi * freqs(i) * t);
    demux_signals(i, :) = filter(h, 1, mixed);
end

scf(1);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, signals(i, :));
    title('Original Signal f=' + string(freqs(i)));
end

scf(2);
clf;
plot(t, fdm_signal);
title('FDM Signal');

scf(3);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, demux_signals(i, :));
    title('Demultiplexed Signal f=' + string(freqs(i)));
end

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

The program successfully simulates FDM and demultiplexing for multiple frequency signals with filtering to recover original signals accurately in Scilab.
