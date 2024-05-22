
---------------------------------------------------------------------
An experimental multi channel CW decoder
---------------------------------------------------------------------

![overview](/skimmer-overview.png?raw=true)

Tuning to a CW transmission on shortwave is not always easy,
transmissions are (often very) short and by the time tuning
is correct, transmission stops.

This expeimental decoder takes a slightly different approach,
with an input rate of 192000 S/s, 500 FFT's per second  are taken
over the incoming samples.
The width of the FFT's is default 1024, such that each "bin" represents
the signal energy in a segment of app 192 Hz. 
The approach to CW decoding is now to consider the subsequent values in
a given bin as input, i.e. samples with a samplerate of 500.

The plugin shows 30 rows. The output of selected decoders is shown on
these rows, where row 16 corresponds to the selected frequency and
the output for the adjacent frequency ranges and centered around this bin.

User selection of the number of bins (i.e. CW decoders) is ny setting
a spinbox value.

--------------------------------------------------------------------------
A note on CW decoding
--------------------------------------------------------------------------

CW decoding needs a "decision maker" between signal or no signal.
The approach taken for the decoders in the plugin is to maintain
two estimated values, as can be guessed, the average value for "yes there
is signal" and "no there is no signal". In a noisy environment the
distinction between "signal" and "noise" is not always clear.

The plugin uses as default the arrival of "signal" is detected when
2/3 of the signal level of "yes there is a signal" is detected, and the
end of a period with signal is detected when the signal level is  down to
a fraction of the peak level.

The user may influence the detection of the start the the "signal" period,
by setting an additional value to indicates that the threshold is set to
the number of dB's as the value indicates.


------------------------------------------------------------------------
The plugin
-------------------------------------------------------------------------

The plugin is extremely simple, a single top line with a few
selectors and 32 lines, one for each bin - if selected.

![overview](/skimmer-1.png?raw=true)

The top line shows spinboxes for selection of the number of bins taken
into account, equally divided in bins below and above the
frequency of the center bin.  Up to 30 bins can be selected.

With the button next to the reset button a threshold - in dB's - can be set,
used to separate spaces from data.

The skimmer povides a choice between 3 widths of the bins. The input has a
samplerate of 192000, using an FFT width of 512 leads to a bin width
of app 375 Hz, an FFT width of 1024 to a bin width of 187, and an FFT width
of 2048 to a bin width of 93Hz.

Of course, a bin width of 375 Hz leads to a maximum span of app 11.5 Khz,
a bin width of 187 to app 5.6 KHz and a bin width of 93 to a span of app 3 KHz.

Finally, the resulting span is shown on the top line.

The test field shows, for the selected bins - 4 colums.
Next to the - inevitable - row number, the center frequency of the
corresponding bin is shown, the third column tells the estimated number of
"words per minute" (based on the PARIS encoding, and the fourth colums
tells the result of the decoding.

