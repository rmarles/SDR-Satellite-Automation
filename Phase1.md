# Phase 1 -- Receive-Only NOAA APT Setup (RDP1B)

This phase configures a receive-only NOAA APT ground station using an
RDP1B SDR.

------------------------------------------------------------------------

## 1️⃣ Hardware Setup

1.  Connect antenna to the **RDP1B SMA input**
2.  Plug RDP1B into USB port
3.  Confirm device appears in SDR software

------------------------------------------------------------------------

## 2️⃣ SDR Software Configuration

Open SDR software (SDR++, SDR#, etc.) and configure:

**Device:** RDP1B\
**Sample Rate:** 2.048 MSPS (or stable default)\
**Gain:** Start \~30--40 dB (adjust later)\
**Mode:** WFM (Wide FM)\
**Bandwidth:** 40--50 kHz

------------------------------------------------------------------------

## 3️⃣ NOAA Frequency Reference

  Satellite   Frequency (MHz)
  ----------- -----------------
  NOAA 15     137.6200
  NOAA 18     137.9125
  NOAA 19     137.1000

Tune to one of these during a pass.

------------------------------------------------------------------------

## 4️⃣ Ground Station Settings (SatDump / Similar)

When adding the ground station:

**Radio Type:** RX Only\
**Device:** RDP1B\
**Location:** Your exact lat/long\
**Altitude:** Approximate is fine

------------------------------------------------------------------------

## 5️⃣ Add Satellite Module

When adding the satellite module:

**Satellite Code:**\
- NOAA-15\
- NOAA-18\
- NOAA-19

(Use the standard satellite name as listed in the software.)

------------------------------------------------------------------------

## 6️⃣ Confirm Signal During Pass

During a scheduled pass:

-   Tune to correct frequency\
-   Observe visible APT "striped" signal in waterfall\
-   Confirm audio demodulation\
-   Start recording/decoding

------------------------------------------------------------------------

## ✅ End of Phase 1

At this point, you should be able to:

-   Track NOAA satellites\
-   Receive APT signal\
-   Record raw pass data

Phase 2 will focus on automated decoding and image processing.
