# Video Translator

## Overview
This project converts a video spoken in Vietnamese into a video spoken in English, including:
- Preserving the original visuals (face, expressions).
- Transcribing and translating the content.
- Generating English speech with prosody similar to the original.
- Synchronizing lip movements (lip-sync) so the mouth matches the new audio.


## Modules

#### 1. Extract Audio from Video
- **Input:**  
  - Original video (e.g., `vi_video.mp4`)  
- **Output:**  
  - Mono 16 kHz WAV audio file (e.g., `vi_audio.wav`)  
- **Tool:**  
  - `ffmpeg`

#### 2. Vietnamese Speech Recognition (ASR)
- **Input:**  
  - Vietnamese audio file (`vi_audio.wav`)  
- **Output:**  
  - Vietnamese text (e.g., `vi_text.txt`)  
- **Model:**  
  - Whisper ([openai/whisper-large-v3-turbo](https://huggingface.co/openai/whisper-large-v3-turbo))

#### 3. Text Translation (Vi → En)
- **Input:**  
  - Vietnamese text (`vi_text.txt`)  
- **Output:**  
  - English text (e.g., `en_text.txt`)  
- **Model:**  
  - VinAI Translate ([vinai/vinai-translate-vi2en-v2](https://huggingface.co/vinai/vinai-translate-vi2en-v2))

#### 4. Text‑to‑Speech (English) with Voice+Prosody Cloning
- **Input:**  
  - English text (`en_text.txt`)  
  - Original Vietnamese audio file (`vi_audio.wav`) as voice reference  
- **Output:**  
  - English WAV audio file (e.g., `en_audio.wav`)  
- **Model:**  
  - Coqui TTS – XTTS v2 ([tts_models/multilingual/multi-dataset/xtts_v2](https://huggingface.co/coqui/XTTS-v2))

#### 5. Lip‑Sync with LatentSync
- **Input:**  
  - Original video (`vi_video.mp4`)  
  - Generated English audio (`en_audio.wav`)  
- **Output:**  
  - Lip‑synced output video (`en_video.mp4`)  
- **Model/Tool:**  
  - [LatentSync](https://github.com/bytedance/LatentSync) (checkpoint `latentsync_unet.pt`)



## Examples
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
    </td>
    <td>
      <video src=https://github.com/user-attachments/assets/7f6ade35-4eee-4bd0-8283-57c9b69a5cd5 controls preload></video>
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
