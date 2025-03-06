---
title: Dapatkan Persegi Panjang untuk Paragraf dalam Pengenalan Gambar OCR
linktitle: Dapatkan Persegi Panjang untuk Paragraf dalam Pengenalan Gambar OCR
second_title: Aspose.OCR .NET API
description: Buka kemampuan OCR tingkat lanjut dengan Aspose.OCR untuk .NET. Ekstrak paragraf persegi panjang dengan mudah.
weight: 11
url: /id/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Persegi Panjang untuk Paragraf dalam Pengenalan Gambar OCR

## Perkenalan

Selamat datang di panduan komprehensif kami tentang memanfaatkan Aspose.OCR untuk .NET untuk mengekstrak paragraf persegi panjang dalam pengenalan gambar OCR. Jika Anda ingin meningkatkan kemampuan pemrosesan dokumen dan memanfaatkan kekuatan Pengenalan Karakter Optik (OCR) dalam aplikasi .NET, Anda berada di tempat yang tepat.

## Prasyarat

Sebelum kita mendalami tutorialnya, pastikan Anda memiliki prasyarat berikut:

- Pengetahuan dasar tentang pengembangan C# dan .NET.
-  Lingkungan pengembangan yang disiapkan dengan Aspose.OCR untuk .NET. Jika Anda belum melakukannya, Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/ocr/net/).
- Pemahaman tentang konsep pemrosesan gambar dan pentingnya OCR dalam mengekstraksi teks dari gambar.

## Impor Namespace

Dalam kode C# Anda, pastikan Anda telah mengimpor namespace yang diperlukan untuk menggunakan Aspose.OCR secara efisien. Sertakan yang berikut ini di bagian atas file Anda:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Langkah 1: Siapkan Direktori Dokumen Anda

Mulailah dengan menginisialisasi jalur ke direktori dokumen Anda tempat gambar untuk pemrosesan OCR disimpan:

```csharp
string dataDir = "Your Document Directory";
```

## Langkah 2: Inisialisasi Instans AsposeOcr

Buat instance kelas AsposeOcr untuk mendapatkan akses ke fungsi OCR:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Langkah 3: Tentukan Jalur Gambar

Tentukan jalur lengkap ke gambar yang ingin Anda proses:

```csharp
string fullPath = dataDir + "sample.png";
```

## Langkah 4: Kenali Gambar dan Dapatkan Paragraf Persegi Panjang

 Panggil`GetRectangles` metode untuk mendapatkan persegi panjang untuk paragraf dalam gambar OCR. Mengatur`detect_areas` ke`true` jika Anda ingin mengekstrak paragraf:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Langkah 5: Cetak Hasil

Cetak koordinat area yang diidentifikasi:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Langkah 6: Kesimpulan

Selamat! Anda telah berhasil menjalankan proses pengenalan gambar OCR untuk mendapatkan persegi panjang untuk paragraf menggunakan Aspose.OCR untuk .NET.

## Kesimpulan

Dalam tutorial ini, kami telah menjelajahi langkah-langkah mendasar untuk mengintegrasikan Aspose.OCR untuk .NET ke dalam aplikasi Anda, sehingga memungkinkan Anda mengekstrak persegi panjang paragraf dari gambar yang diproses OCR. Aspose.OCR menyederhanakan penerapan OCR, menjadikannya alat yang berharga untuk pemrosesan dokumen dan ekstraksi teks.

## FAQ

### Q1: Apakah Aspose.OCR kompatibel dengan format gambar yang berbeda?

A1: Ya, Aspose.OCR mendukung berbagai format gambar, termasuk PNG, JPEG, dan TIFF.

### Q2: Dapatkah saya menggunakan Aspose.OCR untuk pemrosesan batch beberapa gambar?

A2: Tentu saja! Aspose.OCR memfasilitasi pemrosesan batch untuk menangani banyak gambar dengan lancar.

### Q3: Apakah tersedia uji coba gratis untuk Aspose.OCR untuk .NET?

 A3: Ya, Anda dapat menjelajahi uji coba gratis[Di Sini](https://releases.aspose.com/).

### Q4: Bagaimana cara mendapatkan lisensi sementara untuk Aspose.OCR?

 A4: Anda dapat memperoleh lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).

### Q5: Di mana saya dapat menemukan dukungan dan diskusi tambahan terkait Aspose.OCR?

 A5: Pergilah ke[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan dan diskusi komunitas.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
