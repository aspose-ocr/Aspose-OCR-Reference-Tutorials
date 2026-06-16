---
category: general
date: 2026-03-07
description: Ekstrak teks dari file PNG menggunakan C#. Pelajari cara mengonversi
  gambar menjadi teks dengan C# dan baca teks dari gambar yang dipindai dengan cepat.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: id
og_description: Ekstrak teks dari file PNG menggunakan C#. Panduan ini menunjukkan
  cara mengonversi gambar menjadi teks C# dan membaca teks dari gambar yang dipindai
  dengan Aspose OCR.
og_title: Ekstrak Teks dari PNG di C# – Panduan OCR Lengkap
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Ekstrak Teks dari PNG di C# – Panduan OCR Lengkap
url: /id/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari PNG di C# – Panduan OCR Lengkap

Pernah perlu **mengekstrak teks dari file PNG** tetapi tidak tahu harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami hal ini saat pertama kali menghadapi grafik yang dipindai atau screenshot yang harus menjadi teks yang dapat dicari. Kabar baik? Dengan beberapa baris C# dan Aspose OCR Anda dapat mengubah PNG apa pun menjadi string yang dapat diedit dalam sekejap.

Dalam tutorial ini kami akan membahas seluruh proses: mulai dari menemukan PNG di disk, meluncurkan tugas OCR secara paralel, hingga menampilkan pratinjau rapi setiap hasil. Pada akhir tutorial Anda akan tahu cara **convert image to text C#**, dapat **read text from scanned images** secara efisien, dan juga melihat cara terbaik untuk **run OCR on images** tanpa membebani thread UI Anda.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode ini juga bekerja di .NET Core dan .NET Framework)  
- Paket NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Sebuah folder berisi file *.png* yang ingin Anda proses  
- IDE apa saja yang Anda suka (Visual Studio, VS Code, Rider…)

Tidak ada konfigurasi tambahan yang diperlukan; pustaka ini sudah menyertakan semua yang dibutuhkan untuk mendekode PNG, JPEG, TIFF, apa saja.

## Langkah 1: Temukan Semua File PNG – “Extract Text from PNG” Dimulai

Pertama kita harus menemukan setiap PNG yang akan diproses OCR. Menggunakan `Directory.GetFiles` cepat dan dapat diandalkan.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*Mengapa ini penting:* Memindai direktori sekali saja membuat sisa alur kerja tetap sederhana, dan pemeriksaan awal mencegah situasi “tidak ada output” yang diam-diam dan sulit dideteksi nanti.

## Langkah 2: Jalankan Tugas OCR Paralel – Secara Efisien **run OCR on images**

Menjalankan OCR secara berurutan baik untuk beberapa file, tetapi proyek dunia nyata sering berurusan dengan puluhan atau ratusan file. Dengan meluncurkan `Task` per gambar, CPU tetap sibuk sementara pustaka melakukan pekerjaan beratnya.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*Tip pro:* `Task.Run` memindahkan pekerjaan ke thread pool, yang berarti UI Anda (jika ada) tetap responsif. Jika Anda berada di server, pola yang sama dapat diskalakan dengan baik di seluruh core.

## Langkah 3: Tunggu Semua Tugas – Kumpulkan Hasilnya

Sekarang kita menunggu setiap operasi OCR selesai. `Task.WhenAll` mengembalikan array yang berurutan sesuai dengan urutan file asli, sehingga mudah memadukan hasil dengan nama file.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*Catatan kasus tepi:* Jika satu gambar saja melempar pengecualian (file rusak, format tidak didukung) seluruh `WhenAll` akan mengangkat pengecualian tersebut. Anda dapat membungkus `Task.Run` internal dalam try/catch dan mengembalikan string kosong atau pesan diagnostik jika memerlukan toleransi kesalahan.

## Langkah 4: Tampilkan Pratinjau – Verifikasi output **convert image to text C#**

Pratinjau cepat membantu Anda memastikan OCR berhasil sebelum menyimpan data ke tempat lain.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

Output konsol tipikal terlihat seperti:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

Jika pratinjau menampilkan karakter acak, periksa kembali kualitas gambar atau pertimbangkan pra‑pemrosesan (misalnya, binarisasi) – tetapi untuk kebanyakan PNG bersih Aspose OCR akan menghasilkan hasil yang tepat pada percobaan pertama.

## Opsional: Simpan Hasil ke CSV – Kasus Penggunaan Dunia Nyata

Sebagian besar proyek memerlukan teks yang diekstrak dalam format terstruktur. Di bawah ini ada helper kecil yang menulis nama file dan teks OCR lengkap ke file CSV.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

Sekarang Anda dapat mengimpor CSV ke Excel, Power BI, atau sistem downstream apa pun yang mengharapkan **read text from scanned images**.

## Pertanyaan yang Sering Diajukan

**Bagaimana jika PNG saya sangat besar (lebih dari 5 MB)?**  
Aspose OCR secara otomatis menurunkan resolusi gambar besar untuk menjaga penggunaan memori tetap wajar, tetapi Anda dapat mengubah ukuran secara manual dengan `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` untuk membatasi lebar menjadi 2000 px sambil mempertahankan rasio aspek.

**Apakah saya dapat menjalankannya di Linux?**  
Ya. Aspose OCR bersifat lintas‑platform; pastikan dependensi native (`libgdiplus` pada beberapa distro) sudah terpasang.

**Apakah bahasa OCR defaultnya Inggris?**  
Benar. Jika Anda membutuhkan bahasa lain, setel `engine.Language = OcrLanguage.French;` (atau enum lain yang didukung) sebelum memanggil `Recognize()`.

**Bagaimana menangani PDF yang dilindungi password dan berisi PNG?**  
Konversi halaman PDF ke gambar terlebih dahulu (menggunakan Aspose PDF atau pustaka lain), lalu masukkan PNG tersebut ke dalam pipeline yang sama. Prinsip **how to run OCR on images** tetap tidak berubah.

## Contoh Lengkap yang Berfungsi (Async Main)

Berikut adalah program mandiri yang dapat Anda salin‑tempel ke proyek konsol. Program ini mencakup semua bagian di atas, plus helper kecil untuk memvalidasi folder input.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**Output yang diharapkan** (contoh untuk dua PNG):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## Penutup

Kami baru saja membahas semua yang Anda perlukan untuk **extract text from PNG** menggunakan C#. Dari menemukan file, meluncurkan pekerjaan OCR paralel, meninjau string, hingga menyimpannya ke CSV—panduan ini memberikan pola siap produksi untuk skenario **convert image to text C#**.  

Jika Anda siap ke langkah berikutnya, coba jalankan pipeline yang sama untuk file JPEG atau TIFF, bereksperimen dengan bahasa OCR yang berbeda, atau hubungkan hasilnya ke indeks pencarian sehingga Anda dapat **read text from scanned images** secara instan.  

Punya pertanyaan tentang kasus tepi, penyetelan performa, atau lisensi? Tinggalkan komentar atau hubungi komunitas Aspose—selamat coding!  

![Ekstrak teks dari contoh PNG](extract-text-png.png "Ekstrak teks dari PNG menggunakan Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}