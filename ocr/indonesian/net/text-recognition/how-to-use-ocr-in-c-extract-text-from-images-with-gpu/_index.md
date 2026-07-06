---
category: general
date: 2026-02-13
description: Pelajari cara menggunakan OCR dalam C# untuk mengekstrak teks dari file
  gambar, mengaktifkan pemrosesan GPU, dan mengonversi pemindaian menjadi teks dengan
  cepat.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: id
og_description: Bagaimana cara menggunakan OCR di C#? Panduan ini menunjukkan cara
  mengekstrak teks dari file gambar, mengaktifkan pemrosesan GPU, dan mengubah pemindaian
  menjadi teks.
og_title: Cara Menggunakan OCR di C# – Mengekstrak Teks dari Gambar dengan GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Cara Menggunakan OCR di C# – Mengekstrak Teks dari Gambar dengan GPU
url: /id/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

Use hyphens for bullet lists, numbers for ordered list.

Make sure we keep the same indentation.

Now produce final output with all translated content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Mengekstrak Teks dari Gambar dengan GPU

Pernah bertanya-tanya **bagaimana cara menggunakan OCR** untuk mengambil teks dari dokumen yang dipindai tanpa susah payah? Anda bukan satu-satunya—para pengembang terus menanyakan, “Bagaimana saya dapat mengekstrak teks dari file gambar secara efisien?” Kabar baiknya, dengan Aspose.OCR Anda dapat melakukannya, dan bahkan dapat **mengaktifkan pemrosesan GPU** untuk peningkatan kecepatan yang terlihat pada perangkat keras yang didukung.

Dalam tutorial ini kami akan membahas contoh lengkap, end‑to‑end yang menunjukkan **cara menggunakan OCR**, cara **mengekstrak teks dari gambar**, cara **mengonversi scan menjadi teks**, dan apa yang harus dilakukan jika GPU tidak tersedia. Pada akhir tutorial Anda akan memiliki aplikasi konsol C# yang siap dijalankan yang mencetak teks yang dikenali dan memberi tahu apakah GPU sebenarnya digunakan.

## Apa yang Anda Butuhkan

- .NET 6 SDK atau yang lebih baru (kode ini juga bekerja dengan .NET Core)  
- Visual Studio 2022 atau editor apa pun yang Anda sukai  
- Paket Aspose.OCR untuk .NET (tersedia via NuGet)  
- File gambar beresolusi tinggi (misalnya `highres_scan.tif`) untuk diuji  

Tidak memerlukan pengaturan rumit—hanya beberapa perintah NuGet dan Anda siap melanjutkan.

## Langkah 1: Instal Aspose.OCR dan Siapkan Proyek

Hal pertama yang harus dilakukan. Anda harus menambahkan pustaka OCR ke dalam proyek Anda. Buka terminal di folder solusi Anda dan jalankan:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Itu akan membuat proyek konsol baru bernama **OcrDemo** dan menambahkan paket NuGet `Aspose.OCR`. Pustaka tersebut berisi kelas `OcrEngine` yang akan kita gunakan.

> **Pro tip:** Jika Anda menggunakan mesin dengan GPU khusus, pastikan driver grafis terbaru telah terpasang; jika tidak, pustaka akan secara otomatis beralih ke mode CPU.

## Langkah 2: Tulis Kode OCR Lengkap

Sekarang buka `Program.cs` dan ganti isinya dengan yang berikut. Setiap baris diberi komentar sehingga Anda dapat melihat *mengapa* kami melakukan hal tersebut.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Mengapa Ini Berfungsi

- **ProcessingMode = Gpu** memberi tahu engine untuk mencoba GPU terlebih dahulu. Pustaka mengabstraksi panggilan CUDA/OpenCL tingkat rendah, jadi Anda tidak perlu mengelola konteks perangkat secara manual.  
- **IsGpuEnabled** adalah boolean yang mengonfirmasi apakah jalur GPU berhasil. Jika Anda melihat `false`, engine secara otomatis beralih ke CPU—tidak perlu panik.  
- **RecognizeImage** melakukan semua pekerjaan berat: memuat gambar, menjalankan model OCR, dan mengembalikan hasil teks biasa. Tidak perlu memproses bitmap secara manual kecuali Anda memiliki persyaratan khusus (mis., deskewing).

## Langkah 3: Jalankan Aplikasi dan Verifikasi Output

Kompilasi dan jalankan:

```bash
dotnet run
```

Jika semuanya telah disiapkan dengan benar, Anda akan melihat sesuatu seperti:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Jika GPU tidak tersedia, baris pertama akan menampilkan `GPU used: False`, tetapi teks yang diekstrak tetap akan muncul—berkat fallback yang mulus.

> **Pertanyaan umum:** *Bagaimana jika gambar saya berupa JPEG bukan TIFF?*  
> Metode `RecognizeImage` menerima format apa pun yang didukung oleh `System.Drawing` .NET (JPEG, PNG, BMP, dll.). Cukup ubah ekstensi file di `imagePath`.

## Langkah 4: Opsional – Sesuaikan Pengaturan untuk Akurasi Lebih Baik

Aspose.OCR menawarkan beberapa pengaturan yang dapat Anda ubah:

| Setting | Apa Fungsinya | Kapan Digunakan |
|---------|--------------|-----------------|
| `ocrEngine.Language` | Memaksa bahasa tertentu (mis., `OcrLanguage.English`) | Jika Anda mengetahui bahasa dokumen |
| `ocrEngine.PageSegMode` | Mengontrol bagaimana engine membagi halaman menjadi blok | Untuk tata letak multi‑kolom |
| `ocrEngine.DetectOrientation` | Memutar otomatis teks yang tidak tegak lurus | Scan yang mungkin terbalik |

Anda dapat mengatur properti ini sebelum memanggil `RecognizeImage`. Misalnya:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Langkah 5: Visualisasikan Alur (Gambar dengan Teks Alt)

Di bawah ini adalah diagram sederhana yang menggambarkan **cara menggunakan OCR** dengan akselerasi GPU opsional. Ini tidak diperlukan agar kode berjalan, tetapi membantu Anda melihat gambaran besarnya.

![Diagram yang menunjukkan cara menggunakan OCR dengan pemrosesan GPU](/images/ocr-gpu-flow.png)

*Teks alt:* *Diagram yang menunjukkan cara menggunakan OCR dengan pemrosesan GPU, menyoroti fallback ke CPU bila diperlukan.*

## Kasus Pinggir & Pemecahan Masalah

1. **Out‑of‑Memory pada GPU** – Gambar yang sangat besar dapat melebihi memori GPU. Dalam kasus tersebut, pustaka akan beralih kembali ke CPU secara otomatis. Anda dapat memperkecil skala gambar terlebih dahulu untuk menjaga penggunaan memori tetap rendah.  
2. **Format Gambar Tidak Didukung** – Jika `RecognizeImage` melempar *NotSupportedException*, periksa ekstensi file dan pastikan gambar tidak rusak. Mengonversi ke PNG sering menyelesaikan masalah.  
3. **Skor Kepercayaan Rendah** – Ketika hasil OCR berisi banyak karakter yang tidak dapat dibaca, pertimbangkan pra‑pemrosesan (binarisasi, penghilangan noise) atau beralih ke scan dengan resolusi lebih tinggi.  

## Ringkasan: Apa yang Kami Capai

Kami baru saja membahas **cara menggunakan OCR** dalam aplikasi konsol C#, mendemonstrasikan cara **mengekstrak teks dari file gambar**, dan menunjukkan cara **mengaktifkan pemrosesan GPU** untuk hasil yang lebih cepat. Sekarang Anda tahu cara **mengonversi scan menjadi teks**, memverifikasi apakah GPU benar‑benar digunakan, dan menyesuaikan beberapa pengaturan untuk skenario kasus pinggir.

### Langkah Selanjutnya

- Coba masukkan output ke dalam **indeks pencarian** (mis., Elasticsearch) sehingga PDF yang dipindai menjadi dapat dicari.  
- Bereksperimen dengan **pemrosesan batch**—loop melalui folder gambar dan tulis setiap hasil ke file `.txt`.  
- Gabungkan OCR dengan **API terjemahan** untuk secara otomatis menerjemahkan dokumen berbahasa asing yang dipindai.  

Masih ada pertanyaan? Tinggalkan komentar, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}