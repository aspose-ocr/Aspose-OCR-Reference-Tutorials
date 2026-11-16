---
category: general
date: 2026-06-19
description: Buat instance AsposeAI di Python dengan cepat, mencakup konfigurasi model
  default dan callback logging khusus untuk wawasan yang lebih baik.
draft: false
keywords:
- create asposeai instance
- AsposeAI default instance
- Python logging callback
- custom logging for AsposeAI
- AsposeAI model configuration
- using AsposeAI in Python
language: id
og_description: Buat instance AsposeAI di Python dengan cepat. Pelajari pengaturan
  logging default dan kustom untuk integrasi AI yang kuat.
og_title: Buat Instansi AsposeAI di Python – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create AsposeAI instance in Python quickly, covering default model
    configuration and a custom logging callback for better insight.
  headline: Create AsposeAI Instance in Python – Complete Guide
  type: TechArticle
- description: Create AsposeAI instance in Python quickly, covering default model
    configuration and a custom logging callback for better insight.
  name: Create AsposeAI Instance in Python – Complete Guide
  steps:
  - name: 1. Import the AsposeAI class
    text: First we bring the class into the current namespace. This mirrors the typical
      “import‑library” pattern you see in most Python SDKs.
  - name: 2. Spin up the default model configuration
    text: Creating an instance without any arguments gives you the SDK’s built‑in
      model, which is perfect for quick trials.
  - name: 3. Define a simple logging callback
    text: If you want insight into what the SDK is doing—like request payloads or
      internal warnings—you can attach a logging function. Here’s a minimal example
      that just prints to stdout.
  - name: 4. Create an instance that uses the custom logging callback
    text: Now we combine the default model with our logger. The `logging` parameter
      expects a callable that receives a single string argument.
  type: HowTo
tags:
- AsposeAI
- Python
- AI SDK
title: Buat Instansi AsposeAI di Python – Panduan Lengkap
url: /id/python/general/create-asposeai-instance-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Instansi AsposeAI di Python – Panduan Lengkap

Pernahkah Anda perlu **create AsposeAI instance** dalam proyek Python tetapi tidak yakin argumen konstruktor mana yang harus digunakan? Anda tidak sendirian. Baik Anda sedang membuat prototipe demo cepat atau membangun layanan AI tingkat produksi, mendapatkan instansi yang tepat adalah langkah pertama menuju hasil yang dapat diandalkan.

Dalam tutorial ini kami akan membimbing Anda melalui seluruh proses: mulai dari memulai **AsposeAI default instance** hingga menghubungkan **custom logging callback** yang memungkinkan Anda melihat persis apa yang dibisikkan SDK di balik layar. Pada akhir tutorial Anda akan memiliki objek `AsposeAI` yang dapat digunakan dalam skrip apa pun, serta beberapa tips untuk menghindari jebakan umum.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

- Python 3.8 atau lebih baru terpasang (SDK mendukung 3.7+).
- Paket `asposeai` terinstal melalui `pip install asposeai`.
- Terminal atau IDE yang Anda nyaman gunakan (VS Code, PyCharm, atau bahkan editor teks biasa).

Tidak ada kredensial tambahan yang diperlukan untuk model bawaan default, jadi Anda dapat mulai bereksperimen segera.

## Cara Membuat Instansi AsposeAI – Langkah‑per‑Langkah

Berikut adalah panduan singkat berurutan. Setiap langkah menyertakan cuplikan kode, penjelasan **mengapa** langkah tersebut penting, dan pemeriksaan cepat yang dapat Anda jalankan.

### 1. Impor kelas AsposeAI

Pertama kita membawa kelas ke dalam namespace saat ini. Ini mencerminkan pola “import‑library” tipikal yang Anda lihat di sebagian besar SDK Python.

```python
# Step 1: Import the AsposeAI class
from asposeai import AsposeAI
```

> **Mengapa?** Mengimpor mengisolasi API publik SDK, menjaga skrip Anda tetap rapi dan menghindari benturan nama yang tidak disengaja.

### 2. Jalankan konfigurasi model default

Membuat instansi tanpa argumen apa pun memberi Anda model bawaan SDK, yang sempurna untuk percobaan cepat.

```python
# Step 2: Create an instance using the default built‑in model configuration
ai_default = AsposeAI()
```

> **Apa yang terjadi di balik layar?** `AsposeAI()` memuat model bahasa ringan yang terbundel secara lokal. Tidak memerlukan akses jaringan, sehingga Anda dapat menjalankannya secara offline.

### 3. Definisikan callback logging sederhana

Jika Anda ingin wawasan tentang apa yang dilakukan SDK—seperti payload permintaan atau peringatan internal—Anda dapat melampirkan fungsi logging. Berikut contoh minimal yang hanya mencetak ke stdout.

```python
# Step 3: Define a simple logging callback to capture AI messages
def log(message):
    print("[AI] " + message)
```

> **Mengapa callback?** SDK memancarkan event log melalui fungsi yang disediakan pengguna. Desain ini memungkinkan Anda mengarahkan log ke mana saja yang Anda inginkan—stdout, file, atau layanan pemantauan.

### 4. Buat instansi yang menggunakan callback logging khusus

Sekarang kita menggabungkan model default dengan logger kita. Parameter `logging` mengharapkan callable yang menerima satu argumen string.

```python
# Step 4: Create an instance that uses the custom logging callback
ai_with_logging = AsposeAI(logging=log)
```

> **Hasil:** Setiap pesan internal yang dihasilkan SDK kini akan dicetak dengan awalan `[AI]`, memberi Anda visibilitas waktu nyata.

#### Output yang Diharapkan (contoh)

Menjalankan cuplikan di atas tidak akan menghasilkan output langsung karena SDK hanya mencatat selama panggilan inferensi sebenarnya. Untuk melihatnya beraksi, coba panggilan `generate` singkat (ditunjukkan pada bagian berikutnya).

## Menggunakan Instansi AsposeAI Default

Setelah Anda memiliki `ai_default`, Anda dapat memanggil metodenya seperti objek Python lainnya. Berikut contoh dasar generasi teks:

```python
# Generate a short response using the default instance
response = ai_default.generate(prompt="Explain the difference between AI and ML.")
print("Response:", response)
```

Output konsol tipikal:

```
Response: AI (Artificial Intelligence) is the broader concept...
```

Tidak ada logging yang muncul karena kami tidak menyediakan logger, tetapi panggilan berhasil, mengonfirmasi bahwa **create AsposeAI instance** berfungsi langsung dari awal.

## Menambahkan Callback Logging Kustom (Contoh Lengkap)

Mari gabungkan semuanya ke dalam satu skrip yang sekaligus membuat instansi dan mendemonstrasikan logging:

```python
from asposeai import AsposeAI

def log(message):
    # Simple logger that timestamps each line
    from datetime import datetime
    timestamp = datetime.now().strftime("%H:%M:%S")
    print(f"[{timestamp}] [AI] {message}")

# Create the instance with custom logging
ai = AsposeAI(logging=log)

# Trigger a request to see logs in action
result = ai.generate(prompt="What is the capital of France?")
print("Result:", result)
```

Contoh output konsol:

```
[12:34:56] [AI] Sending request to AsposeAI service...
[12:34:56] [AI] Received response (status 200)
Result: Paris
```

> **Mengapa ini penting:** Log menunjukkan siklus hidup permintaan, yang sangat berharga saat men-debug timeout jaringan atau ketidaksesuaian payload.

## Memverifikasi Instansi Berfungsi di Berbagai Lingkungan

Konfigurasi model **AsposeAI** yang kuat harus berperilaku sama di Windows, macOS, dan Linux. Untuk memastikan:

1. Jalankan skrip pada setiap OS.
2. Periksa bahwa string respons tidak kosong dan baris log muncul (jika Anda mengaktifkan logging).
3. Opsional, asersi output dalam unit test:

```python
import unittest

class TestAsposeAI(unittest.TestCase):
    def test_default_instance(self):
        ai = AsposeAI()
        out = ai.generate(prompt="2+2")
        self.assertIn("4", out)

if __name__ == "__main__":
    unittest.main()
```

Jika tes lulus, Anda telah berhasil **create AsposeAI instance** yang berfungsi dalam pipeline CI.

## Kesalahan Umum dan Tips Pro

| Gejala | Penyebab Kemungkinan | Solusi |
|--------|----------------------|--------|
| `ImportError: cannot import name 'AsposeAI'` | Paket tidak terinstal atau lingkungan Python salah | Jalankan `pip install asposeai` pada interpreter yang sama |
| Tidak ada log meskipun sudah memberikan `logging=log` | Tanda tangan callback tidak cocok (harus menerima satu string) | Pastikan `def log(message):` bukan `def log(*args)` |
| `generate` hang selamanya | Jaringan terblokir (saat menggunakan model cloud) | Beralih ke model bawaan default atau konfigurasikan proxy |
| Respons kosong | Prompt terlalu pendek atau model tidak terload | Berikan prompt yang lebih panjang dan jelas; pastikan `ai` bukan `None` |

> **Tips pro:** Jaga logger tetap ringan. I/O berat (seperti menulis ke DB remote) di dalam callback dapat memperlambat inferensi secara dramatis.

## Langkah Selanjutnya – Memperluas Pengaturan AsposeAI Anda

Sekarang Anda tahu cara **create AsposeAI instance** dengan logging default dan kustom, pertimbangkan topik lanjutan berikut:

- **Menggunakan AsposeAI model configuration** untuk memuat model yang telah di‑fine‑tune dari jalur lokal.
- **Mengintegrasikan dengan kode async** (`await ai.generate_async(...)`) untuk layanan throughput tinggi.
- **Mengarahkan log ke file** atau sistem logging terstruktur seperti `loguru` untuk diagnostik produksi.
- **Menggabungkan beberapa instansi** (misalnya, satu untuk jawaban cepat, lainnya untuk penalaran berat) dalam aplikasi yang sama.

Masing‑masing topik ini membangun di atas fondasi yang telah kami letakkan, memungkinkan Anda skala dari skrip sederhana ke backend AI‑powered yang lengkap.

---

*Selamat coding! Jika Anda mengalami kendala saat mencoba **create AsposeAI instance**, tinggalkan komentar di bawah—saya siap membantu.*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengekstrak OCR – Konfigurasi OCR](/ocr/english/net/ocr-configuration/)
- [Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Ekstrak Teks dari Gambar Menggunakan Operasi OCR pada Folder](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}