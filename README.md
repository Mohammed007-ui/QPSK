# QPSK
# Aim
Write a Python program for the modulation and demodulation of QPSK.
# Tools required
Python 3.x

NumPy

Matplotlib

Scipy (optional for signal filtering)
# Program
```
import numpy as np
import matplotlib.pyplot as plt

# Input bits
bits = np.random.randint(0, 2, 100)

# QPSK Mapping: 00 -> 45°, 01 -> 135°, 11 -> 225°, 10 -> 315°
mapping = {
    (0, 0): (1/np.sqrt(2), 1/np.sqrt(2)),
    (0, 1): (-1/np.sqrt(2), 1/np.sqrt(2)),
    (1, 1): (-1/np.sqrt(2), -1/np.sqrt(2)),
    (1, 0): (1/np.sqrt(2), -1/np.sqrt(2))
}

# Modulation
I = []
Q = []
symbols = []
for i in range(0, len(bits), 2):
    b_pair = (bits[i], bits[i+1])
    i_val, q_val = mapping[b_pair]
    I.append(i_val)
    Q.append(q_val)
    symbols.append(complex(i_val, q_val))

# Plot Constellation Diagram
plt.figure(figsize=(6, 6))
plt.scatter(I, Q, color='blue')
plt.axhline(0, color='black', linewidth=0.5)
plt.axvline(0, color='black', linewidth=0.5)
plt.grid(True)
plt.title("QPSK Constellation Diagram")
plt.xlabel("In-phase (I)")
plt.ylabel("Quadrature (Q)")
plt.axis('equal')
plt.show()

# Demodulation
received_bits = []
for sym in symbols:
    angle = np.angle(sym)
    if -np.pi/4 <= angle < np.pi/4:
        received_bits += [1, 0]
    elif np.pi/4 <= angle < 3*np.pi/4:
        received_bits += [0, 1]
    elif angle >= 3*np.pi/4 or angle < -3*np.pi/4:
        received_bits += [0, 0]
    elif -3*np.pi/4 <= angle < -np.pi/4:
        received_bits += [1, 1]

# Accuracy
bit_errors = np.sum(bits != received_bits[:len(bits)])
print(f"Bit Errors: {bit_errors} / {len(bits)}")

```
# Output Waveform
```
![image](https://github.com/user-attachments/assets/cb3d6590-5460-4996-8f48-6389292afe3b)

```
# Results
```
The QPSK modulation and demodulation were successfully implemented. The constellation diagram shows four distinct points representing the four possible symbol states. The bit error rate depends on noise and simulation assumptions — here, no noise is added, so the demodulation is perfect.


```
