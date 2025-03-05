---
title: Dapatkan Hasil sebagai JSON dalam Pengenalan Gambar OCR
linktitle: Dapatkan Hasil sebagai JSON dalam Pengenalan Gambar OCR
second_title: Aspose.OCR .NET API
description: Bebaskan kekuatan Aspose.OCR untuk .NET. Pelajari cara mendapatkan hasil OCR dalam format JSON dengan mudah. Tingkatkan pengenalan gambar Anda dengan panduan langkah demi langkah ini.
type: docs
weight: 12
url: /id/net/text-recognition/get-result-as-json/
---
## Perkenalan

Dalam lanskap teknologi yang terus berkembang, Pengenalan Karakter Optik (OCR) berperan sebagai alat penting yang memungkinkan mesin menafsirkan dan mengekstrak informasi dari gambar. Aspose.OCR untuk .NET memberdayakan pengembang untuk mengintegrasikan kemampuan OCR ke dalam aplikasi mereka dengan lancar. Tutorial ini akan memandu Anda melalui proses mendapatkan hasil OCR dalam format JSON menggunakan Aspose.OCR untuk .NET.

## Prasyarat

Sebelum mempelajari tutorial, pastikan Anda memiliki prasyarat berikut:

- Visual Studio: Pastikan Anda telah menginstal Visual Studio di sistem Anda.
-  Aspose.OCR untuk .NET: Unduh dan instal perpustakaan dari[Aspose.OCR untuk dokumentasi .NET](https://reference.aspose.com/ocr/net/).

## Impor Namespace

Untuk memulai integrasi, impor namespace yang diperlukan:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Langkah 1: Siapkan Direktori Dokumen Anda

Mulailah dengan menentukan jalur ke direktori dokumen Anda:

```csharp
string dataDir = "Your Document Directory";
```

## Langkah 2: Inisialisasi Aspose.OCR

Buat instance Aspose.OCR untuk memanfaatkan fungsinya:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Langkah 3: Kenali Gambar

Memanfaatkan mesin OCR untuk mengenali teks dalam gambar:

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

## Langkah 4: Tampilkan Hasil Pengenalan di JSON

Tampilkan hasil pengenalan dalam format JSON:

```csharp
Console.WriteLine(result.GetJson());
```

## Langkah 5: Selesaikan Eksekusi

Akhiri proses dengan pesan sukses:

```csharp
Console.WriteLine("GetResultAsJson executed successfully");
```

## Kesimpulan

Aspose.OCR untuk .NET menyederhanakan integrasi kemampuan OCR ke dalam aplikasi Anda. Dengan mengikuti panduan langkah demi langkah ini, Anda dapat dengan mudah memperoleh hasil OCR dalam format JSON, sehingga meningkatkan efisiensi alur kerja pengenalan gambar Anda.

## FAQ

### Q1: Apakah uji coba gratis tersedia untuk Aspose.OCR untuk .NET?

 A1: Ya, Anda dapat mengakses uji coba gratis[Di Sini](https://releases.aspose.com/).

### Q2. Di mana saya dapat menemukan dokumentasi Aspose.OCR untuk .NET?

 A2: Dokumentasi tersedia[Di Sini](https://reference.aspose.com/ocr/net/).

### Q3. Bagaimana saya bisa mendapatkan lisensi sementara Aspose.OCR untuk .NET?

 A3: Kunjungi[Link ini](https://purchase.aspose.com/temporary-license/) untuk opsi lisensi sementara.

### Q4. Di mana saya bisa mendapatkan dukungan komunitas untuk Aspose.OCR untuk .NET?

 A4: Terlibat dengan komunitas di[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16).

### Q5: Dapatkah saya membeli lisensi Aspose.OCR untuk .NET?

 A5: Ya, Anda bisa membeli lisensinya[Di Sini](https://purchase.aspose.com/buy).