---
title: Dapatkan Pilihan untuk Karakter yang Dikenali dalam Pengenalan Gambar OCR
linktitle: Dapatkan Pilihan untuk Karakter yang Dikenali dalam Pengenalan Gambar OCR
second_title: Aspose.OCR .NET API
description: Tingkatkan aplikasi .NET Anda dengan Aspose.OCR untuk pengenalan karakter yang akurat. Ikuti panduan langkah demi langkah kami untuk mengambil pilihan karakter yang dikenali dalam pengenalan gambar.
type: docs
weight: 10
url: /id/net/text-recognition/get-choices-for-recognized-characters/
---
## Perkenalan

Membuka kekuatan Pengenalan Karakter Optik (OCR) sangat penting di era digital saat ini, dan Aspose.OCR untuk .NET menonjol sebagai solusi tangguh untuk pengenalan karakter yang akurat. Dalam tutorial ini, kita akan mempelajari fitur spesifik: mendapatkan pilihan untuk karakter yang dikenali. Di akhir panduan ini, Anda akan mengintegrasikan fungsi ini dengan lancar ke dalam aplikasi .NET Anda.

## Prasyarat

Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:

- Pengetahuan dasar tentang pengembangan C# dan .NET.
- Visual Studio diinstal pada mesin Anda.
-  Aspose.OCR untuk perpustakaan .NET, yang dapat Anda unduh[Di Sini](https://releases.aspose.com/ocr/net/).

## Impor Namespace

Di proyek C# Anda, mulailah dengan mengimpor namespace yang diperlukan:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Langkah 1: Inisialisasi Aspose.OCR

Mulailah dengan menginisialisasi instance Aspose.OCR:

```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";

// Inisialisasi instance AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Langkah 2: Tentukan Jalur Gambar

Tetapkan jalur untuk gambar yang ingin Anda analisis:

```csharp
//Jalur Gambar
string fullPath = dataDir + "sample.png";
```

## Langkah 3: Kenali Gambar

Jalankan proses pengenalan gambar:

```csharp
// Kenali gambar
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    // Pengaturan default atau khusus
});
```

## Langkah 4: Dapatkan Pilihan untuk Karakter yang Diakui

Ambil pilihan untuk karakter yang dikenali:

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## Langkah 5: Cetak Hasilnya

Menampilkan teks pengenalan dan pilihan:

```csharp
// Hasil cetak
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

Ulangi langkah-langkah ini, sesuaikan sesuai dengan kebutuhan aplikasi Anda.

## Kesimpulan

Dalam tutorial ini, kita telah menjelajahi cara memanfaatkan Aspose.OCR untuk .NET guna mendapatkan pilihan karakter yang dikenali dalam pengenalan gambar. Fitur ini menambahkan dimensi baru pada kemampuan OCR Anda, sehingga meningkatkan fleksibilitas aplikasi Anda.

## FAQ

### Q1: Apakah Aspose.OCR untuk .NET cocok untuk pemrosesan dokumen skala besar?

A1: Tentu saja! Aspose.OCR untuk .NET dirancang untuk menangani dokumen dalam jumlah besar dengan efisiensi dan akurasi.

### Q2: Dapatkah saya menggunakan Aspose.OCR untuk .NET dalam aplikasi web?

A2: Ya, Anda dapat mengintegrasikan Aspose.OCR untuk .NET ke dalam aplikasi web, menjadikannya serbaguna untuk berbagai skenario pengembangan.

### Q3: Apakah ada opsi lisensi yang tersedia untuk Aspose.OCR untuk .NET?

 A3: Ya, Anda dapat menjelajahi opsi lisensi dan melakukan pembelian[Di Sini](https://purchase.aspose.com/buy).

### Q4: Bagaimana saya bisa mendapatkan dukungan atau mengajukan pertanyaan tentang Aspose.OCR untuk .NET?

 A4: Kunjungi[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk mendapatkan dukungan, mengajukan pertanyaan, dan terhubung dengan komunitas.

### Q5: Apakah ada uji coba gratis yang tersedia untuk Aspose.OCR untuk .NET?

 A5: Ya, Anda dapat mengakses uji coba gratis[Di Sini](https://releases.aspose.com/) untuk merasakan kemampuan Aspose.OCR untuk .NET.