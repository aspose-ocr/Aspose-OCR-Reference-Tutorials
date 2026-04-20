---
category: general
date: 2026-02-16
description: Buat PDF yang dapat dicari dari gambar TIFF menggunakan Aspose OCR. Pelajari
  cara mengonversi TIFF ke PDF, melakukan OCR gambar ke PDF, dan mengenali teks dari
  gambar dalam C#.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- ocr image to pdf
- recognize text from image
- convert scanned image pdf
language: id
og_description: Buat PDF yang dapat dicari dengan cepat. Tutorial ini menunjukkan
  cara mengonversi TIFF ke PDF, melakukan OCR pada gambar ke PDF, dan mengenali teks
  dari gambar dengan Aspose OCR.
og_title: Buat PDF yang Dapat Dicari dari TIFF – Panduan OCR Aspose
tags:
- Aspose OCR
- C#
- PDF/A
- Document Processing
title: Buat PDF yang Dapat Dicari dari TIFF – Panduan Langkah-demi-Langkah Aspose
  OCR
url: /id/net/text-recognition/create-searchable-pdf-from-tiff-aspose-ocr-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari TIFF – Panduan Langkah‑per‑Langkah Aspose OCR

Pernahkah Anda perlu **membuat PDF yang dapat dicari** dari TIFF yang dipindai tetapi tidak yakin perpustakaan mana yang dapat menangani pekerjaan berat? Anda tidak sendirian. Dalam banyak proyek otomasi kantor, kami berakhir dengan tumpukan file TIFF yang terlihat seperti gambar, bukan teks. Kabar baiknya? Dengan Aspose OCR Anda dapat **mengonversi tiff ke pdf**, menjalankan OCR pada gambar, dan menghasilkan PDF/A‑2b yang sepenuhnya dapat dicari.

Dalam tutorial ini kami akan menelusuri contoh C# lengkap yang dapat dijalankan, yang menunjukkan secara tepat cara **membuat PDF yang dapat dicari**, mengapa setiap langkah penting, dan jebakan apa yang harus diwaspadai. Pada akhir tutorial Anda akan dapat **mengenali teks dari gambar** file, **OCR gambar ke pdf**, dan bahkan **mengonversi pdf gambar yang dipindai** yang memenuhi standar arsip.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mereferensikan paket NuGet Aspose OCR.  
- Kode tepat yang diperlukan untuk **membuat PDF yang dapat dicari** dari file TIFF.  
- Mengapa memuat model bahasa yang tepat sangat penting untuk OCR yang akurat.  
- Tips menangani pemindaian besar, TIFF multi‑halaman, dan kepatuhan PDF/A.  
- Di mana menemukan file hasil dan cara memverifikasi bahwa teks dapat dicari.

### Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| .NET 6.0 atau lebih baru (runtime .NET terbaru apa pun) | Aspose OCR menyediakan binary untuk .NET Standard 2.0+, yang dapat dijalankan di mana saja mulai dari .NET Core hingga .NET Framework. |
| Visual Studio 2022 (atau VS Code dengan ekstensi C#) | Memberikan IntelliSense dan manajemen NuGet yang mudah. |
| Lisensi Aspose OCR yang aktif (atau kunci evaluasi gratis) | Versi percobaan gratis membatasi jumlah halaman; lisensi menghilangkan watermark dan mengaktifkan output PDF/A‑2b. |
| File TIFF yang ingin Anda proses (misalnya `input.tif`) | Ini adalah gambar sumber yang akan kami ubah menjadi **PDF yang dapat dicari**. |

> **Pro tip:** Jika Anda bekerja dengan TIFF multi‑halaman, Aspose OCR akan memperlakukan setiap halaman sebagai gambar terpisah secara otomatis—tidak perlu kode tambahan.

---

## Langkah 1: Instal Paket NuGet Aspose OCR

Pertama, tambahkan perpustakaan ke proyek Anda. Buka **Package Manager Console** dan jalankan:

```powershell
Install-Package Aspose.OCR
```

Atau, jika Anda lebih suka antarmuka grafis, cari “Aspose.OCR” di **NuGet Package Manager** dan klik **Install**. Ini akan mengunduh semua DLL yang diperlukan, termasuk model bahasa yang akan kita gunakan nanti.

> **Mengapa langkah ini?** Tanpa paket, kelas `OcrEngine` tidak ada, dan Anda akan mendapatkan error pada waktu kompilasi. Pendekatan NuGet memastikan Anda memiliki versi yang tepat (saat ini 23.12) dan secara otomatis mengunduh semua dependensi transitif.

---

## Langkah 2: Inisialisasi OCR Engine

Membuat instance engine adalah baris kode pertama yang sebenarnya Anda tulis. Anggap `OcrEngine` sebagai otak yang melakukan semua pekerjaan berat.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine – this object will manage the entire pipeline
OcrEngine ocrEngine = new OcrEngine();
```

> **Apa yang terjadi?** Konstruktor menyiapkan buffer internal dan mempersiapkan engine untuk memuat model bahasa. Jika Anda melewatkan langkah ini, pemanggilan selanjutnya seperti `LoadLanguage` akan melempar `NullReferenceException`.

---

## Langkah 3: Muat Model Bahasa Inggris (atau bahasa lain)

Akurasi OCR bergantung pada model bahasa yang Anda muat. Untuk kebanyakan dokumen Barat, bahasa Inggris sudah cukup, tetapi Aspose mendukung puluhan bahasa.

```csharp
// Load English language data – essential for recognizing Latin characters
ocrEngine.LoadLanguage(LanguageModel.English);
```

> **Mengapa memuat model?** Engine membutuhkan representasi statistik bentuk karakter. Tanpa model, Anda akan mendapatkan hasil yang tidak dapat dibaca atau kosong. Jika Anda perlu **mengenali teks dari gambar** dalam bahasa Prancis, ganti `LanguageModel.English` dengan `LanguageModel.French`.

---

## Langkah 4: Berikan Gambar TIFF dan Hasilkan PDF/A‑2b

Sekarang kami menunjuk engine ke file sumber kami. Helper `ImageStream.FromFile` membaca TIFF (single‑ atau multi‑page) ke memori.

```csharp
// Step 4: Assign the TIFF image to the engine
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

// Run OCR and produce a PDF/A‑2b document – this is the searchable PDF we want
PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);
```

> **Apa yang dilakukan?** `RecognizePdfA` melakukan tiga aksi di balik layar:  
> 1️⃣ Menjalankan OCR pada setiap halaman TIFF.  
> 2️⃣ Menyisipkan teks yang dikenali sebagai lapisan tak terlihat.  
> 3️⃣ Membungkus semuanya dalam kontainer PDF/A‑2b, yang merupakan standar ISO untuk preservasi jangka panjang.  

Jika Anda hanya membutuhkan PDF biasa (tanpa kepatuhan arsip), Anda dapat memanggil `ocrEngine.RecognizePdf()` sebagai gantinya. Namun untuk kebanyakan skenario perusahaan, PDF/A‑2b adalah pilihan paling aman.

---

## Langkah 5: Simpan PDF yang Dapat Dicari ke Disk

Akhirnya, tulis hasilnya ke file. Metode `Save` menerima path dan menangani semua I/O.

```csharp
// Save the generated searchable PDF to your output folder
searchablePdf.Save("YOUR_DIRECTORY/output.pdf");
```

Saat Anda membuka `output.pdf` di Adobe Reader, Anda harus dapat mengetik kata di kotak pencarian dan langsung menemukan hasilnya—meskipun file asli hanyalah gambar. Itulah keajaiban alur kerja **membuat PDF yang dapat dicari**.

---

## Mengonversi TIFF ke PDF – Ringkasan Cepat

Berikut adalah program lengkap yang siap dijalankan dan mengikat semua langkah bersama. Silakan salin‑tempel ke aplikasi console dan tekan **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the desired language model (English in this case)
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 3️⃣ Point the engine at the TIFF you want to convert
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

        // 4️⃣ Recognize the image and produce a PDF/A‑2b (searchable PDF)
        PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);

        // 5️⃣ Persist the result to disk
        searchablePdf.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("✅ Searchable PDF created successfully!");
    }
}
```

**Hasil yang diharapkan:** `output.pdf` muncul di `YOUR_DIRECTORY`. Buka, pilih alat teks, dan Anda akan melihat teks yang dapat dipilih serta dicari di atas gambar raster asli.

---

## OCR Gambar ke PDF – Menangani Kasus Khusus

### TIFF Multi‑Halaman

Jika file sumber Anda berisi lebih dari satu halaman, Aspose OCR secara otomatis memproses setiap halaman dan menambahkan halaman yang sesuai di PDF. Tidak diperlukan loop tambahan.

### File Besar & Manajemen Memori

Untuk pemindaian berukuran gigabyte, pertimbangkan mengaktifkan **mode streaming**:

```csharp
ocrEngine.Image = ImageStream.FromFile("large.tif", useMemoryCache: false);
```

Ini memberi tahu engine untuk membaca potongan dari disk alih‑alih memuat seluruh gambar ke RAM—ideal untuk pekerjaan batch sisi server.

### Format Output Berbeda

Kadang‑kadang Anda tidak memerlukan PDF/A‑2b melainkan PDF biasa. Ganti pemanggilan menjadi:

```csharp
PdfResult plainPdf = ocrEngine.RecognizePdf();
plainPdf.Save("plain.pdf");
```

Atau, jika Anda hanya menginginkan teks mentah (tanpa PDF), gunakan:

```csharp
string extractedText = ocrEngine.RecognizeText();
System.IO.File.WriteAllText("text.txt", extractedText);
```

Variasi ini menangani skenario **mengonversi pdf gambar yang dipindai** di mana sistem hilir hanya menerima PDF biasa.

---

## Pro Tips untuk OCR yang Handal

- **DPI penting:** Pemindaian pada 300 DPI atau lebih tinggi memberikan tingkat pengenalan terbaik. Di bawah 200 DPI Anda akan melihat penurunan akurasi.  
- **Pra‑pemrosesan:** Jika TIFF berisik, jalankan melalui `ocrEngine.Image = ImageProcessor.Deskew(...).Apply(ocrEngine.Image);` sebelum pengenalan.  
- **Lisensi:** Ingat untuk menetapkan lisensi di awal aplikasi (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`). Tanpa lisensi output akan berisi watermark “Evaluation”.  
- **Pemrosesan batch:** Bungkus logika inti dalam loop `foreach` pada direktori berisi TIFF untuk **mengonversi tiff ke pdf** secara massal.

---

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja di Linux?**  
J: Tentu saja. Aspose OCR menargetkan .NET Standard, sehingga Anda dapat menjalankan binary yang sama di Windows, Linux, atau macOS dengan runtime .NET 6.

**T: Bagaimana jika saya perlu mengenali bahasa selain Inggris?**  
J: Cukup ganti `LanguageModel.English` dengan enum yang sesuai, misalnya `LanguageModel.Spanish`. Anda juga dapat memuat beberapa bahasa secara bersamaan untuk dokumen campuran.

**T: Bisakah saya menyematkan font khusus di PDF/A?**  
J: Ya. Gunakan `ocrEngine.Options.PdfOptions.Font = PdfFont.CreateFont("path/to/font.ttf");` sebelum memanggil `RecognizePdfA`.

---

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **membuat PDF yang dapat dicari** dari gambar TIFF menggunakan Aspose OCR. Mulai dari menginstal paket NuGet, memuat model bahasa yang tepat, hingga menghasilkan PDF/A‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}