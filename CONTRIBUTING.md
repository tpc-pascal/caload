# Hướng dẫn đóng góp

Vui lòng đọc kỹ các hướng dẫn dưới đây trước khi bắt đầu đóng góp.

---

## 1. Thiết lập môi trường phát triển

```bash
git clone https://github.com/tpc-pascal/caload.git
cd caload
pip install -r hf/requirements.txt
sudo apt install aria2 ffmpeg
```

---

## 2. Quy trình gửi đóng góp

1. **Fork** dự án về tài khoản cá nhân của bạn.
2. **Tạo Branch mới:**
   - Tính năng mới: `git checkout -b feat/ten-tinh-nang`
   - Sửa lỗi: `git checkout -b fix/ten-loi`
   - Tài liệu: `git checkout -b docs/ten-tai-lieu`
3. **Commit:** Sử dụng tiếng Việt hoặc tiếng Anh, nhưng phải rõ nghĩa.
   - Ví dụ: `feat: thêm bộ giải mã AV1`
4. **Push & PR:** Đẩy branch lên GitHub và tạo **Pull Request**.

---

## 3. Quy chuẩn viết mã

- **Nhất quán:** Tuân thủ các quy tắc đặt tên đã có sẵn trong dự án.
- **Gọn nhẹ:** Ưu tiên throughput hơn abstraction. Không thêm comment trừ khi thực sự cần.

---

## 4. Kiểm thử

Trước khi gửi Pull Request, vui lòng đảm bảo:

- Code chạy được trên máy cá nhân mà không gây lỗi.
- Không làm ảnh hưởng đến các tính năng cũ.

---

## 5. Liên hệ

Nếu có bất kỳ thắc mắc nào:

- [Mở một Issue](https://github.com/tpc-pascal/caload/issues)
- [Thảo luận (Discussions)](https://github.com/tpc-pascal/caload/discussions)
