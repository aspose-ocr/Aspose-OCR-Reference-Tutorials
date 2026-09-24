---
category: general
date: 2026-01-15
description: Cara melakukan OCR di C# dengan cepat dan aman. Pelajari cara mengekstrak
  teks dari gambar, memuat gambar untuk OCR, dan memproses gambar dengan OCR menggunakan
  Aspose OCR.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image for OCR
- process image with OCR
- offline OCR C#
- Aspose OCR tutorial
language: id
og_description: Cara melakukan OCR di C# secara offline. Tutorial langkah demi langkah
  ini menunjukkan cara mengekstrak teks dari gambar, memuat gambar untuk OCR, dan
  memproses gambar dengan OCR menggunakan Aspose.
og_title: Cara Melakukan OCR di C# – Panduan Ekstraksi Teks Offline
tags:
- OCR
- C#
- Aspose
title: Cara Melakukan OCR di C# – Panduan Ekstraksi Teks Offline
url: /id/net/text-recognition/how-to-perform-ocr-in-c-offline-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Panduan Ekstraksi Teks Offline

Pernah bertanya-tanya **bagaimana cara melakukan OCR** dalam aplikasi C# tanpa mengirim data apa pun ke cloud? Anda tidak sendirian. Banyak pengembang membutuhkan cara yang dapat diandalkan untuk *mengekstrak teks dari gambar* sambil menjaga semuanya tetap di‑lokasi—terutama ketika menangani dokumen sensitif.

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan cara **memuat gambar untuk OCR**, mengonfigurasi mesin Aspose OCR untuk penggunaan offline, dan akhirnya **memproses gambar dengan OCR** untuk mendapatkan teks bersih yang dapat dicari. Tanpa layanan eksternal, tanpa panggilan jaringan tersembunyi—hanya kode C# murni yang dapat Anda sisipkan ke proyek .NET apa pun.

> **Apa yang akan Anda dapatkan:** program mandiri yang membaca file PNG, menjalankan pengenalan bahasa Prancis, dan mencetak hasilnya ke konsol. Kami juga akan membahas jebakan umum, penyesuaian opsional, dan ide langkah selanjutnya sehingga Anda dapat menyesuaikan solusi untuk bahasa atau skenario apa pun.

## Prasyarat

- **.NET 6.0** (atau runtime .NET terbaru apa pun). Versi lama tetap dapat bekerja, tetapi sintaks yang ditunjukkan sesuai dengan SDK saat ini.
- **Aspose.OCR for .NET** paket NuGet. Instal dengan `dotnet add package Aspose.OCR`.
- Sebuah folder bernama `OCRResources` yang berisi paket bahasa yang Anda perlukan (dapat diunduh dari situs Aspose).  
- File gambar (`offline_test.png`) yang ingin Anda kenali.  
- IDE dasar seperti Visual Studio, VS Code, atau Rider.

Jika Anda belum memiliki salah satu dari ini, dapatkan sekarang—jika tidak, kode tidak akan dapat dikompilasi.

## Langkah 1: Siapkan Mesin OCR Offline (Kata Kunci Utama dalam Aksi)

Hal pertama yang perlu kita lakukan adalah **bagaimana cara melakukan OCR** tanpa mengakses internet. Itu berarti mengarahkan `OcrEngine` ke direktori sumber daya lokal dan menonaktifkan semua unduhan otomatis.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine for offline use
        var ocrEngine = new OcrEngine
        {
            // Tell the engine where the language files live
            ResourcePath = @"YOUR_DIRECTORY\OCRResources",
            // Prevent the SDK from trying to fetch missing files online
            AllowOnlineDownload = false
        };
```

**Mengapa ini penting:** Dengan mengatur `AllowOnlineDownload` ke `false`, Anda menjamin proses tetap sepenuhnya lokal. Ini sangat penting untuk lingkungan dengan kepatuhan ketat (kesehatan, keuangan, dll.) di mana data tidak boleh pernah keluar dari lokasi.

## Langkah 2: Muat Gambar untuk OCR

Setelah mesin siap, kita perlu **memuat gambar untuk OCR**. Aspose menyediakan metode statis yang nyaman yang membaca format umum (PNG, JPEG, TIFF) langsung ke dalam objek `OcrImage`.

```csharp
        // 2️⃣ Load the image you want to recognize
        var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY\offline_test.png");
```

> **Tip pro:** Jika gambar Anda berada dalam stream (misalnya, berasal dari basis data), gunakan `OcrImage.FromStream(yourStream)` sebagai gantinya. Ini menghindari file sementara dan dapat meningkatkan kinerja.

## Langkah 3: Pilih Bahasa dan Proses Gambar dengan OCR

Dengan gambar berada di memori, akhirnya kita **memproses gambar dengan OCR**. Metode `Recognize` menerima baik gambar maupun nilai enum `Language`. Pada contoh ini kami memilih bahasa Prancis, tetapi Anda dapat menggantinya dengan bahasa apa pun yang telah Anda unduh.

```csharp
        // 3️⃣ Perform OCR using the desired language (French in this case)
        var ocrResult = ocrEngine.Recognize(ocrImage, Language.French);
```

**Apa yang terjadi di balik layar?** Mesin menjalankan serangkaian langkah pra‑pemrosesan—binarisasi, penghilangan noise, analisis tata letak—sebelum mengirim data piksel ke jaringan saraf OCR. Objek hasil berisi teks polos, skor kepercayaan, dan bahkan kotak pembatas jika Anda membutuhkannya nanti.

## Langkah 4: Ekstrak Teks dari Gambar dan Tampilkan

Bagian terakhir dari teka‑teki adalah **mengekstrak teks dari gambar** dan melakukan sesuatu yang berguna dengannya. Untuk demo ini kami cukup menulis teks ke konsol, tetapi Anda dapat menyimpannya di basis data, mengirimnya ke indeks pencarian, atau meneruskannya ke layanan lain.

```csharp
        // 4️⃣ Output the recognized text
        System.Console.WriteLine("=== OCR Result ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
=== OCR Result ===
Bonjour, ceci est un test d'OCR hors ligne.
```

Jika output terlihat berantakan, periksa kembali bahwa paket bahasa yang tepat ada di `OCRResources`. Karakter yang hilang sering menunjukkan file sumber daya yang tidak ada atau tidak cocok.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah seluruh program, siap untuk dikompilasi. Ganti jalur placeholder dengan direktori Anda yang sebenarnya.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class OfflineDemo
{
    static void Main()
    {
        // Step 1 – Configure the offline OCR engine
        var ocrEngine = new OcrEngine
        {
            ResourcePath = @"C:\MyProject\OCRResources", // <-- adjust this
            AllowOnlineDownload = false
        };

        // Step 2 – Load the image you want to recognize
        var ocrImage = OcrImage.FromFile(@"C:\MyProject\offline_test.png"); // <-- adjust this

        // Step 3 – Run OCR (choose the language you need)
        var ocrResult = ocrEngine.Recognize(ocrImage, Language.French);

        // Step 4 – Display the extracted text
        System.Console.WriteLine("=== OCR Result ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **Output yang diharapkan:** Konsol mencetak teks persis yang muncul di `offline_test.png`. Jika gambar berisi bahasa Inggris, ubah `Language.French` menjadi `Language.English`.

## Pertanyaan Umum & Kasus Tepi

| Question | Answer |
|----------|--------|
| *Bagaimana jika saya membutuhkan beberapa bahasa dalam satu gambar?* | Panggil `Recognize` dua kali—sekali per bahasa—atau gunakan `Language.AutoDetect` (jika Anda mengaktifkan sumber daya online). |
| *Gambar saya adalah TIFF multi‑halaman; dapatkah saya memproses semua halaman?* | Ya. Lakukan loop melalui setiap halaman dengan `OcrImage.FromMultiPageFile` dan kirim setiap potongan ke `Recognize`. |
| *Bagaimana cara meningkatkan akurasi pada pemindaian kualitas rendah?* | Pra‑proses bitmap sendiri (misalnya, tingkatkan kontras, koreksi kemiringan) sebelum mengirimnya ke `OcrImage`. |
| *Bisakah saya menjalankan ini di dalam kontainer Docker?* | Tentu saja. Cukup salin folder `OCRResources` ke dalam image kontainer dan atur `ResourcePath` sesuai. |
| *Apakah ada cara untuk mendapatkan skor kepercayaan?* | Objek `OcrResult` menyediakan `Confidence` per karakter; iterasi `ocrResult.Characters` jika Anda memerlukan data yang lebih rinci. |

## Tips Pro untuk OCR Siap Produksi

1. **Cache mesin** – Membuat `OcrEngine` baru per permintaan menambah beban. Simpan instance singleton jika aplikasi Anda memproses banyak gambar.
2. **Validasi ukuran input** – Gambar yang sangat besar dapat menyebabkan pengecualian OutOfMemory. Ubah ukuran ke DPI yang wajar (300 dpi adalah keseimbangan yang baik).
3. **Keamanan thread** – Mesin itu sendiri thread‑safe, tetapi file sumber daya di bawahnya bersifat read‑only, sehingga Anda dapat memparalelkan panggilan dengan aman.
4. **Logging** – Tangkap `ocrResult.Text` dan setiap error ke log terstruktur; ini membantu ketika Anda perlu mengaudit hasil OCR untuk kepatuhan.

## Langkah Selanjutnya (Manfaatkan Kata Kunci Sekunder)

- **Ekstrak teks dari gambar** dalam mode batch: tulis utilitas konsol kecil yang menelusuri folder, menjalankan kode di atas, dan menulis setiap hasil ke file `.txt`.
- **Muat gambar untuk OCR** dari API web: ekspos endpoint yang menerima string base‑64, mendekodekannya, dan menjalankan pipeline offline yang sama.
- **Proses gambar dengan OCR** dalam pipeline CI/CD: otomatisasi pembuatan PDF yang dapat dicari sebagai bagian dari proses build dokumentasi Anda.

## Kesimpulan

Anda kini memiliki jawaban lengkap, end‑to‑end untuk **bagaimana cara melakukan OCR** di C# tanpa pernah menyentuh internet. Dengan mengonfigurasi `OcrEngine` untuk penggunaan offline, memuat gambar Anda dengan benar, dan memanggil `Recognize` dengan bahasa yang tepat, Anda dapat secara andal **mengekstrak teks dari gambar** dalam lingkungan .NET apa pun.

Ingat, kunci keberhasilan OCR adalah sumber daya yang baik, pra‑pemrosesan yang tepat, dan penanganan kasus tepi seperti dokumen multi‑halaman. Jangan ragu untuk bereksperimen dengan bahasa lain, menyesuaikan pengaturan mesin, atau mengintegrasikan kode ke dalam alur kerja yang lebih besar.

Selamat coding, semoga teks Anda selalu dapat dibaca! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}