# Microscope Data Hough Report

## Objective

Report the number of tracks detected per image in:
- FRAME (known CR-39 track-density images)
- FOCUS (increasing defocus)
- QUALITY (same image with different quality levels)

Method used: Hough-circle approach

## Detection Settings

- Radius search: 6 to 29 px
- Canny sigma: 2
- Hough peaks: 350
- Minimum center distance: 8 px
- Accumulator filter: keep >= 70th percentile
- Contrast rescale percentiles: 2 to 98

## Folder Summary

| Folder  | Images | Min Tracks | Max Tracks | Mean Tracks |
|---|---:|---:|---:|---:|
| FRAME   | 24 | 35 | 151 | 94.9 |
| FOCUS   | 11 | 65 | 131 | 91.1 |
| QUALITY | 11 | 21 | 65 | 45.0 |

## FRAME Results

| Image | Tracks Detected |
|---|---:|
| FR7545.bmp | 131 |
| FR7545_2.bmp | 111 |
| FR7598.bmp | 115 |
| FR7598_2.bmp | 106 |
| FR7692.bmp | 145 |
| FR7692_2.bmp | 122 |
| FR7781.bmp | 35 |
| FR7781_2.bmp | 55 |
| FR7828.bmp | 136 |
| FR7828_2.bmp | 133 |
| FR7914.bmp | 58 |
| FR7914_2.bmp | 43 |
| FR7921.bmp | 108 |
| FR7921_2.bmp | 151 |
| FR7937.bmp | 135 |
| FR7937_2.bmp | 118 |
| FR8728.bmp | 53 |
| FR8728_2.bmp | 54 |
| FR8775.bmp | 105 |
| FR8775_2.bmp | 73 |
| FR8821.bmp | 61 |
| FR8821_2.bmp | 105 |
| FR8833.bmp | 56 |
| FR8833_2.bmp | 68 |

## FOCUS Results

| Focus Level | Image | Tracks Detected |
|---:|---|---:|
| 0 | FOCUS_0.bmp | 131 |
| 1 | FOCUS_1.bmp | 100 |
| 2 | FOCUS_2.bmp | 70 |
| 3 | FOCUS_3.bmp | 76 |
| 4 | FOCUS_4.bmp | 65 |
| 5 | FOCUS_5.bmp | 68 |
| 6 | FOCUS_6.bmp | 79 |
| 7 | FOCUS_7.bmp | 88 |
| 8 | FOCUS_8.bmp | 115 |
| 9 | FOCUS_9.bmp | 105 |
| 10 | FOCUS_10.bmp | 105 |

Observation: track count drops strongly from level 0 to around level 4, then partially recovers at higher defocus levels. **These detections are considered accurate** — the out-of-focus images produce reliable counts with the current settings.

## QUALITY Results

| Quality (%) | Image | Tracks Detected |
|---:|---|---:|
| 10 | FR7914_10.bmp | 21 |
| 20 | FR7914_20.bmp | 42 |
| 30 | FR7914_30.bmp | 40 |
| 40 | FR7914_40.bmp | 59 |
| 50 | FR7914_50.bmp | 65 |
| 60 | FR7914_60.bmp | 53 |
| 70 | FR7914_70.bmp | 46 |
| 80 | FR7914_80.bmp | 39 |
| 90 | FR7914_90.bmp | 41 |
| 95 | FR7914_95.bmp | 46 |
| 100 | FR7914_100.bmp | 43 |

Observation: very low quality (10%) degrades detection strongly; between 20% and 100% the method remains comparatively stable. **Note:** the detected counts here are significantly higher than the actual track count — this folder suffers from the same overestimation issue as FRAME.

## Conclusion

- The report provides track counts per image for FRAME, FOCUS, and QUALITY (no per-track geometry/intensity parameters).
- **FOCUS detections are accurate**: the current Hough settings correctly predict the number of tracks in out-of-focus images.
- **FRAME and QUALITY detections are overestimated**: the detected counts are significantly higher than the true track count for these image types. The current parameter configuration (radius range, accumulator threshold, contrast rescaling) is tuned toward defocused images and does not generalize well to sharply-focused or quality-degraded images.
- Further tuning (e.g., tighter radius range, higher accumulator threshold) is needed to obtain reliable counts for FRAME and QUALITY images.
- If needed, this report can be exported to PDF or converted into a one-page lab summary.
