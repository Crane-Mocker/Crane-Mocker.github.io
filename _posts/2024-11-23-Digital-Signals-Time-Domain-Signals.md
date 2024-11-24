---
layout: post
title:  "Time-Domain Signals"
date:   2024-11-23
categories: Digital Communication
---

# Digital Signals Theory: Time-Domain Signals

[Digital Signal Theory](https://brianmcfee.net/dstbook-site/content/intro.html) learning notes.

## Signals

$x$ is always used to refer to signals.

- $x(t)$ denotes a **continuous-time signal**. $t$ can be any real number.
- $x[n]$ denotes a **discrete-time signal**. $n$ must be an integer.
- $x(t) \leftrightarrow X(f)$ denotes the Fourier Transform of $x(t)$.

Signal processing, for example, applying a low-pass filter to remove hight frequenct content, can be thought as applying **function $g$** to an **input signal $x$** to produce an **output signal $y$**: $y = g(x)$.

### Standard conventions

Input signals: $x(t)$
Output signals: $y(t)$

time: $t$
discrete quantities: $n$, $m$, or $k$. Those are measured from $0$. A sequence of length $N$ is indexed by $n = 0, 1, \ldots, N-1$.
Unless otherwise stated, we will by default assume that signals are 0-valued when $t$ or $n$ are negative.

![](https://brianmcfee.net/dstbook-site/_images/bf6db09349b4c4500caefee2f17d5714ec1cb268b124a817605730cd349bcdca.svg)

Angles: $\theta$ or $\phi$, measured in radians. (e.g. $2\pi$ radians is one full rotation)

$j$ is the imaginary unit, $j^2 = -1$. (Mathematicians use $i$ instead of $j$)

Complex numbers, with a real and imaginary component, will be denoted by $z$ or $\omega$.

### Periodicity and waves

A signal $x(t)$ is **periodic** if there exists some finite $t_0 \gt 0$ such that $x(t + t_0) = x(t)$ for all $t$.
$t_0$: **fundamental period** of signal $x$

If a signal doesn't have a fundamental period, it is **aperiodic**.

The idea of periods provides a natural way to think about the **frequency**: how many cycles does a signal complete in one second?
If a signal $x(t)$ has a fundamental period $t_0$, then the **fundamental frequency** of the signal is $f_0 = 1/t_0$.
Frequency is measured in **Hertz (Hz)**, which 1 Hz is one cycle per second.
If a signal is aperiodic, and has $t_0 = \infty$, then its fundamental frequency is denoted to be $f_0 = 0$.

**Waves** is often used synonymously with the more specific **sinusoids**.
What makes sinusoids special? Rotation models repetition, and sinusoids are the simplest signals that repeat themselves.

Every wave can be expressed in the standardized form: $x(t) = A \cos(2\pi \cdot f \cdot t + \phi)$

```python
import numpy as np

'''
t: time in seconds (real number)
amplitude: amplitude scaling (real number)
frequency: cycles per second (real number)
phase: phase offset in radians (real number)
'''

def x(t, amplitude, frequency, phase):
    return amplitude * np.cos(2 * np.pi * frequency * t + phase)
```

- $A$: amplitude, how high it can rise or fall from 0. Changing $A$ will stretch or compress the wave vertically.
- $f$: frequency, how many cycles it completes in one second. Changing $f$ will stretch or compress the wave horizontally.
- $\phi$: the **phase** offset of the wave, the starting position (in radians) at time $t = 0$. Changing $\phi$ will shift the wave left or right.

The cosine function has a horizontal **symmetry**: $cos(\theta) = cos(-\theta)$. This means that the cosine wave is **even** (sometimes called an **even function**).
The sine function is horizontal **antisymmetric**: $sin(-\theta) = -sin(\theta)$.

Every cosine can be express as a sine with an appropriate phase offset, and vice versa.
$sin(\theta) = cos(\pi/2 - \theta)$
$cos(\theta) = sin(\pi/2 - \theta)$

## Digital sampling

The basic scheme for **digitizing** an **analog signal** is to measure the signal $x(t)$ at a sequence of uniformly spaced time points.
$t_s$: **sampling period**, measuing the number of seconds between each sample. Must be positive.
The resulting sequence of samples will be: $x(0), x(t_s), x(2t_s), \ldots$
The n-th sample represents the signal at time $n \cdot t_s$. $x[n] = x(n \cdot t_s)$

![](https://brianmcfee.net/dstbook-site/_images/ed42949307d30d1ce6c83eabf49be9980cdbd746e1cb8a6dcfd649d9ddd09527.svg)

$x[n]$ is a **discrete-time signal** (or **discrete signal**).

### Tone generation

A wave (idealized signal) at frequency $f_0$ is expressed as a function of time $t$ by $x(t) = \cos(2\pi \cdot f_0 \cdot t)$.
The idealized signal can be sampled by substituting $t = n / f_s$. $x[n] = \cos(2\pi \cdot f_0 \cdot n / f_s)$

```python
for n in range(N):
    x[n] = np.cos(2 * np.pi * f0 * n / fs)
```

A faster way is to pre-allocate all values of $n$ as a vector, `n = [0, 1, 2, ..., N-1]`:

```python
n = np.arange(N)
x = np.cos(2 * np.pi * f0 * n / fs)
```

Sample a pure tone at 220 Hz, with a sampling rate 8 kHz, for 1.5 seconds:

```python
import numpy as np
from IPython.display import Audio

fs = 8000
duration = 1.5
N = int(fs * duration)

f0 = 220
n = np.arange(N)
x = np.cos(2 * np.pi * f0 * n / fs)
Audio(x, rate=fs)
```

### Aliasing

**Aliasing** is the phenomenon where two distinct continuous signals $x_1(t)$ and $x_2(t)$ produce the same sequence of sample values $x[n]$.

----------
Theorem (Aliasing):

Given a sampling rate $f_s$, two frequencies $f$ and $f'$ are aliases of each other if for some integer $k$,
$f' = f + k \cdot f_s$

If sampled at rate $f_{s'}$ two waves $x$ (at frequency $f$) and $y$ (at frequency $f'$)
$x[n] = A \cdot \cos(2\pi \cdot f \cdot n / f_s + \phi)$
$y[n] = A \cdot \cos(2\pi \cdot f' \cdot n / f_s + \phi)$

will produce identical samples: $x[n] = y[n]$ for all $n$.

--------

Aliasing is unavoidable when sampling: there will always be frequencies that look the same after sampling. The consequence of aliasing is that once you've sampled a signal, you may not be able to determine the frequency of the original signal.

Within the context of audio, one of the most important applications of aliasing is Fast Fourier Transform (FFT) algorithms.

### The Nyquist-Shannon sampling theorem

Under mild conditions, every continuous signal can be expressed as a **combination of sinusoids**.

$x(t) = A_1 \cdot \cos(2\pi \cdot f_1 \cdot t + \phi_1) + A_2 \cdot \cos(2\pi \cdot f_2 \cdot t + \phi_2) + \ldots$

When sampling a signal to produce $x[n]$:

$x[n] = A_1 \cdot \cos(2\pi \cdot f_1 \cdot n / f_s + \phi_1) + A_2 \cdot \cos(2\pi \cdot f_2 \cdot n / f_s + \phi_2) + \ldots$

A signal $x(t)$ is **bandlimited** if it can be expressed as a combination (weighted sum) of pure sinuoids, whose frequencies lie between $f_{-}$ and $f_{+}$.
The **bandwidth** of the signal is $f_{+} - f_{-}$, representing the size of the band of frequencies.

The basic idea of Nyquist-Shannon theorem is that the sampling rate $f_s$ is sufficiently large compared to the bandwidth of the signal, then aliasing can't hurt us: aliases must have zero amplitude.

----------
Theorem (Nyquist-Shannon):
If $x(t)$ band-limited to the range $f_{-} \ldots f_{+}$, then any sampling rate $f_s \ge f_{+} - f_{-}$ is sufficient to prevent aliasing.

---------

The Nyquist-Shannon theorem tells us how to choose a sampling rate. In hardware analog-to-digital converters (ADCs), to ensure that $x(t)$ is band-limited, an analog filter is used to filter the continuous signal and remove any frequencies above $f_{+}$ before sampling.

Intuitively, we set $f_{-} = 0$ and $f_{+}$ to be the maximum frequency. However, this approach won't work. For example, any wave with a negative frequency can be equivalently represneted as a wave with positive frequency and a different phase, and produce identical signals.
For cosine waves, $\cos(-\theta) = \cos(\theta)$, it implies $\cos(2\pi \cdot (-f) \cdot t + \phi) = \cos(2\pi \cdot f \cdot t - \phi)$.
For sine wave, $\sin(-\theta) = -\sin(\theta) = \sin(\theta -\pi)$, it implies $\sin(2\pi \cdot (-f) \cdot t + \phi) = \sin(2\pi \cdot f \cdot t + \pi - \phi)$.

If we wanted to filter out negative frequencies (i.e., set $f_{-} = 0$), then we must necessarily also filter out positive frequencies as well, because $f$ and $-f$ are indistinguishable from each other.

The symmetry argument above tells us that we must have $f_{-} = -f_{+}$, which leads to the more common formula for sampling rate in the Nyquist-Shannon theorem:
$f_s \ge 2 \cdot f_{+}$
Because $f_{+} - f_{-} = 2 \cdot f_{+}$

For a fixed sampling rate $f_s$, the highest frequency that can be measured without aliasing artifacts is $f_s / 2$, known as the **Nyquist frequency**.

### Quantization

Digitized audio has two properties: **sampling rate** and **precision**.

**Two's complement**: the most common way to represent signed integers on computers.
For example, to calculate decimal number $-6$ in binary from $6$:
(1) $+6$ in decimal is $0110$ in binary. The leftmost bit (the first $0$) is the sign bit.
(2) Flip all bits: $1001$
(3) Add $1$: $1001 + 1 = 1010$
To verifiy $1010$ has the value of $-6$: $-1 \times 2^3 + 0 \times 2^2 + 1 \times 2^1 + 0 \times 2^0 = -6$

**Precision**, also known as **bit depth**, refers to how many *bits* are used to represent each sample in a digital signal.
We typically think of signals as taking on continuous real values, but computers **quantize** these values to be drawn from a fixed, finite set of numbers.

High precision -> more distinct values -> can represent smaller differences -> get a more accurate representation of the continuous signal
The cost: storing and transmitting more data

Fundamentally, quantization reduces the number of distinct values that can be observed in a signal.

Voltages in the range [-V, +V]
For uniform quantization into n-bit integer representation, we have $2^n$ distinct numbers.
If $q$ represents an n-bit quantized integer value $-2^{n-1} \le q \le 2^{n-1} - 1$, then we can map $q$ to a value $v(q)$:
$v(q) = V \cdot (q / 2^{n-1})$
This process is lossy, in that not every continuous input value can be realized by a specific quantized number $q$.
This fact rases the question: how accurate the quantization is?

One commonly used method to evaluate a quantization scheme is to measure its **dynamic range**: the ratio of its loudest value $v_{+}$ to its quietest (non-zero) value $v_{-}$, measured in decibels (dB).
To compute dynamic range $R_{dB}$ for quantized voltages, we need to square them:
$R_{dB} = 10 \cdot \log_{10}(v_{+} / v_{-})^2 = 20 \cdot \log_{10}(v_{+} / v_{-})$
We'll need to calculate the smallest and largest (absolute) values:
The smallest values is attained by $q=1$: $v_{-} = v(1) = V / 2^{n-1}$
The largest value is attained by $q=-2^{n-1}$: $v_{+} = |v(-2^{n-1})| = V(2^{n-1}/2^{n-1}$ 
So, $v_{+} / v_{-} = 2^{n-1}$ (Common factor: $V / 2^{n-1}$)
So $R_{dB} = 20 \cdot \log_{10}(2^{n-1}) = (n-1) \cdot 20 \log_{10}(2) \approx (n-1) \cdot 6.02 [dB]$

Most computers use **floating point** representation for numerical data, and have dedicated hardware for carrying out mathematical operations. Floating point numbers are still technically quantized, but the quantization level is so small that we treat them as though they were not quantized.



