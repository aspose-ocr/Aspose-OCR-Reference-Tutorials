---
date: 2025-12-21
description: Pelajari cara melakukan OCR dan mengekstrak teks dari gambar menggunakan
  Aspose.OCR untuk .NET. Panduan langkah demi langkah ini menunjukkan pengenalan teks
  multibahasa dan pemilihan bahasa.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Cara Melakukan OCR dengan Pemilihan Bahasa di Aspose.OCR
url: /id/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR dengan Pemilihan Bahasa di Aspose.OCR

## Pendahuluan

Jika Anda perlu **cara melakukan OCR** pada gambar dan mengekstrak teks dari file gambar dalam aplikasi .NET, Aspose.OCR untuk .NET menyediakan solusi yang cepat, akurat, dan mendukung bahasa. Pada tutorial ini kami akan menelusuri contoh dunia nyata yang menunjukkan pengenalan gambar OCR dengan pemilihan bahasa, sehingga Anda dapat mengambil teks multibahasa dari foto hanya dengan beberapa baris kode.

## Jawaban Cepat
- **Apa yang dilakukan Aspose.OCR?** Ia mengenali teks cetak dan tulisan tangan dalam gambar serta mengembalikan teks yang diekstrak.  
- **Apakah saya dapat memilih bahasa?** Ya – Anda dapat menentukan bahasa yang didukung seperti English, German, Spanish, Chinese, dll.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi diperlukan untuk penggunaan produksi.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Apakah koreksi kemiringan otomatis?** Anda dapat mengaktifkan `AutoSkew` dan menyesuaikan pengaturan `SkewAngle`.

## Mengapa Memilih Aspose.OCR untuk Tugas OCR?

- **Akurasi tinggi** pada berbagai jenis font dan kualitas gambar.  
- **Pemilihan bahasa bawaan** menghilangkan kebutuhan paket bahasa eksternal.  
- **API sederhana** yang terintegrasi bersih dengan proyek C# yang ada.  
- **Tanpa ketergantungan eksternal** – semuanya berjalan secara lokal, menjaga keamanan data Anda.

## Prasyarat

Sebelum kita masuk ke kode, pastikan Anda telah menyiapkan prasyarat berikut:

- Aspose.OCR untuk .NET: Pastikan Anda telah menginstal pustaka Aspose.OCR. Anda dapat mengunduhnya dari [halaman unduhan Aspose.OCR untuk .NET](https://releases.aspose.com/ocr/net/).

- Lingkungan Pengembangan: Siapkan lingkungan kerja dengan aplikasi .NET. Jika belum melakukannya, lihat [dokumentasi](https://reference.aspose.com/ocr/net/) untuk petunjuk detail.

## Impor Namespace

Di aplikasi .NET Anda, mulailah dengan mengimpor namespace yang diperlukan:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Langkah 1: Inisialisasi Aspose.OCR

Mulailah dengan menginisialisasi sebuah instance dari kelas Aspose.OCR. Ini menyiapkan dasar untuk memanfaatkan kemampuan OCR dalam aplikasi Anda.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Langkah 2: Tentukan Jalur Gambar

Selanjutnya, definisikan jalur ke gambar yang ingin Anda lakukan OCR. Pastikan gambar dapat diakses oleh aplikasi Anda.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Langkah 3: Kenali Gambar dengan Pemilihan Bahasa

Sekarang masuk ke operasi OCR inti. Manfaatkan pustaka Aspose.OCR untuk mengenali teks dari gambar yang telah ditentukan. Sesuaikan pengaturan pengenalan, termasuk pemilihan bahasa.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Langkah 4: Cetak dan Tampilkan Hasil

Setelah operasi OCR selesai, cetak dan tampilkan hasilnya, termasuk teks yang dikenali, area, peringatan, dan representasi JSON.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Masalah Umum dan Tips

- **Pemilihan bahasa yang salah** – Jika output terlihat berantakan, periksa kembali properti `Language` apakah sudah sesuai dengan bahasa gambar sumber.  
- **Gambar miring** – Aktifkan `AutoSkew` atau sesuaikan secara manual `SkewAngle` untuk meningkatkan akurasi pada pemindaian yang condong.  
- **File besar** – Proses gambar berukuran besar secara bertahap atau kurangi resolusi sebelum memberi ke `RecognizeImage` untuk menghemat memori.

## Kesimpulan

Selamat! Anda telah mempelajari **cara melakukan OCR** dengan pemilihan bahasa menggunakan Aspose.OCR untuk .NET. Tutorial ini menunjukkan cara mengekstrak teks dari file gambar, menyesuaikan pengaturan pengenalan, dan menangani konten multibahasa dengan mudah.

## FAQ

### Q1: Apakah Aspose.OCR cocok untuk pengenalan teks multibahasa?

A1: Ya, Aspose.OCR mendukung berbagai bahasa, memberikan fleksibilitas untuk tugas OCR multibahasa.

### Q2: Bisakah saya menyesuaikan pengaturan OCR untuk karakteristik gambar tertentu?

A2: Tentu! Sesuaikan parameter seperti sudut kemiringan, pengenalan baris, dan deteksi area untuk mengoptimalkan OCR pada berbagai skenario.

### Q3: Di mana saya dapat menemukan dukungan tambahan atau diskusi komunitas?

A3: Kunjungi [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan dan diskusi dengan komunitas.

### Q4: Apakah ada versi percobaan gratis?

A4: Ya, jelajahi [percobaan gratis](https://releases.aspose.com/) untuk merasakan kemampuan Aspose.OCR.

### Q5: Bagaimana cara membeli Aspose.OCR untuk .NET?

A5: Untuk membeli, kunjungi [halaman pembelian](https://purchase.aspose.com/buy).

---

**Terakhir Diperbarui:** 2025-12-21  
**Diuji Dengan:** Aspose.OCR 24.11 untuk .NET  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}