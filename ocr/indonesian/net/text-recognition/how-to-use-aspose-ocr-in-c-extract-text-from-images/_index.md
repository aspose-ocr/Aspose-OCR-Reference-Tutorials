---
category: general
date: 2026-06-19
description: Cara menggunakan Aspose OCR di C# untuk mengekstrak teks dari gambar,
  menjalankan OCR pada gambar, dan mengenali teks dari pemindaian – panduan langkah
  demi langkah.
draft: false
keywords:
- how to use aspose
- extract text from images
- run ocr on images
- recognize text from scans
language: id
og_description: Cara menggunakan Aspose OCR di C# untuk mengekstrak teks dari gambar,
  menjalankan OCR pada gambar, dan mengenali teks dari pemindaian – panduan lengkap.
og_title: Cara Menggunakan Aspose OCR di C# – Ekstrak Teks dari Gambar
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to use Aspose OCR in C# to extract text from images, run OCR on
    images, and recognize text from scans – step‑by‑step guide.
  headline: How to Use Aspose OCR in C# – Extract Text from Images
  type: TechArticle
tags:
- Aspose
- OCR
- C#
- Image Processing
title: Cara Menggunakan Aspose OCR di C# – Ekstrak Teks dari Gambar
url: /id/net/text-recognition/how-to-use-aspose-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Aspose OCR di C# – Mengekstrak Teks dari Gambar

Pernah bertanya‑tanya **cara menggunakan Aspose** untuk mengambil kata‑kata dari foto sebuah dokumen? Anda bukan orang pertama yang menggaruk kepala tentang hal itu. Pada tutorial ini kami akan membimbing Anda melalui contoh praktis end‑to‑end yang menunjukkan secara tepat cara mengekstrak teks dari gambar, menjalankan OCR pada gambar secara batch, dan bahkan mengenali teks dari pemindaian hanya dengan beberapa baris C#.

Kami akan mulai dengan menyiapkan mesin Aspose OCR, kemudian memberi daftar file JPEG, dan akhirnya mencetak setiap hasil ke konsol. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dipakai ulang di proyek .NET mana pun—tanpa langkah misterius, tanpa referensi yang hilang.

## Apa yang Anda Perlukan

Sebelum kita mulai, pastikan Anda memiliki:

* .NET 6.0 SDK atau yang lebih baru (kode ini bekerja di .NET Core dan .NET Framework)  
* Paket **Aspose.OCR** NuGet yang valid (Anda dapat memperoleh kunci percobaan gratis dari situs Aspose)  
* Folder yang berisi beberapa gambar hasil pemindaian atau foto teks (JPEG atau PNG dapat digunakan)  
* IDE favorit Anda—Visual Studio, Rider, atau bahkan VS Code sudah cukup.

Itu saja. Tanpa perpustakaan OCR berat, tanpa alat baris perintah eksternal. Hanya Aspose dan beberapa baris kode.

## Langkah 1: Instal Paket NuGet Aspose.OCR

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Perintah ini mengunduh versi terbaru (per Juni 2026 versi 22.9) dan menambahkan referensi ke file `.csproj` Anda. Jika Anda lebih suka UI Visual Studio, klik kanan **Dependencies → Manage NuGet Packages** dan cari “Aspose.OCR”.

> **Pro tip:** Perhatikan tanggal kedaluwarsa lisensi; percobaan gratis berlaku selama 30 hari dan setelah itu Anda memerlukan kunci komersial.

## Langkah 2: Konfigurasikan Mesin OCR – “Cara Menggunakan Aspose” Dimulai Di Sini

Setelah paket terpasang, mari buat mesin OCR dan beri tahu bahasa yang akan dicari. Pada kebanyakan kasus bahasa Inggris sudah cukup, tetapi Aspose mendukung lebih dari 70 bahasa.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System.Collections.Generic;

// Configure the OCR engine to use English language
var ocrConfig = new OcrEngineConfig { Language = Language.English };
using var ocrEngine = new OcrEngine(ocrConfig);
```

Mengapa kita membungkus `OcrEngine` dalam pernyataan `using`? Karena ia mengimplementasikan `IDisposable`. Membebaskan (dispose) akan melepaskan sumber daya native (seperti memori tak terkelola) yang dialokasikan mesin OCR secara internal—sesuatu yang sangat Anda inginkan pada layanan produksi yang memproses puluhan file per menit.

## Langkah 3: Buat Daftar Jalur Gambar – Menyiapkan **Run OCR on Images**

Bagian selanjutnya adalah `List<string>` sederhana yang menunjuk ke setiap gambar yang ingin diproses. Anda dapat membuat daftar ini secara manual (seperti yang kami lakukan di bawah) atau menghasilkan secara dinamis dengan `Directory.GetFiles`.

```csharp
// Prepare a list of image file paths to be processed
var imagePaths = new List<string>
{
    @"C:\Scans\page1.jpg",
    @"C:\Scans\page2.jpg",
    @"C:\Scans\page3.jpg"
};
```

Jika gambar Anda berada di subfolder relatif terhadap executable, cukup letakkan `Path.Combine` di sana. Kuncinya adalah urutan daftar dipertahankan—Aspose akan mengembalikan hasil dalam urutan yang sama, sehingga mencocokkan output dengan input menjadi sangat mudah.

## Langkah 4: **Run OCR on Images** dalam Satu Batch

Aspose OCR bersinar ketika Anda perlu memproses banyak file sekaligus. Metode `ProcessBatch` menerima daftar yang baru saja kita buat dan mengembalikan `IList<OcrResult>` di mana setiap elemen berisi teks yang dikenali, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya nanti.

```csharp
// Run OCR on the entire batch and obtain results in the same order
IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);
```

Di balik layar, Aspose memunculkan thread native untuk mempercepat pekerjaan, sehingga Anda mendapatkan skala hampir linear dengan inti CPU. Untuk beban kerja besar Anda mungkin ingin menyesuaikan properti `OcrEngineConfig.ThreadCount`, tetapi deteksi otomatis default sudah cukup baik untuk kebanyakan skenario desktop.

## Langkah 5: Tampilkan **Recognized Text from Scans** – Verifikasi Output

Akhirnya, mari iterasi hasil dan cetak setiap blok teks. Kami juga akan menampilkan nama file asli sehingga Anda dapat melihat output mana yang berasal dari pemindaian mana.

```csharp
// Iterate through the results and display the recognized text for each image
for (int i = 0; i < ocrResults.Count; i++)
{
    System.Console.WriteLine($"--- Result for {imagePaths[i]} ---");
    System.Console.WriteLine(ocrResults[i].Text);
}
```

Saat Anda menjalankan program, konsol akan menampilkan sesuatu seperti:

```
--- Result for C:\Scans\page1.jpg ---
Invoice #12345
Date: 06/15/2026
Total: $1,250.00

--- Result for C:\Scans\page2.jpg ---
Terms and Conditions
...
```

Itulah titik manis—**cara menggunakan Aspose** untuk mengubah tumpukan PDF atau JPEG yang dipindai menjadi teks yang dapat dicari dan diedit.

![How to Use Aspose OCR example output](image-placeholder.png "How to Use Aspose OCR example output")

*Teks alt gambar: “Contoh output Aspose OCR yang menunjukkan teks yang dikenali dari pemindaian.”*

## Opsional: Menyetel Akurasi – Ketika **Extract Text from Images** Membutuhkan Dorongan

Jika Anda menemukan karakter yang hilang atau kata yang berantakan, coba penyesuaian berikut:

| Setting | Apa fungsinya | Kapan digunakan |
|---------|--------------|----------------|
| `ocrConfig.DetectOrientation = true` | Memutar otomatis gambar yang miring | Buku yang dipindai sering dalam mode potret |
| `ocrConfig.Preprocess = true` | Menerapkan peningkatan kontras dan pengurangan noise | Foto kualitas rendah yang diambil dengan ponsel |
| `ocrConfig.CharacterWhitelist = "0123456789"` | Membatasi pengenalan hanya pada angka | Mengekstrak total faktur atau nomor seri |
| `ocrEngine.SetPageSegmentationMode(PageSegMode.SingleBlock)` | Menganggap seluruh halaman sebagai satu blok teks | Ketika tata letak sederhana dan Anda menginginkan kecepatan |

Cobalah flag‑flag ini sampai skor kepercayaan (tersedia via `ocrResults[i].Confidence`) naik di atas 0.9. Ingat, semakin baik gambar sumber, semakin baik hasil OCR—jadi sedikit pra‑pemrosesan di Photoshop atau ImageMagick dapat menghemat berjam‑jam debugging.

## Contoh Lengkap yang Siap Dipakai – Copy‑Paste

Berikut adalah program lengkap yang dapat Anda kompilasi dan jalankan apa adanya. Ganti saja jalur file dengan folder Anda sendiri.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine (how to use Aspose OCR)
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,
            DetectOrientation = true,          // optional: auto‑rotate
            Preprocess = true                  // optional: improve low‑quality scans
        };
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 2️⃣ List of image files (run OCR on images)
        var imagePaths = new List<string>
        {
            @"C:\Scans\page1.jpg",
            @"C:\Scans\page2.jpg",
            @"C:\Scans\page3.jpg"
        };

        // 3️⃣ Process the batch (extract text from images)
        IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);

        // 4️⃣ Show the results (recognize text from scans)
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Result for {imagePaths[i]} ---");
            Console.WriteLine(ocrResults[i].Text);
            Console.WriteLine($"Confidence: {ocrResults[i].Confidence:P2}");
            Console.WriteLine(); // blank line for readability
        }
    }
}
```

Kompilasi dengan `dotnet run` dan saksikan konsol terisi dengan teks bersih yang dapat dicari. Itulah seluruh alur kerja **cara menggunakan aspose** dalam kurang dari 50 baris kode.

## Kesalahan Umum & Cara Mengatasinya

* **NullReferenceException pada `ocrResults[i]`** – Ini biasanya berarti mesin tidak dapat membuka file (jalur salah, format tidak didukung). Periksa kembali ekstensi file dan izin akses.
* **Karakter sampah** – Jika Anda melihat simbol “�”, gambar kemungkinan disimpan dengan encoding non‑UTF‑8. Konversi gambar ke PNG lossless terlebih dahulu, atau aktifkan `ocrConfig.Preprocess`.
* **Bottleneck kinerja** – Untuk batch lebih dari 100 gambar, pertimbangkan pemrosesan paralel dengan `Parallel.ForEach` dan instance `OcrEngine` terpisah per thread. Aspose bersifat thread‑safe selama setiap thread memiliki mesinnya masing‑masing.

## Langkah Selanjutnya – Selami Lebih Dalam

Setelah Anda menguasai dasar **cara menggunakan Aspose** untuk OCR, Anda mungkin ingin mengeksplor:

* **Ekspor ke PDF yang dapat dicari** – Gunakan `Aspose.Pdf` untuk menyematkan teks yang dikenali kembali ke file PDF, menjadikan dokumen yang dipindai benar‑benar dapat dicari.
* **Integrasi dengan Azure Functions** – Jalankan OCR secara otomatis ketika gambar baru masuk ke kontainer Azure Blob.
* **Menggabungkan dengan model bahasa AI** – Masukkan teks yang diekstrak ke ChatGPT atau Claude untuk rangkuman, ekstraksi entitas, atau terjemahan.

Setiap topik tersebut secara alami mencakup kata kunci sekunder kami—**extract text from images**, **run OCR on images**, dan **recognize text from scans**—sehingga Anda akan terus melihat pola yang sama sambil memperluas keahlian.

## Kesimpulan

Kami telah menelusuri contoh lengkap yang siap produksi yang menjawab pertanyaan **cara menggunakan Aspose** untuk mengekstrak teks dari gambar, menjalankan OCR pada gambar secara massal, dan mengenali teks dari pemindaian dengan kode minimal. Dengan mengonfigurasi mesin, menyiapkan daftar jalur file, memproses batch, dan mencetak hasil, Anda kini memiliki fondasi kuat untuk proyek otomatisasi dokumen apa pun.

Cobalah, sesuaikan flag konfigurasi, dan segera Anda akan mengubah gunung‑gunung kertas menjadi teks yang dapat dicari.


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}