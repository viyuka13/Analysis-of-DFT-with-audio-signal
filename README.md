# EXP 1 B:  ANALYSIS OF DFT WITH AUDIO SIGNAL

# AIM: 

  To analyze audio signal by removing unwanted frequency. 

# APPARATUS REQUIRED: 
   
   PC installed with SCILAB/Python. 

# PROGRAM: 
```c
// -----------------------------------------------------
// EXP 1 : ANALYSIS OF DFT WITH AUDIO SIGNAL
// AIM: To analyze audio signal by removing unwanted frequency.
// -----------------------------------------------------

// ---------- READ AUDIO FILE ----------
[x, fs] = wavread("D:\SEM-3\DTSP\Exps\1B\input.wav");

// ---------- CONVERT TO MONO IF STEREO ----------
if size(x,2) == 2 then
    x = (x(:,1) + x(:,2)) / 2;  // average channels
end

// ---------- CREATE TIME AXIS ----------
N = length(x);
t = (0:N-1) / fs;

// ---------- PLOT ORIGINAL SIGNAL ----------
figure(1);
plot(t, x);
xlabel("Time (s)");
ylabel("Amplitude");
title("Original Audio Signal");

// ---------- COMPUTE DFT ----------
X = fft(x);
magX = abs(X);
f = (0:N-1) * (fs / N);

// ---------- PLOT MAGNITUDE SPECTRUM ----------
figure(2);
plot(f, magX);
xlabel("Frequency (Hz)");
ylabel("Magnitude");
title("Magnitude Spectrum");

// ---------- TOP 10 DOMINANT FREQUENCIES ----------
[sorted_vals, idx] = gsort(magX, "g", "i");

disp("Top 10 Dominant Frequencies:");
for k = 1:10
    freq = f(idx(k));
    mag = sorted_vals(k);
    mprintf("%0.2f Hz (Magnitude = %.2e)\n", freq, mag);
end

// ---------- SIMPLE LOW-PASS FILTER ----------
cutoff = 5000;   // frequency above this is removed
H = ones(X);      // filter mask

for k = 1:N
    if f(k) > cutoff then
        H(k) = 0;
    end
end

// ---------- APPLY FILTER ----------
X_filtered = X .* H;

// ---------- INVERSE FFT ----------
x_filtered = real(ifft(X_filtered));

// ---------- PLOT FILTERED SIGNAL ----------
figure(3);
plot(t, x_filtered);
xlabel("Time (s)");
ylabel("Amplitude");
title("Filtered Audio Signal");

// ---------- PLOT FILTERED MAGNITUDE SPECTRUM ----------
figure(4);
plot(f, abs(X_filtered));
xlabel("Frequency (Hz)");
ylabel("Magnitude");
title("Filtered Magnitude Spectrum");

```


# OUTPUT: 

<img width="825" height="400" alt="1" src="https://github.com/user-attachments/assets/afc87bf0-35c1-4e54-b121-2693e726c0c5" />


<img width="822" height="401" alt="3" src="https://github.com/user-attachments/assets/51f0a45a-3e38-4d1e-86d6-80681aaf17ff" />


Top 10 Dominant Frequencies:
  1) 2774.40 Hz (Magnitude = 4.44e-02)
      
  2) 45225.60 Hz (Magnitude = 4.44e-02)
      
  3) 2987.26 Hz (Magnitude = 6.77e-02)
      
  4) 45012.74 Hz (Magnitude = 6.77e-02)
      
  5) 3371.15 Hz (Magnitude = 7.18e-02)
      
  6) 44628.85 Hz (Magnitude = 7.18e-02)
      
  7) 4046.75 Hz (Magnitude = 8.68e-02)
  
  8) 43953.25 Hz (Magnitude = 8.68e-02)
  
  9) 3436.18 Hz (Magnitude = 9.23e-02)
  
  10) 44563.82 Hz (Magnitude = 9.23e-02)

# RESULTS
Hence analyze audio signal by removing unwanted frequency is sucessfully verified.
