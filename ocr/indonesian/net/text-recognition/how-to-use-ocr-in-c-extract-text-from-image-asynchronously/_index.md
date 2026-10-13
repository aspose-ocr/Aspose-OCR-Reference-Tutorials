---
category: general
date: 2026-02-25
description: Cara menggunakan OCR dengan cepat di C# untuk mengekstrak teks dari gambar,
  memuat gambar untuk OCR, dan mengatur bahasa OCR dengan Aspose OCR. Panduan langkah
  demi langkah.
draft: false
keywords:
- how to use OCR
- extract text from image
- load image for OCR
- set OCR language
language: id
og_description: Pelajari cara menggunakan OCR di C# untuk mengekstrak teks dari gambar,
  memuat gambar untuk OCR, dan mengatur bahasa OCR menggunakan Aspose OCR. Contoh
  lengkap async.
og_title: Cara Menggunakan OCR di C# – Panduan Async Lengkap
tags:
- C#
- Aspose OCR
- async programming
title: Cara Menggunakan OCR di C# – Mengekstrak Teks dari Gambar Secara Asinkron
url: /id/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Ekstrak Teks dari Gambar Secara Asinkron

Pernahkah Anda perlu **how to use OCR** pada sebuah kwitansi, faktur, atau formulir yang dipindai dan bertanya-tanya mengapa contoh kode yang Anda temukan entah tidak lengkap atau terjebak di dunia sinkron? Anda bukan satu-satunya. Dalam banyak aplikasi dunia nyata Anda ingin **extract text from image** tanpa membekukan UI, dan Anda juga menginginkan fleksibilitas untuk memilih bahasa yang tepat untuk pengenalan.  

Dalam tutorial ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan secara tepat cara **load image for OCR**, mengonfigurasi opsi **set OCR language**, dan menjalankan pengenalan secara asinkron. Pada akhir Anda akan memiliki aplikasi konsol mandiri yang mencetak teks yang dikenali ke konsol, plus beberapa tips untuk menangani kasus tepi dan menskalakan solusi.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework)  
- Paket NuGet Aspose.OCR (`Aspose.OCR`) terpasang  
- File gambar contoh (misalnya `receipt.jpg`) ditempatkan di folder yang dapat Anda referensikan  
- Pengetahuan dasar C# – Anda tidak memerlukan trik async lanjutan, cukup dasar-dasarnya  

Jika Anda belum memiliki salah satu dari itu, dapatkan paket NuGet dengan `dotnet add package Aspose.OCR` dan buat folder sederhana untuk gambar uji Anda. Tidak perlu yang rumit.

---

## Cara Menggunakan OCR: Implementasi Langkah‑per‑Langkah

Di bawah ini kami membagi proses menjadi empat langkah logis. Setiap langkah memiliki header H2 sendiri, dan header pertama mengulang kata kunci utama untuk memenuhi SEO.

### Langkah 1 – Inisialisasi Mesin OCR (How to Use OCR)

Hal pertama yang Anda butuhkan adalah sebuah instance `OcrEngine`. Anggaplah ini sebagai otak di balik operasi; ia menyimpan konfigurasi, gambar, dan hasil.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task RunAsync()
    {
        // Create the OCR engine – this object will manage everything.
        var ocrEngine = new OcrEngine();

        // Next steps will configure it further.
```

**Why this matters:**  
Membuat engine sekali dan menggunakannya kembali dapat meningkatkan kinerja saat Anda memproses banyak gambar. Ini juga memberi Anda satu tempat untuk mengatur opsi global seperti bahasa.

### Langkah 2 – Atur Bahasa OCR (Set OCR Language Properly)

Jika Anda melewatkan pemilihan bahasa, Aspose OCR secara default menggunakan Bahasa Inggris, yang mungkin cukup untuk kwitansi tetapi tidak untuk dokumen asing. Mengatur bahasa hanya memerlukan satu baris:

```csharp
        // Set the recognition language to English.
        // You can change OcrLanguage.French, OcrLanguage.Spanish, etc.
        ocrEngine.Config.Language = OcrLanguage.English;
```

**Pro tip:**  
Ketika Anda memerlukan dukungan multibahasa, Anda dapat melewatkan array bahasa (`OcrLanguage.English | OcrLanguage.French`). Engine akan mencoba masing‑masing dalam urutan, yang berguna untuk kwitansi dengan bahasa campuran.

### Langkah 3 – Muat Gambar untuk OCR (Load Image for OCR Efficiently)

Sekarang kami mengarahkan engine ke file yang ingin dibaca. Aspose menyediakan `ImageStream.FromFile`, yang mengabstraksi penanganan stream di bawahnya.

```csharp
        // Load the image you want to analyze.
        // Replace the path with the actual location of your image file.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

**Edge case:**  
Jika path file salah atau format gambar tidak didukung, `FromFile` akan melempar exception. Bungkus ini dalam try/catch jika Anda membangun UI yang kuat.

### Langkah 4 – Lakukan Pengenalan Asinkron (Extract Text from Image)

Di sinilah keajaiban terjadi. Metode `RecognizeAsync` menjalankan OCR pada thread latar belakang, membebaskan thread pemanggil—sempurna untuk UI atau aplikasi web.

```csharp
        // Run OCR asynchronously.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Display the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**What you’ll see:**  
Jika `receipt.jpg` berisi teks “Total: $12.34”, output konsol akan menjadi:

```
OCR completed:
Total: $12.34
```

**Why async?**  
OCR sinkron dapat memblokir thread selama beberapa detik, terutama pada gambar beresolusi tinggi. Menggunakan `await` membuat aplikasi Anda tetap responsif dan berintegrasi baik dengan pipeline permintaan ASP.NET Core.

---

## Contoh Kerja Penuh

Salin seluruh potongan di bawah ini ke dalam proyek konsol baru (`dotnet new console`) dan jalankan. Ingat untuk mengganti `YOUR_DIRECTORY/receipt.jpg` dengan path sebenarnya ke gambar Anda.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task Main(string[] args)
    {
        await RunAsync();
    }

    public static async Task RunAsync()
    {
        // Step 1: Create the OCR engine.
        var ocrEngine = new OcrEngine();

        // Step 2: Set the OCR language (English by default).
        ocrEngine.Config.Language = OcrLanguage.English;

        // Step 3: Load the image you want to process.
        // Ensure the file exists; otherwise an exception is thrown.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // Step 4: Perform asynchronous OCR recognition.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Output the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Expected output** (asumsi gambar berisi teks Bahasa Inggris yang dapat dibaca):

```
OCR completed:
Your extracted text appears here, line by line.
```

Jika Anda melihat string kosong, periksa kembali bahwa gambar jelas dan pengaturan bahasa cocok dengan teks.

---

## Kesalahan Umum dan Cara Menghindarinya

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blank result** | Gambar beresolusi rendah atau bahasa yang salah | Gunakan pemindaian dengan resolusi lebih tinggi, atau atur `ocrEngine.Config.Language` ke bahasa yang tepat |
| **Exception on `FromFile`** | Path salah atau format tidak didukung | Verifikasi path, gunakan path absolut, atau konversi gambar ke PNG/JPEG terlebih dahulu |
| **Performance lag** | Batch besar diproses secara sinkron | Proses gambar secara paralel menggunakan `Task.WhenAll` dan gunakan kembali satu instance `OcrEngine` |
| **Memory leak** | Tidak membuang (dispose) stream pada kode pemuatan khusus | Gunakan `ImageStream.FromFile` yang menangani disposal, atau gunakan blok `using` jika Anda memuat secara manual |

**Bonus tip:**  
Jika Anda perlu mengekstrak data terstruktur (mis., pasangan kunci‑nilai dari kwitansi), pertimbangkan memproses `ocrResult.Text` dengan ekspresi reguler atau pustaka NLP ringan.

---

## Memperluas Solusi

Sekarang Anda sudah tahu **how to use OCR** untuk satu gambar, Anda mungkin bertanya, “Bagaimana jika saya memiliki puluhan kwitansi setiap malam?”  

- **Batch processing:** Bungkus logika `RunAsync` dalam loop dan kumpulkan hasilnya dalam sebuah list.  
- **Parallelism:** Gunakan `Parallel.ForEach` dengan dukungan async (`Parallel.ForEachAsync` di .NET 6) untuk menjalankan beberapa pengenalan secara bersamaan.  
- **Persisting results:** Simpan `ocrResult.Text` ke dalam basis data, atau tulis ke CSV untuk analitik downstream.  

Semua ekstensi ini tetap bergantung pada langkah inti yang telah kami bahas: menginisialisasi engine, mengatur bahasa, memuat gambar, dan memanggil `RecognizeAsync`.

---

## Ringkasan Visual

![contoh cara menggunakan OCR](/images/ocr-example.png "cara menggunakan OCR di C# dengan Aspose OCR")

*Diagram di atas menggambarkan alur dari memuat gambar hingga menerima teks yang dikenali.*

---

## Kesimpulan

Kami baru saja menelusuri contoh lengkap yang siap produksi yang menunjukkan **how to use OCR** di C# untuk **extract text from image**, **load image for OCR**, dan **set OCR language** dengan benar—semua sambil menjaga UI tetap responsif dengan panggilan asinkron.  

Dalam satu skrip mandiri Anda kini memiliki semua yang diperlukan untuk mulai menarik teks dari foto, kwitansi, atau dokumen yang dipindai. Dari sini Anda dapat menskalakan ke batch, menambahkan penanganan error, atau mengintegrasikan hasil ke alur kerja yang lebih besar.

Siap untuk langkah selanjutnya? Coba ganti `OcrLanguage.English` dengan bahasa lain, bereksperimen dengan format gambar yang berbeda, atau hubungkan output ke basis data sederhana. Kemungkinannya seluas dokumen yang perlu Anda baca.

Ada pertanyaan atau mengalami kendala? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}