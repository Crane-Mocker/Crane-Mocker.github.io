---
layout: post
title:  "High-Pass Filter"
date:   2024-11-23
categories: Digital Communication
---

# High-Pass Filter

## Low-Pass, High-Pass, Band-Pass, Band-Stop Filters

**Digital filters** are used for two general purposes: 

- separation of signals that have been combined, and 
- restoration of signals that have been distorted in some way. 

A **LPF (Low-pass filter)** only allows low frequencies to pass through.

![](https://www.electronicsforu.com/wp-contents/uploads/2017/11/low-pass-filter.jpg)

A **HPF (High-Pass Filter)** passes signals with a frequency higher than a certain **cutoff frequency** and attenuates signals with frequencies lower than the cutoff frequency.

![](https://www.electronicsforu.com/wp-contents/uploads/2017/11/high-pass-filter.jpg)

A **band-pass filter** is a combination of a HPF and an LPF. It allows only a selected range of frequencies to pass through.

![](https://www.electronicsforu.com/wp-contents/uploads/2017/11/BPF-ideal.jpg)

A **band stop filter**  blocks a selected range of frequencies.

## The Chebyshev Responses and Chebyshev Filters

**Attenuation**: a general term that refers to any **reduction** in the strength of a signal. Sometimes called **los**s, attenuation is a natural consequence of signal transmission over long distances.
**Roll-off**: a rate at which attenuation increases beyond the cutoff frequency. The steepness of the transition between the pass-band and stop-band.
**Ripple**: the maximum amplitude error of the filter in the passband in dB.

The **Chebyshev response** is a mathematical strategy for achieving a faster roll-off by allowing ripple in the frequency response. Analog and digital filters that
use this approach are called **Chebyshev filters**.

## Butterworth Filters

The Butterworth filter is a type of signal processing filter designed to have a frequency response that is as flat as possible in the passband. 

> An ideal electrical filter should not only completely reject the unwanted frequencies but should also have uniform sensitivity for the wanted frequencies

## Ref

https://en.wikipedia.org/wiki/High-pass_filter
https://www.analog.com/media/en/technical-documentation/dsp-book/dsp_book_Ch20.pdf
https://www.dspguide.com/
https://www.rfpage.com/low-pass-high-pass-and-band-pass-filters-simple-explanation/
https://www.electronicsforu.com/technology-trends/learn-electronics/band-stop-high-low-pass-filter
https://training.dewesoft.com/online/course/filters
https://www.techtarget.com/searchnetworking/definition/attenuation
https://ocw.mit.edu/courses/res-6-007-signals-and-systems-spring-2011/6ffe3f6c387555a8db26f1f3bbaddfb5_MITRES_6_007S11_lec24.pdf
https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.butter.html
https://en.wikipedia.org/wiki/Butterworth_filter