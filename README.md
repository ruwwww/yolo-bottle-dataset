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
  - 1K<n<10K
---

# yolo-bottle-multiclass

Dataset deteksi objek 5 kelas untuk demo kasir kulkas kejujuran ES HMSI (webcam).

## Kelas

| id | kelas | jumlah capture |
|----|-------|----------------|
| 0 | bottle | 146 |
| 1 | ballpoint_box | 376 |
| 2 | computer_mouse | 143 |
| 3 | teh_pucuk | 178 |
| 4 | golda | 196 |
| **Total** | | **1.039** |

## Isi

- `images/train` 746 gambar, `images/val` 186 gambar (JPG)
- `labels/train`, `labels/val` label YOLO (txt, `class cx cy w h`, ternormalisasi)
- `data.yaml` siap dipakai Ultralytics
- `classes.txt`, `labeling.csv` (metadata proses labeling)

## Asal data

Frame webcam yang di-capture manual per kelas di depan kulkas, lalu dilabeli otomatis dengan
Moondream (text-guided bbox) di server GPU. Label kosong = negatif (tidak ada
objek), sengaja disimpan untuk menekan false positive.

## Latih

```bash
yolo detect train data=data.yaml model=yolo11s.pt epochs=100 imgsz=640
```

Hasil referensi (yolo11s, 100 epoch):
- Precision: 0.982
- Recall: 0.840
- mAP50: 0.829 (bottle: 0.995, teh_pucuk: 0.995, golda: 0.995, computer_mouse: 0.967)
- mAP50-95: 0.790

Model: https://github.com/ruwwww/yolo-bottle-model
Kode: https://github.com/ruwwww/yolo-bottle
