
# Ex-07: Spectral Analysis, Spectral Density and Time-Invariant Linear Filters
## NAME : Sukhmeet Kaur G
## REG NO : 23050001032
## Aim
To perform spectral analysis on a simulated time series, identify dominant frequencies using a periodogram, apply a moving-average filter, and compare the spectral density before and after filtering.

## Objectives
1. To generate a time series containing multiple frequencies and random noise.
2. To calculate and plot the periodogram.
3. To identify the dominant frequency in the time series.
4. To apply a moving-average linear filter.
5. To compare the original and filtered time series.
6. To study the effect of changing the signal frequency, filter window size, and noise.
7. To observe the effect of adding another frequency component.

## Program

```python
# Step 1: Import Required Libraries
import numpy as np
import matplotlib.pyplot as plt
from scipy import signal

# Step 2: Generate Time Points
n = 500
t = np.arange(n)

# Step 3: Generate a Time Series with Two Frequencies and Noise
np.random.seed(42)

x = (
    np.sin(2 * np.pi * 0.05 * t)
    + 0.5 * np.sin(2 * np.pi * 0.20 * t)
    + 0.3 * np.random.randn(n)
)

# Step 4: Plot the Original Time Series
plt.figure(figsize=(10, 4))
plt.plot(t, x)
plt.title("Original Time Series")
plt.xlabel("Time")
plt.ylabel("Value")
plt.grid(True)
plt.show()

# Step 5: Calculate and Plot the Periodogram
frequency, power = signal.periodogram(x)

plt.figure(figsize=(10, 4))
plt.plot(frequency, power)
plt.title("Spectral Density of Original Time Series")
plt.xlabel("Frequency")
plt.ylabel("Power")
plt.grid(True)
plt.show()

# Step 6: Identify the Dominant Frequency
peak_index = np.argmax(power[1:]) + 1
dominant_frequency = frequency[peak_index]

print("Dominant Frequency:", dominant_frequency)

# Step 7: Apply a 5-Point Moving-Average Filter
window = 5
filtered = np.convolve(
    x, np.ones(window) / window, mode="same"
)

# Step 8: Compare Original and Filtered Time Series
plt.figure(figsize=(10, 4))
plt.plot(t, x, label="Original")
plt.plot(t, filtered, label="Filtered")
plt.title("Original vs Filtered Time Series")
plt.xlabel("Time")
plt.ylabel("Value")
plt.legend()
plt.grid(True)
plt.show()

# Step 9: Compare Spectral Density Before and After Filtering
f_original, p_original = signal.periodogram(x)
f_filtered, p_filtered = signal.periodogram(filtered)

plt.figure(figsize=(10, 4))
plt.plot(f_original, p_original, label="Original")
plt.plot(f_filtered, p_filtered, label="Filtered")
plt.title("Spectral Density Before and After Filtering")
plt.xlabel("Frequency")
plt.ylabel("Power")
plt.legend()
plt.grid(True)
plt.show()

# Step 10: Student Task 1 - Change Frequency from 0.05 to 0.10
x_task1 = (
    np.sin(2 * np.pi * 0.10 * t)
    + 0.5 * np.sin(2 * np.pi * 0.20 * t)
    + 0.3 * np.random.randn(n)
)

f_task1, p_task1 = signal.periodogram(x_task1)

plt.figure(figsize=(10, 4))
plt.plot(f_task1, p_task1)
plt.title("Task 1: Effect of Changing Frequency")
plt.xlabel("Frequency")
plt.ylabel("Power")
plt.grid(True)
plt.show()

# Step 11: Student Task 2 - Change Window Size to 10
window = 10
filtered_task2 = np.convolve(
    x, np.ones(window) / window, mode="same"
)

plt.figure(figsize=(10, 4))
plt.plot(t, x, label="Original")
plt.plot(t, filtered_task2, label="Filtered (Window = 10)")
plt.title("Task 2: Effect of Increasing Filter Window")
plt.xlabel("Time")
plt.ylabel("Value")
plt.legend()
plt.grid(True)
plt.show()

# Step 12: Student Task 3 - Generate a Signal Without Noise
x_task3 = (
    np.sin(2 * np.pi * 0.05 * t)
    + 0.5 * np.sin(2 * np.pi * 0.20 * t)
)

f_task3, p_task3 = signal.periodogram(x_task3)

plt.figure(figsize=(10, 4))
plt.plot(f_task3, p_task3)
plt.title("Task 3: Spectral Density Without Noise")
plt.xlabel("Frequency")
plt.ylabel("Power")
plt.grid(True)
plt.show()

# Step 13: Student Task 4 - Add Another Frequency Component
x_task4 = (
    np.sin(2 * np.pi * 0.05 * t)
    + 0.5 * np.sin(2 * np.pi * 0.20 * t)
    + 0.3 * np.sin(2 * np.pi * 0.30 * t)
    + 0.3 * np.random.randn(n)
)

f_task4, p_task4 = signal.periodogram(x_task4)

plt.figure(figsize=(10, 4))
plt.plot(f_task4, p_task4)
plt.title("Task 4: Spectral Density with an Additional Frequency")
plt.xlabel("Frequency")
plt.ylabel("Power")
plt.grid(True)
plt.show()
```

## Output
<img width="844" height="393" alt="image" src="https://github.com/user-attachments/assets/c983c379-51be-4bb3-8854-7746ab2728b9" />
<img width="850" height="393" alt="image" src="https://github.com/user-attachments/assets/dd9be462-708d-4a3b-bdca-84e925727f43" />
<img width="252" height="41" alt="image" src="https://github.com/user-attachments/assets/2cc298bb-af66-429c-98eb-a00a259880de" />
<img width="844" height="393" alt="image" src="https://github.com/user-attachments/assets/f14e7956-5ed4-45a8-a406-63c66b3eb590" />
<img width="850" height="393" alt="image" src="https://github.com/user-attachments/assets/4a77607f-54fa-4903-98da-e5e519f9f741" />
<img width="850" height="393" alt="image" src="https://github.com/user-attachments/assets/def5040d-4a15-4d08-8e13-7d0ee1242cc1" />
<img width="844" height="393" alt="image" src="https://github.com/user-attachments/assets/bba19733-e87f-43fd-8f20-da734dc13bb7" />
<img width="850" height="393" alt="image" src="https://github.com/user-attachments/assets/a868ce85-e9a2-45dc-a6cb-ef402ee98e56" />
<img width="850" height="393" alt="image" src="https://github.com/user-attachments/assets/f9c89c87-3f9a-4f44-ae58-c195b3a1b93a" />


## Result
Spectral analysis was performed successfully using the periodogram to identify dominant frequencies. A moving-average filter was applied to smooth the time series, and the spectral density before and after filtering was compared. The effects of changing frequency, removing noise, increasing the filter window, and adding another frequency component were studied.
