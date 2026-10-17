# CIT Voice Studio

Phần mềm chuyển văn bản tiếng Việt thành giọng nói, chạy hoàn toàn trên máy tính của bạn.

Không cần tài khoản. Không cần Internet sau khi cài. Văn bản và giọng nói của bạn không bị gửi đi đâu cả.

Chạy trên **Windows**, **Linux** và **macOS**.

> Trạng thái: repo đang được hoàn thiện. Bản cài đặt sẽ được phát hành tại tab **Releases**.

---

## Tính năng

- **Giọng đọc tiếng Việt có sẵn**: nam và nữ, giọng Bắc, Trung, Nam, nhiều phong cách (tin tức, kể chuyện, đọc truyện…).
- **Nghe thử từng giọng** trước khi chọn.
- Chỉnh tốc độ đọc và xuất **WAV** (48 kHz) hoặc **MP3**.
- **Thẻ cảm xúc** chèn trong câu: `[cười]`, `[thở dài]`, `[hắng giọng]`.
- **Thẻ nghỉ** tạo khoảng lặng: `[nghỉ 2s]`, `[nghỉ 500ms]`.
- **Từ điển phát âm**: tự đặt cách đọc cho từ viết tắt hay tên riêng.
- **Tạo hàng loạt**: đặt mốc `[P1]`, `[P2]`… để tách thành nhiều file audio.
- **Phụ đề cho video**: tạo audio kèm phụ đề `.srt` khớp theo từng câu.

---

## Kết nối từ phần mềm khác (API)

Khi ứng dụng đang mở, nó chạy sẵn máy chủ API tại `http://127.0.0.1:8001`. Phần mềm khác, script hay AI Agent gọi vào đó để tạo giọng nói tự động.

| Method | Đường dẫn | Việc |
|---|---|---|
| `GET` | `/health` | Trạng thái máy chủ |
| `GET` | `/voices` | Danh sách giọng đọc |
| `GET` `POST` | `/stream` | Đọc theo thời gian thực |
| `POST` | `/api/tts/generate` | Văn bản thành WAV/MP3 |
| `POST` | `/api/tts/generate-with-subtitles` | Audio kèm phụ đề `.srt` |
| `POST` | `/api/tts/conversation` | Hội thoại nhiều người nói |

Ví dụ nhanh (Python):

```python
import requests

r = requests.post(
    "http://127.0.0.1:8001/api/tts/generate",
    json={"text": "Xin chào từ phần mềm khác.", "voice_id": "Minh Đức"},
)
open("giong-noi.wav", "wb").write(r.content)
```

Tài liệu đầy đủ khi app đang chạy: `http://127.0.0.1:8001/docs` và `http://127.0.0.1:8001/openapi.json`.

---

## Dùng kèm template video Remotion

Template [github.com/quyen2867/remotion-video-template](https://github.com/quyen2867/remotion-video-template) có sẵn provider `cit` (giọng đọc offline). Đặt trong `.env`:

```env
TTS_PROVIDER=cit
CIT_TTS_BASE_URL=http://127.0.0.1:8001
CIT_TTS_VOICE=Hải Đăng
CIT_TTS_SPEED=1.1
```

Mở ứng dụng CIT Voice Studio trước khi sinh audio.

---

## Giấy phép

Phát hành theo Apache License 2.0.
