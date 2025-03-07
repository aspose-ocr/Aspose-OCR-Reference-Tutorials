---
title: Atur Jumlah Thread dalam Pengenalan Gambar OCR
linktitle: Atur Jumlah Thread dalam Pengenalan Gambar OCR
second_title: Aspose.OCR .NET API
description: Buka efisiensi OCR di .NET. Atur jumlah thread dengan mudah menggunakan Aspose.OCR. Meningkatkan akurasi dan kecepatan.
weight: 11
url: /id/net/ocr-settings/set-threads-count/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur Jumlah Thread dalam Pengenalan Gambar OCR

## Perkenalan

Selamat datang di dunia Aspose.OCR untuk .NET, tempat teknologi Pengenalan Karakter Optik (OCR) mutakhir memenuhi integrasi tanpa batas ke dalam aplikasi .NET Anda. Dalam tutorial ini, kita akan mempelajari aspek spesifik: mengatur Jumlah Thread di Pengenalan Gambar OCR. Fitur canggih ini mengoptimalkan kinerja tugas OCR Anda, memastikan efisiensi dan akurasi.

## Prasyarat

Sebelum kita memulai perjalanan ini, pastikan Anda memiliki prasyarat berikut:

-  Aspose.OCR untuk .NET: Pastikan Anda telah menginstal perpustakaan. Jika belum, Anda dapat mendownloadnya[Di Sini](https://releases.aspose.com/ocr/net/).

- Contoh Gambar: Siapkan contoh gambar di direktori dokumen yang Anda tunjuk.

Sekarang, mari selami langkah-langkahnya.

## Impor Namespace

Pertama, pastikan untuk menyertakan namespace yang diperlukan dalam aplikasi .NET Anda:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Langkah 1: Inisialisasi Instans Aspose.OCR

Sekarang, inisialisasi instance kelas AsposeOcr di aplikasi Anda:

```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";

// Inisialisasi instance AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Langkah 2: Kenali Gambar

Selanjutnya, mari kenali teks pada gambar menggunakan Jumlah Thread yang ditentukan:

```csharp
// Kenali gambar
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    ThreadsCount = 2 // 0 - berarti penghitungan otomatis
});
```

## Langkah 3: Tampilkan Teks yang Dikenali

Setelah pengenalan, tampilkan teks yang dikenali:

```csharp
// Menampilkan teks yang dikenali
Console.WriteLine(result.RecognitionText);
```

## Kesimpulan

Kesimpulannya, mengatur Jumlah Thread dalam Pengenalan Gambar OCR menggunakan Aspose.OCR untuk .NET adalah proses mudah yang meningkatkan kinerja secara signifikan. Bereksperimenlah dengan jumlah thread yang berbeda untuk menemukan pengaturan optimal untuk aplikasi Anda.

## FAQ

### Q1: Bisakah saya mengatur jumlah thread ke nol untuk perhitungan otomatis?

 A1: Tentu saja! Pengaturan`ThreadsCount` ke nol memungkinkan Aspose.OCR menghitung jumlah thread optimal secara otomatis.

### Q2: Bagaimana cara mendapatkan lisensi sementara Aspose.OCR untuk .NET?

 A2: Kunjungi[Link ini](https://purchase.aspose.com/temporary-license/) untuk memperoleh lisensi sementara untuk tujuan pengujian.

### Q3: Di mana saya dapat menemukan dokumentasi komprehensif untuk Aspose.OCR untuk .NET?

 A3: Lihat[dokumentasi](https://reference.aspose.com/ocr/net/) untuk panduan rinci tentang Aspose.OCR.

### Q4: Apakah ada uji coba gratis yang tersedia untuk Aspose.OCR untuk .NET?

 A4: Ya, Anda dapat menjelajahi uji coba gratis[Di Sini](https://releases.aspose.com/).

### Q5: Butuh bantuan atau ingin terhubung dengan komunitas?

 A5: Kunjungi[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan dan interaksi komunitas.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
