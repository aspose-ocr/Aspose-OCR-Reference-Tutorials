---
title: Tentukan Karakter yang Diizinkan dalam Pengenalan Gambar OCR
linktitle: Tentukan Karakter yang Diizinkan dalam Pengenalan Gambar OCR
second_title: Aspose.OCR .NET API
description: Buka kunci OCR yang tepat di .NET dengan Aspose.OCR. Kenali teks dari gambar dengan mudah. Unduh sekarang untuk pengalaman pengembangan yang transformatif.
weight: 13
url: /id/net/ocr-settings/specify-allowed-characters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tentukan Karakter yang Diizinkan dalam Pengenalan Gambar OCR

## Perkenalan

Dalam lanskap teknologi yang terus berkembang, Pengenalan Karakter Optik (OCR) telah muncul sebagai alat transformatif yang memungkinkan mesin memahami teks dari gambar. Aspose.OCR untuk .NET menonjol sebagai solusi yang kuat, memberikan integrasi tanpa batas bagi pengembang yang mencari kemampuan OCR yang kuat dalam aplikasi .NET mereka.

## Prasyarat

Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:

- Pengetahuan kerja tentang pengembangan .NET.
-  Aspose.OCR untuk perpustakaan .NET. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/ocr/net/).
- Keakraban dengan Visual Studio atau lingkungan pengembangan .NET pilihan lainnya.

## Impor Namespace

Dalam proyek .NET Anda, impor namespace yang diperlukan untuk memanfaatkan fungsionalitas Aspose.OCR untuk .NET secara efektif:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Sekarang, mari kita bagi tutorialnya menjadi serangkaian langkah komprehensif:

## Langkah 1: Tentukan Karakter yang Diizinkan dalam Pengenalan Gambar OCR

Untuk memulai, siapkan jalur ke direktori dokumen Anda:

```csharp
string dataDir = "Your Document Directory";
```

## Langkah 2: Inisialisasi Aspose.OCR dengan Simbol yang Diizinkan

Buat instance AsposeOcr, tentukan simbol yang diizinkan. Dalam hal ini, kami mengizinkan angka (0-9):

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## Langkah 3: Kenali Gambar

Manfaatkan instance AsposeOcr untuk mengenali teks dari gambar:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## Langkah 4: Tampilkan Teks yang Dikenali

Cetak teks yang dikenali ke konsol:

```csharp
Console.WriteLine(result);
```

## Langkah 5: Kasus Kedua - Kenali Gambar dengan Pengaturan Tertentu

Inisialisasi instance AsposeOcr lainnya, kali ini dengan pengaturan yang lebih spesifik:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## Langkah 6: Tampilkan Teks yang Dikenali Kasus Kedua

Cetak teks yang dikenali dari case kedua ke konsol:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## Langkah 7: Eksekusi Berhasil

Terakhir, konfirmasikan keberhasilan eksekusi tutorial SpecifyAllowedCharacters:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Dengan mengikuti langkah-langkah ini, Anda telah membuka kemampuan untuk menentukan karakter yang diizinkan dalam pengenalan gambar OCR menggunakan Aspose.OCR untuk .NET.

## Kesimpulan

Aspose.OCR untuk .NET memberdayakan pengembang untuk mengintegrasikan kemampuan OCR ke dalam aplikasi mereka dengan lancar, membuka pintu bagi solusi inovatif di berbagai domain. Manfaatkan kekuatan OCR dan tingkatkan proyek Anda dengan pengenalan teks yang akurat.

## FAQ

### Q1: Apakah Aspose.OCR untuk .NET cocok untuk pemula dan pengembang berpengalaman?

A1: Tentu saja! Aspose.OCR untuk .NET melayani pengembang dari semua tingkat keahlian, menyediakan fungsionalitas intuitif untuk integrasi yang lancar.

### Q2: Dapatkah saya menggunakan Aspose.OCR untuk .NET untuk mengenali karakter dalam berbagai bahasa?

A2: Ya, Aspose.OCR mendukung pengenalan dalam berbagai bahasa, menjadikannya serbaguna untuk beragam aplikasi.

### Q3: Seberapa sering Aspose.OCR untuk .NET diperbarui?

 A3: Pembaruan dirilis secara berkala untuk memastikan kompatibilitas dengan teknologi terbaru dan mengatasi potensi masalah. Periksalah[dokumentasi](https://reference.aspose.com/ocr/net/) untuk informasi terbaru.

### Q4: Apakah ada uji coba gratis yang tersedia untuk Aspose.OCR untuk .NET?

 A4: Ya, Anda dapat menjelajahi kemampuan Aspose.OCR dengan mengunduh[uji coba gratis](https://releases.aspose.com/).

### Q5: Di mana saya dapat mencari bantuan atau terhubung dengan komunitas untuk mendapatkan dukungan?

 A5: Kunjungi[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk terlibat dengan masyarakat dan mendapatkan bantuan ahli.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
