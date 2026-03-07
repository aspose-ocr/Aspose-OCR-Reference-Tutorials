---
category: general
date: 2026-03-07
description: Contoh Aspose OCR yang menunjukkan cara mengaktifkan pemeriksaan ejaan,
  menambahkan kamus khusus, memuat OCR gambar, dan memperbaiki kesalahan OCR dengan
  cepat.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: id
og_description: Contoh OCR Aspose yang memandu Anda melalui mengaktifkan pemeriksaan
  ejaan, menambahkan kamus khusus, memuat gambar untuk OCR, dan memperbaiki kesalahan
  OCR umum.
og_title: Contoh OCR Aspose – Aktifkan Pemeriksaan Ejaan & Perbaiki Kesalahan
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Contoh Aspose OCR – Aktifkan Pemeriksaan Ejaan dan Perbaiki Kesalahan di C#
url: /id/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Contoh Aspose OCR – Aktifkan Pemeriksaan Ejaan dan Perbaiki Kesalahan dalam C#

Pernah membutuhkan **contoh Aspose OCR** yang tidak hanya membaca teks dari gambar tetapi juga membersihkan kesalahan ejaan yang mengganggu? Anda bukan satu‑satunya. Dalam banyak proyek dunia nyata output OCR mentah dipenuhi typo, terutama ketika gambar sumber berisi font kontras rendah atau catatan tulisan tangan.  

Kabar baik? Dengan Aspose.OCR Anda dapat **mengaktifkan pemeriksaan ejaan**, menambahkan kamus Anda sendiri, dan mendapatkan string yang rapi hanya dalam beberapa baris kode. Di bawah ini Anda akan melihat **cara mengaktifkan pemeriksaan ejaan**, **cara menambahkan kamus**, dan **cara memuat OCR gambar** sehingga Anda akhirnya dapat **memperbaiki kesalahan OCR** tanpa menggaruk kepala.

Dalam tutorial ini kami akan membahas semua yang Anda perlukan—dari instalasi NuGet hingga program lengkap yang dapat dijalankan dan mencetak teks yang telah dikoreksi. Pada akhir tutorial Anda akan memiliki **contoh Aspose OCR** yang solid dan siap disisipkan ke proyek .NET mana pun.

## Prasyarat

- .NET 6.0 SDK atau yang lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework)
- Visual Studio 2022 atau IDE kompatibel C# lainnya
- File gambar (`typed_text.png`) yang berisi teks bahasa Inggris yang jelas dan diketik
- Akses internet untuk mengunduh paket NuGet Aspose.OCR

Tidak ada pustaka pihak ketiga lain yang diperlukan.

---

## Langkah 1 – Instal Paket NuGet Aspose.OCR (Load Image OCR)

Sebelum kita menulis kode apa pun, kita memerlukan pustaka yang menggerakkan mesin OCR.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, klik kanan proyek → *Manage NuGet Packages* → cari **Aspose.OCR** dan tekan *Install*.  

Menginstal paket memberi Anda akses ke `OcrEngine`, `ImageStream`, dan utilitas pemeriksaan ejaan bawaan yang akan kita gunakan nanti. Setelah paket terpasang, Anda siap untuk **memuat OCR gambar**.

## Langkah 2 – Buat Instance OCR Engine

Membuat engine adalah langkah konkret pertama dalam setiap **contoh Aspose OCR**. Anggap `OcrEngine` sebagai otak yang akan menganalisis bitmap dan menghasilkan teks.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

Konstruktor `OcrEngine` tidak memerlukan parameter apa pun, sehingga mudah dan bersih untuk prototipe cepat.

## Langkah 3 – Cara Mengaktifkan Pemeriksaan Ejaan (dan Mengapa Penting)

Output OCR mentah sering berisi kata yang salah dikenali seperti “teh” alih‑alih “the”. Mengaktifkan pemeriksa ejaan bawaan memungkinkan Aspose secara otomatis mengganti kesalahan tersebut dengan ejaan yang paling mungkin benar.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Mengapa mengaktifkan pemeriksaan ejaan?**  
> - **Akurasi:** Pemeriksaan ejaan pasca‑proses dapat meningkatkan akurasi teks keseluruhan sebesar 10‑15 % untuk dokumen tercetak.  
> - **Pengalaman pengguna:** Teks bersih berarti lebih sedikit pembersihan lanjutan ketika Anda memasukkan hasil ke indeks pencarian atau pipeline analitik.

## Langkah 4 – Cara Menambahkan Kamus (Kata‑Kata Khusus)

Kadang‑kadang kamus default tidak mengenal nama merek, kode produk, atau jargon khusus domain Anda. Di sinilah **cara menambahkan kamus** berperan.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Anda dapat memberi array, list, atau bahkan membaca dari file jika memiliki kosakata khusus yang besar. Pemeriksa ejaan kini akan memperlakukan entri tersebut sebagai sah, mencegah koreksi yang keliru.

## Langkah 5 – Muat Gambar untuk OCR (Load Image OCR)

Setelah engine dikonfigurasi, kita perlu menunjuk ke gambar yang ingin dibaca. Helper `ImageStream.FromFile` menyederhanakan detail pembacaan file.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Tip:** Jika gambar Anda berada di sub‑folder proyek, atur properti *Copy to Output Directory* menjadi *Copy always* sehingga jalur dapat diselesaikan pada runtime.

## Langkah 6 – Lakukan Pengakuan dan Perbaiki Kesalahan OCR

Dengan semua pengaturan selesai, satu panggilan ke `Recognize()` menjalankan pipeline OCR, menerapkan pemeriksaan ejaan, dan menyimpan hasil yang telah dibersihkan di `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Output yang Diharapkan

Misalkan `typed_text.png` berisi kalimat `The quick brown fox jumps over teh lazy dog`, konsol akan menampilkan:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

Perhatikan bagaimana “teh” secara otomatis dikoreksi menjadi “the”. Jika Anda menambahkan “OCRify” ke kamus khusus dan gambar berisi kata tersebut, engine akan membiarkannya tidak berubah.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste Ready)

Berikut adalah program lengkap yang dapat Anda tempel ke proyek konsol baru. Program ini mencakup semua langkah di atas, plus beberapa komentar untuk kejelasan.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

Simpan sebagai `Program.cs`, jalankan `dotnet run`, dan Anda akan melihat kalimat yang telah dikoreksi tercetak di konsol.

---

## Pertanyaan yang Sering Diajukan & Kasus Edge

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika gambar berupa PDF multi‑halaman?** | Aspose.OCR dapat menangani halaman PDF sebagai gambar. Gunakan `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` dan lakukan loop untuk setiap halaman. |
| **Bisakah saya mengubah bahasa selain Inggris?** | Tentu saja. Atur `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (atau bahasa lain yang didukung). |
| **Kamus khusus saya sangat besar—apakah akan memengaruhi performa?** | Menambahkan ribuan kata menimbulkan biaya awal yang kecil, tetapi pencarian bersifat O(1) berkat hash‑set di baliknya. Untuk kosakata yang sangat besar, pertimbangkan memuatnya sekali saat aplikasi mulai. |
| **Bagaimana jika engine OCR melempar pengecualian karena gambar rusak?** | Bungkus `Recognize()` dalam blok try‑catch dan periksa `ocrEngine.LastError`. Anda juga dapat memvalidasi dimensi gambar terlebih dahulu dengan `ocrEngine.Image.Width` dan `Height`. |
| **Apakah saya memerlukan lisensi untuk penggunaan produksi?** | Evaluasi gratis cukup untuk pengujian, tetapi lisensi komersial menghilangkan watermark evaluasi dan membuka kinerja penuh. |

---

## Kesimpulan

Anda kini memiliki **contoh lengkap Aspose OCR** yang memperlihatkan **cara mengaktifkan pemeriksaan ejaan**, **cara menambahkan kamus**, **memuat OCR gambar**, dan **cara memperbaiki kesalahan OCR** dengan cara yang bersih dan siap produksi. Dengan mengonfigurasi pemeriksa ejaan dan memberi daftar kata khusus, Anda secara dramatis meningkatkan kualitas teks yang diekstrak tanpa menulis logika pasca‑proses sendiri.

Siap untuk langkah selanjutnya? Coba ganti bahasa ke Spanyol, gunakan PDF multi‑halaman, atau integrasikan output ke indeks Azure Cognitive Search yang dapat dicari. Pola yang sama tetap berlaku—cukup ubah flag bahasa dan mungkin perluas kamus khusus.

Jika panduan ini membantu Anda, beri bintang di GitHub, bagikan kepada rekan tim, atau tinggalkan komentar di bawah. Selamat coding, dan semoga hasil OCR Anda selalu bebas kesalahan!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}