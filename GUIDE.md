# Hướng dẫn sử dụng CALOAD

## Yêu cầu

- Python 3.10+
- aria2, ffmpeg (bắt buộc)
- yt-dlp, tqdm, psutil, gradio (tuỳ chọn theo nhu cầu)

## Chuẩn bị

```
caload/
├── .github/workflows/
│   ├── sync.yml            # Đồng bộ hf/ + release assets lên HF
│   └── wake.yml            # Cron giữ thức HF Space
├── src/
│   └── caload.py           # Core toolkit
├── hf/
│   ├── app.py
│   ├── requirements.txt
│   └── README.md
├── colab.ipynb
├── CONTRIBUTING.md
├── CREDITS.md
├── LICENSE
└── README.md
```

> Dữ liệu đầu vào (video, file, archive) và đầu ra (output) không có trong repo — chúng được tải về hoặc sao chép trong quá trình sử dụng. Workflow `sync.yml` tự động đồng bộ lên Hugging Face Spaces.

## Chạy local

```bash
git clone https://github.com/tpc-pascal/caload.git
cd caload
pip install -r hf/requirements.txt
sudo apt install aria2 ffmpeg
python hf/app.py
```

Mở trình duyệt tại `http://localhost:7860`.

## Chạy trên Hugging Face Spaces

Truy cập: [huggingface.co/spaces/tpc-pascal/caload](https://huggingface.co/spaces/tpc-pascal/caload)

Tạo một [GitHub Release](https://github.com/tpc-pascal/caload/releases) mới, workflow sẽ tự động đồng bộ lên HF Spaces.

## Chạy trên Google Colab

Mở `colab.ipynb` và chạy lần lượt các cell.

## Sử dụng cơ bản

### Tải file với aria2c (32 kết nối song song)

```python
from src.caload import Aria2Downloader
dl = Aria2Downloader()

# Tải một file
dl.download("https://example.com/file.zip")

# Tải nhiều file cùng lúc
dl.multi(["https://example.com/file1.zip", "https://example.com/file2.zip"])
```

### Tải YouTube chất lượng cao nhất

```python
from src.caload import YoutubeDownloader
yt = YoutubeDownloader()

# Video + audio chất lượng cao nhất
yt.best("https://youtube.com/watch?v=...")

# Chỉ lấy audio (MP3)
yt.audio("https://youtube.com/watch?v=...", fmt="mp3")
```

### Nén video với GPU (NVENC)

```python
from src.caload import FFmpegProcessor
ff = FFmpegProcessor()

# Nén nhanh
ff.compress("input.mp4", mode="fast")

# Nén cân bằng (mặc định)
ff.compress("input.mp4", mode="balanced")

# Nén tối đa
ff.compress("input.mp4", mode="max_compress")

# Dùng HEVC (h.265) thay vì H.264
ff.compress("input.mp4", mode="balanced", hevc=True)
```

### Xử lý hàng loạt

```python
from src.caload import BatchProcessor, FFmpegProcessor
import glob

ff = FFmpegProcessor()
bp = BatchProcessor()

# Quét tất cả video .mp4 trong thư mục
videos = glob.glob("/content/drive/MyDrive/videos/*.mp4")

# Nén tất cả, tự động bỏ qua file lỗi
results = bp.run(videos, ff.compress, desc="Đang nén")
print(f"Thành công: {len(results)}/{len(videos)}")
```

### Google Drive

```python
from src.caload import DriveManager
drive = DriveManager()
drive.mount()
drive.ensure()

# Quét video trong Drive
videos = drive.scan_videos()
for v in videos:
    print(f"  {v}")
```

### Giải nén archive

```python
from src.caload import ArchiveTool
arc = ArchiveTool()
arc.extract("/content/data.zip")  # Hỗ trợ .zip, .7z, .rar
```

### Giám sát tài nguyên

```python
from src.caload import ResourceMonitor
m = ResourceMonitor()
print(m.summary())

# Giám sát liên tục
def hien_thi(snap):
    print(f"CPU: {snap['cpu']:.1f}% | RAM: {snap['mem_u']:.2f}GB")
m.start(callback=hien_thi)
```

## Các thao tác video nâng cao

```python
from src.caload import VideoTools
vt = VideoTools()

# Cắt video
vt.trim("input.mp4", "output.mp4", start="00:01:00", dur="00:00:30")

# Ghép video
vt.merge(["part1.mp4", "part2.mp4"], "merged.mp4")

# Tạo thumbnail
vt.thumbnail("video.mp4", "thumb.jpg")

# Trích xuất audio
vt.extract_audio("video.mp4", "audio.mp3")
```

## Chuyển đổi audio

```python
from src.caload import AudioTool
at = AudioTool()
at.convert("input.mp3", "flac")   # MP3 → FLAC
at.convert("input.wav", "mp3")    # WAV → MP3
```

## Chuyển đổi ảnh

```python
from src.caload import ImageTool
it = ImageTool()
it.convert("photo.png", "jpg")    # PNG → JPG
it.convert("photo.jpg", "webp")   # JPG → WebP
```
