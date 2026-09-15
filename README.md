# EXP 4 B : Design-of-FIR-Filters-using-Hamming-window
#          DESIGN OF FIR DIGITAL FILTERS USING HAMMING WINDOW
# AIM: 
          
  To generate design of FIR digital filters using Hamming Window using SCILAB 

# APPARATUS REQUIRED: 

  PC Installed with SCILAB 

# PROGRAM for LPF,HPF,BPF, BSF
```
clc;
clear;
close;

// Specifications
N = 21;
M = 10;

fc = 0.3;
f1 = 0.2;
f2 = 0.5;

// Column vector
n = (0:N-1)';

// Hamming Window
w = 0.54 - 0.46*cos(2*%pi*n/(N-1));

hLP = zeros(N,1);

for k = 1:N
    if n(k) == M then
        hLP(k) = fc;
    else
        hLP(k) = sin(%pi*fc*(n(k)-M)) / ...
                 (%pi*(n(k)-M));
    end
end

hLP = hLP .* w;

hHP = zeros(N,1);

for k = 1:N
    if n(k) == M then
        hHP(k) = 1-fc;
    else
        hHP(k) = -sin(%pi*fc*(n(k)-M)) / ...
                 (%pi*(n(k)-M));
    end
end

hHP = hHP .* w;

hBP = zeros(N,1);

for k = 1:N
    if n(k) == M then
        hBP(k) = f2-f1;
    else
        hBP(k) = (sin(%pi*f2*(n(k)-M)) - ...
                  sin(%pi*f1*(n(k)-M))) / ...
                  (%pi*(n(k)-M));
    end
end

hBP = hBP .* w;

hBS = zeros(N,1);

for k = 1:N
    if n(k) == M then
        hBS(k) = 1-f2+f1;
    else
        hBS(k) = (sin(%pi*f1*(n(k)-M)) - ...
                  sin(%pi*f2*(n(k)-M))) / ...
                  (%pi*(n(k)-M));
    end
end

hBS = hBS .* w;

disp(hLP,"LPF Coefficients =");
disp(hHP,"HPF Coefficients =");
disp(hBP,"BPF Coefficients =");
disp(hBS,"BSF Coefficients =");

scf(1);
clf();

subplot(2,2,1);
plot2d3(n,hLP);
xtitle("FIR LPF - Hamming Window","n","h(n)");
xgrid();

subplot(2,2,2);
plot2d3(n,hHP);
xtitle("FIR HPF - Hamming Window","n","h(n)");
xgrid();

subplot(2,2,3);
plot2d3(n,hBP);
xtitle("FIR BPF - Hamming Window","n","h(n)");
xgrid();

subplot(2,2,4);
plot2d3(n,hBS);
xtitle("FIR BSF - Hamming Window","n","h(n)");
xgrid();

xLP = zeros(1024,1);
xHP = zeros(1024,1);
xBP = zeros(1024,1);
xBS = zeros(1024,1);

xLP(1:N) = hLP;
xHP(1:N) = hHP;
xBP(1:N) = hBP;
xBS(1:N) = hBS;

HLP = fft(xLP,1);
HHP = fft(xHP,1);
HBP = fft(xBP,1);
HBS = fft(xBS,1);

f = (0:511)'/512;

magLP = abs(HLP(1:512));
magHP = abs(HHP(1:512));
magBP = abs(HBP(1:512));
magBS = abs(HBS(1:512));

scf(2);
clf();

subplot(2,2,1);
plot(f,magLP);
xtitle("LPF Frequency Response","Frequency / pi","Magnitude");
xgrid();

subplot(2,2,2);
plot(f,magHP);
xtitle("HPF Frequency Response","Frequency / pi","Magnitude");
xgrid();

subplot(2,2,3);
plot(f,magBP);
xtitle("BPF Frequency Response","Frequency / pi","Magnitude");
xgrid();

subplot(2,2,4);
plot(f,magBS);
xtitle("BSF Frequency Response","Frequency / pi","Magnitude");
xgrid();

```
# OUTPUT for LPF,HPF,BPF, BSF

<img width="1917" height="1198" alt="image" src="https://github.com/user-attachments/assets/2aa19041-46d0-4ef1-b96d-ffc5d05d9280" />

<img width="1917" height="1198" alt="image" src="https://github.com/user-attachments/assets/ffc6d65e-6bfc-4d86-ab52-a58ed2388bb6" />

# RESULT

The design of FIR filters using Hamming Window is successfully completed using SCILAB.
