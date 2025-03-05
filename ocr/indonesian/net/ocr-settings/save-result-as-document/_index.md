---
title: Simpan Hasil sebagai Dokumen dalam Pengenalan Gambar OCR
linktitle: Simpan Hasil sebagai Dokumen dalam Pengenalan Gambar OCR
second_title: Aspose.OCR .NET API
description: Buka potensi Aspose.OCR untuk .NET. Kenali teks dalam gambar dengan mudah dan simpan hasilnya dalam berbagai format dokumen.
type: docs
weight: 10
url: /id/net/ocr-settings/save-result-as-document/
---
## Perkenalan

Selamat datang di dunia pengenalan karakter optik (OCR) yang menarik dengan Aspose.OCR untuk .NET! Dalam tutorial komprehensif ini, kita akan mempelajari seluk-beluk penggunaan Aspose.OCR untuk mengenali teks dalam gambar dan mendemonstrasikan cara menyimpan hasilnya dalam berbagai format dokumen.

## Prasyarat

Sebelum kita memulai perjalanan OCR ini, pastikan Anda memiliki prasyarat berikut:

-  Aspose.OCR untuk .NET. Pastikan Anda telah menginstal perpustakaan Aspose.OCR. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/ocr/net/).

-  Direktori Dokumen: Miliki direktori khusus untuk dokumen Anda, dan perbarui`dataDir` variabel dalam kode yang disediakan sesuai.

## Impor Namespace

Mulailah dengan mengimpor namespace yang diperlukan. Ini adalah elemen penyusun yang akan memberdayakan kode Anda dengan kemampuan OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Sekarang, mari kita bagi contoh ini menjadi beberapa langkah:

## Langkah 1: Inisialisasi Aspose.OCR

```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";

// Inisialisasi instance AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Langkah ini menetapkan tahapan dengan menginisialisasi API Aspose.OCR.

## Langkah 2: Kenali Gambar

```csharp
// Kenali gambar
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

Di sini, kami menggunakan Aspose.OCR untuk mengenali teks dalam gambar yang ditentukan (ganti "sample.png" dengan file gambar Anda).

## Langkah 3: Simpan Hasil dalam Format Berbeda

```csharp
// Simpan hasilnya dalam format pilihan Anda
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Sesuaikan langkah ini berdasarkan kebutuhan Anda. Aspose.OCR memungkinkan Anda menyimpan teks yang dikenali dalam berbagai format dokumen seperti DOCX, TXT, PDF, dan XLSX.

## Langkah 4: Tampilkan Pesan Sukses

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

Pesan konfirmasi sederhana untuk memberi tahu Anda bahwa proses telah selesai tanpa hambatan.

Dengan mengikuti langkah-langkah ini, Anda telah berhasil memanfaatkan kekuatan Aspose.OCR untuk .NET dalam mengenali teks dalam gambar dan menyimpan hasilnya dalam format dokumen berbeda.

## Kesimpulan

Kesimpulannya, Aspose.OCR untuk .NET membuka banyak kemungkinan untuk pengenalan teks dalam gambar. Baik Anda mengekstrak data atau membuat dokumen yang dapat dicari, Aspose.OCR menyederhanakan proses dengan API intuitifnya.

## FAQ

### Q1. Apakah Aspose.OCR kompatibel dengan format gambar yang berbeda?

A1: Ya, Aspose.OCR mendukung berbagai format gambar, memastikan fleksibilitas dalam tugas OCR Anda.

### Q2: Dapatkah saya menyesuaikan pengaturan pengenalan untuk akurasi yang lebih baik?

A2: Tentu saja! Aspose.OCR menyediakan pengaturan pengenalan untuk menyempurnakan proses OCR sesuai dengan kebutuhan spesifik Anda.

### Q3: Apakah tersedia uji coba gratis?

 A3: Ya, Anda dapat memulai uji coba gratis[Di Sini](https://releases.aspose.com/).

### Q4: Bagaimana saya bisa mendapatkan lisensi sementara untuk Aspose.OCR?

 A4: Lisensi sementara dapat diperoleh[Di Sini](https://purchase.aspose.com/temporary-license/).

### Q5: Di mana saya bisa mencari bantuan atau terhubung dengan komunitas?

 A5: Bergabunglah dengan komunitas Aspose.OCR di[Asumsikan Forum](https://forum.aspose.com/c/ocr/16) untuk dukungan dan diskusi.