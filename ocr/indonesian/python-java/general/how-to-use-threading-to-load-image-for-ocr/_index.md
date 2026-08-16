---
category: general
date: 2026-04-26
description: Cara menggunakan threading untuk memuat gambar untuk OCR di Python. Pelajari
  pemrosesan OCR async dengan callback, thread latar belakang, dan pemuatan gambar
  dalam beberapa langkah saja.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: id
og_description: Cara menggunakan threading untuk memuat gambar untuk OCR di Python.
  Panduan ini menampilkan contoh lengkap yang dapat dijalankan dengan callback dan
  eksekusi di latar belakang.
og_title: Cara Menggunakan Threading untuk Memuat Gambar untuk OCR
tags:
- Python
- Threading
- OCR
- Image Processing
title: Cara Menggunakan Threading untuk Memuat Gambar untuk OCR
url: /id/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Threading untuk Memuat Gambar untuk OCR

Pernah bertanya-tanya **bagaimana cara menggunakan threading** untuk memuat gambar untuk OCR tanpa membekukan aplikasi Anda? Ini adalah skenario yang muncul baik Anda sedang membangun pemindai desktop, layanan web, atau skrip sederhana yang memproses gambar besar. Kabar baik? Beberapa baris Python dan pola threading yang tepat akan membuat UI Anda tetap responsif sementara mesin OCR bekerja.

Dalam tutorial ini kami akan membahas contoh lengkap, end‑to‑end: memuat PNG besar, memulai OCR pada thread latar belakang, dan menangani hasilnya dengan callback. Pada akhir Anda tidak hanya akan mengetahui **bagaimana cara menggunakan threading** tetapi juga bagaimana **memuat gambar untuk OCR** dengan cara yang bersih dan dapat digunakan kembali.

## Apa yang Anda Butuhkan

- Python 3.9+ (sintaks yang kami gunakan bekerja pada versi terbaru apa pun)
- `pillow` untuk penanganan gambar (`pip install pillow`)
- `pytesseract` sebagai pembungkus tipis di atas Tesseract OCR (`pip install pytesseract`)
- Mesin Tesseract OCR terpasang di mesin Anda (unduh dari [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- File gambar besar yang ingin Anda proses (`large_image.png` dalam panduan ini)

Tidak ada kerangka kerja tambahan, tidak async/await—hanya `threading` klasik dan sebuah callback.

## Langkah 1: Impor Modul Threading (Diperlukan untuk Eksekusi Latar Belakang)

Hal pertama yang kami lakukan adalah mengimpor modul `threading`. Modul ini menyediakan kelas `Thread`, yang memungkinkan kami menjalankan fungsi apa pun di thread OS terpisah.

```python
import threading
```

*Mengapa ini penting*: Jika Anda menjalankan OCR pada thread utama, program Anda (terutama GUI) akan membeku sampai OCR selesai. Dengan mendelegasikan pekerjaan ke thread latar belakang, thread utama tetap bebas untuk memperbarui UI, menangani input pengguna, atau memulai tugas lain.

## Langkah 2: Definisikan Callback yang Akan Dipanggil Ketika OCR Selesai

Callback hanyalah sebuah fungsi yang dipanggil oleh potongan kode lain ketika selesai. Di sini kami akan mencetak teks yang dikenali, tetapi Anda dapat menyimpannya, mengirimnya melalui jaringan, atau memperbarui widget UI.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Tips profesional*: Jaga callback tetap ringan. Pemrosesan berat di dalam callback mengalahkan tujuan threading karena tetap akan memblokir thread yang memanggilnya (seringkali thread utama).

## Langkah 3: Muat Gambar yang Ingin Anda Proses

Memuat gambar adalah hal terpisah dari OCR, tetapi tetap merupakan bagian dari alur kerja keseluruhan. Menggunakan Pillow membuat ini menjadi sangat mudah.

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*Mengapa kami melakukannya di sini*: Jika gambar sangat besar, memuatnya pada thread utama dapat menyebabkan gangguan. Pada banyak aplikasi dunia nyata Anda juga akan memindahkan pemuatan ke thread, tetapi demi kejelasan kami tetap melakukannya secara sinkron.

## Langkah 4: Buat Pembungkus Mesin OCR Kecil

Potongan kode asli menggunakan `engine.process_async`. Kami akan meniru itu dengan kelas kecil yang memulai thread secara internal dan memanggil callback yang diberikan ketika selesai.

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*Penjelasan*:  
- `_run_ocr` melakukan pekerjaan berat.  
- `process_async` membuat objek `Thread`, menandainya sebagai daemon (sehingga interpreter dapat keluar meskipun thread masih berjalan), dan memulainya.  
- Callback menerima teks OCR atau pesan error.

## Langkah 5: Sambungkan Semua dan Lakukan Pekerjaan Lain Sementara OCR Berjalan

Sekarang kami mengatur seluruh alur: memuat gambar, menginstansiasi mesin, memulai OCR async, dan menjaga thread utama tetap sibuk dengan hal lain (di sini kami hanya mencetak pesan).

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**Output yang diharapkan (dipotong untuk singkat):**

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

Jika OCR gagal, callback akan mencetak pesan error alih-alih teks.

---

## Mengapa Pendekatan Ini Bekerja Lebih Baik Daripada Loop Sederhana

- **Responsiveness**: Thread utama tidak pernah terblokir pada panggilan OCR, yang dapat memakan beberapa detik untuk gambar besar.
- **Scalability**: Anda dapat menjalankan beberapa instance `SimpleOcrEngine`, masing‑masing pada threadnya sendiri, untuk memproses batch gambar secara bersamaan.
- **Separation of Concerns**: Memuat, memproses, dan menangani hasil dipisahkan dengan bersih, membuat kode lebih mudah diuji dan dipelihara.

## Kesalahan Umum dan Cara Menghindarinya

| Pitfall | What Happens | Fix |
|---------|--------------|-----|
| Lupa menandai thread sebagai *daemon* | Script tetap berjalan setelah pekerjaan utama selesai karena thread OCR masih hidup. | Set `worker.daemon = True` **or** `join()` thread sebelum keluar. |
| Menggunakan variabel global untuk hasil tanpa kunci | Kondisi balapan dapat merusak data ketika beberapa thread menulis secara bersamaan. | Lewatkan hasil melalui callback (seperti yang kami lakukan) atau gunakan kontainer thread‑safe seperti `queue.Queue`. |
| Memuat gambar besar pada thread utama | UI membeku sebelum OCR latar belakang bahkan dimulai. | Pindahkan pemuatan gambar ke thread juga, atau gunakan teknik lazy loading. |
| Tidak menangani pengecualian di dalam thread pekerja | Pengecualian yang tidak tertangkap secara diam-diam menghentikan thread, meninggalkan Anda tanpa hasil. | Bungkus logika OCR dalam `try/except` dan teruskan error ke callback. |

## Memperluas Pola Ini

- **Progress Reporting**: Gunakan `queue.Queue` bersama untuk mengirim persentase kemajuan intermediat dari thread OCR ke thread utama.
- **Thread Pool**: Untuk pemrosesan batch, ganti objek `Thread` individual dengan `concurrent.futures.ThreadPoolExecutor`.
- **GUI Integration**: Pada aplikasi Tkinter atau PyQt, jadwalkan callback dengan `after()` (Tkinter) atau `QTimer.singleShot` (Qt) untuk memastikan pembaruan UI terjadi pada thread utama.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}