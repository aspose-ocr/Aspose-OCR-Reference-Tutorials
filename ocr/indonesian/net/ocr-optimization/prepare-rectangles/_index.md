---
date: 2026-02-25
description: Pelajari cara mengekstrak teks dari gambar menggunakan Aspose.OCR untuk
  .NET. Panduan ini memandu Anda melalui persiapan persegi panjang untuk pengenalan
  gambar OCR dan meningkatkan akurasi.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Cara Mengekstrak Teks dari Gambar dengan Menyiapkan Persegi Panjang di OCR
url: /id/net/ocr-optimization/prepare-rectangles/
weight: 11
---

 Asked Questions" -> "## Pertanyaan yang Sering Diajukan". Ensure markdown formatting preserved.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Siapkan Persegi Panjang dalam Pengenalan Gambar OCR

## Pendahuluan

Optical Character Recognition (OCR) penting untuk mengubah konten visual menjadi teks yang dapat dicari dan diedit. Dalam tutorial ini Anda akan **mengekstrak teks dari gambar** dengan menyiapkan persegi panjang khusus yang memfokuskan mesin OCR pada wilayah tertentu. Menggunakan Aspose.OCR untuk .NET, kami akan memandu Anda melalui setiap langkah—dari menyiapkan proyek hingga mengambil teks yang dikenali—sehingga Anda dapat mengintegrasikan fungsi gambar‑ke‑teks yang kuat ke dalam aplikasi .NET Anda.

## Jawaban Cepat
- **Apa arti “extract text from image”?** Itu berarti mengonversi karakter visual dalam sebuah gambar menjadi string yang dapat dibaca mesin.  
- **Perpustakaan mana yang membantu ini di .NET?** Aspose.OCR untuk .NET.  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Versi percobaan gratis dapat digunakan untuk pengujian; lisensi diperlukan untuk produksi.  
- **Bisakah saya menargetkan area tertentu?** Ya, dengan mendefinisikan persegi panjang yang membatasi ruang lingkup OCR.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Apa itu “extract text from image” dengan persegi panjang?
Ketika Anda mendefinisikan zona persegi panjang pada sebuah gambar, mesin OCR hanya memproses zona tersebut. Ini meningkatkan akurasi, mengurangi waktu pemrosesan, dan memungkinkan Anda mengabaikan latar belakang yang berisik atau bagian yang tidak relevan.

## Mengapa menyiapkan persegi panjang sebelum OCR?
- **Fokus pada konten yang relevan:** Lewati header, footer, atau grafik dekoratif.  
- **Tingkatkan kinerja:** Wilayah yang lebih kecil berarti pengenalan yang lebih cepat.  
- **Tingkatkan akurasi:** Lebih sedikit noise visual menghasilkan hasil yang lebih bersih.

## Mengapa ini penting untuk proyek dunia nyata
Banyak dokumen bisnis—tanda terima, faktur, kartu identitas—memiliki tata letak campuran di mana hanya bagian tertentu yang berisi teks berharga. Dengan menggunakan persegi panjang, Anda dapat mengekstrak hanya bidang yang diperlukan, secara dramatis mengurangi pekerjaan pasca‑pemrosesan dan meningkatkan keandalan keseluruhan alur otomatisasi Anda.

## Kasus penggunaan umum
- **Otomasi entri data:** Mengambil bidang tertentu dari formulir yang dipindai.  
- **Pemeriksaan kepatuhan:** Mengisolasi dan memverifikasi blok teks hukum.  
- **Pengindeksan konten:** Mengindeks hanya judul atau keterangan gambar untuk mesin pencari.  

## Prasyarat

- Familiaritas dengan pengembangan C# dan .NET.  
- Perpustakaan Aspose.OCR untuk .NET terpasang – Anda dapat mengunduhnya **[di sini](https://releases.aspose.com/ocr/net/)**.  
- Sebuah gambar contoh (misalnya `sample.png`) yang berisi teks yang ingin Anda ekstrak.

## Impor Namespace

Pertama, bawa namespace yang diperlukan ke dalam ruang lingkup:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Langkah 1: Siapkan Direktori Dokumen Anda

Tentukan lokasi file gambar Anda dan buat instance mesin OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Cara mengekstrak teks dari gambar menggunakan beberapa persegi panjang

### Langkah 2: Kenali Gambar dengan Beberapa Persegi Panjang

#### 2.1 Definisikan persegi panjang

Buat daftar objek `Rectangle` yang menandai area yang ingin Anda scan dengan mesin OCR.

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

### Langkah 3: Kenali Gambar dengan Pengaturan Pengenalan (Pendekatan Alternatif)

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

- **Koordinat persegi panjang tidak tepat:** Pastikan nilai `X`, `Y`, `Width`, dan `Height` sesuai dengan wilayah yang Anda inginkan.  
- **Kualitas gambar:** Gambar beresolusi rendah dapat menghasilkan hasil OCR yang buruk; pertimbangkan pra‑pemrosesan (mis., binarisasi).  
- **Hasil kosong:** Pastikan persegi panjang memang berisi teks; jika tidak, mesin akan mengembalikan string kosong.

## Pemecahan Masalah dan Praktik Terbaik

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| Tidak ada output atau string kosong | Persegi panjang berada di luar batas gambar | Periksa kembali dimensi gambar dan koordinat persegi panjang |
| Karakter rusak | Kontras buruk atau noise | Terapkan pembersihan gambar (grayscale, threshold) sebelum OCR |
| Kinerja lambat pada file besar | Terlalu banyak persegi panjang atau gambar sangat besar | Bagi gambar atau kurangi jumlah persegi panjang bila memungkinkan |

## Kesimpulan

Anda kini telah mempelajari cara **mengekstrak teks dari gambar** dengan menyiapkan persegi panjang khusus menggunakan Aspose.OCR untuk .NET. Teknik ini memberi Anda kontrol detail atas proses OCR, membantu Anda membangun fitur ekstraksi teks yang lebih cepat dan lebih akurat dalam aplikasi Anda.

## Pertanyaan yang Sering Diajukan

**Q:** Bisakah saya menggunakan Aspose.OCR untuk .NET dengan kerangka .NET lainnya?  
**A:** Ya, Aspose.OCR untuk .NET kompatibel dengan berbagai kerangka .NET.

**Q:** Apakah ada versi percobaan gratis untuk Aspose.OCR untuk .NET?  
**A:** Tentu! Anda dapat mengakses versi percobaan gratis **[di sini](https://releases.aspose.com/)**.

**Q:** Bagaimana cara mendapatkan dukungan untuk Aspose.OCR untuk .NET?  
**A:** Kunjungi **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** untuk dukungan khusus.

**Q:** Bisakah saya memperoleh lisensi sementara untuk tujuan pengujian?  
**A:** Ya, Anda dapat memperoleh lisensi sementara **[di sini](https://purchase.aspose.com/temporary-license/)**.

**Q:** Di mana saya dapat menemukan dokumentasi untuk Aspose.OCR untuk .NET?  
**A:** Dokumentasi tersedia **[di sini](https://reference.aspose.com/ocr/net/)**.

---

**Terakhir Diperbarui:** 2026-02-25  
**Diuji Dengan:** Aspose.OCR 24.11 untuk .NET  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}