---
category: general
date: 2026-02-17
description: Jalankan OCR pada gambar menggunakan Aspose OCR di C#. Pelajari cara
  mengekstrak teks dari jpg, memproses gambar untuk OCR, dan memuat gambar untuk OCR
  dengan kode langkah demi langkah.
draft: false
keywords:
- run OCR on image
- extract text from jpg
- preprocess image for OCR
- load image for OCR
language: id
og_description: Jalankan OCR pada gambar menggunakan Aspose OCR di C#. Panduan ini
  menunjukkan cara mengekstrak teks dari JPG, memproses gambar terlebih dahulu, dan
  memuat gambar untuk OCR.
og_title: Jalankan OCR pada Gambar dengan Aspose OCR – Panduan Lengkap C#
tags:
- Aspose OCR
- C#
- Image Processing
title: Jalankan OCR pada Gambar dengan Aspose OCR – Panduan Lengkap C#
url: /id/net/text-recognition/run-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Gambar dengan Aspose OCR – Panduan Lengkap C#

Pernah perlu **menjalankan OCR pada file gambar** tetapi tidak yakin harus mulai dari mana? Dalam banyak aplikasi dunia nyata – misalnya pemindai faktur atau pelacak kwitansi – rintangan pertama adalah mendapatkan teks yang dapat diandalkan dari JPEG. Kabar baiknya? Dengan Aspose OCR Anda dapat **menjalankan OCR pada file gambar** hanya dengan beberapa baris kode C#, dan Anda juga akan belajar cara **mengekstrak teks dari jpg**, **memproses gambar untuk OCR**, serta **memuat gambar untuk OCR** tanpa harus mencari-cari di dokumentasi yang tersebar.

Dalam tutorial ini kami akan menelusuri contoh lengkap yang siap disalin‑tempel yang menunjukkan secara tepat cara menyiapkan mesin, menambahkan filter pra‑pemrosesan yang berguna, memberi gambar ke pengenal, dan mencetak hasilnya ke konsol. Pada akhir tutorial Anda akan memiliki program mandiri yang dapat dimasukkan ke proyek .NET apa pun dan mulai menarik teks dari gambar segera.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode ini juga berfungsi di .NET Core)  
- Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Contoh JPEG (`input.jpg`) yang ditempatkan di folder yang dapat Anda referensikan  
- Pemahaman dasar tentang sintaks C# (tidak ada yang rumit)

Jika Anda sudah memiliki semua komponen tersebut, bagus – mari kita mulai. Jika belum, dapatkan paket NuGet dan gambar uji; sisanya mengasumsikan Anda sudah melakukannya.

## Langkah 1: Buat OCR Engine – Inti dari Menjalankan OCR pada Gambar

Hal pertama yang harus Anda lakukan untuk **menjalankan OCR pada data gambar** adalah menginstansiasi `OcrEngine`. Objek ini menyimpan semua konfigurasi dan status yang diperlukan untuk pengenalan.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // Step 1 – create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Mengapa ini penting:** `OcrEngine` adalah pintu gerbang ke pipeline pengenalan Aspose. Tanpa itu Anda tidak dapat mengakses filter, paket bahasa, atau metode `Recognize`.

## Langkah 2: Tambahkan Filter Pra‑Pemrosesan – Tingkatkan Akurasi Saat Anda Mengekstrak Teks dari JPG

Gambar yang diambil langsung dari kamera jarang sempurna. Sudut miring atau butiran acak dapat mengacaukan bahkan algoritma OCR terbaik. Menambahkan beberapa filter sebelum Anda **mengekstrak teks dari jpg** dapat secara dramatis meningkatkan hasil.

```csharp
        // Step 2 – add preprocessing filters
        // Deskew corrects rotation; DenoiseGaussian reduces visual noise
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });
```

> **Tips pro:** Jika gambar sumber Anda sudah bersih, Anda dapat melewatkan `DenoiseGaussianFilter`. Terlalu banyak penyaringan dapat menghapus karakter yang samar.

## Langkah 3: Muat Gambar untuk OCR – Memberi Mesin JPEG

Sekarang tiba bagian di mana Anda **memuat gambar untuk OCR**. Aspose menyediakan helper `ImageStream.FromFile` yang membungkus jalur file menjadi aliran yang dipahami mesin.

```csharp
        // Step 3 – specify the path to the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        // Load the image and run OCR in one call
        var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));
```

> **Kasus tepi:** Jika file tidak ada, `FromFile` akan melempar `FileNotFoundException`. Bungkus pemanggilan dalam try/catch jika Anda mengharapkan file yang hilang saat runtime.

## Langkah 4: Ambil dan Tampilkan Teks yang Diakui

Akhirnya, setelah mesin selesai, Anda dapat mengakses hasil teks polos melalui properti `Text`. Mencetaknya ke konsol sudah cukup untuk demo cepat, tetapi Anda juga dapat menuliskannya ke basis data atau file teks.

```csharp
        // Step 4 – output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output yang diharapkan**

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
```

Konten tepatnya akan bergantung pada gambar yang Anda masukkan, tetapi Anda seharusnya melihat blok teks yang terformat rapi, bukan karakter acak.

![Diagram yang menunjukkan pipeline OCR – menjalankan OCR pada gambar, pra‑pemrosesan, memuat, mengenali](/images/ocr-pipeline.png "diagram pipeline menjalankan OCR pada gambar")

### Mengapa Setiap Langkah Penting

| Langkah | Tujuan | Apa yang Terjadi Jika Dilewati |
|---------|--------|--------------------------------|
| **Buat mesin** | Menginisialisasi struktur internal | Tidak ada pengenal yang tersedia – Anda akan mendapatkan `NullReferenceException`. |
| **Tambahkan filter** | Meningkatkan akurasi dengan memperbaiki rotasi dan noise | Gambar miring atau berisik menghasilkan output yang berantakan. |
| **Muat gambar** | Menyediakan bitmap mentah ke mesin | Mesin tidak memiliki apa‑apa untuk diproses, menghasilkan bidang `Text` yang kosong. |
| **Baca hasil** | Mengekstrak string teks polos untuk penggunaan lebih lanjut | Anda telah menjalankan OCR tetapi tidak pernah melihat hasilnya – tidak terlalu berguna! |

## Variasi Umum & Cara Menyesuaikan Proses

### Mengubah Paket Bahasa

Aspose OCR mendukung banyak bahasa secara bawaan. Jika Anda perlu **menjalankan OCR pada file gambar** yang berisi, misalnya, teks Prancis atau Jerman, atur properti `Language` sebelum memanggil `Recognize`.

```csharp
ocrEngine.Language = OcrLanguage.French;
```

### Menangani PDF Multi‑Halaman

Jika sumber Anda adalah PDF multi‑halaman bukan JPEG tunggal, Anda dapat mengonversi setiap halaman menjadi gambar terlebih dahulu (menggunakan Aspose.PDF) dan kemudian memberi setiap gambar ke pipeline yang sama. Loop melalui halaman sangat mudah:

```csharp
foreach (var pageImage in pdfPagesAsImages)
{
    var result = ocrEngine.Recognize(ImageStream.FromMemory(pageImage));
    Console.WriteLine(result.Text);
}
```

### Mengatasi File Besar

Saat memproses gambar beresolusi tinggi, konsumsi memori dapat melonjak. Pertimbangkan menurunkan resolusi gambar sebelum Anda **memuat gambar untuk OCR**:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

var loadOptions = new JpegLoadOptions { Width = 1024, Height = 768 };
using (var img = (Image)Image.Load(imagePath, loadOptions))
{
    var stream = new MemoryStream();
    img.Save(stream, new JpegOptions());
    var ocrResult = ocrEngine.Recognize(ImageStream.FromMemory(stream.ToArray()));
}
```

## Contoh Lengkap yang Siap Dijalankan

Berikut adalah program lengkap yang menggabungkan semua yang telah dibahas. Salin‑tempel ke proyek konsol baru, ganti `YOUR_DIRECTORY` dengan folder yang berisi `input.jpg`, dan tekan **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add useful preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });

        // 3️⃣ Load the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        try
        {
            // Recognize text – this is where we actually run OCR on image
            var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));

            // 4️⃣ Print the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

### Verifikasi Hasil

1. Jalankan program.  
2. Periksa konsol – Anda harus melihat teks yang ada pada `input.jpg`.  
3. Jika output terlihat kacau, coba sesuaikan nilai `Sigma` pada `DenoiseGaussianFilter` atau tambahkan filter tambahan seperti `ContrastEnhancementFilter`.

## Ringkasan & Langkah Selanjutnya

Kami baru saja membahas cara **menjalankan OCR pada file gambar** menggunakan Aspose OCR, mulai dari menyiapkan mesin hingga menghasilkan teks bersih yang dapat dibaca. Poin pentingnya:

- Buat instance `OcrEngine`.  
- **Pra‑proses gambar untuk OCR** dengan filter seperti `DeskewFilter` dan `DenoiseGaussianFilter`.  
- **Muat gambar untuk OCR** menggunakan `ImageStream.FromFile`.  
- Panggil `Recognize` dan baca `ocrResult.Text` untuk **mengekstrak teks dari jpg**.

Ingin melangkah lebih jauh? Coba ide‑ide berikut:

- **Pemrosesan batch** – baca folder berisi JPEG dan keluarkan setiap hasil ke file `.txt` terpisah.  
- **Integrasi dengan Azure Blob Storage** – ambil gambar dari cloud, jalankan OCR, lalu simpan teks kembali.  
- **Kombinasikan dengan NLP** – beri teks yang diekstrak ke model pemahaman bahasa untuk mengkategorikan faktur secara otomatis.  

Silakan bereksperimen dengan kombinasi filter yang berbeda, paket bahasa, atau bahkan beralih ke PNG dan TIFF – pipeline yang sama bekerja selama Anda **memuat gambar untuk OCR** dengan benar.

---

Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa dokumentasi Aspose OCR untuk pengaturan lanjutan. Selamat coding, dan nikmati mengubah gambar menjadi teks yang dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}