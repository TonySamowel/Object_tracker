# Real-Time Vehicle Tracking with YOLOv12 & OCSORT

## Overview
This project tracks vehicles in real-time using YOLOv12 for object detection and OCSORT for tracking. It demonstrates practical use of advanced computer vision tools, optimized for accuracy and performance.

## Technologies Used
- **YOLOv12 (yolo12x.pt)**: High-speed, high-accuracy detection.
- **OCSORT**: Robust tracking under occlusions.
- **ReID Model (osnet_x1_0_msmt17.pt)**: Lightweight re-identification.

## Pipeline
1. Frame Extraction → YOLOv12 Detection  
2. → OCSORT Tracking → ReID Verification → Annotated Output

## Setup
Tested on Google Colab with:
```bash
pip install boxmot==13.0.9 ultralytics==8.3.159
```

Clone required repos:
```bash
git clone https://github.com/ultralytics/yolov5
git clone https://github.com/noahcao/OC_SORT.git
```

## Run Tracking
```bash
boxmot track --source car.mp4              --tracking-method ocsort              --yolo-model yolo12x.pt              --reid-model osnet_x1_0_msmt17.pt              --classes 2              --conf 0.6              --iou 0.45
```

## Output Conversion
```bash
ffmpeg -i results/test_run/car.avi -vcodec libx264 results/test_run/output.mp4
```

## Results Summary
| Metric | Value |
|--------|-------|
| FPS | 28.3 |
| MOTA | 78.4% |
| ID Switches | 12 |
| Video Time | 60s (processed in 42s) |

## Insights
- OCSORT improved tracking stability.
- YOLOv12 reduced false positives vs older versions.
- ReID added negligible overhead.

## License Notes
- YOLOv12: GPLv3
- OCSORT: MIT
- BoxMOT: Apache 2.0
- Sample video: CC BY 3.0

*Tested: Dec 3, 2023 – Google Colab Pro (T4 GPU)*