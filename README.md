This spectrum analyzer project was done using STM32F407VGT MCU, STM32F4 Dicovery + Open407V-D boards and SSD1289 touchscreen display.
There are three ADCs in the STM32F407VGT MCU whose individual upper sampling rates are 2.4 and 3.2 MSPS respectively for 12bit and 8bit modes.
The ADCs can also be used in interleaved mode and up to 9.6MSPS sampling rate can be achieved. 
Since the sampling rate is equal to Nyquist–Shannon frequency of the spectrum analyzer, the highest allowable frequency component in the input signal is half of the sampling rate.
With the current setting in the code, an ADC module is individually used at 2MSPS sample rate at most and therefore, the highest frequency band of the input signal is 1MHz. Frequency band of the signal spanning from 400Hz to 1MHz is changed by two soft buttons on the touchscreen.
Amplitude of the signal is shown in mili Volt scale, but it can be also converted to dB-mV scale after getting logarithm of the FFT results.

Currently the project lacks an active anti aliasing filter to remove frequencies higher than the highest allowable frequency and its details will be uploaded later. Moreover, since characteristics of the anti-aliasing filter change for each different upper frequency selection and it is hard to modify an external hardware analog filter, adjustable FIR or IIR low pass filtering should be applied with a constant sampling rate. This will be also done next.

In the "photos" folder there are some taken photograps where you can see how the analyzer looks. Unfortunately, I currently do not have a nice signal generator to show some results, but for the photos I exploited the 50Hz grid noise in the air by touching the input :) . In the relevant photo, you will see the 50Hz, 150Hz and 250Hz components meaning that center, 3rd and 5th harmonics are active. This occurs because the ADC is single ended without mid-reference biasing, accepts signals with amplitudes between 0 and 3 Volts and cuts negative side of the sampled signal. Therefore, the ADC only samples positive side of the 50Hz sine signal which only has odd numbered harmonic components.