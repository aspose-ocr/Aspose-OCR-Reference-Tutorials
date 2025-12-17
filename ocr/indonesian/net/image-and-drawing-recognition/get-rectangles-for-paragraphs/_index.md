---
date: 2025-12-17
description: Pelajari cara mengekstrak persegi panjang untuk paragraf dalam gambar
  OCR menggunakan Aspose.OCR untuk .NET – panduan utama tentang cara mengekstrak persegi
  panjang dan mengekstrak koordinat paragraf.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Cara Mengekstrak Persegi Panjang untuk Paragraf dalam Pengenalan Gambar OCR
url: /id/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekstrak Persegi Panjang untuk Paragraf dalam Pengenalan Gambar OCR

## Introduction

Selamat datang di panduan komprehensif kami tentang **cara mengekstrak persegi panjang** untuk paragraf dalam pengenalan gambar OCR dengan Aspose.OCR untuk .NET. Jika Anda ingin meningkatkan pipeline pemrosesan dokumen, menarik batas paragraf, dan mengotomatisasi ekstraksi data, Anda berada di tempat yang tepat. Kami akan memandu Anda melalui setiap langkah—dari menyiapkan lingkungan hingga mencetak koordinat persegi panjang—sehingga Anda dapat mulai menggunakan hasil OCR segera.

## Quick Answers
- **Apa arti “mengekstrak persegi panjang”?** Mengembalikan kotak pembatas (x, y, lebar, tinggi) dari area teks yang terdeteksi.  
- **Metode API mana yang menyediakan persegi panjang?** `AsposeOcr.GetRectangles` dengan `AreasType.PARAGRAPHS`.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Versi percobaan gratis dapat digunakan untuk pengujian; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya memproses beberapa gambar sekaligus?** Ya—lakukan loop pada daftar gambar Anda dan panggil `GetRectangles` untuk setiap file.  
- **Format apa saja yang didukung?** PNG, JPEG, TIFF, BMP, dan banyak lagi.

## What is “how to extract rectangles” in OCR?
Dalam terminologi OCR, mengekstrak persegi panjang berarti mengidentifikasi batas geometris yang melingkupi setiap paragraf atau baris teks dalam sebuah gambar. Koordinat ini memungkinkan Anda menyorot, memotong, atau menganalisis lebih lanjut bagian tertentu dari dokumen yang dipindai.

## Why extract paragraph coordinates?
- **Pemrosesan lanjutan yang presisi** – Anda dapat memasukkan setiap persegi panjang ke dalam alur kerja berikutnya (mis., terjemahan, penyensoran).  
- **UI/UX yang lebih baik** – menampilkan kotak pembatas di atas gambar asli untuk menunjukkan kepada pengguna di mana teks ditemukan.  
- **Otomatisasi batch** – dengan cepat menemukan dan mengisolasi paragraf di seluruh kumpulan dokumen besar.

## Prerequisites

- Pengetahuan dasar tentang C# dan pengembangan .NET.  
- Lingkungan pengembangan dengan Aspose.OCR untuk .NET terpasang – Anda dapat mengunduhnya [di sini](https://releases.aspose.com/ocr/net/).  
- Familiaritas dengan konsep pemrosesan gambar dan mengapa OCR penting untuk mengekstrak teks dari file yang dipindai.

## Import Namespaces

Dalam file C# Anda, impor namespace yang diperlukan agar kelas OCR tersedia:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Step 1: Set Up Your Document Directory

Definisikan folder yang berisi gambar yang ingin Anda analisis:

```csharp
string dataDir = "Your Document Directory";
```

## Step 2: Initialize AsposeOcr Instance

Buat objek `AsposeOcr` – ini memberi Anda akses ke semua fungsi OCR:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Step 3: Specify the Image Path

Tunjuk file gambar yang tepat yang ingin Anda proses:

```csharp
string fullPath = dataDir + "sample.png";
```

## Step 4: Recognize Image and Get Paragraph Rectangles

Panggil metode `GetRectangles`. Menetapkan `detect_areas` ke `true` memberi tahu mesin untuk mengembalikan persegi panjang **paragraf**:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Step 5: Print Results

Keluarkan koordinat sehingga Anda dapat melihat **koordinat paragraf yang diekstrak** yang terdeteksi:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Common Issues and Solutions

| Masalah | Alasan | Solusi |
|-------|--------|-----|
| Tidak ada persegi panjang yang dikembalikan | Kualitas gambar terlalu rendah atau `AreasType` salah | Pastikan gambar jelas dan gunakan `AreasType.PARAGRAPHS`. |
| Koordinat off‑by‑one | Ketidaksesuaian skala DPI | Atur DPI yang tepat saat memuat gambar atau gunakan `api.Config.Dpi`. |
| Pengecualian lisensi | Menjalankan tanpa lisensi yang valid di produksi | Terapkan lisensi sementara atau permanen melalui `api.SetLicense`. |

## Frequently Asked Questions

**T: Apakah Aspose.OCR kompatibel dengan berbagai format gambar?**  
J: Ya, Aspose.OCR mendukung PNG, JPEG, TIFF, BMP, dan banyak format umum lainnya.

**T: Bisakah saya menggunakan Aspose.OCR untuk pemrosesan batch banyak gambar?**  
J: Tentu saja! Lakukan loop pada koleksi jalur file dan panggil `GetRectangles` untuk setiap gambar.

**T: Apakah ada percobaan gratis untuk Aspose.OCR untuk .NET?**  
J: Ya, Anda dapat menjelajahi percobaan gratis [di sini](https://releases.aspose.com/).

**T: Bagaimana cara mendapatkan lisensi sementara untuk Aspose.OCR?**  
J: Anda dapat memperoleh lisensi sementara [di sini](https://purchase.aspose.com/temporary-license/).

**T: Di mana saya dapat menemukan dukungan tambahan dan diskusi terkait Aspose.OCR?**  
J: Kunjungi [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan komunitas dan diskusi.

## Conclusion

Dalam tutorial ini kami telah menunjukkan **cara mengekstrak persegi panjang** untuk paragraf menggunakan Aspose.OCR untuk .NET, melangkah melalui setiap potongan kode, dan menjelaskan cara menafsirkan koordinat yang dikembalikan. Dengan mengintegrasikan langkah-langkah ini ke dalam aplikasi Anda, Anda dapat secara andal menarik batas paragraf, meningkatkan alur kerja dokumen, dan membangun solusi yang lebih cerdas berbasis OCR.

---

**Terakhir Diperbarui:** 2025-12-17  
**Diuji Dengan:** Aspose.OCR 24.11 for .NET  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}