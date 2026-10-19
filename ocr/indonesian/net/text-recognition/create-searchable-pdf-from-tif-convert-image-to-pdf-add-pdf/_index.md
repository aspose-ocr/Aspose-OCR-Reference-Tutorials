---
category: general
date: 2026-04-04
description: Buat PDF yang dapat dicari dari gambar TIF di C# – pelajari cara mengonversi
  gambar ke PDF, menambahkan metadata PDF, dan menghasilkan dokumen yang dapat dicari
  menggunakan Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: id
og_description: Buat PDF yang dapat dicari dari file TIF dengan C#. Konversi gambar
  ke PDF, tambahkan metadata PDF, dan hasilkan dokumen yang dapat dicari menggunakan
  Aspose.OCR.
og_title: Buat PDF yang Dapat Dicari dari TIF – Panduan Langkah demi Langkah
tags:
- Aspose.OCR
- C#
- PDF generation
title: Buat PDF yang Dapat Dicari dari TIF – Konversi Gambar ke PDF, Tambahkan Metadata
  PDF
url: /id/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari TIF – Panduan Lengkap C#

Pernahkah Anda perlu **membuat PDF yang dapat dicari** dari faktur yang dipindai tetapi tidak yakin bagaimana menjaga teks tetap dapat dicari dan metadata file tetap rapi? Anda tidak sendirian. Dalam banyak proyek otomatisasi PDF harus dapat dibaca mesin dan ditandai dengan benar dengan informasi seperti judul, penulis, dan ambang kepercayaan.  

Dalam panduan ini kami akan menelusuri solusi lengkap yang **mengonversi gambar ke PDF**, menyisipkan **metadata PDF**, dan menyaring hasil OCR dengan kepercayaan rendah—semua dengan library Aspose.OCR. Pada akhir tutorial Anda akan memiliki potongan kode siap pakai yang dapat ditempatkan di proyek .NET mana pun, serta beberapa tips untuk menangani kasus tepi.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga berfungsi pada .NET Framework 4.6+)  
- Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Gambar TIF yang ingin Anda ubah menjadi PDF yang dapat dicari (misalnya `input.tif`)  
- Familiaritas dasar dengan C# dan Visual Studio (atau IDE favorit Anda)

Tidak ada layanan eksternal lain yang diperlukan—seluruh proses berjalan secara lokal.

## Langkah 1 – Siapkan Mesin OCR (Buat Inti PDF yang Dapat Dicari)

Hal pertama yang kita butuhkan adalah instance `OcrEngine` yang mengetahui bahasa apa yang harus dikenali. Pada kebanyakan skenario bisnis Bahasa Inggris sudah cukup, tetapi Anda dapat mengganti `Language.English` dengan bahasa lain yang didukung.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Mengapa ini penting:** Mesin OCR melakukan pekerjaan berat mengubah piksel raster menjadi teks Unicode. Menetapkan bahasa dengan benar meningkatkan akurasi dan mengurangi jumlah kata dengan kepercayaan rendah yang kemudian akan disaring.

> **Pro tip:** Jika Anda memproses dokumen multibahasa, buat beberapa instance mesin atau gunakan `Language.Multilingual` agar Aspose menangani deteksi bahasa secara otomatis.

## Langkah 2 – Muat Gambar TIF (Buat PDF dari TIF)

Sekarang kita mengarahkan mesin ke file sumber. Helper `ImageStream.FromFile` membaca gambar ke dalam stream yang dapat dikonsumsi oleh mesin OCR.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Anda mungkin bertanya, *“Apakah saya bisa memberi JPEG atau PNG sebagai gantinya?”* Tentu—Aspose.OCR mendukung sebagian besar format raster. Cukup ubah ekstensi file dan Anda siap melanjutkan.

## Langkah 3 – Konfigurasikan Opsi PDF (Tambahkan Metadata ke PDF)

Sebelum mengonversi, kita mendefinisikan objek `PdfOptions`. Di sinilah kita **menambahkan metadata PDF** seperti judul dan penulis, serta memberi tahu mesin untuk mengabaikan kata‑kata yang kepercayaannya di bawah ambang tertentu.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**Apa yang terjadi di sini?**  
- `Title` dan `Author` menjadi bagian dari kamus informasi dokumen PDF, sehingga file lebih mudah diindeks dalam sistem manajemen dokumen.  
- `MinConfidence` berfungsi sebagai pengaman: OCR sering salah membaca karakter yang pudar; menyaringnya membuat lapisan yang dapat dicari tetap bersih dan meningkatkan ekstraksi teks selanjutnya.

Jika Anda memerlukan metadata khusus (misalnya `Subject`, `Keywords`), Anda dapat mengaturnya melalui `PdfOptions.CustomProperties`.

## Langkah 4 – Konversi Gambar ke PDF yang Dapat Dicari (Konversi Gambar ke PDF)

Dengan mesin yang sudah siap dan opsi yang ditetapkan, pemanggilan akhir melakukan konversi. Ia menulis PDF yang dapat dicari ke disk, menyematkan lapisan teks OCR di bawah gambar asli.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Setelah baris ini dijalankan, `output.pdf` berisi:
- Gambar TIF asli sebagai latar visual  
- Lapisan teks tak terlihat yang dapat dibaca mesin pencari dan operasi salin‑tempel  
- Metadata yang kita definisikan sebelumnya (judul, penulis, dll.)

### Hasil yang Diharapkan

Buka PDF yang dihasilkan di Adobe Reader atau penampil PDF apa pun dan coba pilih teks. Anda seharusnya dapat menyalin kalimat yang sesuai dengan pemindaian asli. Dialog **Properties** dokumen akan menampilkan judul “Invoice #12345” dan penulis “MyCompany”.

## Langkah 5 – Verifikasi Penyaringan Kepercayaan (Mengapa MinConfidence Membantu)

Ada baiknya memastikan bahwa kata‑kata dengan kepercayaan rendah memang telah dihapus. Anda dapat memeriksa teks tersembunyi PDF menggunakan alat seperti `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Jika kata tersebut tidak pernah muncul, filter `MinConfidence` berfungsi sebagaimana mestinya. Sesuaikan ambang (misalnya `0.7f`) jika Anda memerlukan penyaringan yang lebih agresif atau lebih lunak.

## Langkah 6 – Menangani Banyak Halaman (Buat PDF yang Dapat Dicari dari TIF Multi‑Halaman)

Banyak faktur datang dalam bentuk TIFF multi‑halaman. Aspose.OCR memperlakukan setiap frame sebagai halaman terpisah secara otomatis. Cukup arahkan mesin ke file multi‑halaman; pemanggilan `ConvertToSearchablePdf` yang sama akan menghasilkan PDF yang dapat dicari dengan banyak halaman.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Kasus tepi:** Jika sebuah halaman kosong, OCR mungkin masih menghasilkan lapisan teks kosong, yang tidak berbahaya. Namun, Anda dapat melewatkan halaman kosong dengan memeriksa `ocrEngine.HasText` sebelum konversi.

## Langkah 7 – Mengemas Contoh Lengkap (Semua Langkah Bersama)

Berikut adalah program tunggal yang siap dijalankan dan menggabungkan semua langkah. Ganti `YOUR_DIRECTORY` dengan jalur folder sebenarnya di mesin Anda.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Jalankan program (`dotnet run` atau tekan **F5** di Visual Studio) dan Anda akan melihat pesan konfirmasi. PDF yang dihasilkan berada di samping gambar sumber Anda, siap untuk diindeks atau diarsipkan.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

| Pertanyaan | Jawaban |
|------------|---------|
| **Bisakah saya menambahkan font khusus ke lapisan yang dapat dicari?** | Lapisan OCR menggunakan Unicode; tampilan visual ditentukan oleh gambar di bawahnya, jadi tidak diperlukan penyematan font tambahan. |
| **Bagaimana jika TIF saya berwarna?** | Aspose.OCR secara otomatis mengonversi gambar berwarna ke grayscale untuk OCR, tetapi Anda dapat mempertahankan warna asli di PDF dengan mengatur `PdfOptions.PreserveColor = true`. |
| **Apakah library ini thread‑safe?** | Setiap instance `OcrEngine` harus digunakan oleh satu thread saja. Untuk pemrosesan paralel, buat engine terpisah per thread. |
| **Bagaimana cara mengenkripsi PDF?** | Gunakan `PdfOptions.Security` untuk menetapkan kata sandi dan izin setelah konversi OCR. |

## Langkah Selanjutnya (Perluas Toolkit PDF Anda)

- **Pemrosesan batch:** Loop melalui folder berisi TIFF dan hasilkan PDF yang dapat dicari untuk masing‑masing.  
- **Pasca‑pemrosesan:** Gunakan Aspose.PDF untuk menggabungkan PDF yang dihasilkan menjadi satu dokumen master.  
- **Metadata lanjutan:** Isi bidang XMP khusus untuk integrasi yang lebih baik dengan SharePoint atau sistem ECM.  

Semua ekstensi ini dibangun di atas pola inti yang baru saja kita bahas: **buat PDF yang dapat dicari**, **konversi gambar ke PDF**, dan **tambahkan metadata PDF**.

---

*Selamat coding! Jika Anda menemui kendala, tinggalkan komentar di bawah atau periksa dokumentasi Aspose.OCR untuk pembaruan API terbaru.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}