---
date: 2025-12-19
description: Pelajari cara melakukan OCR pada gambar arsip, mengonversi gambar menjadi
  teks, dan mengekstrak teks dari file arsip menggunakan Aspose.OCR untuk .NET.
linktitle: How to Perform OCR on Archive Images with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Cara Melakukan OCR pada Gambar Arsip dengan Aspose.OCR untuk .NET
url: /id/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR pada Gambar Arsip dengan Aspose.OCR untuk .NET

## Pendahuluan

Dalam tutorial komprehensif ini Anda akan menemukan **cara melakukan OCR** pada file gambar yang diarsipkan menggunakan pustaka Aspose.OCR untuk .NET. Baik Anda perlu **mengonversi gambar menjadi teks** atau **mengekstrak teks dari arsip** file, panduan langkah‑demi‑langkah di bawah ini akan memandu Anda melalui semuanya—dari menyiapkan lingkungan pengembangan hingga mengambil teks yang dikenali dari setiap gambar di dalam arsip ZIP.

## Jawaban Cepat
- **Apa yang dibahas dalam tutorial?** Melakukan OCR pada gambar arsip (ZIP) dengan Aspose.OCR untuk .NET.  
- **Kata kunci utama apa yang ditargetkan?** *how to perform ocr*.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi komersial diperlukan untuk produksi.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Bisakah saya menyesuaikan pengaturan pengenalan?** Ya—gunakan `RecognitionSettings` untuk menyesuaikan akurasi.

## Apa itu OCR dan Mengapa Menggunakannya pada Arsip?

Optical Character Recognition (OCR) mengubah gambar yang dipindai atau PDF menjadi teks yang dapat dicari dan diedit. Ketika gambar digabungkan dalam sebuah arsip (misalnya, file ZIP), mengekstrak dan mengenali setiap gambar sekaligus menghemat waktu dan mengurangi kompleksitas kode. Metode `RecognizeMultipleImages` milik Aspose.OCR membuat proses ini menjadi sederhana.

## Prasyarat

- Visual Studio 2019 atau lebih baru (atau IDE apa pun yang kompatibel dengan .NET).  
- .NET Framework 4.5 + atau .NET Core 3.1 + terpasang.  
- Akses ke pustaka Aspose.OCR untuk .NET (tautan unduhan di bawah).  
- Lisensi Aspose.OCR yang valid untuk penggunaan produksi (versi percobaan tersedia).

## Impor Namespace

Dalam proyek .NET Anda, pastikan untuk mengimpor namespace yang diperlukan untuk mengakses fungsionalitas yang disediakan oleh Aspose.OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Unduh dan Instal Aspose.OCR untuk .NET

Unduh paket terbaru dari halaman rilis **[di sini](https://releases.aspose.com/ocr/net/)** dan ikuti langkah instalasi NuGet standar atau instalasi manual.

## Dapatkan Lisensi

Dapatkan lisensi dari **[halaman pembelian](https://purchase.aspose.com/buy)** atau coba **[versi percobaan gratis](https://releases.aspose.com/)**. Letakkan file lisensi di root proyek Anda dan muat pada runtime seperti yang dijelaskan dalam dokumentasi Aspose.

## Langkah 1: Siapkan Direktori Dokumen Anda

Mulailah dengan menginisialisasi jalur ke direktori dokumen Anda:

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **Tip Pro:** Gunakan `Path.Combine` untuk penanganan jalur lintas‑platform.

## Langkah 2: Inisialisasi Aspose.OCR

Buat instance dari kelas Aspose.OCR untuk memulai operasi OCR:

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## Langkah 3: Tentukan Jalur Gambar

Tentukan jalur lengkap ke gambar arsip Anda (file ZIP yang berisi gambar yang ingin Anda baca):

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## Langkah 4: Kenali Gambar

Jalankan pengenalan OCR pada arsip yang ditentukan menggunakan pengaturan default atau khusus. Panggilan ini secara otomatis mengekstrak setiap gambar dari ZIP dan menjalankan OCR pada masing‑masing:

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> Anda dapat menyesuaikan `RecognitionSettings` untuk meningkatkan akurasi bagi bahasa tertentu atau kualitas gambar.

## Langkah 5: Cetak Hasil

Lakukan perulangan pada hasil dan cetak teks yang dikenali untuk setiap gambar di dalam arsip:

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

Output menampilkan indeks setiap gambar diikuti oleh string yang diekstrak, secara efektif **mengonversi gambar menjadi teks** dan **mengekstrak teks dari file arsip**.

## Masalah Umum & Pemecahan Masalah

| Masalah | Penyebab | Solusi |
|-------|-------|----------|
| Tidak ada teks yang dikembalikan | Kualitas gambar terlalu rendah | Pralakukan pemrosesan gambar (mis., binarisasi) atau sesuaikan `RecognitionSettings.Dpi` |
| Pengecualian saat membaca ZIP | Jalur arsip tidak valid | Verifikasi `fullPath` mengarah ke file `.zip` yang valid dan aplikasi memiliki izin membaca |
| Lisensi tidak diterapkan | File lisensi hilang atau tidak dimuat | Panggil `License license = new License(); license.SetLicense("Aspose.OCR.lic");` sebelum membuat instance `AsposeOcr` |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan Aspose.OCR untuk .NET tanpa lisensi?**  
A: Ya, versi percobaan gratis tersedia untuk evaluasi, tetapi versi berlisensi diperlukan untuk penerapan produksi.

**Q: Apakah pustaka ini mendukung arsip ZIP yang dilindungi kata sandi?**  
A: Saat ini, `RecognizeMultipleImages` bekerja dengan file ZIP standar. Untuk arsip terenkripsi, ekstrak gambar terlebih dahulu menggunakan pustaka pihak ketiga, kemudian berikan array gambar ke mesin OCR.

**Q: Bagaimana cara meningkatkan akurasi untuk teks tulisan tangan?**  
A: Aktifkan flag `RecognitionSettings.EnableHandwritingRecognition` dan berikan pengaturan DPI yang lebih tinggi (mis., 300).

**Q: Apakah ada cara untuk mendapatkan skor kepercayaan untuk setiap baris yang dikenali?**  
A: Setiap `RecognitionResult` berisi properti `Confidence` yang dapat Anda catat atau gunakan untuk menyaring hasil dengan kepercayaan rendah.

## Kesimpulan

Anda kini memiliki alur kerja lengkap yang siap produksi untuk **melakukan OCR pada gambar arsip**, **mengonversi gambar menjadi teks**, dan **mengekstrak teks dari file arsip** menggunakan Aspose.OCR untuk .NET. Integrasikan ini ke dalam aplikasi Anda untuk memungkinkan repositori dokumen yang dapat dicari, entri data otomatis, atau skenario apa pun yang memerlukan ekstraksi teks gambar secara massal.

## Sumber Daya Tambahan

- **Forum Aspose.OCR:** Untuk dukungan komunitas dan skenario lanjutan, kunjungi [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16).  
- **Lisensi Sementara:** Jika Anda memerlukan evaluasi jangka pendek, minta [lisensi sementara](https://purchase.aspose.com/temporary-license/).  
- **Dokumentasi Resmi:** Tetap up‑to‑date dengan perubahan API terbaru dengan meninjau [dokumentasi](https://reference.aspose.com/ocr/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-19  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose