---
date: 2025-12-22
description: Pelajari cara mengekstrak teks dari gambar menggunakan Aspose.OCR untuk
  .NET. Panduan ini memandu Anda dalam menyiapkan persegi panjang untuk pengenalan
  gambar OCR dan meningkatkan akurasi.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Cara Mengekstrak Teks dari Gambar dengan Menyiapkan Persegi Panjang di OCR
url: /id/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Siapkan Persegi Panjang dalam Pengenalan Gambar OCR

## Pendahuluan

Optical Character Recognition (OCR) sangat penting untuk mengubah konten visual menjadi teks yang dapat dicari dan diedit. Pada tutorial ini Anda akan **mengekstrak teks dari gambar** dengan menyiapkan persegi panjang khusus yang memfokuskan mesin OCR pada wilayah tertentu. Menggunakan Aspose.OCR untuk .NET, kami akan membimbing Anda melalui setiap langkah—dari menyiapkan proyek hingga mengambil teks yang dikenali—sehingga Anda dapat mengintegrasikan fungsionalitas gambar‑ke‑teks yang kuat ke dalam aplikasi .NET Anda.

## Jawaban Cepat
- **Apa arti “mengekstrak teks dari gambar”?** Itu berarti mengubah karakter visual dalam sebuah gambar menjadi string yang dapat dibaca mesin.  
- **Perpustakaan mana yang membantu ini di .NET?** Aspose.OCR untuk .NET.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Versi percobaan gratis dapat digunakan untuk pengujian; lisensi diperlukan untuk produksi.  
- **Bisakah saya menargetkan area tertentu?** Ya, dengan mendefinisikan persegi panjang yang membatasi ruang lingkup OCR.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Apa itu “mengekstrak teks dari gambar” dengan persegi panjang?
Ketika Anda mendefinisikan zona persegi panjang pada sebuah gambar, mesin OCR hanya memproses zona‑zona tersebut. Ini meningkatkan akurasi, mengurangi waktu pemrosesan, dan memungkinkan Anda mengabaikan latar belakang berisik atau bagian yang tidak relevan.

## Mengapa menyiapkan persegi panjang sebelum OCR?
- **Fokus pada konten yang relevan:** Lewati header, footer, atau grafik dekoratif.  
- **Tingkatkan kinerja:** Wilayah yang lebih kecil berarti pengenalan lebih cepat.  
- **Perbaiki akurasi:** Lebih sedikit noise visual menghasilkan hasil yang lebih bersih.

## Prasyarat

- Familiaritas dengan C# dan pengembangan .NET.  
- Perpustakaan Aspose.OCR untuk .NET terpasang – Anda dapat mengunduhnya **[di sini](https://releases.aspose.com/ocr/net/)**.  
- Sebuah gambar contoh (misalnya `sample.png`) yang berisi teks yang ingin Anda ekstrak.

## Mengimpor Namespace

Pertama, bawa namespace yang diperlukan ke dalam ruang lingkup:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Langkah 1: Menyiapkan Direktori Dokumen Anda

Tentukan lokasi file gambar Anda dan buat instance mesin OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Cara mengekstrak teks dari gambar menggunakan beberapa persegi panjang

### Langkah 2: Mengenali Gambar dengan Beberapa Persegi Panjang

#### 2.1 Definisikan persegi panjang

Buat daftar objek `Rectangle` yang menggambarkan area yang ingin dipindai oleh mesin OCR.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Lakukan pengenalan OCR

Berikan jalur gambar dan daftar persegi panjang ke `RecognizeImage`. Metode ini mengembalikan koleksi string—setiap entri sesuai dengan satu persegi panjang.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Langkah 3: Mengenali Gambar dengan Pengaturan Pengenalan (Pendekatan Alternatif)

Jika Anda lebih suka menggunakan `RecognitionSettings`, Anda dapat mencapai hasil yang sama dengan pemanggilan API yang sedikit berbeda.

#### 3.1 Definisikan pengaturan pengenalan

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Tampilkan teks yang dikenali

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Masalah Umum & Tips

- **Koordinat persegi panjang tidak tepat:** Pastikan nilai `X`, `Y`, `Width`, dan `Height` benar-benar memetakan wilayah yang diinginkan.  
- **Kualitas gambar:** Gambar beresolusi rendah dapat menghasilkan hasil OCR yang buruk; pertimbangkan pra‑pemrosesan (misalnya binarisasi).  
- **Hasil kosong:** Pastikan bahwa persegi panjang memang berisi teks; jika tidak, mesin akan mengembalikan string kosong.

## Kesimpulan

Anda kini telah mempelajari cara **mengekstrak teks dari gambar** dengan menyiapkan persegi panjang khusus menggunakan Aspose.OCR untuk .NET. Teknik ini memberi Anda kontrol detail atas proses OCR, membantu Anda membangun fitur ekstraksi teks yang lebih cepat dan lebih akurat dalam aplikasi Anda.

## Pertanyaan yang Sering Diajukan

**T:** Apakah saya dapat menggunakan Aspose.OCR untuk .NET dengan kerangka .NET lainnya?  
**J:** Ya, Aspose.OCR untuk .NET kompatibel dengan berbagai kerangka .NET.

**T:** Apakah ada versi percobaan gratis untuk Aspose.OCR untuk .NET?  
**J:** Tentu saja! Anda dapat mengakses versi percobaan **[di sini](https://releases.aspose.com/)**.

**T:** Bagaimana cara mendapatkan dukungan untuk Aspose.OCR untuk .NET?  
**J:** Kunjungi **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** untuk dukungan khusus.

**T:** Bisakah saya memperoleh lisensi sementara untuk tujuan pengujian?  
**J:** Ya, Anda dapat memperoleh lisensi sementara **[di sini](https://purchase.aspose.com/temporary-license/)**.

**T:** Di mana saya dapat menemukan dokumentasi untuk Aspose.OCR untuk .NET?  
**J:** Dokumentasi tersedia **[di sini](https://reference.aspose.com/ocr/net/)**.

---

**Terakhir Diperbarui:** 2025-12-22  
**Diuji Dengan:** Aspose.OCR 24.11 untuk .NET  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}