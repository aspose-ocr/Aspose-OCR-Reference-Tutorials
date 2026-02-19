---
category: general
date: 2026-02-19
description: Pelajari cara melakukan OCR batch dengan Aspose.OCR di C#. Panduan ini
  menunjukkan cara mengekstrak teks dari gambar dan mengonversi gambar ke txt secara
  efisien.
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: id
og_description: Cara melakukan OCR batch dengan Aspose.OCR di C#. Ekstrak teks dari
  gambar dan konversi gambar ke txt dalam beberapa langkah mudah.
og_title: Cara Batch OCR di C# – Konversi Gambar ke Teks Cepat
tags:
- OCR
- C#
- Aspose
title: Cara Melakukan OCR Batch di C# – Ekstrak Teks dari Gambar dengan Cepat
url: /id/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Batch OCR di C# – Panduan Langkah‑demi‑Langkah Lengkap

Pernah bertanya-tanya **bagaimana cara batch OCR** seluruh folder gambar tanpa menulis program terpisah untuk setiap file? Anda bukan satu‑satunya. Banyak pengembang menemui kendala ketika mereka harus mengekstrak teks dari puluhan—atau bahkan ribuan—halaman yang dipindai, kwitansi, atau tangkapan layar. Kabar baik? Dengan Aspose.OCR Anda dapat mengotomatisasi seluruh alur kerja, **extract text from images**, dan **convert images to txt** dengan hanya beberapa baris kode.

Dalam tutorial ini kami akan menelusuri contoh lengkap yang siap dijalankan yang menunjukkan secara tepat cara menyiapkan OCR batch processor, menyesuaikan preprocessing, menangani paralelisme, dan menulis setiap hasil ke file `.txt`. Pada akhir tutorial Anda akan memiliki aplikasi konsol mandiri yang dapat Anda masukkan ke proyek .NET mana pun.

## Apa yang Anda Butuhkan

- .NET 6.0 atau yang lebih baru (kode ini juga bekerja pada .NET Core dan .NET Framework)
- Paket NuGet Aspose.OCR untuk .NET (`Aspose.OCR`)  
- Sebuah folder berisi file gambar (`.png`, `.jpg`, dll.) yang ingin Anda proses
- Jumlah RAM yang cukup; demo ini menggunakan 4 thread paralel tetapi Anda dapat menyesuaikannya

Tidak ada layanan eksternal, tidak ada file konfigurasi tersembunyi—hanya kode C# murni yang dapat Anda kompilasi dan jalankan hari ini.

![Diagram illustrating how to batch ocr processing flow](/images/how-to-batch-ocr-flow.png "how to batch ocr flow diagram")

## Langkah 1: Instal Aspose.OCR dan Siapkan Proyek

Pertama, tambahkan paket Aspose.OCR ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

Mengapa ini penting: Aspose.OCR menyertakan mesin OCR, data bahasa, dan utilitas preprocessing, sehingga Anda tidak memerlukan binary pihak ketiga apa pun. Setelah paket terpasang, buat aplikasi konsol baru (atau tambahkan kode ke yang sudah ada) dan impor namespace yang diperlukan:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

Pernyataan `using` ini memberi Anda akses ke kelas batch processor dan helper I/O yang berguna.

## Langkah 2: Konfigurasikan OCR Batch Processor

Sekarang kami akan menginstansiasi `OcrBatchProcessor` dan memberi tahu bahasa yang akan dicari, cara membersihkan gambar, serta berapa banyak thread yang dijalankan secara paralel. Inilah inti dari **bagaimana cara batch OCR** secara efisien.

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**Mengapa mengaktifkan Deskew?** Banyak dokumen yang dipindai tidak sejajar sempurna; algoritma deskew memutar kembali gambar ke garis dasar yang lurus, yang sering meningkatkan tingkat pengenalan sebesar 10‑15 %.

## Langkah 3: Sambungkan Callback Hasil untuk Menyimpan File Teks

Batch processor memicu sebuah event untuk setiap gambar yang selesai diproses. Kami akan berlangganan ke `ResultProcessed` sehingga dapat menulis setiap hasil OCR ke file `.txt`—secara efektif **convert images to txt** secara langsung.

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

Tips cepat: Jika Anda perlu mempertahankan struktur folder asli, Anda dapat memodifikasi `txtPath` untuk menyertakan subfolder atau direktori output terpisah.

## Langkah 4: Jalankan Batch pada Folder Gambar Anda

Yang tersisa hanyalah mengarahkan processor ke folder yang berisi gambar yang ingin Anda **extract text from images**. Metode `ProcessFolder` memindai subfolder secara rekursif, sehingga Anda dapat menaruh seluruh pohon pemindaian dan membiarkan pustaka menangani sisanya.

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

Saat Anda menjalankan program, Anda akan melihat output konsol seperti:

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

Setiap gambar kini memiliki file `.txt` saudara yang berisi teks yang diekstrak.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel ke `Program.cs`:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### Output yang Diharapkan

- Untuk setiap `*.png` atau `*.jpg` di direktori sumber, file `*.txt` yang bersesuaian muncul di sampingnya.
- Konsol mencetak satu baris per file, memberikan umpan balik secara langsung.
- Jika sebuah gambar tidak dapat dibaca (file rusak, format tidak didukung), Aspose.OCR mencatat error tetapi tetap melanjutkan pemrosesan sisanya—berkat ketangguhan bawaan mesin batch.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya perlu memproses PDF alih-alih gambar?

Aspose.OCR dapat menerima halaman PDF sebagai gambar secara internal, tetapi Anda harus mengonversi PDF ke gambar raster terlebih dahulu (misalnya, menggunakan Aspose.PDF). Setelah Anda memiliki PNG, kode batch yang sama dapat digunakan tanpa perubahan.

### Bisakah saya mengubah bahasa secara dinamis?

Ya. Properti `Language` menerima nilai enum `Language` apa pun (Spanyol, Prancis, Mandarin, dll.). Jika Anda memiliki dokumen multibahasa, pertimbangkan menjalankan dua kali proses—satu per bahasa—atau gunakan `Language.AutoDetect`.

### Bagaimana cara membatasi batch hanya pada tipe file tertentu?

`ProcessFolder` menerima opsi `SearchOption` dan `string[] extensions` secara opsional. Contoh:

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### Bagaimana dengan percepatan GPU?

Aspose.OCR mendukung GPU melalui konfigurasi `OcrEngine`, namun `MaxDegreeOfParallelism` pada batch processor tetap menjadi kontrol utama untuk konkruensi. Jika Anda memiliki GPU yang kompatibel, aktifkan di pengaturan engine sebelum membuat `OcrBatchProcessor`.

### Bagaimana menangani folder yang sangat besar (puluhan ribu file)?

- Tingkatkan `MaxDegreeOfParallelism` dengan hati‑hati; terlalu banyak thread dapat menghabiskan memori.
- Gunakan folder output khusus untuk menghindari kekacauan.
- Secara periodik flush log ke disk untuk mencegah penumpukan memori.

## Tips Profesional untuk OCR Berkualitas Tinggi

- **DPI Penting**: Gambar dengan 300 DPI atau lebih menghasilkan akurasi terbaik. Jika pemindaian Anda lebih rendah, pertimbangkan up‑scaling dengan filter bikubik sebelum diproses.
- **Pengurangan Noise**: Aktifkan `Preprocessing.NoiseRemoval` jika gambar sumber berbutir.
- **Penamaan File**: Jaga nama file tetap pendek dan alfanumerik; karakter khusus dapat mengacaukan logika path callback.
- **Logging**: Ganti `Console.WriteLine` dengan logger yang tepat (misalnya, `Serilog`) untuk beban kerja produksi.

## Langkah Selanjutnya

Setelah Anda menguasai **bagaimana cara batch OCR**, Anda mungkin ingin:

- **Extract text from images** dan mengirimkan output ke indeks pencarian (misalnya, Elasticsearch) untuk pencarian teks penuh.
- **Convert images to txt** lalu menjalankan pemrosesan bahasa alami (NLP) untuk mengklasifikasikan dokumen secara otomatis.
- Bereksperimen dengan **different language packs** atau kamus khusus untuk terminologi industri tertentu.

Jika Anda penasaran tentang post‑processing, lihat tutorial “Parsing OCR output with regular expressions” atau “Storing OCR results in a SQL database”.

---

**Selamat coding!** Jangan ragu untuk menyesuaikan paralelisme, menambah langkah preprocessing, atau membungkus seluruh proses dalam layanan Windows untuk pemantauan berkelanjutan. Langit adalah batasnya ketika Anda menggabungkan kemampuan batch Aspose.OCR dengan sedikit kepintaran .NET.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}