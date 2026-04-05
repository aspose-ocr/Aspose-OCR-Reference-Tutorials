---
category: general
date: 2026-04-04
description: Pelajari cara menggunakan Aspose untuk mengekstrak data struk, memuat
  gambar struk, dan melakukan OCR pada gambar struk dengan contoh lengkap C#. Panduan
  langkah demi langkah untuk pengembang.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: id
og_description: Cara menggunakan Aspose untuk mengekstrak data struk dari gambar struk
  yang dipindai. Kode C# lengkap, penjelasan, dan tips untuk pemrosesan gambar struk
  OCR.
og_title: Cara Menggunakan Aspose – Ekstrak Data Struk dari Gambar
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Cara Menggunakan Aspose – Ekstrak Data Kwitansi dari Gambar dalam C#
url: /id/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Aspose – Mengekstrak Data Resi dari Gambar dalam C#

Pernah bertanya‑tanya **cara menggunakan Aspose** untuk mengambil informasi terstruktur dari foto sebuah resi? Anda tidak sendirian. Baik Anda membangun aplikasi pelacakan pengeluaran atau mengotomatisasi entri faktur, masalahnya sama: Anda memiliki file PNG atau JPEG, dan Anda memerlukan nama merchant, tanggal, serta total amount tanpa harus mengetik secara manual.

Begini—Aspose.OCR membuat seluruh alur kerja itu menjadi sangat mudah. Dalam tutorial ini kami akan menunjukkan cara memuat gambar resi, menjalankan OCR, dan akhirnya mengekstrak data resi dengan beberapa baris kode C#. Pada akhir tutorial Anda akan memiliki program konsol yang dapat dijalankan dan mencetak merchant, tanggal, serta total amount langsung ke konsol.

> **Quick win:** Jika Anda hanya membutuhkan kode, lompat ke bagian “Contoh Kerja Lengkap” di bagian bawah dan salin‑tempel.

## Apa yang Anda Butuhkan

- **.NET 6.0 atau lebih baru** (API ini bekerja dengan .NET Core dan .NET Framework)
- **Aspose.OCR untuk .NET** paket NuGet (`Install-Package Aspose.OCR`)
- Contoh gambar resi (PNG, JPG, atau BMP) yang disimpan secara lokal
- Visual Studio 2022 atau editor apa pun yang mendukung proyek C#

Tidak ada pustaka pihak ketiga lain yang diperlukan. Satu‑satunya prasyarat adalah pemahaman dasar tentang aplikasi konsol C#—jika Anda pernah menulis “Hello World”, Anda siap melanjutkan.

## Langkah 1 – Instal dan Referensikan Aspose.OCR

Untuk **cara menggunakan Aspose**, pertama‑tama Anda perlu menambahkan pustaka ke proyek Anda. Buka Package Manager Console dan jalankan:

```powershell
Install-Package Aspose.OCR
```

Atau, gunakan UI NuGet dan cari “Aspose.OCR”. Setelah terpasang, tambahkan namespace yang diperlukan di bagian atas file Anda:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Pro tip:** Pastikan paket NuGet Anda selalu terbarui. Sampai saat ini (April 2026) versi stabil terbaru adalah 23.11.0, yang mencakup perbaikan kinerja OCR pada resi beresolusi tinggi.

## Langkah 2 – Muat Gambar Resi

Saat Anda **memuat gambar resi**, ada dua sumber umum: jalur lokal atau stream dari permintaan web. Untuk tutorial ini kami akan menyederhanakannya dengan membaca dari disk:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

Ganti `YOUR_DIRECTORY/receipt.png` dengan jalur sebenarnya ke file resi Anda. Jika Anda menangani unggahan pengguna, Anda dapat memberi `MemoryStream` ke `ImageStream.FromStream`.

> **Mengapa ini penting:** Menentukan bahasa (English) memberi tahu mesin OCR kumpulan karakter apa yang diharapkan, sehingga mengurangi pengenalan yang keliru—terutama penting ketika Anda **ocr receipt image** yang berisi angka dan simbol.

## Langkah 3 – Jalankan OCR dan Tangkap Informasi Tata Letak

Langkah OCR tidak hanya menghasilkan teks mentah; ia juga menangkap tata letak, yang sangat penting untuk ekstraksi terstruktur di kemudian hari.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

Setelah `Recognize()` selesai, `ocrEngine` menyimpan baik teks biasa maupun data posisi setiap kata. Ini menjadi dasar untuk langkah selanjutnya di mana kami akan meminta Aspose untuk “**cara mengekstrak resi**” secara otomatis.

## Langkah 4 – Inisialisasi Layout Recognizer

Aspose menyediakan kelas `LayoutRecognizer` yang memahami cara resi biasanya diatur (merchant di atas, baris tanggal, total di bagian bawah). Anda cukup memberikan engine OCR yang telah dikonfigurasi:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

Di balik layar, recognizer menerapkan serangkaian heuristik—seperti mencari simbol mata uang atau pola tanggal—untuk memetakan teks mentah ke bidang semantik.

## Langkah 5 – Ekstrak Data Resi Terstruktur

Sekarang bagian yang menyenangkan: **ekstrak data resi**. Satu pemanggilan metode melakukan semua pekerjaan berat:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` adalah objek bertipe `ReceiptData` (didefinisikan dalam `Aspose.OCR.Structured`). Ia berisi tiga properti utama:

- `Merchant` – nama toko
- `Date` – tanggal pembelian sebagai `DateTime` (jika terdeteksi)
- `TotalAmount` – total amount sebagai `decimal`

Jika engine tidak menemukan bidang tertentu, properti tersebut akan bernilai `null` atau `0`. Anda dapat menambahkan logika fallback bila diperlukan (misalnya, meminta pengguna untuk mengonfirmasi).

## Langkah 6 – Tampilkan Informasi yang Diekstrak

Akhirnya, keluarkan hasil ke konsol. Di sinilah Anda melihat hasil kerja Anda:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

String format (`:d` dan `:C`) menghasilkan tanggal singkat dan string mata uang masing‑masing, sehingga output menjadi mudah dibaca manusia.

### Output yang Diharapkan

Dengan asumsi resi berasal dari “Coffee Corner”, tanggal 2025‑12‑01, dengan total $4.75, konsol akan menampilkan:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

Jika ada bidang yang hilang, Anda akan melihat baris kosong atau nilai default—sangat membantu untuk debugging.

## Kasus Khusus & Kesalahan Umum

### 1. Gambar Resolusi Rendah
Jika gambar resi blur atau di bawah 150 dpi, akurasi OCR menurun drastis. Membesarkan gambar dengan filter bilinear sederhana sebelum memberi ke Aspose dapat meningkatkan hasil.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. Resi Non‑English
Contoh utama menggunakan `Language.English`. Untuk resi multibahasa, atur `Language` ke enum yang sesuai (misalnya `Language.French`) atau gunakan `Language.AutoDetect` jika Anda tidak yakin.

### 3. Beberapa Resi dalam Satu Gambar
Layout recognizer Aspose mengharapkan satu resi per gambar. Jika Anda memiliki foto beberapa resi berdampingan, Anda harus memproses gambar terlebih dahulu—memotong setiap resi menjadi file terpisah sebelum menjalankan OCR.

### 4. Simbol Mata Uang Hilang
Kadang total amount muncul tanpa tanda `$`. Recognizer tetap menangkap angka, tetapi Anda mungkin perlu memproses string lebih lanjut untuk memastikan penempatan desimal yang benar.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## Pro Tips untuk Produksi

- **Cache engine OCR** jika Anda memproses banyak resi secara batch; menggunakan kembali instance yang sama mengurangi beban alokasi.
- **Log teks OCR mentah** (`ocrEngine.Text`) untuk jejak audit. Ini berguna ketika suatu bidang gagal diekstrak.
- **Bungkus seluruh alur dalam try/catch** dan tampilkan pesan error yang ramah (misalnya, “Tidak dapat membaca resi, silakan unggah gambar yang lebih jelas”).

## Contoh Kerja Lengkap

Berikut adalah aplikasi konsol mandiri yang dapat Anda kompilasi dan jalankan apa adanya. Cukup ganti jalur gambar dan Anda siap.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Menjalankan kode**

1. Buat proyek konsol .NET baru (`dotnet new console -n ReceiptExtractor`).
2. Tambahkan paket Aspose.OCR (`dotnet add package Aspose.OCR`).
3. Ganti `Program.cs` yang dihasilkan dengan potongan kode di atas.
4. Letakkan gambar resi pada jalur yang Anda tentukan.
5. Build dan jalankan (`dotnet run`).

Anda akan melihat merchant, tanggal, dan total tercetak persis seperti yang ditunjukkan sebelumnya.

## Penutup

Dalam panduan ini kami membahas **cara menggunakan Aspose** untuk **memuat gambar resi**, menjalankan **ocr receipt image**, dan akhirnya **mengekstrak data resi** dengan hanya beberapa baris kode. Inti utama adalah Aspose.OCR melakukan pekerjaan berat—setelah engine OCR dikonfigurasi, `LayoutRecognizer` mengubah teks mentah menjadi objek terstruktur yang dapat Anda percayai.

Langkah selanjutnya? Coba masukkan nilai yang diekstrak ke dalam basis data, buat ringkasan PDF resi, atau bahkan gunakan dalam model machine‑learning untuk klasifikasi pengeluaran. Anda juga dapat bereksperimen dengan tipe dokumen terstruktur lain seperti faktur atau label pengiriman—`ExtractInvoiceData` milik Aspose berfungsi dengan cara yang sangat mirip.

Punya pertanyaan tentang kasus khusus atau ingin melihat cara menangani PDF multi‑halaman? Tinggalkan komentar atau lihat dokumentasi resmi Aspose.OCR untuk skenario lanjutan. Selamat coding, dan nikmati kemudahan **cara menggunakan Aspose** untuk otomatisasi resi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}