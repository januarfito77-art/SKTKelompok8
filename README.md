# SKTKelompok8
Tugas Proyek untuk Sistem Kontrol Terdistribusi  Kelompok 8

# 🌡️ ESP32-S3 + DWSIM Integration  
### Modbus RS485 SHT20 → InfluxDB & ThingsBoard

Proyek ini merupakan bagian dari **Tugas Akhir** yang mengintegrasikan sistem **embedded sensor ESP32-S3 (Rust)** dengan **simulasi proses industri (DWSIM)**. Data suhu dan kelembapan dari **sensor SHT20 (XY-MD02)** dikirim melalui **Modbus TTL–RS485**, diproses oleh firmware Rust, lalu diteruskan ke **InfluxDB** dan **ThingsBoard** untuk visualisasi real-time.

---
## 🧩 Struktur Proyek
```text
├── datadwsim/
│ ├── dwsim_report.ods # File hasil simulasi DWSIM
│ ├── uploader.py # Python bridge → InfluxDB & ThingsBoard
│ └── pycache/ # Cache Python
└── SKTkel8/
├── Cargo.toml # Konfigurasi & dependensi proyek Rust
├── src/ # Source code utama ESP32-S3
├── build.rs # Script build firmware
└── target/ # Hasil build firmware
```

## ⚙️ Deskripsi Teknis
### **1. ESP32-S3 (Rust)**
- Bahasa: **Rust** menggunakan framework `esp-idf-sys`  
- Komunikasi: **Modbus RS485 TTL**  
- Sensor: **SHT20 (XY-MD02)** untuk suhu & kelembapan  
- Pengiriman data: **MQTT** → ThingsBoard dan **HTTP Line Protocol** → InfluxDB  

### **2. Python Bridge**
- File utama: `datadwsim/uploader.py`  
- Fungsi:
  - Membaca data dari `dwsim_report.ods`  
  - Membandingkan hasil simulasi DWSIM dengan data sensor nyata  
  - Mengirim data ke **InfluxDB** & **ThingsBoard** secara otomatis  
  - Mendukung *auto-loop* dan *backoff* saat koneksi gagal  
---
## 🚀 Cara Menjalankan
### **1. Python Uploader**
```bash
cd datadwsim
python3 uploader.py
atau python uploader.py
```
### **Noted untuk Influx DB dan Thingsboard**
- INFLUX_URL_BASE=http://localhost:8086 (Ini diatur sesuaikan pada device)
- INFLUX_BUCKET=Sensorskt
- INFLUX_TOKEN=<token>
- THINGSBOARD_HOST=mqtt://thingsboard.cloud (ini diatur sesuaikan pada device)
### **2. Rust uploader**
```bash
cd SKTkel8
cargo build --release
cargo run
```
---
## 📊 Arsitektur Sistem
```text
[SHT20 Sensor]
      │ (RS485 Modbus)
      ▼
 [ESP32-S3 (Rust Firmware)]
      │ Wi-Fi (MQTT)
      ├──► InfluxDB (data logger)
      └──► ThingsBoard (visualisasi)
      ▲
 [Python Bridge] ◄── DWSIM (.ods simulation)
```
---
## ⭐ Fitur Unggulan
- ✅ Integrasi penuh hardware–software  
- ✅ Sinkronisasi hasil DWSIM & sensor nyata  
- ✅ Upload otomatis ke InfluxDB & ThingsBoard  
- ✅ Efisien: kirim hanya saat file berubah  
- ✅ Visualisasi real-time dashboard  
---

## 👩‍💻 Author
-Ahmad Radhy, S.Si., M.Si
-Yanuar Rahmansyah
-Syahira Arliya Putri Subekti
-Institut Teknologi Sepuluh Nopember (ITS)
-Departemen Teknik Instrumentasi





