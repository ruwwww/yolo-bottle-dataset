---
license: other
task_categories:
  - object-detection
tags:
  - yolo
  - ultralytics
  - kasir-kulkas
  - indonesian
size_categories:
  - n<1K
---

# yolo-bottle-multiclass

Dataset deteksi objek untuk demo kasir kulkas kejujuran (webcam).

## Kelas

| id | kelas | jumlah kotak (train+val) |
|----|-------|--------------------------|
| 0 | bottle | 146 |
| 1 | ballpoint_box | 83 |
| 2 | computer_mouse | 139 |

## Isi

- `images/train` 446 gambar, `images/val` 112 gambar (JPG)
- `labels/train`, `labels/val` label YOLO (txt, `class cx cy w h`, ternormalisasi)
- `data.yaml` siap dipakai Ultralytics
- `classes.txt`, `labeling.csv` (metadata proses labeling)

## Asal data

Frame webcam yang di-capture manual per kelas, lalu dilabeli otomatis dengan
Moondream (text-guided bbox) di server GPU. Label kosong = negatif (tidak ada
objek), sengaja disimpan untuk menekan false positive.

## Latih

```bash
yolo detect train data=data.yaml model=yolo11s.pt epochs=100 imgsz=640
```

Hasil referensi (yolo11s, 100 epoch): mAP50 0.748, mAP50-95 0.656.
Model: https://huggingface.co/ruwwww/yolo-bottle-multiclass-yolo11s
Kode: https://github.com/ruwwww/yolo-bottle
