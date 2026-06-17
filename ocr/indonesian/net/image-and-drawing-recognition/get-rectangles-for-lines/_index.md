---
date: 2026-02-22
description: Pelajari cara melakukan analisis tata letak OCR dengan mengenali baris
  teks dalam gambar dan mengekstrak persegi panjang baris menggunakan Aspose.OCR untuk
  .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Analisis Tata Letak OCR – Dapatkan Persegi Panjang Baris dari Gambar
url: /id/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analisis Tata Letak OCR – Dapatkan Persegi Panjang Garis dari Gambar

## Pendahuluan

Dalam tutorial ini Anda akan menemukan **cara mendapatkan persegi panjang baris OCR** dengan Aspose.OCR untuk .NET. Pada akhir panduan Anda akan dapat **mengenali baris teks dalam sebuah gambar** dan **mengekstrak koordinat baris** untuk setiap baris yang terdeteksi—sempurna untuk pemrosesan lanjutan seperti **analisis tata letak OCR**, ekstraksi data, atau rendering khusus.

## Jawaban Cepat
- **Apa arti “get OCR line rectangles”?** Itu mengembalikan kotak pembatas (bounding box) dari setiap baris teks yang terdeteksi dalam sebuah gambar.  
- **Metode API mana yang digunakan?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Format gambar yang didukung?** PNG, JPEG, BMP, TIFF, dan lainnya.  
- **Bisakah saya menjalankannya di .NET Core?** Ya, Aspose.OCR sepenuhnya mendukung .NET Core dan .NET 5/6.

## Prasyarat

Sebelum menyelami tutorial, pastikan Anda memiliki prasyarat berikut:

- Pengetahuan dasar tentang C# dan pengembangan .NET.  
- Lingkungan pengembangan terintegrasi (IDE) seperti Visual Studio.  
- Perpustakaan Aspose.OCR untuk .NET terpasang. Anda dapat mengunduhnya [di sini](https://releases.aspose.com/ocr/net/).  
- Sebuah gambar contoh yang berisi teks untuk pengenalan OCR.

## Impor Namespace

Pastikan Anda memiliki namespace yang diperlukan diimpor ke proyek Anda. Tambahkan baris berikut ke bagian atas file C# Anda:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Sekarang, mari kita uraikan proses mendapatkan persegi panjang untuk baris dalam pengenalan gambar OCR menjadi langkah‑langkah yang mudah diikuti.

## Analisis Tata Letak OCR – Panduan Langkah‑per‑Langkah

### Langkah 1: Siapkan Direktori Dokumen Anda

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Ganti `"Your Document Directory"` dengan jalur sebenarnya ke folder yang berisi gambar contoh Anda.

### Langkah 2: Inisialisasi Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Buat instance dari kelas `AsposeOcr` untuk mengakses fungsionalitas OCR.

### Langkah 3: Tentukan Jalur Gambar

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Tentukan jalur lengkap ke gambar yang ingin Anda lakukan OCR.

### Langkah 4: Kenali Gambar dan Dapatkan Persegi Panjang

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Metode `GetRectangles` mengembalikan daftar objek `Rectangle`, masing‑masing mewakili koordinat baris teks yang terdeteksi. Inilah inti dari **mendapatkan persegi panjang baris OCR** dan memungkinkan **analisis tata letak OCR**.

### Langkah 5: Cetak Hasil

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Cetak koordinat area yang terdeteksi ke konsol. Anda akan melihat nilai‑nilai yang dapat Anda gunakan nanti untuk **mengekstrak koordinat baris** untuk pemrosesan khusus.

## Mengapa Menggunakan Aspose.OCR untuk Persegi Panjang Baris?

- **Akurasi tinggi** – Algoritma canggih mendeteksi baris bahkan pada gambar yang berisik atau miring.  
- **Lintas‑platform** – Berfungsi pada .NET Framework, .NET Core, dan .NET 5/6.  
- **Tanpa ketergantungan eksternal** – Perpustakaan .NET murni, tanpa DLL native yang harus disertakan.  
- **Output kaya** – Selain persegi panjang baris, Anda juga dapat mengambil kata, karakter, dan skor kepercayaan.

## Masalah Umum dan Solusinya

| Masalah | Solusi |
|-------|----------|
| **Tidak ada persegi panjang yang dikembalikan** | Pastikan gambar berisi teks horizontal yang jelas dan `AreasType.LINES` telah ditentukan. |
| **Koordinat tidak tepat** | Verifikasi DPI gambar; gambar beresolusi rendah dapat menyebabkan batas yang tidak akurat. |
| **Bottleneck kinerja pada gambar besar** | Ubah ukuran gambar ke resolusi yang wajar sebelum memanggil `GetRectangles`. |
| **Pengecualian lisensi** | Gunakan lisensi percobaan untuk pengujian; terapkan lisensi penuh untuk produksi guna menghindari batas evaluasi. |

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya mengekstrak kata individual alih‑alih seluruh baris?**  
J: Ya, gunakan `AreasType.WORDS` dengan metode `GetRectangles` yang sama untuk memperoleh kotak pembatas tingkat kata.

**T: Apakah API mendukung PDF multi‑halaman?**  
J: Konversi setiap halaman PDF menjadi gambar terlebih dahulu, kemudian panggil `GetRectangles` pada setiap gambar.

**T: Bagaimana cara menangani teks yang diputar?**  
J: Aktifkan opsi auto‑rotate dalam pengaturan OCR atau pra‑putar gambar sebelum diproses.

**T: Apakah ada cara untuk mendapatkan skor kepercayaan untuk setiap baris?**  
J: Setelah memperoleh persegi panjang, panggil `api.RecognizeImage(...).Lines` untuk mengakses objek baris yang mencakup nilai kepercayaan.

**T: Versi .NET apa yang kompatibel?**  
J: Perpustakaan ini bekerja dengan .NET Framework 4.5+, .NET Core 3.1+, dan .NET 5/6.

## Kasus Penggunaan di Dunia Nyata

- **Analisis tata letak dokumen OCR** – Masukkan persegi panjang baris ke dalam mesin tata letak untuk merekonstruksi struktur kolom.  
- **Ekstraksi data otomatis** – Gunakan koordinat untuk memotong baris individual untuk pipeline NLP lanjutan.  
- **Rendering khusus** – Tempelkan kotak pembatas pada gambar asli untuk verifikasi visual atau overlay UI.  

## Kesimpulan

Selamat! Anda telah berhasil **mendapatkan persegi panjang baris OCR** untuk sebuah gambar menggunakan Aspose.OCR untuk .NET. Dengan kotak pembatas di tangan, Anda kini dapat memasukkan koordinat baris ke dalam alur kerja lanjutan seperti rendering khusus, ekstraksi data, atau **analisis tata letak OCR**.

---

**Terakhir Diperbarui:** 2026-02-22  
**Diuji Dengan:** Aspose.OCR 24.11 untuk .NET  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}