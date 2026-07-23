---
date: 2026-07-23
description: Pelajari cara mengekstrak teks dari gambar menggunakan Aspose.OCR untuk
  .NET, menyiapkan persegi panjang untuk meningkatkan akurasi OCR, dan mengonversi
  gambar menjadi teks secara efisien.
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: Siapkan Persegi Panjang dalam Pengenalan Gambar OCR
og_description: Ekstrak teks dari gambar menggunakan Aspose.OCR untuk .NET. Pelajari
  cara menyiapkan persegi panjang, meningkatkan akurasi OCR, dan mengonversi gambar
  menjadi teks secara efisien.
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: Ekstrak Teks dari Gambar dengan Persegi Panjang – Panduan OCR
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: Ekstrak Teks dari Gambar dengan Persegi Panjang – Panduan OCR
url: /id/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Persegi Panjang – Panduan OCR

## Pendahuluan

Optical Character Recognition (OCR) memungkinkan Anda **mengekstrak teks dari gambar** sehingga file menjadi dapat dicari dan dapat diedit. Dalam tutorial ini kami akan menunjukkan cara meningkatkan akurasi OCR dengan menyiapkan persegi panjang khusus yang memfokuskan mesin pada zona tepat yang Anda butuhkan. Menggunakan Aspose.OCR untuk .NET, Anda akan melihat alur kerja lengkap—dari penyiapan proyek hingga mengambil string yang dikenali—sehingga Anda dapat menyematkan konversi gambar‑ke‑teks yang handal ke dalam aplikasi .NET apa pun.

## Jawaban Cepat
- **Apa arti “extract text from image”?** Itu mengubah karakter visual dalam gambar menjadi string yang dapat dibaca mesin.  
- **Perpustakaan mana yang menangani ini di .NET?** Aspose.OCR untuk .NET menyediakan mesin OCR lengkap.  
- **Apakah saya memerlukan lisensi untuk produksi?** Versi percobaan gratis cukup untuk pengembangan; lisensi komersial diperlukan untuk penyebaran.  
- **Bisakah saya membatasi OCR ke zona tertentu?** Ya—definisikan persegi panjang untuk menargetkan hanya area yang berisi teks berguna.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Apa itu “extract text from image” dengan persegi panjang?
Proses `extract text from image` membaca karakter di dalam zona persegi panjang yang didefinisikan, mengabaikan segala hal lainnya. Dengan membatasi OCR ke zona tersebut Anda mendapatkan akurasi lebih tinggi, pemrosesan lebih cepat, dan upaya pasca‑pemrosesan yang lebih sedikit. Pendekatan ini memisahkan teks yang Anda butuhkan sambil membuang grafik latar belakang, elemen dekoratif, dan kebisingan visual lain yang dapat membingungkan mesin OCR.

## Mengapa menyiapkan persegi panjang sebelum OCR?
Menyiapkan persegi panjang memungkinkan Anda memusatkan mesin OCR pada bagian gambar yang paling relevan, yang meningkatkan kecepatan dan presisi. Dengan mempersempit area analisis, Anda mengurangi jumlah data yang harus diperiksa mesin, menghasilkan hasil lebih cepat dan lebih sedikit kesalahan pengenalan yang disebabkan oleh gangguan visual yang tidak diperlukan.

- **Fokus pada konten relevan:** Lewati header, footer, atau grafik dekoratif yang dapat membingungkan mesin.  
- **Tingkatkan kinerja:** Wilayah yang lebih kecil memerlukan lebih sedikit perhitungan, memotong waktu proses hingga 40 % pada pemindaian besar.  
- **Tingkatkan akurasi:** Mengurangi kebisingan visual meningkatkan tingkat pengenalan karakter dari ~85 % menjadi >95 % pada dokumen yang berisik.

## Mengapa ini penting untuk proyek dunia nyata
Banyak dokumen bisnis—kwitansi, faktur, kartu identitas—mencampur teks dengan logo atau kode batang. Dengan menggambar persegi panjang di sekitar bidang yang benar‑benar Anda butuhkan, Anda mengekstrak hanya data berharga, mengurangi pekerjaan pembersihan selanjutnya dan meningkatkan keandalan alur kerja otomatis. Ekstraksi terarah ini mengurangi upaya pasca‑pemrosesan dan membantu menjaga kepatuhan terhadap standar penanganan data.

## Kasus penggunaan umum
- **Otomatisasi entri data:** Mengambil bidang spesifik dari formulir yang dipindai atau kwitansi pengeluaran.  
- **Pemeriksaan kepatuhan:** Memisahkan klausa hukum atau pernyataan regulasi untuk verifikasi.  
- **Pengindeksan konten:** Mengindeks hanya judul atau keterangan gambar untuk visibilitas mesin pencari.

## Prasyarat

- Pengetahuan dasar tentang C# dan pengembangan .NET.  
- Aspose.OCR untuk .NET library installed – download it **[di sini](https://releases.aspose.com/ocr/net/)** or browse all releases **[di sini](https://releases.aspose.com/)**.  
- Sebuah gambar contoh (misalnya `sample.png`) yang berisi teks yang ingin Anda ekstrak.

## Impor Namespace

Pernyataan `using` membawa mesin OCR dan kelas geometri ke dalam ruang lingkup.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Langkah 1: Siapkan Direktori Dokumen Anda

Tentukan folder yang menyimpan gambar Anda dan buat instance mesin OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Cara mengekstrak teks dari gambar menggunakan beberapa persegi panjang
Muat gambar sekali, lalu berikan daftar persegi panjang ke mesin OCR. Setiap persegi panjang mendefinisikan wilayah minat, dan mesin mengembalikan string terpisah untuk setiap wilayah, memungkinkan Anda menangani bidang secara individual dan menggabungkan hasil sesuai kebutuhan.

### Definisikan persegi panjang

`Rectangle` objek menggambarkan koordinat X‑Y dan ukuran setiap zona yang ingin Anda pindai.  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### Lakukan pengenalan OCR

Metode `RecognizeImage` memproses gambar menggunakan daftar persegi panjang yang diberikan dan mengembalikan teks yang dikenali untuk setiap wilayah.  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Cara mengekstrak teks dari gambar menggunakan RecognitionSettings (Pendekatan Alternatif)
Jika Anda lebih suka panggilan berbasis pengaturan, Anda dapat mencapai hasil yang sama dengan `RecognitionSettings`. Objek ini memungkinkan Anda menggabungkan definisi persegi panjang bersama bahasa, DPI, dan opsi OCR lainnya, menyediakan panggilan API bersih dengan satu parameter.

### Definisikan pengaturan pengenalan

`RecognitionSettings` memungkinkan Anda menggabungkan daftar persegi panjang dan opsi tambahan (mis., bahasa, DPI) ke dalam satu objek.  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### Tampilkan teks yang dikenali

Iterasikan string yang dikembalikan dan keluarkan teks setiap wilayah.  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Masalah Umum & Tips

- **Koordinat persegi panjang tidak tepat:** Verifikasi bahwa `X`, `Y`, `Width`, dan `Height` sesuai dengan area yang dimaksud.  
- **Kualitas gambar:** Gambar beresolusi rendah atau sangat terkompresi menurunkan hasil OCR; pertimbangkan pra‑pemrosesan seperti binarisasi.  
- **Hasil kosong:** Pastikan persegi panjang benar‑benar berisi teks yang dapat dibaca; jika tidak, mesin mengembalikan string kosong.

## Pemecahan Masalah dan Praktik Terbaik

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| Tidak ada output atau string kosong | Persegi panjang di luar batas gambar | Periksa kembali dimensi gambar dan koordinat persegi panjang |
| Karakter kacau | Kontras buruk atau noise | Terapkan konversi ke skala abu‑abu dan thresholding sebelum OCR |
| Kinerja lambat pada file besar | Terlalu banyak persegi panjang atau gambar sangat besar | Bagi gambar atau kurangi jumlah persegi panjang bila memungkinkan |

## Kesimpulan

Anda kini tahu cara **mengekstrak teks dari gambar** dengan menyiapkan persegi panjang khusus menggunakan Aspose.OCR untuk .NET. Pendekatan ini memberi Anda kontrol yang tepat atas proses OCR, menghasilkan fitur ekstraksi teks yang lebih cepat dan lebih akurat untuk solusi .NET apa pun.

## Pertanyaan yang Sering Diajukan

**Q:** Apakah saya dapat menggunakan Aspose.OCR untuk .NET dengan kerangka kerja .NET lainnya?  
**A:** Ya, Aspose.OCR untuk .NET bekerja dengan .NET Framework 4.5+, .NET Core 3.1+, dan .NET 5/6/7.

**Q:** Apakah tersedia versi percobaan gratis?  
**A:** Tentu saja! Unduh percobaan **[di sini](https://releases.aspose.com/)**.

**Q:** Di mana saya dapat mendapatkan dukungan untuk Aspose.OCR untuk .NET?  
**A:** Kunjungi **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** untuk bantuan khusus.

**Q:** Apakah saya dapat memperoleh lisensi sementara untuk pengujian?  
**A:** Ya, lisensi sementara tersedia **[di sini](https://purchase.aspose.com/temporary-license/)**.

**Q:** Di mana dokumentasi resmi?  
**A:** Referensi API lengkap dapat ditemukan **[di sini](https://reference.aspose.com/ocr/net/)**.

**Terakhir Diperbarui:** 2026-07-23  
**Diuji Dengan:** Aspose.OCR 24.11 untuk .NET  
**Penulis:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutorial Terkait

- [Cara Menarik Persegi Panjang untuk Paragraf dalam Pengenalan Gambar OCR](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [Cara OCR Gambar – Lakukan OCR pada Gambar dalam Pengenalan Gambar OCR](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Cara Menarik Teks dari Gambar Menggunakan Aspose.OCR untuk .NET](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}