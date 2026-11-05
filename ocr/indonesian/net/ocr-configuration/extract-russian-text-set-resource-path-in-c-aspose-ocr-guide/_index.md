---
category: general
date: 2025-12-29
description: Ekstrak teks Rusia dengan Aspose OCR di C#. Pelajari cara mengatur jalur
  sumber daya, memuat gambar OCR, dan membaca paspor Rusia dengan cepat.
draft: false
keywords:
- extract russian text
- set resource path
- read russian passport
- load image ocr
- extract text image
language: id
og_description: Ekstrak teks Rusia dengan Aspose OCR di C#. Ikuti panduan langkah
  demi langkah ini untuk mengatur jalur sumber daya, memuat OCR gambar, dan membaca
  paspor Rusia secara efisien.
og_title: Ekstrak teks Rusia & atur jalur sumber daya di C# – Panduan Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: ekstrak teks Rusia & atur jalur sumber daya di C# – panduan Aspose OCR
url: /id/net/ocr-configuration/extract-russian-text-set-resource-path-in-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ekstrak teks Rusia & atur jalur sumber daya di C# – Panduan Aspose OCR

Pernah perlu **mengekstrak teks Rusia** dari paspor yang dipindai tetapi tidak yakin harus mulai dari mana? Dalam tutorial ini kami akan memandu Anda melalui seluruh proses—cara mengekstrak teks Rusia menggunakan Aspose OCR, cara mengatur jalur sumber daya, dan cara memuat gambar dengan benar sehingga Anda dapat membaca data paspor Rusia dalam sekejap.

Anda akan melihat contoh lengkap yang dapat dijalankan, mempelajari mengapa setiap baris penting, dan mendapatkan beberapa tips praktis yang menyelamatkan Anda dari jebakan umum. Tidak ada tautan “lihat dokumentasi” yang samar—hanya solusi mandiri yang dapat Anda salin‑tempel dan jalankan hari ini.

## Apa yang Anda perlukan sebelum kita mulai

- **.NET 6.0** (atau versi .NET terbaru; API stabil pada 5.x‑7.x)
- Paket NuGet **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`)
- Sebuah folder di disk yang berisi model bahasa Rusia yang disertakan dengan Aspose OCR (biasanya `Resources\Russian` setelah Anda mengekstrak paket)
- Gambar paspor Rusia (misalnya `russian_passport.jpg`) yang ditempatkan di folder tersebut

Itu saja. Tidak ada layanan tambahan, tidak ada kunci cloud, hanya setup lokal.

## ekstrak teks Rusia – ikhtisar langkah‑demi‑langkah

Berikut adalah peta jalan singkat apa yang akan kita capai:

1. **Atur jalur sumber daya** agar mesin dapat menemukan model bahasa Rusia.  
2. **Buat instance OcrEngine** dan beri tahu bahwa kita bekerja dengan bahasa Rusia.  
3. **Muat gambar paspor** menggunakan `Image.Load` milik Aspose.  
4. **Jalankan pengenalan OCR** dan tangkap hasilnya.  
5. **Cetak teks yang diekstrak** ke konsol (atau gunakan sesuai kebutuhan).

Setiap langkah dibahas dalam bagiannya masing‑masing, lengkap dengan kode, penjelasan, dan kotak “Tips Pro”.

---

## atur jalur sumber daya untuk model bahasa Rusia

Aspose OCR menyediakan file data bahasa secara terpisah dari DLL inti. Jika Anda tidak menunjuk perpustakaan ke folder yang tepat, akan muncul pengecualian seperti *“Unable to find language resources”*. Pemanggilan `ResourceManager.SetLocalResourcePath` menyelesaikan masalah ini.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Resources;

// 👉 Replace this with the absolute path on your machine
string resourceFolder = @"C:\AsposeOCR\Resources";

// Step 1: Tell Aspose where to find the language models
ResourceManager.SetLocalResourcePath(resourceFolder);
```

**Mengapa ini penting:**  
Menetapkan jalur sumber daya sekali di awal akan menyimpan file bahasa dalam cache selama proses berjalan, sehingga Anda tidak membayar biaya I/O pada setiap panggilan pengenalan.  

**Tips Pro:** Simpan jalur tersebut dalam file konfigurasi (`appsettings.json`) jika Anda berencana memindahkan aplikasi antar lingkungan. Dengan begitu Anda menghindari hard‑coding jalur.

---

## buat mesin OCR dan tentukan bahasa Rusia

Setelah mesin tahu ke mana harus mencari, kita membuat instance `OcrEngine` dan mengatur properti `Language`‑nya menjadi `Language.Russian`. Ini memberi tahu pengenalan karakter set dan heuristik mana yang harus dipakai.

```csharp
// Step 2: Initialize the OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.Russian
};
```

**Mengapa ini penting:**  
Aspose OCR mendukung lebih dari 30 bahasa, tetapi Anda harus secara eksplisit memilih satu. Memilih bahasa yang salah dapat menurunkan akurasi secara dramatis karena mesin menerapkan kamus dan logika segmentasi yang berbeda.

---

## muat gambar ocr – membaca foto paspor Rusia

Dengan mesin siap, langkah berikutnya adalah memuat gambar paspor. `Image.Load` milik Aspose bekerja dengan kebanyakan format raster (JPEG, PNG, BMP, TIFF).  

```csharp
// Step 3: Load the passport image you want to process
string imagePath = Path.Combine(resourceFolder, "russian_passport.jpg");
Image sourceImage = Image.Load(imagePath);
```

**Kasus tepi umum:** Jika gambar Anda berupa TIFF multi‑halaman, Anda harus memilih frame yang tepat (`sourceImage.GetFrame(0)`). Untuk kebanyakan paspor, JPEG tunggal sudah cukup.

---

## baca paspor Rusia dan ekstrak teks gambar

Sekarang saatnya kerja berat: jalankan `Recognize` dan tangkap teksnya. Metode ini mengembalikan `OcrResult` yang berisi string polos, skor kepercayaan, dan informasi tata letak opsional.

```csharp
// Step 4: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(sourceImage);
```

**Mengapa Anda mungkin ingin lebih:**  
Jika Anda memerlukan kotak pembatas untuk setiap kata (berguna untuk menyorot), panggil `ocrEngine.Recognize(sourceImage, true)` dan periksa `ocrResult.Regions`.

---

## keluarkan teks yang diekstrak – verifikasi hasil

Akhirnya, tampilkan string yang dikenali ke konsol. Dalam aplikasi dunia nyata Anda mungkin akan menyimpannya ke basis data atau mengirimnya ke rutin validasi.

```csharp
// Step 5: Print the recognized Russian text
Console.WriteLine("=== Extracted Russian Text ===");
Console.WriteLine(ocrResult.Text);
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
=== Extracted Russian Text ===
ПАСПОРТ РОССИЙСКОЙ ФЕДЕРАЦИИ
Серия 45 12 № 1234567
Дата выдачи: 12.03.2015
...
```

Jika output terlihat berantakan, periksa kembali bahwa gambar beresolusi tinggi (≥300 dpi) dan bahwa Anda memang telah menunjuk ke folder model bahasa Rusia.

---

## contoh lengkap, siap‑jalankan

Berikut seluruh program yang digabungkan ke dalam satu file `Program.cs`. Salin, sesuaikan jalur `resourceFolder`, dan tekan **F5**.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Resources;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Set the path to the language resources folder
        // -------------------------------------------------
        string resourceFolder = @"C:\AsposeOCR\Resources";
        ResourceManager.SetLocalResourcePath(resourceFolder);

        // -------------------------------------------------
        // 2️⃣ Create an OCR engine for Russian language
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.Russian
        };

        // -------------------------------------------------
        // 3️⃣ Load the passport image you want to process
        // -------------------------------------------------
        string imagePath = Path.Combine(resourceFolder, "russian_passport.jpg");
        Image sourceImage = Image.Load(imagePath);

        // -------------------------------------------------
        // 4️⃣ Run the OCR recognizer
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Show the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Extracted Russian Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output konsol yang diharapkan** (dipotong untuk singkat):

```
=== Extracted Russian Text ===
ПАСПОРТ РОССИЙСКОЙ ФЕДЕРАЦИИ
Серия 45 12 № 1234567
Дата рождения: 01.01.1990
...
```

Jalankan program beberapa kali dengan pemindaian paspor yang berbeda untuk melihat bagaimana mesin menangani kondisi pencahayaan yang beragam. Anda akan cepat mengetahui kualitas gambar mana yang memberikan hasil **ekstrak teks Rusia** terbaik.

---

## daftar periksa pemecahan masalah – jebakan umum

| Gejala | Penyebab yang mungkin | Solusi |
|--------|-----------------------|--------|
| `Unable to find language resources` | Jalur `resourceFolder` salah | Pastikan folder berisi file `Russian\*.dat` |
| Output kosong | Resolusi gambar terlalu rendah (<300 dpi) | Gunakan pemindaian beresolusi lebih tinggi atau perbesar dengan `Image.Resize` |
| Cyrillic berantakan (tanda tanya) | Encoding konsol bukan UTF‑8 | Tambahkan `Console.OutputEncoding = System.Text.Encoding.UTF8;` di awal |
| Skor kepercayaan rendah | Gambar paspor memiliki silau atau blur | Pralakukan dengan `Image.AdjustContrast` atau bersihkan hasil pindai |

---

## langkah selanjutnya – melampaui ekstraksi dasar

Sekarang Anda dapat **mengekstrak teks Rusia** dan telah menguasai **menetapkan jalur sumber daya**, pertimbangkan ekstensi berikut:

- **Pemrosesan batch** – iterasi melalui folder berisi gambar paspor, simpan tiap hasil ke CSV.  
- **Validasi data** – gunakan ekspresi reguler untuk mengekstrak nomor paspor, tanggal, dan nama dari string OCR mentah.  
- **Pendekatan hibrida** – gabungkan Aspose OCR dengan model jaringan saraf untuk zona yang sulit dibaca.  
- **Lokalisasi** – ubah `Language` menjadi `Language.English` atau `Language.Ukrainian` dan gunakan kembali basis kode yang sama.

Setiap ide ini bergantung pada langkah inti yang telah kita bahas: mengatur jalur sumber daya, memuat gambar, dan memanggil `Recognize`.

---

## kesimpulan

Dalam panduan ini kami menunjukkan cara **mengekstrak teks Rusia** dari gambar paspor menggunakan Aspose OCR, langkah demi langkah—dari **menetapkan jalur sumber daya** hingga **memuat gambar ocr** dan akhirnya **membaca data paspor Rusia**. Kode lengkap yang siap salin‑tempel memungkinkan Anda memulai dalam hitungan menit, dan tips pemecahan masalah membantu menghindari jalan buntu yang umum.

Silakan modifikasi contoh, bereksperimen dengan kualitas gambar yang berbeda, atau integrasikan output ke dalam pipeline verifikasi identitas yang lebih besar. Jika Anda menemui kendala, tinjau kembali daftar periksa atau tinggalkan komentar di bawah—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}