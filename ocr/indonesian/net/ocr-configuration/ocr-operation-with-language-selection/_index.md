---
date: 2026-02-25
description: Pelajari cara mengekstrak teks gambar dengan C# menggunakan Aspose.OCR
  untuk .NET. Panduan langkah demi langkah ini menunjukkan OCR multibahasa, pemilihan
  bahasa, dan tips praktis.
linktitle: Extract image text C# with language selection using Aspose.OCR
second_title: Aspose.OCR .NET API
title: Ekstrak teks gambar C# dengan pemilihan bahasa menggunakan Aspose.OCR
url: /id/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak teks gambar C# dengan pilihan bahasa menggunakan Aspose.OCR

## Pendahuluan

Jika Anda perlu **extract image text C#** dari gambar dan PDF dalam aplikasi .NET, Aspose.OCR untuk .NET menawarkan solusi yang cepat, akurat, dan mendukung bahasa. Dalam tutorial ini kami akan membahas contoh dunia nyata yang memperlihatkan pengenalan gambar OCR dengan pilihan bahasa, sehingga Anda dapat mengambil teks multibahasa dari gambar hanya dengan beberapa baris kode. Pada akhir tutorial Anda akan melihat betapa mudahnya mengintegrasikan OCR ke dalam proyek C# Anda dan mengapa pendekatan ini menjadi pilihan yang solid untuk beban kerja produksi.

## Jawaban Cepat
- **Apa yang dilakukan Aspose.OCR?** Ia mengenali teks cetak dan tulisan tangan dalam gambar serta mengembalikan teks yang diekstrak.  
- **Apakah saya dapat memilih bahasa?** Ya – Anda dapat menentukan bahasa yang didukung seperti English, German, Spanish, Chinese, dll.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi diperlukan untuk penggunaan produksi.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Apakah koreksi kemiringan otomatis?** Anda dapat mengaktifkan `AutoSkew` dan menyesuaikan pengaturan `SkewAngle`.  

## Apa itu “extract image text C#”?

Mengekstrak teks gambar dalam C# berarti menggunakan sebuah pustaka untuk membaca konten visual sebuah gambar (PNG, JPEG, TIFF, dll.) dan mengubahnya menjadi teks yang dapat dicari dan diedit. Aspose.OCR menyediakan kemampuan ini secara lokal, tanpa mengirim data ke layanan eksternal, sehingga alur kerja Anda tetap aman dan patuh.

## Mengapa Memilih Aspose.OCR untuk Tugas OCR?

- **Akurasi tinggi** pada berbagai jenis font dan kualitas gambar.  
- **Pemilihan bahasa bawaan** menghilangkan kebutuhan paket bahasa eksternal.  
- **API sederhana** yang terintegrasi mulus dengan proyek C# yang ada, memudahkan **extract image text C#**.  
- **Tanpa ketergantungan eksternal** – semuanya berjalan secara lokal, menjaga keamanan data Anda.  

## Prasyarat

Sebelum kita masuk ke kode, pastikan Anda telah menyiapkan hal‑hal berikut:

- Aspose.OCR untuk .NET: Pastikan Anda telah menginstal pustaka Aspose.OCR. Anda dapat mengunduhnya dari [halaman unduhan Aspose.OCR untuk .NET](https://releases.aspose.com/ocr/net/).

- Lingkungan Pengembangan: Siapkan lingkungan kerja dengan aplikasi .NET. Jika belum melakukannya, lihat [dokumentasi](https://reference.aspose.com/ocr/net/) untuk petunjuk detail.

## Impor Namespace

Dalam aplikasi .NET Anda, mulailah dengan mengimpor namespace yang diperlukan:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Langkah 1: Inisialisasi Aspose.OCR

Mulailah dengan menginisialisasi sebuah instance dari kelas Aspose.OCR. Ini menyiapkan fondasi untuk menggunakan kemampuan OCR dalam aplikasi Anda.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Langkah 2: Tentukan Jalur Gambar

Selanjutnya, definisikan jalur ke gambar yang ingin Anda proses dengan OCR. Pastikan gambar dapat diakses oleh aplikasi Anda.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Langkah 3: Kenali Gambar dengan Pilihan Bahasa

Berikutnya adalah operasi OCR inti. Manfaatkan pustaka Aspose.OCR untuk mengenali teks dari gambar yang telah ditentukan. Sesuaikan pengaturan pengenalan, termasuk pilihan bahasa, untuk mengoptimalkan proses **extract image text C#**.

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

- **Pemilihan bahasa yang salah** – Jika output terlihat berantakan, periksa kembali bahwa properti `Language` sesuai dengan bahasa gambar sumber.  
- **Gambar miring** – Aktifkan `AutoSkew` atau sesuaikan secara manual `SkewAngle` untuk akurasi lebih baik pada pemindaian yang miring.  
- **File besar** – Proses gambar berukuran besar secara bertahap atau kurangi resolusi sebelum memberi ke `RecognizeImage` untuk menghemat memori.  

## Pertanyaan yang Sering Diajukan

**Q: Apakah Aspose.OCR cocok untuk pengenalan teks multibahasa?**  
A: Ya, Aspose.OCR mendukung berbagai bahasa, memberikan fleksibilitas untuk tugas OCR multibahasa.

**Q: Bisakah saya menyesuaikan pengaturan OCR untuk karakteristik gambar tertentu?**  
A: Tentu! Sesuaikan parameter seperti sudut kemiringan, pengenalan baris, dan deteksi area untuk mengoptimalkan OCR pada berbagai skenario.

**Q: Di mana saya dapat menemukan dukungan tambahan atau diskusi komunitas?**  
A: Kunjungi [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan dan diskusi dengan komunitas.

**Q: Apakah ada versi percobaan gratis?**  
A: Ya, jelajahi [free trial](https://releases.aspose.com/) untuk merasakan kemampuan Aspose.OCR.

**Q: Bagaimana cara membeli Aspose.OCR untuk .NET?**  
A: Untuk membeli, kunjungi [halaman pembelian](https://purchase.aspose.com/buy).

## Kesimpulan

Selamat! Anda telah mempelajari **cara extract image text C#** dengan pilihan bahasa menggunakan Aspose.OCR untuk .NET. Tutorial ini menunjukkan cara mengkonfigurasi mesin OCR, memilih bahasa yang tepat, dan menangani hasilnya, memberikan fondasi yang kuat untuk membangun fitur ekstraksi teks multibahasa dalam aplikasi Anda.

---

**Last Updated:** 2026-02-25  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}