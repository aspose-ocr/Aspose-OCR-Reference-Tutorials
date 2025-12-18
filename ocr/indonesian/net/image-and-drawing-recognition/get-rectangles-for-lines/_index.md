---
date: 2025-12-17
description: Pelajari cara mendapatkan persegi panjang baris OCR menggunakan Aspose.OCR
  untuk .NET untuk mengenali baris teks dalam gambar dan mengekstrak koordinat baris
  dengan mudah.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: Dapatkan Persegi Panjang Garis OCR untuk Baris Teks Gambar
url: /id/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Persegi Panjang Garis OCR untuk Baris Teks Gambar

## Pendahuluan

Dalam tutorial ini Anda akan menemukan **cara mendapatkan persegi panjang garis OCR** dengan Aspose.OCR untuk .NET. Pada akhir panduan Anda akan dapat **mengenali baris teks dalam sebuah gambar** dan **mengekstrak koordinat baris** untuk setiap baris yang terdeteksi—sempurna untuk pemrosesan lanjutan seperti analisis tata letak, ekstraksi data, atau rendering khusus.

## Jawaban Cepat
- **Apa arti “get OCR line rectangles”?** Itu mengembalikan kotak pembatas setiap baris teks yang terdeteksi dalam sebuah gambar.  
- **Metode API mana yang digunakan?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Format gambar yang didukung?** PNG, JPEG, BMP, TIFF, dan lainnya.  
- **Bisakah saya menjalankannya di .NET Core?** Ya, Aspose.OCR sepenuhnya mendukung .NET Core dan .NET 5/6.

## Prasyarat

Sebelum memulai tutorial, pastikan Anda memiliki prasyarat berikut:

- Pengetahuan dasar tentang C# dan pengembangan .NET.  
- Lingkungan pengembangan terintegrasi (IDE) seperti Visual Studio.  
- Perpustakaan Aspose.OCR untuk .NET terpasang. Anda dapat mengunduhnya [di sini](https://releases.aspose.com/ocr/net/).  
- Contoh gambar yang berisi teks untuk pengenalan OCR.

## Impor Namespace

Pastikan Anda telah mengimpor namespace yang diperlukan ke proyek Anda. Tambahkan baris berikut ke bagian atas file C# Anda:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Sekarang, mari kita uraikan proses mendapatkan persegi panjang untuk baris dalam pengenalan gambar OCR menjadi langkah‑langkah yang mudah diikuti.

## Langkah 1: Siapkan Direktori Dokumen Anda

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Ganti `"Your Document Directory"` dengan jalur sebenarnya ke folder yang berisi contoh gambar Anda.

## Langkah 2: Inisialisasi Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Buat instance dari kelas `AsposeOcr` untuk mengakses fungsi OCR.

## Langkah 3: Tentukan Jalur Gambar

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Tentukan jalur lengkap ke gambar yang ingin Anda lakukan OCR.

## Langkah 4: Kenali Gambar dan Dapatkan Persegi Panjang

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Metode `GetRectangles` mengembalikan daftar objek `Rectangle`, masing‑masing mewakili koordinat baris teks yang terdeteksi. Ini adalah inti dari **mendapatkan persegi panjang garis OCR**.

## Langkah 5: Cetak Hasil

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Cetak koordinat area yang terdeteksi ke konsol. Anda akan melihat nilai‑nilai yang dapat Anda gunakan nanti untuk **mengekstrak koordinat baris** untuk pemrosesan khusus.

## Mengapa Menggunakan Aspose.OCR untuk Persegi Panjang Garis?

- **Akurasi tinggi** – Algoritma canggih mendeteksi garis bahkan pada gambar yang berisik atau miring.  
- **Lintas‑platform** – Berfungsi pada .NET Framework, .NET Core, dan .NET 5/6.  
- **Tanpa ketergantungan eksternal** – Perpustakaan .NET murni, tanpa DLL native yang harus disertakan.  
- **Output kaya** – Selain persegi panjang garis, Anda juga dapat mengambil kata, karakter, dan skor kepercayaan.

## Masalah Umum dan Solusinya

| Masalah | Solusi |
|-------|----------|
| **Tidak ada persegi panjang yang dikembalikan** | Pastikan gambar berisi teks horizontal yang jelas dan `AreasType.LINES` telah ditentukan. |
| **Koordinat tidak tepat** | Verifikasi DPI gambar; gambar beresolusi rendah dapat menyebabkan batas yang tidak akurat. |
| **Bottleneck kinerja pada gambar besar** | Ubah ukuran gambar ke resolusi yang wajar sebelum memanggil `GetRectangles`. |
| **Pengecualian lisensi** | Gunakan lisensi percobaan untuk pengujian; terapkan lisensi penuh untuk produksi agar menghindari batas evaluasi. |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya mengekstrak kata individual alih‑alih seluruh baris?**  
A: Ya, gunakan `AreasType.WORDS` dengan metode `GetRectangles` yang sama untuk mendapatkan kotak pembatas tingkat kata.

**Q: Apakah API mendukung PDF multi‑halaman?**  
A: Konversi setiap halaman PDF menjadi gambar terlebih dahulu, kemudian panggil `GetRectangles` pada setiap gambar.

**Q: Bagaimana cara menangani teks yang diputar?**  
A: Aktifkan opsi auto‑rotate di pengaturan OCR atau pra‑putar gambar sebelum diproses.

**Q: Apakah ada cara untuk mendapatkan skor kepercayaan untuk setiap baris?**  
A: Setelah mendapatkan persegi panjang, panggil `api.RecognizeImage(...).Lines` untuk mengakses objek baris yang menyertakan nilai kepercayaan.

**Q: Versi .NET apa yang kompatibel?**  
A: Perpustakaan ini bekerja dengan .NET Framework 4.5+, .NET Core 3.1+, dan .NET 5/6.

## Kesimpulan

Selamat! Anda telah berhasil **mendapatkan persegi panjang garis OCR** untuk sebuah gambar menggunakan Aspose.OCR untuk .NET. Dengan kotak pembatas di tangan, Anda kini dapat memasukkan koordinat baris ke dalam alur kerja lanjutan seperti rendering khusus, ekstraksi data, atau analisis tata letak.

---

**Terakhir Diperbarui:** 2025-12-17  
**Diuji Dengan:** Aspose.OCR 24.11 untuk .NET  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}