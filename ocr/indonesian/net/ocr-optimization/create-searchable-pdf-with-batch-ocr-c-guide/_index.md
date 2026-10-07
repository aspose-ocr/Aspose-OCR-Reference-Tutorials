---
category: general
date: 2025-12-29
description: Buat PDF yang dapat dicari dari gambar hasil pemindaian menggunakan pemrosesan
  batch Aspose OCR. Pelajari cara mengonversi gambar ke PDF, mempersiapkan gambar
  untuk OCR, dan meluruskan dokumen yang dipindai.
draft: false
keywords:
- create searchable pdf
- batch ocr processing
- convert images to pdf
- preprocess images for ocr
- deskew scanned documents
language: id
og_description: Buat PDF yang dapat dicari dari gambar yang dipindai menggunakan pemrosesan
  batch Aspose OCR. Pelajari cara mengonversi gambar ke PDF, melakukan pra‑pemrosesan
  gambar untuk OCR, dan meluruskan dokumen yang dipindai.
og_title: Buat PDF yang dapat dicari dengan OCR batch – Panduan C#
tags:
- OCR
- C#
- PDF/A
- Aspose
title: Buat PDF yang Dapat Dicari dengan OCR Batch – Panduan C#
url: /id/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang dapat dicari dengan batch OCR – Panduan C#

Pernah perlu **membuat PDF yang dapat dicari** dari tumpukan gambar yang dipindai tetapi terhenti pada langkah pertama? Anda tidak sendirian—banyak pengembang mengalami hal yang sama ketika berhadapan dengan pemindaian yang berantakan, halaman yang tidak rata, atau sekadar konversi massal biasa.  

Berita baik? Dengan Aspose OCR Anda dapat membuat pipeline **pemrosesan batch OCR** yang tidak hanya **mengonversi gambar ke PDF** tetapi juga **memproses gambar untuk OCR** dan bahkan **memperbaiki kemiringan dokumen yang dipindai** secara otomatis. Dalam tutorial ini kami akan membahas seluruh proses, mulai dari menyiapkan mesin hingga memoles output, sehingga Anda dapat menjalankannya pada folder berkas dan mendapatkan PDF/A‑2b yang dapat dicari.

> **Apa yang akan Anda dapatkan:** sebuah aplikasi konsol C# tunggal yang dapat dijalankan, yang mengambil direktori gambar (atau PDF), membersihkan setiap halaman, menjalankan OCR, dan menempatkan file PDF/A‑2b yang dapat dicari di samping sumber. Tanpa potongan kode terpisah, hanya satu solusi yang koheren.

## Prasyarat

- .NET 6 SDK atau yang lebih baru (kode ini juga dapat dikompilasi dengan .NET Core).  
- Paket NuGet Aspose OCR (`Aspose.OCR`).  
- Folder berisi gambar yang dipindai (TIFF, JPEG, PNG) atau PDF yang ingin Anda ubah menjadi PDF yang dapat dicari.  
- (Opsional) Kunci lisensi asli—jika tidak, mode percobaan akan menambahkan watermark, tetapi tetap dapat digunakan untuk pengujian.

Jika Anda sudah memiliki semuanya, mari kita mulai.

## Gambaran Umum – Bagaimana seluruh pipeline membuat PDF yang dapat dicari

1. **Aktifkan mode percobaan** (atau muat lisensi Anda).  
2. **Konfigurasikan `OcrBatchProcessor`** – beri tahu di mana membaca berkas, di mana menulis PDF, format apa yang digunakan, dan berapa banyak thread yang dijalankan secara paralel.  
3. **Pra‑proses setiap gambar** – perbaiki kemiringan, hilangkan noise, dan hapus latar belakang sehingga mesin OCR melihat halaman yang bersih.  
4. **Jalankan batch** – Aspose memproses setiap berkas, menjalankan OCR, dan menulis PDF/A‑2b yang dapat dicari.  
5. **Beritahu selesai** – pesan konsol sederhana, tetapi Anda dapat menambahkan logger atau webhook.

Itulah alur tingkat tinggi. Kode di bawah ini mengimplementasikan setiap langkah dengan banyak komentar, sehingga Anda dapat menyesuaikan bagian mana pun tanpa merusak keseluruhan.

## Langkah 1 – Aktifkan mode percobaan (atau muat lisensi Anda)

Sebelum Anda dapat memanggil kelas Aspose apa pun, Anda harus memberi tahu perpustakaan bahwa Anda memiliki lisensi. Untuk percobaan cepat, mode percobaan sudah cukup.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

// Activate trial mode – replace with OcrEngine.SetLicense("YourLicenseFile.lic") for production
OcrEngine.EnableTrialMode();
```

> **Tips pro:** letakkan aktivasi lisensi di bagian paling atas `Program.cs`. Jika Anda lupa, mesin akan melemparkan pengecualian saat pertama kali memanggil `Process()`.

## Langkah 2 – Konfigurasikan mesin pemrosesan batch OCR

Di sinilah kita menyiapkan objek **pemrosesan batch OCR**. Perhatikan bahwa `InputFolder` dan `OutputFolder` sama dalam contoh ini, tetapi Anda dapat memisahkannya jika diinginkan.

```csharp
// Define where your source images live and where the searchable PDFs should be saved
var ocrBatch = new OcrBatchProcessor
{
    // Folder that contains the images or PDFs to be processed
    InputFolder = @"C:\Scans\Incoming",

    // Folder where searchable PDF/A‑2b files will be saved
    OutputFolder = @"C:\Scans\Processed",

    // Choose the output format – searchable PDF/A‑2b (perfect for archiving)
    OutputFormat = SaveFormat.SearchablePdf,

    // Limit the number of concurrent OCR operations to avoid CPU spikes
    MaxDegreeOfParallelism = 3,

    // Pre‑process each image: deskew, denoise, and remove background
    Preprocess = img => ImageFilters
                            .Deskew(img)          // fixes rotated pages
                            .Denoise()            // reduces speckles
                            .RemoveBackground()   // clears colored backgrounds
};
```

### Mengapa pengaturan ini penting

- **`MaxDegreeOfParallelism`**: Menjalankan terlalu banyak thread OCR dapat membebani CPU Anda, terutama pada workstation yang sederhana. Tiga thread adalah titik optimal untuk kebanyakan laptop quad‑core.  
- **pipeline `Preprocess`**: Ketiga filter bersama-sama secara dramatis meningkatkan akurasi OCR. Deskew memperbaiki masalah “pemindaian miring” yang umum, denoise menghilangkan noise acak, dan penghapusan latar belakang memastikan mesin hanya melihat teks hitam‑di‑atas‑putih.  
- **`SaveFormat.SearchablePdf`**: Ini membuat berkas PDF/A‑2b yang siap arsip dan dapat dicari—sebuah persyaratan untuk banyak standar kepatuhan.

## Langkah 3 – Jalankan batch dan saksikan keajaiban terjadi

Menjalankan batch semudah memanggil `Process()`. Metode ini akan menunggu hingga semua berkas selesai, kemudian mengembalikan hasil. Jika Anda memerlukan pelaporan kemajuan, Anda dapat menautkan ke acara `ProgressChanged` (tidak ditampilkan di sini).

```csharp
// Start processing – this will walk through every file in InputFolder
ocrBatch.Process();

// Let the user (or calling script) know we’re finished
Console.WriteLine("All files processed. Searchable PDFs are ready.");
```

Ketika konsol mencetak baris akhir, Anda akan menemukan PDF yang dapat dicari untuk setiap gambar input di `C:\Scans\Processed`. Buka salah satunya di Adobe Reader, tekan **Ctrl+F**, dan Anda dapat mencari teks yang baru saja diekstrak dari pemindaian.

## Langkah 4 – Program lengkap yang dapat dijalankan (siap salin‑tempel)

Di bawah ini adalah program **lengkap, mandiri** yang dapat Anda masukkan ke dalam proyek konsol baru (`dotnet new console`). Pastikan Anda telah menambahkan paket NuGet Aspose.OCR terlebih dahulu (`dotnet add package Aspose.OCR`).

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

namespace CreateSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Activate trial mode (replace with real license for production)
            OcrEngine.EnableTrialMode();

            // 2️⃣ Configure batch OCR processing
            var ocrBatch = new OcrBatchProcessor
            {
                InputFolder = @"C:\Scans\Incoming",   // 👉 change to your source folder
                OutputFolder = @"C:\Scans\Processed", // 👉 change to your target folder
                OutputFormat = SaveFormat.SearchablePdf,
                MaxDegreeOfParallelism = 3,
                Preprocess = img => ImageFilters
                                        .Deskew(img)          // fixes rotated pages
                                        .Denoise()            // cleans up noise
                                        .RemoveBackground()   // strips colored backgrounds
            };

            // 3️⃣ Run the batch
            ocrBatch.Process();

            // 4️⃣ Notify completion
            Console.WriteLine("All files processed. Searchable PDFs are ready.");
        }
    }
}
```

### Output yang diharapkan

```
All files processed. Searchable PDFs are ready.
```

Setelah dijalankan, menavigasi ke `C:\Scans\Processed` akan menampilkan sekumpulan berkas `.pdf`—setiap berkas dapat dicari, masing‑masing mematuhi PDF/A‑2b. Buka salah satu berkas, ketik kata yang Anda tahu ada dalam pemindaian asli, dan voilà, teks tersebut disorot.

## Pertanyaan umum & penanganan kasus tepi

### Bagaimana jika folder sumber saya sudah berisi PDF?

Aspose OCR dapat mengimpor PDF secara langsung; ia akan meraster setiap halaman, menerapkan filter **preprocess** yang sama, dan menyematkan lapisan OCR. Tidak diperlukan kode tambahan.

### Bagaimana cara mengubah format output menjadi PDF biasa (tidak dapat dicari)?

Ganti `SaveFormat.SearchablePdf` dengan `SaveFormat.Pdf`. Anda akan kehilangan lapisan teks yang dapat dicari, tetapi kualitas visual tetap sama.

### Pemindaian saya berwarna—apakah penghapusan latar belakang mempengaruhinya?

`RemoveBackground()` menargetkan latar belakang non‑putih sambil mempertahankan teks utama. Jika Anda perlu mempertahankan grafik berwarna, Anda dapat menghilangkan filter tersebut:

```csharp
.Preprocess = img => ImageFilters.Deskew(img).Denoise()
```

### Saya menjalankan di server dengan RAM terbatas—bisakah saya mengurangi jumlah thread?

Tentu saja. Atur `MaxDegreeOfParallelism` ke `1` atau `2`. Batch akan memakan waktu lebih lama, tetapi penggunaan memori akan tetap rendah.

## Ringkasan visual (opsional)

Jika Anda suka diagram cepat, bayangkan alur ini:

![Alur kerja membuat PDF yang dapat dicari – menunjukkan folder input → pra‑pemrosesan → OCR → output PDF yang dapat dicari](/images/ocr-workflow.png)

*​Teks alt gambar:* **Diagram alur kerja membuat PDF yang dapat dicari** – menggambarkan pemrosesan batch OCR, konversi, dan langkah deskew.

## Kesimpulan

Anda kini memiliki solusi **lengkap, siap produksi** untuk **membuat PDF yang dapat dicari** dari kumpulan gambar yang dipindai. Dengan memanfaatkan **pemrosesan batch OCR**, Anda dapat **mengonversi gambar ke PDF**, **memproses gambar untuk OCR**, dan secara otomatis **memperbaiki kemiringan dokumen yang dipindai**—semua dengan hanya beberapa baris kode C#.

Langkah selanjutnya? Coba tambahkan skema penamaan khusus, hubungkan kerangka logging untuk menangkap skor kepercayaan OCR, atau bereksperimen dengan `ImageFilters` lain seperti `Sharpen()` untuk teks yang pudar. API Aspose OCR cukup fleksibel untuk berkembang bersama kebutuhan Anda.

Selamat coding, semoga PDF Anda selalu dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}