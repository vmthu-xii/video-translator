# Video Translator

## Mô tả tổng quan
Dự án chuyển một video nói Tiếng Việt thành video nói Tiếng Anh, bao gồm:
- Giữ nguyên hình ảnh gốc (khuôn mặt, biểu cảm).  
- Nhận dạng và dịch nội dung.
- Sinh giọng Tiếng Anh với ngữ điệu tương tự gốc.
- Đồng bộ khẩu hình (lip‑sync) để miệng khớp với audio mới.


## Các Module

### Module 1: Trích xuất Audio từ Video
- **Input:**  
  - Video gốc (ví dụ `vi_video.mp4`)  
- **Output:**  
  - File audio WAV mono 16 kHz (ví dụ `vi_audio.wav`)  
- **Tool:**  
  - `ffmpeg`


### Module 2: Nhận dạng tiếng Việt (ASR)
- **Input:**  
  - File audio Tiếng Việt (`vi_audio.wav`)  
- **Output:**  
  - Văn bản Tiếng Việt (`vi_text.txt`)  
- **Model:**  
  - Whisper ([openai/whisper-large-v3-turbo](https://huggingface.co/openai/whisper-large-v3-turbo)) với `task="transcribe", language="vi"`.


### Module 3: Dịch văn bản (Vi → En)
- **Input:**  
  - Văn bản Tiếng Việt (`vi_text.txt`)  
- **Output:**  
  - Văn bản Tiếng Anh (`en_text.txt`)  
- **Model:**  
  - VinAI Translate ([vinai/vinai-translate-vi2en-v2](https://huggingface.co/vinai/vinai-translate-vi2en-v2)).


### Module 4: Text‑to‑Speech (Tiếng Anh) với Voice+Prosody Cloning
- **Input:**  
  - Văn bản Tiếng Anh (`en_text.txt`)  
  - File audio gốc Tiếng Việt (`vi_audio.wav`) làm tham chiếu giọng
- **Output:**  
  - File audio Tiếng Anh WAV (ví dụ `en_audio.wav`)  
- **Model:**  
  - Coqui TTS – XTTS v2 ([tts_models/multilingual/multi-dataset/xtts_v2](https://huggingface.co/coqui/XTTS-v2))  


### Module 5: Lip‑Sync với LatentSync
- **Input:**  
  - Video gốc (`vi_video.mp4`)  
  - File audio Tiếng Anh sinh ra (`en_audio.wav`)  
- **Output:**  
  - Video đầu ra đồng bộ khẩu hình (`en_video.mp4`)  
- **Model/Tool:**  
  - LatentSync (`scripts.inference` + checkpoint `latentsync_unet.pt`)  


<table class="center">
<tr style="font-weight: bolder;text-align:center;">
  <td width="50%"><b>Original video</b></td>
  <td width="50%"><b>Lip-synced video</b></td>
</tr>
  <tr>
    <td>
      <video src=https://github.com/user-attachments/assets/a653cec6-a960-4a20-9ab1-e8794a29e188 controls preload></video>
    </td>
    <td>
      <video src=https://github.com/user-attachments/assets/50d9b953-eb11-445d-b955-6af5ef9a3216 controls preload></video>
    </td>
  </tr>
  <tr>
    <td>
      <video src=https://github.com/user-attachments/assets/58e72ade-3e21-414d-8f88-fca93a6e7dbb controls preload></video>
    </td>
    <td>
      <video src=https://github.com/user-attachments/assets/d6ca6a73-d675-4fae-aedb-0780b0e2965a controls preload></video>
    </td>
  </tr>
</table>
