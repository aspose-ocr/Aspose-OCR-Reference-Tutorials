---
category: general
date: 2026-03-28
description: Cara melakukan OCR ROI di Python – Pelajari cara mengatur opsi pra‑pemrosesan
  untuk mengekstrak teks secara akurat dari wilayah gambar tertentu.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: id
og_description: Cara OCR ROI di Python – Panduan ini menunjukkan cara mengatur pra‑pemrosesan
  untuk mengekstrak teks secara andal dari wilayah gambar yang ditentukan.
og_title: Cara OCR ROI di Python – Cara mengatur pra‑pemrosesan
tags:
- OCR
- Python
- Aspose
title: Cara OCR ROI di Python – Cara mengatur pra‑pemrosesan
url: /id/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara OCR ROI di Python – Cara Mengatur Pra‑pemrosesan

Pernah bertanya‑tanya **bagaimana cara OCR ROI** pada gambar faktur yang berisik tanpa harus memuat seluruh halaman ke memori? Anda tidak sendirian. Dalam banyak proyek dunia nyata kami hanya membutuhkan beberapa bidang—nama pelanggan, alamat, total—sehingga memindai seluruh dokumen menjadi berlebihan.  

Kabar baiknya? Dengan Aspose OCR Anda dapat memberi tahu mesin **di mana harus mencari** dan bahkan memintanya membersihkan gambar terlebih dahulu. Dalam tutorial ini kami akan membahas **cara mengatur pra‑pemrosesan**, mendefinisikan Region of Interest (ROI), dan mengekstrak teks bersih hanya dalam beberapa baris Python.

Pada akhir panduan ini Anda akan memiliki skrip siap‑jalankan yang mengekstrak blok‑blok tertentu dari faktur, kwitansi, atau formulir apa pun. Tidak memerlukan alat tambahan, hanya Aspose OCR dan sedikit logika Python.

---

## Apa yang Anda Butuhkan

- **Python 3.8+** (kode ini bekerja pada versi terbaru apa pun)  
- **Aspose OCR for Python via .NET** – instal dengan `pip install aspose-ocr`  
- Sebuah gambar contoh (misalnya `invoice.png`) yang ditempatkan di folder yang dapat Anda referensikan  
- Pengetahuan dasar tentang fungsi Python dan sintaks berorientasi objek  

Jika Anda sudah memiliki semua ini, bagus—langsung saja ke kode.

---

![How to OCR ROI diagram](ocr-roi.png "How to OCR ROI example")

*Alt text: diagram cara OCR ROI yang menampilkan kotak‑kotak ROI pada gambar faktur*

---

## Langkah 1 – Inisialisasi OCR Engine (Cara OCR ROI)

Sebelum kita dapat memberi tahu mesin *di mana* harus mencari, kita memerlukan sebuah instance dari prosesor OCR. Objek ini menyimpan semua konfigurasi dan menjalankan proses pengenalan.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Mengapa ini penting*: Kelas `OcrEngine` mengabstraksi pekerjaan berat (deteksi font, analisis tata letak, dll.). Dengan membuat satu mesin saja Anda menghindari inisialisasi ulang sumber daya berat untuk setiap gambar, sehingga kinerja tetap cepat.

---

## Langkah 2 – Muat Gambar Sumber Anda (Cara OCR ROI)

Aspose Storage memudahkan pemuatan gambar. Arahkan ke jalur file, dan Anda akan mendapatkan objek `Image` yang siap diproses.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Tip*: Jika Anda bekerja dengan aliran (misalnya, gambar yang diunggah melalui API web), Anda dapat memberikan objek `BytesIO` ke `Image.load` alih‑alih jalur file.

---

## Langkah 3 – Definisikan Region of Interest (ROI)

Sekarang kita menjawab pertanyaan inti **bagaimana cara OCR ROI**: kami memberi tahu mesin persegi panjang tepat yang berisi data yang kami butuhkan. Setiap ROI didefinisikan oleh sudut kiri‑atasnya (`x`, `y`) dan ukurannya (`width`, `height`).

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*Mengapa menggunakan ROI?*  
- **Kecepatan** – Mesin melewati bagian gambar yang tidak relevan.  
- **Akurasi** – Dengan fokus pada area kecil, noise di tempat lain tidak akan mengacaukan pengenalan.  
- **Fleksibilitas** – Anda dapat menambahkan sebanyak mungkin ROI yang diperlukan; mesin mengembalikan daftar hasil dalam urutan yang sama.

---

## Langkah 4 – Cara Mengatur Pra‑pemrosesan untuk Akurasi OCR Lebih Baik

Gambar yang diambil langsung dari pemindai atau ponsel sering mengalami kemiringan, kontras rendah, atau pencahayaan tidak merata. Aspose OCR menyediakan objek `PreprocessingOptions` yang memungkinkan Anda mengaktifkan perbaikan umum sebelum proses pengenalan dijalankan.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Bagaimana ini membantu*:  
- **Deskew** menghilangkan kemiringan yang membuat bentuk karakter menjadi ambigu.  
- **Binarize** mengurangi noise warna, memberikan mesin OCR gambar biner yang bersih.  
- **Contrast** memperkuat goresan yang pudar, sangat berguna untuk kwitansi yang memudar.

Anda dapat bereksperimen dengan flag‑flag ini—matikan satu dan lihat apakah output berubah. Itulah semangat **cara mengatur pra‑pemrosesan** secara efektif.

---

## Langkah 5 – Lakukan OCR Hanya dalam ROI yang Didefinisikan

Dengan mesin, gambar, ROI, dan pra‑pemrosesan siap, saatnya memanggil `recognize`. Metode ini mengembalikan objek `OcrResult` yang berisi koleksi `regions`—setiap entri cocok dengan urutan ROI yang kami berikan.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Di balik layar*: Mesin memotong setiap ROI, menerapkan pipeline pra‑pemrosesan, dan menjalankan model pengenalan pada potongan yang telah dibersihkan. Karena kami memberikan daftar, hasilnya mempertahankan urutan yang sama, memudahkan pasca‑pemrosesan.

---

## Langkah 6 – Baca dan Gunakan Teks yang Diekstrak (Cara OCR ROI)

Akhirnya, iterasikan daftar `regions` dan cetak—atau simpan—string yang dikenali. Objek `Region` memiliki properti `text` yang berisi hasil Unicode.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Output yang diharapkan (contoh)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Jika teks terlihat berantakan, tinjau kembali **cara mengatur pra‑pemrosesan**: mungkin tingkatkan `contrast` atau nonaktifkan `binarize` untuk logo berwarna.

---

## Kesalahan Umum dan Pro Tips

| Masalah | Mengapa Terjadi | Solusi (Cara Mengatur Pra‑pemrosesan) |
|---------|----------------|--------------------------------------|
| Teks miring muncul sebagai gibberish | `deskew` dinonaktifkan atau gambar terlalu diputar | Aktifkan `preprocessing_options.deskew = True` |
| Angka menjadi titik atau goresan stray | Kontras rendah atau binarisasi berlebihan | Turunkan `contrast` (misalnya, `1.2`) atau set `binarize = False` |
| Koordinat ROI meleset beberapa piksel | DPI berbeda atau skala pemindai | Gunakan alat (misalnya Paint.NET) untuk mengukur posisi piksel tepat, atau tambahkan margin kecil (`+5` piksel) pada setiap ROI |
| Hasil kosong untuk suatu region | ROI berada di luar batas gambar | Verifikasi dimensi gambar: `source_image.width`, `source_image.height` |

---

## Memperluas Solusi (Cara OCR ROI dalam Berbagai Skenario)

- **ROI Dinamis**: Jika faktur Anda memiliki tata letak variabel, Anda dapat pertama‑tama menjalankan OCR cepat seluruh halaman untuk menemukan kata kunci (“Customer:”, “Address:”) lalu menghitung ROI secara dinamis.  
- **Pemrosesan Batch**: Bungkus langkah‑langkah di atas dalam sebuah fungsi dan loop melalui folder gambar. Ingat untuk menggunakan kembali instance `ocr_engine` yang sama agar penggunaan memori tetap rendah.  
- **Ekspor ke JSON**: Alih‑alih mencetak, bangun dictionary dan dump dengan `json.dumps`; ini memudahkan integrasi downstream (misalnya mengirim ke sistem ERP).

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## Kesimpulan

Anda kini memiliki contoh lengkap yang dapat dijalankan yang menunjukkan **cara OCR ROI** di Python sambil menguasai **cara mengatur pra‑pemrosesan** untuk akurasi optimal. Dengan membatasi mesin pada persegi panjang yang Anda butuhkan dan membersihkan gambar terlebih dahulu, Anda memperoleh hasil yang lebih cepat dan bersih—sempurna untuk otomatisasi faktur, digitalisasi formulir, atau skenario apa pun di mana hanya sebagian halaman yang penting.

Siap untuk langkah selanjutnya? Cobalah menyesuaikan koordinat ROI untuk tipe dokumen lain, atau bereksperimen dengan flag pra‑pemrosesan tambahan seperti `sharpen` atau `noise_reduction`. Fleksibilitas Aspose OCR memungkinkan Anda menyesuaikan pipeline untuk hampir semua kualitas gambar.

Jika Anda menemui kendala, periksa output konsol untuk region kosong dan tinjau kembali pengaturan pra‑pemrosesan. Selamat coding, semoga OCR Anda selalu akurat!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}