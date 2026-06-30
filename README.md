# ⚡ CALOAD
Bộ công cụ đa phương tiện — Tải file siêu tốc, nén video, tải YouTube, xử lý hàng loạt.

[![caload logo](https://raw.githubusercontent.com/tpc-pascal/caload/main/assets/logo.svg)](https://github.com/tpc-pascal/caload/blob/main/assets/logo.svg)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tpc-pascal/caload/blob/main/colab.ipynb)

## Tính năng

| Tính năng | Công cụ | Hiệu năng |
|-----------|---------|-----------|
| Tải file | aria2c — 32 kết nối | Nhanh hơn 32x |
| YouTube | yt-dlp + aria2c | Chất lượng cao nhất, phụ đề, thumbnail |
| Nén video | FFmpeg + NVENC (T4/L4/A100) | Tăng tốc GPU |
| Xử lý hàng loạt | ThreadPoolExecutor | Chịu lỗi, tiếp tục khi fail |
| Giải nén | ZIP / 7z / RAR | Nén & giải nén |
| Đám mây | Google Drive | Mount & quét thư mục |

## Cấu trúc

```
caload/
├── colab.ipynb          # Notebook Colab
├── assets/              # Logo
├── LICENSE              # MIT
└── README.md
```

## Bắt đầu nhanh (Colab)

Mở `colab.ipynb` trên Google Colab và chạy các cell.

## Giấy phép

MIT
