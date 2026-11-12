# Oil Palm Fruit Ripeness Detection (YOLOv5)

Detects oil palm **fresh fruit bunches (FFB / TBS)** in images, video or a webcam stream and classifies their ripeness, using a YOLOv5s model fine-tuned on oil palm bunch images. Grading ripeness consistently matters at harvest and at the mill, because it affects oil yield and quality.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![YOLOv5](https://img.shields.io/badge/Ultralytics-YOLOv5-111F68?style=flat-square)

## Classes

| Class (as labelled) | Meaning |
| --- | --- |
| `TBS mentah` | Unripe bunch |
| `Kurang masak` | Under-ripe bunch |
| `TBS masak` | Ripe bunch |
| `Terlalu masak` | Overripe bunch |
| `TBS abnormal` | Abnormal bunch |
| `Janjang kosong` | Empty bunch (no fruit left) |

## Results

Training outputs are in [`Hasil Training/`](Hasil%20Training). On the validation set the confusion matrix shows 0.98–1.00 of each class predicted correctly, with the main errors being some background regions picked up as bunches.

| Confusion matrix | Training curves |
| --- | --- |
| <img src="Hasil%20Training/confusion_matrix.png" alt="Confusion matrix" width="420"> | <img src="Hasil%20Training/results.png" alt="Training and validation curves" width="420"> |

| Validation labels | Model predictions |
| --- | --- |
| <img src="Hasil%20Training/val_batch0_labels.jpg" alt="Validation batch with ground-truth labels" width="420"> | <img src="Hasil%20Training/val_batch0_pred.jpg" alt="Validation batch with predictions" width="420"> |

Also included: F1 and precision-recall curves (`F1_curve.png`, `PR_curve.png`).

## Repository layout

```text
├── Hasil Training/                      # Training results and best weights (thebest.pt)
└── Klasifikasi Kematangan Buah Sawit/   # YOLOv5 code base
    ├── programsawit.pt                  # Trained ripeness model
    ├── yolov5s.pt                       # Pre-trained base weights
    ├── detect.py · train.py · val.py · export.py
    ├── models/ · utils/ · data/
    └── requirements.txt
```

`programsawit.pt` and `Hasil Training/thebest.pt` are the same trained model (identical files).

## Getting started

```bash
git clone https://github.com/rzkydell/kematangan-buah-sawit.git
cd "kematangan-buah-sawit/Klasifikasi Kematangan Buah Sawit"
pip install -r requirements.txt
```

Run detection with the trained model:

```bash
# webcam
python detect.py --weights programsawit.pt --source 0

# an image, a folder or a video
python detect.py --weights programsawit.pt --source path/to/images
```

Results are saved to `runs/detect/exp*`. All standard YOLOv5 options (`--conf-thres`, `--img`, `--device`, …) are available.

The training dataset is not included in this repository.

## Credits and license

Built on [Ultralytics YOLOv5](https://github.com/ultralytics/yolov5), which is licensed under AGPL-3.0; the bundled YOLOv5 code keeps that license. No separate license has been added for the trained model and results yet.

## Author

**Rizky Delianngi** · [Portfolio](https://rzkydell.vercel.app/en#research) · [GitHub](https://github.com/rzkydell)

<details>
<summary>Ringkasan (Bahasa Indonesia)</summary>

Deteksi dan klasifikasi kematangan tandan buah segar (TBS) kelapa sawit dengan YOLOv5s yang dilatih ulang, dalam enam kelas: TBS mentah, kurang masak, TBS masak, terlalu masak, TBS abnormal, dan janjang kosong. Model terlatih (`programsawit.pt`) dan hasil pelatihan (confusion matrix, kurva) disertakan; dataset tidak disertakan.

</details>
