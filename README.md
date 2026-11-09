# Sistem Deteksi Kantuk (Drowsiness Detection System)

Projek **Computer Vision** berbasis **MediaPipe Face Mesh**, **OpenCV**, dan **Deep Learning (MobileNetV2 / TensorFlow)** untuk mendeteksi rasa kantuk dan ketidakfokusan (menoleh/menunduk) secara *real-time*.

## Fitur Utama

- **Deteksi Mata Tertutup (Kantuk)**:
  - Versi Web (`app.py`): Menggunakan pendekatan *AI Hybrid* — ekstraksi *landmark* area mata menggunakan **MediaPipe Face Mesh**, lalu diklasifikasikan dengan model CNN **MobileNetV2** (`mobilenetv2_eye_classifier.keras`).
  - Versi Desktop (`main.py`): Menggunakan perhitungan *Eye Aspect Ratio* (EAR) dan visualisasi *dotted UI* futuristik beserta efek peringatan visual & suara.
- **Deteksi Posisi Kepala (Menoleh / Menunduk)**: Menghitung rasio jarak *landmark* hidung terhadap pipi kiri dan kanan serta mendeteksi hilangnya wajah dari tangkapan kamera.
- **Sistem Peringatan Audio & Visual**: Memutar alarm peringatan (`alarm.mp3` dan `menghadap.mp3`) ketika mata tertutup melebihi ambang waktu atau saat pengguna tidak menghadap kamera.
- **Antarmuka Web & Dukungan Docker**: Dilengkapi *web server* berbasis **Flask** (`app.py`, `templates/index.html`) dan konfigurasi **Docker** (`DockerFile`) untuk *deployment*.

## Struktur Projek

```text
├── app.py                              # Aplikasi Web Flask (Hybrid MediaPipe + MobileNetV2)
├── main.py                             # Aplikasi Desktop OpenCV + Pygame Audio
├── buat_suara.py                       # Script generator audio alarm menggunakan gTTS
├── mobilenetv2_eye_classifier.keras    # Model CNN MobileNetV2 pengklasifikasi mata
├── static/
│   ├── alarm.mp3                       # Audio peringatan saat mengantuk
│   └── menghadap.mp3                   # Audio peringatan saat tidak menghadap kamera
├── templates/
│   └── index.html                      # Antarmuka web deteksi kantuk real-time
├── requirements.txt                    # Daftar dependensi Python
└── DockerFile                          # Konfigurasi container Docker
```

## Cara Menjalankan

### 1. Persiapan Environment
```bash
pip install -r requirements.txt
```

### 2. Menjalankan Versi Web (Flask)
```bash
python app.py
```
Buka browser dan akses `http://localhost:5000`.

### 3. Menjalankan Versi Desktop (OpenCV)
```bash
python main.py
```
Tekan tombol `q` pada jendela kamera untuk keluar.
