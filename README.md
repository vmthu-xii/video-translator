
# Video Translator

## Overview
This project converts a video spoken in Vietnamese into a video spoken in English, including:
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



## Demo
<table class="center">
<tr style="font-weight: bolder;text-align:center;">
  <td width="33%"><b>Original video</b></td>
  <td width="33%"><b>Lip-synced video</b></td>
  <td width="33%"><b>Improved video</b></td>
</tr>
  <tr>
    <td>
      <video src=https://github.com/user-attachments/assets/d483493f-fba9-4a50-8cda-dad5843a45f3 controls preload></video>
    </td>
    <td>
      <video src=https://github.com/user-attachments/assets/888e784f-eb3d-41a9-94d0-9f19d5eba02a controls preload></video>
    </td>
    <td>
      <video src=https://github.com/user-attachments/assets/3a8a37e9-3ac7-42cd-9da2-a5f7c1d4a1f7 controls preload></video>
    </td>
  </tr>
  <tr>
    <td>
      <video src=https://github.com/user-attachments/assets/e31b9a53-777e-4c81-8758-f7a17a872c28 controls preload></video>
    </td>
    <td>
      <video src=https://github.com/user-attachments/assets/1f71ee9c-d094-44ba-b610-17a4f9d16604 controls preload></video>
    </td>
    <td>
      <video src=https://github.com/user-attachments/assets/6f55e20e-1d61-4a7f-838f-829e393e03e0 controls preload></video>
    </td>
  </tr>
</table>

## Acknowledgement

- This repo is built on [LatentSync](https://github.com/bytedance/LatentSync). 
Thanks for their generous contributions to the open-source community!
