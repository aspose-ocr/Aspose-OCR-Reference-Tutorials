---
category: general
date: 2026-01-12
description: Pelajari cara menampilkan info dari AsposeAI dengan mencantumkan model
  lokal, menampilkan nama model, ukuran, dan cap waktu terakhir digunakan dalam contoh
  Python yang jelas.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: id
og_description: 'Cara menampilkan info dari AsposeAI: daftar model lokal, tampilkan
  nama model, ukuran, dan cap waktu terakhir digunakan dengan panduan lengkap Python.'
og_title: Cara Menampilkan Info – Daftar Model Lokal, Nama, Ukuran, Terakhir Digunakan
tags:
- AsposeAI
- Python
- Model Management
title: Cara Menampilkan Info – Daftar Model Lokal, Nama, Ukuran, Terakhir Digunakan
url: /id/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menampilkan Info – Daftar Model Lokal, Nama, Ukuran, Terakhir Digunakan

Pernah bertanya-tanya **bagaimana menampilkan info** dari instalasi AsposeAI Anda tanpa harus menggali log atau UI? Anda bukan satu-satunya. Dalam banyak pipeline data‑science hal pertama yang Anda butuhkan adalah sekilas cepat model mana yang ada di mesin Anda, apa namanya, seberapa besar, dan kapan terakhir Anda menggunakannya.

Itulah yang akan kami bahas: potongan kode Python yang ringkas, end‑to‑end, yang **menampilkan daftar model lokal**, kemudian **menampilkan nama model**, **menunjukkan ukuran model**, dan **menunjukkan timestamp terakhir digunakan**. Tanpa pustaka eksternal, tanpa sihir tersembunyi—hanya klien AsposeAI yang sudah Anda miliki.

Pada akhir tutorial ini Anda akan dapat menempelkan kode ke skrip apa pun, menjalankannya, dan langsung mendapatkan tabel rapi model yang tersimpan secara lokal. Ini sempurna untuk memeriksa kesehatan lingkungan, membangun dasbor kesehatan, atau sekadar memenuhi rasa ingin tahu tentang apa yang tersembunyi di disk.

## Prasyarat

- Python 3.8 atau lebih baru (contoh menggunakan f‑strings, jadi 3.6+ wajib)
- Paket `asposeai` terinstal (`pip install asposeai`)
- Lisensi AsposeAI yang aktif atau kunci percobaan (klien akan mengambil kredensial dari variabel lingkungan atau file konfigurasi)

Jika Anda sudah mencentang semua itu, bagus—mari kita mulai.

## Langkah 1: Cara Menampilkan Info – Inisialisasi Klien AsposeAI

Sebelum kita dapat **menampilkan daftar model lokal**, kita memerlukan objek klien yang berkomunikasi dengan runtime AsposeAI. Langkah ini adalah fondasi; tanpa itu sisa kode akan menghasilkan `NameError`.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Mengapa ini penting*: Menginisialisasi klien membuat sesi dengan mesin inferensi lokal, memuat pustaka native yang diperlukan. Ini juga memvalidasi bahwa lisensi Anda aktif, mencegah error misterius nantinya saat Anda mencoba menanyakan model.

> **Pro tip**: Jika Anda menjalankan ini di server CI, setel `ASPOSEAI_LICENSE` di lingkungan sehingga klien dapat memulai tanpa prompt interaktif.

## Langkah 2: Daftar Model Lokal – Mengambil Model yang Tersedia

Sekarang klien sudah siap, kita dapat **menampilkan daftar model lokal**. Metode `list_local()` mengembalikan koleksi objek, masing‑masing memiliki properti seperti `name`, `size_mb`, dan `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*Apa yang terjadi di balik layar*: `list_local()` memindai direktori tempat AsposeAI menyimpan cache file model (`~/.asposeai/models` secara default) dan membangun objek metadata ringan. Ini cepat karena tidak memuat bobot model—hanya membaca manifest JSON kecil.

Jika Anda pernah bertanya-tanya apakah model tertentu sudah di‑cache, panggilan ini adalah cara tercepat untuk mengkonfirmasi.

## Langkah 3: Tampilkan Nama Model, Tampilkan Ukuran Model, dan Tampilkan Terakhir Digunakan

Dengan model di tangan, akhirnya kita **menampilkan info** dengan mengiterasi koleksi dan mencetak setiap atribut. Di sinilah kita **menampilkan nama model**, **menunjukkan ukuran model**, dan **menunjukkan terakhir digunakan** semua dalam satu baris rapi.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Output yang diharapkan** (timestamp Anda akan berbeda):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Mengapa kami memformatnya seperti ini*: Garis hubung (`–`) memisahkan bidang untuk keterbacaan, dan baris header membuat output konsol mudah dipindai. Jika Anda membutuhkan format yang dapat dibaca mesin nanti (CSV, JSON), Anda dapat dengan mudah mengganti pemanggilan `print` dengan `writer.writerow` atau `json.dump`.

### Menangani Kasus Edge

- **Tidak ada model yang di‑cache** – `list_local()` mengembalikan daftar kosong. Loop akan langsung dilewati, meninggalkan hanya header. Anda mungkin ingin menambahkan guard:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Atribut hilang** – Dalam kasus jarang, manifest dapat rusak. Mengakses `model_info.last_used` dapat menghasilkan `AttributeError`. Bungkus `print` dalam `try/except` jika Anda mengantisipasi masalah tersebut.

- **Direktori model besar** – Jika Anda memiliki ratusan model, pertimbangkan mem‑paging output atau menulis ke file alih‑alih mencetak ke konsol.

## Ringkasan Visual (Opsional)

Jika Anda lebih suka petunjuk visual cepat, diagram di bawah ini menggambarkan alur dari inisialisasi klien hingga tampilan akhir.  

![Diagram yang menunjukkan cara menampilkan info dari klien AsposeAI](/images/how-to-display-info.png "diagram cara menampilkan info")

*Teks alternatif*: **cara menampilkan info** – skematik inisialisasi klien AsposeAI, daftar model, dan penampilan info.

## Skrip Lengkap yang Berfungsi

Menggabungkan semuanya, berikut skrip lengkap yang siap dijalankan:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Simpan ini sebagai `list_models.py`, buat dapat dieksekusi (`chmod +x list_models.py`), dan jalankan:

```bash
./list_models.py
```

Anda akan melihat daftar rapi yang ditunjukkan sebelumnya.

## Kesimpulan

Kami telah membahas **cara menampilkan info** dari AsposeAI dengan **menampilkan daftar model lokal**, kemudian **menampilkan nama model**, **menunjukkan ukuran model**, dan **menunjukkan timestamp terakhir digunakan**. Pendekatan ini ringan, hanya memerlukan paket standar `asposeai`, dan dapat disisipkan ke pipeline otomatisasi atau sesi debugging apa pun.

Dari sini Anda mungkin:

- Ekspor output ke CSV untuk analisis spreadsheet (`modul csv`).
- Masukkan timestamp ke dasbor pemantauan untuk memberi peringatan pada model yang sudah lama tidak dipakai.
- Gabungkan skrip ini dengan `aspose_ai.download()` untuk secara otomatis memperbarui model yang belum digunakan dalam waktu lama.

Ingat, visibilitas yang jelas terhadap inventaris model Anda menghemat waktu, mengurangi penumpukan penyimpanan, dan menjaga layanan AI Anda berjalan lancar. Cobalah skrip ini, sesuaikan formatnya sesuai selera, dan biarkan menjadi alat penting di kotak peralatan Anda.

Selamat coding, semoga model Anda selalu segar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}