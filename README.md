# Ham Satellite Automation Project

![License](https://img.shields.io/badge/license-MIT-green.svg)
![Platform](https://img.shields.io/badge/platform-Windows%2011-blue.svg)
![Automation](https://img.shields.io/badge/automation-PowerShell-blue)
![SDR](https://img.shields.io/badge/SDR-SDR++-orange)
![Status](https://img.shields.io/badge/status-Phase%201%20Foundation-yellow)
![Ham Radio](https://img.shields.io/badge/domain-Ham%20Radio-red)

------------------------------------------------------------------------

## Project Overview

Automated satellite reception framework using:

-   **SDR++**
-   **Gpredict**
-   **PowerShell**
-   **FFmpeg**
-   **VB-Audio Cable**
-   **MMSSTV / RX-SSTV**

Designed for modular, JSON-driven satellite behavior and clean Doppler
separation of responsibility.

------------------------------------------------------------------------

## 1. Project Goals

-   Gpredict controls Doppler and frequency via rigctl.
-   AOS triggers a PowerShell automation script.
-   Script loads satellite-specific JSON configuration.
-   Script sets SDR mode (FM / USB).
-   Script starts audio recording using FFmpeg.
-   Script optionally launches SSTV decoder.
-   LOS cleanly stops recording and decoder.
-   Logs are written for traceability.
-   System is modular and expandable.

------------------------------------------------------------------------

## 2. Architecture Overview

    Gpredict
       ├── Rigctl → SDR++ (frequency + doppler)
       └── AOS/LOS Event Hook → satellite_handler.ps1
                ├── Load JSON config
                ├── Set SDR mode via rigctl
                ├── Start/Stop FFmpeg recording
                └── Launch/Close SSTV software

Separation of responsibility:

  Component     Responsibility
  ------------- -------------------------------------
  Gpredict      Satellite tracking, Doppler, timing
  SDR++         RF front end and demodulation
  PowerShell    Automation logic
  JSON Config   Satellite-specific behavior

------------------------------------------------------------------------

## 3. Directory Structure

    C:\HamAutomation\
    │
    ├── satellite_handler.ps1
    ├── configs\
    │     ├── ISS.json
    │     └── ArcticSat.json
    │
    ├── recordings\
    ├── logs\
    └── tools\
          ├── ffmpeg.exe

------------------------------------------------------------------------

## 4. JSON Configuration Schema

### Example: ISS.json

``` json
{
  "mode": "FM",
  "bandwidth": 12000,
  "record": true,
  "sstv": false
}
```

### Example: ArcticSat.json

``` json
{
  "mode": "USB",
  "bandwidth": 2400,
  "record": true,
  "sstv": true,
  "decoder": "MMSSTV"
}
```

------------------------------------------------------------------------

## 5. Implementation Phases

### Phase 1 -- Foundation

-   Verify SDR++ rigctl server enabled.
-   Configure Gpredict radio control.
-   Confirm Doppler tracking works.
-   Create folder structure.

### Phase 2 -- Script Skeleton

-   Create `satellite_handler.ps1`
-   Accept parameters: Satellite + Event (AOS / LOS)
-   Load JSON config.
-   Add logging.
-   Manual execution test.

### Phase 3 -- Recording Automation

-   Install VB-Audio Cable.
-   Route SDR++ audio to VB-Cable.
-   Use FFmpeg to record.
-   Start on AOS, stop on LOS.
-   Timestamped filenames.

### Phase 4 -- Mode Switching

-   Use rigctl commands to set FM or USB.
-   Validate mode changes correctly.

### Phase 5 -- SSTV Integration

-   Launch MMSSTV on AOS if enabled.
-   Close on LOS.
-   Verify image decode.

### Phase 6 -- Hardening

-   PID tracking.
-   Lock files.
-   Structured logging.
-   Error handling.

------------------------------------------------------------------------

## 6. Future Enhancements

-   Add NOAA weather satellites.
-   Add APRS or telemetry decode.
-   Email decoded SSTV images.
-   NAS sync automation.
-   Highest elevation satellite auto-selection.

------------------------------------------------------------------------

## 7. Success Criteria

-   Zero manual interaction per pass.
-   Correct mode per satellite.
-   Clean recording lifecycle.
-   Stable SSTV decoding.
-   Easily extendable via JSON.

------------------------------------------------------------------------

**Generated:** 2026-02-22 20:08:15
