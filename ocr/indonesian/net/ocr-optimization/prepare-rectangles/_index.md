---
title: Siapkan Persegi Panjang dalam Pengenalan Gambar OCR
linktitle: Siapkan Persegi Panjang dalam Pengenalan Gambar OCR
second_title: Aspose.OCR .NET API
description: Buka potensi Aspose.OCR untuk .NET dengan panduan komprehensif kami. Pelajari langkah demi langkah cara mempersiapkan persegi panjang untuk pengenalan gambar. Tingkatkan aplikasi .NET Anda dengan integrasi OCR yang lancar.
type: docs
weight: 11
url: /id/net/ocr-optimization/prepare-rectangles/
---
## Perkenalan

Dalam lanskap teknologi yang terus berkembang, Pengenalan Karakter Optik (OCR) memainkan peran penting dalam mengubah gambar menjadi teks yang dapat dibaca mesin. Aspose.OCR untuk .NET menonjol sebagai solusi tangguh bagi pengembang yang mencari integrasi kemampuan OCR ke dalam aplikasi .NET mereka. Dalam panduan komprehensif ini, kita akan menjelajahi proses menyiapkan persegi panjang dalam pengenalan gambar OCR menggunakan Aspose.OCR untuk .NET.

## Prasyarat

Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:

- Pengetahuan kerja tentang pengembangan .NET.
-  Aspose.OCR untuk perpustakaan .NET diinstal. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/ocr/net/).
- Pemahaman dasar tentang konsep pengenalan gambar.

## Impor Namespace

Mari kita mulai dengan mengimpor namespace yang diperlukan untuk memulai perjalanan OCR kita:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Langkah 1: Siapkan Direktori Dokumen Anda

 Mulailah dengan menentukan direktori tempat dokumen Anda disimpan. Mengganti`"Your Document Directory"` dengan jalur sebenarnya ke dokumen Anda.

```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";

// Inisialisasi instance AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Langkah 2: Kenali Gambar dengan Banyak Persegi Panjang

Pada langkah ini, kami akan mendemonstrasikan cara mengenali teks dari gambar menggunakan beberapa persegi panjang. Ikuti sub-langkah berikut:

### 2.1 Mendefinisikan Persegi Panjang

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 Melakukan Pengenalan OCR

```csharp
// kasus pertama
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Menampilkan teks yang dikenali
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Langkah 3: Kenali Gambar dengan Pengaturan Pengenalan

Pada langkah ini, kami akan menampilkan metode alternatif menggunakan RecognitionSettings untuk pengenalan gambar:

### 3.1 Tentukan Pengaturan Pengenalan

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 Menampilkan Teks yang Dikenali

```csharp
// Menampilkan teks yang dikenali
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Kesimpulan

Selamat! Anda telah berhasil menavigasi proses menyiapkan persegi panjang dalam pengenalan gambar OCR menggunakan Aspose.OCR untuk .NET. Panduan ini memberdayakan Anda untuk mengintegrasikan OCR dengan lancar ke dalam aplikasi .NET Anda, sehingga meningkatkan kemampuan pengenalan teksnya.

### FAQ

### Q1: Dapatkah saya menggunakan Aspose.OCR untuk .NET dengan kerangka .NET lainnya?

A1: Ya, Aspose.OCR untuk .NET kompatibel dengan berbagai kerangka .NET.

### Q2: Apakah tersedia uji coba gratis untuk Aspose.OCR untuk .NET?

 A2: Tentu saja! Anda dapat mengakses uji coba gratis[Di Sini](https://releases.aspose.com/).

### Q3: Bagaimana cara mendapatkan dukungan untuk Aspose.OCR untuk .NET?

 A3: Kunjungi[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan khusus.

### Q4: Bisakah saya mendapatkan lisensi sementara untuk tujuan pengujian?

 A4: Ya, Anda bisa mendapatkan lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).

### Q5: Di mana saya dapat menemukan dokumentasi Aspose.OCR untuk .NET?

 A5: Dokumentasi tersedia[Di Sini](https://reference.aspose.com/ocr/net/).