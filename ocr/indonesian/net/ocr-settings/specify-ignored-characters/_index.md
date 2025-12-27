---
date: 2025-12-27
description: Jelajahi dukungan bahasa OCR tingkat lanjut dan kemampuan dengan Aspose.OCR
  untuk .NET. Efisien, akurat, dan ramah pengembang.
linktitle: OCR Language Support – Ignored Characters in Image Recognition
second_title: Aspose.OCR .NET API
title: Dukungan Bahasa OCR – Karakter yang Diabaikan dalam Pengenalan Gambar
url: /id/net/ocr-settings/specify-ignored-characters/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dukungan Bahasa OCR: Menentukan Karakter yang Diabaikan dalam Pengenalan Gambar

## Introduction

Dukungan bahasa OCR merupakan fondasi otomasi dokumen modern, memungkinkan aplikasi membaca teks dari gambar dengan berbagai alfabet dan simbol. Dalam tutorial ini Anda akan belajar cara memberi tahu **Aspose.OCR for .NET** untuk mengabaikan karakter tertentu selama pengenalan—trik penting ketika Anda membutuhkan output yang lebih bersih atau ingin menyaring noise seperti nomor halaman atau simbol dekoratif. Pada akhir panduan, Anda akan memiliki potongan kode siap‑jalankan yang mendemonstrasikan fitur ini secara menyeluruh.

## Quick Answers
- **Apa arti “karakter yang diabaikan”?** Karakter yang dilewati oleh mesin OCR saat membangun string hasil.  
- **Mengapa menggunakannya?** Meningkatkan akurasi ketika simbol tertentu tidak relevan dengan logika bisnis Anda.  
- **Metode API mana yang menangani ini?** `RecognitionSettings.IgnoredCharacters`.  
- **Bisakah saya menggabungkannya dengan paket bahasa?** Ya—karakter yang diabaikan bekerja bersama bahasa apa pun yang Anda muat.  
- **Apakah lisensi diperlukan?** Lisensi sementara atau penuh diperlukan untuk penggunaan produksi.

## Prerequisites

Before delving into the rich functionality provided by Aspose.OCR for .NET, make sure you have the following prerequisites in place:

1. Aspose.OCR Installation  

   Pastikan Anda telah berhasil menginstal Aspose.OCR untuk .NET. Anda dapat menemukan file yang diperlukan di [halaman unduhan](https://releases.aspose.com/ocr/net/).

2. Document Directory Setup  

   Siapkan direktori khusus untuk dokumen Anda. Ini akan penting untuk menjalankan contoh secara mulus. Perbarui variabel `dataDir` dalam contoh dengan path ke direktori dokumen Anda.

3. Temporary License (Optional)  

   Jika Anda menjelajahi Aspose.OCR untuk .NET dengan lisensi sementara, dapatkan dari [sini](https://purchase.aspose.com/temporary-license/).

## Import Namespaces

To kickstart your journey with Aspose.OCR for .NET, you'll need to import the necessary namespaces. Add the following lines to your code:

```csharp
using System.IO;

using Aspose.OCR;
using System;
```

## Why Specify Ignored Characters?

Dalam banyak skenario dunia nyata—seperti memproses faktur, kwitansi, atau formulir multibahasa—Anda mungkin menemukan karakter berulang yang bukan bagian dari data bermakna (misalnya, tanda hubung sebagai pemisah, nomor halaman, atau simbol dekoratif). Dengan memberi tahu mesin OCR untuk melewati karakter tersebut, Anda mengurangi upaya pasca‑pemrosesan dan meningkatkan keandalan keseluruhan analitik hilir.

## Step‑by‑Step Guide

### Step 1: Set Up Your Document Directory

Mulailah dengan menentukan direktori tempat dokumen Anda disimpan. Ganti `"Your Document Directory"` dengan path sebenarnya ke dokumen Anda.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

### Step 2: Initialize Aspose.OCR

Buat instance mesin OCR. Objek ini akan menangani semua panggilan pengenalan selanjutnya.

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Step 3: Recognize Image with Ignored Characters

Berikan file gambar bersama dengan objek `RecognitionSettings` yang mencantumkan karakter yang ingin Anda abaikan. Pada contoh ini kami mengabaikan karakter `a`, `b`, dan `1`.

```csharp
// Recognize image with specified ignored characters
RecognitionResult result = api.RecognizeImage(dataDir + "SpanishOCR.bmp", new RecognitionSettings
{
    IgnoredCharacters = "ab1"
});
```

### Step 4: Display Recognized Text

Terakhir, keluarkan teks yang telah dibersihkan ke konsol atau tujuan lain yang Anda pilih.

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);
```

## Common Issues & Tips

- **Path tidak benar:** Pastikan `dataDir` diakhiri dengan pemisah path (`\` atau `/`) yang sesuai untuk OS Anda.  
- **Bahasa tidak didukung:** Mesin OCR harus memiliki paket bahasa untuk gambar sumber; jika tidak, karakter yang diabaikan tidak akan diterapkan dengan benar.  
- **Kesalahan lisensi:** Jika Anda melihat pengecualian lisensi, pastikan file lisensi sementara direferensikan dengan benar dalam proyek Anda.

## Conclusion

Aspose.OCR untuk .NET memberi kekuatan kepada pengembang dengan kemampuan OCR tingkat lanjut, mempermudah proses mengubah gambar menjadi teks yang dapat diedit dan dapat dicari. Dengan mengikuti panduan langkah‑demi‑langkah ini, Anda telah belajar cara mengecualikan karakter yang tidak diinginkan, menjadikan pipeline OCR Anda lebih bersih dan lebih dapat diandalkan. Jelajahi [dokumentasi](https://reference.aspose.com/ocr/net/) untuk wawasan lebih dalam dan temukan bagaimana Aspose.OCR dapat meningkatkan proyek OCR Anda.

## Frequently Asked Questions

### Q1: Apakah saya dapat menggunakan Aspose.OCR untuk .NET dalam proyek non‑komersial?

A1: Ya, Aspose.OCR untuk .NET dapat digunakan baik dalam proyek komersial maupun non‑komersial. Lihat [detail lisensi](https://purchase.aspose.com/buy) untuk informasi lebih lanjut.

### Q2: Apakah tersedia percobaan gratis?

A2: Tentu! Anda dapat mengakses percobaan gratis [di sini](https://releases.aspose.com/) untuk mengeksplorasi fitur dan manfaat Aspose.OCR untuk .NET sebelum membuat komitmen.

### Q3: Bagaimana saya dapat mendapatkan dukungan untuk Aspose.OCR?

A3: Untuk pertanyaan atau bantuan, kunjungi [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk terhubung dengan komunitas dan mencari saran ahli.

### Q4: Bahasa apa saja yang didukung Aspose.OCR?

A4: Aspose.OCR mendukung berbagai bahasa, menjadikannya pilihan serbaguna untuk tugas OCR. Lihat dokumentasi untuk daftar lengkap.

### Q5: Apakah saya dapat membeli lisensi sementara untuk Aspose.OCR?

A5: Ya, jika Anda memerlukan lisensi sementara, Anda dapat mendapatkannya [di sini](https://purchase.aspose.com/temporary-license/) untuk penggunaan jangka pendek.

---

**Last Updated:** 2025-12-27  
**Tested With:** Aspose.OCR 23.12 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}