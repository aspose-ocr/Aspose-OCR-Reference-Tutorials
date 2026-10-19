---
category: general
date: 2026-03-18
description: Buat PDF yang dapat dicari menggunakan Aspose OCR di C#. Konversi gambar
  ke PDF, tambahkan lapisan teks OCR, dan tulis byte PDF ke file dalam beberapa langkah
  mudah.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: id
og_description: Buat PDF yang dapat dicari dengan cepat menggunakan Aspose OCR di
  C#. Pelajari cara mengonversi gambar ke PDF, menambahkan lapisan teks OCR, dan menulis
  byte PDF ke file.
og_title: Buat PDF yang Dapat Dicari dari Gambar – Panduan OCR C# Cepat
tags:
- OCR
- PDF
- C#
- Aspose
title: Buat PDF yang Dapat Dicari dari Gambar dengan OCR – Panduan C#
url: /id/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang dapat dicari dari Gambar dengan OCR – Panduan C#

Pernah perlu **membuat PDF yang dapat dicari** dari gambar yang dipindai? Dengan Aspose OCR Anda dapat melakukannya dalam beberapa baris kode, tanpa memerlukan perpustakaan berat. Dalam tutorial ini kami akan **mengonversi gambar ke PDF**, menambahkan **lapisan teks OCR** di atasnya, dan akhirnya **menulis byte PDF ke file** sehingga Anda mendapatkan dokumen PDF/A‑2b yang sesuai standar dan dapat dicari oleh pengguna Anda.

Jika Anda bertanya-tanya mengapa harus repot membuat PDF yang dapat dicari alih-alih file gambar biasa, pikirkan pengalaman pengguna: PDF yang dapat dicari memungkinkan orang menyalin, memilih, dan mengindeks teks—sangat berguna untuk arsip, dokumen hukum, atau alur kerja apa pun yang memerlukan ekstraksi teks di kemudian hari. Mari kita mulai.

## Apa yang Anda Butuhkan

- .NET 6 atau lebih baru (kode ini juga bekerja pada .NET Framework 4.7+)
- Paket NuGet Aspose.OCR (`Aspose.OCR` versi 23.10 atau lebih baru)
- Gambar raster (`.png`, `.jpg`, dll.) yang ingin Anda ubah menjadi PDF yang dapat dicari
- Pengetahuan C# yang cukup—tidak perlu hal rumit, hanya dasar-dasarnya

Itu saja. Tidak ada alat eksternal, tidak ada konverter tambahan. Semua pekerjaan berat ditangani oleh mesin Aspose OCR.

## Buat PDF yang Dapat Dicari – Ikhtisar

Sebelum kita menyelam ke kode, mari kita rangkum prosesnya:

1. **Instantiate** mesin OCR – objek ini mengetahui cara membaca teks dari gambar.  
2. **Load** gambar sumber – kami akan memberi `ImageStream` ke mesin.  
3. **Configure** opsi penyimpanan PDF/A‑2b – ini memberi tahu Aspose untuk menyematkan teks yang dikenali sebagai lapisan tersembunyi.  
4. **Run** OCR dan **capture** byte PDF yang dihasilkan.  
5. **Write** byte tersebut ke disk, menghasilkan file PDF yang dapat dicari akhir.

Setiap langkah tersebut langsung berkorespondensi dengan satu atau dua baris C#, sehingga seluruh alur kerja terasa seperti skrip kecil bukan proyek besar.

## Langkah 1: Mengonversi Gambar ke PDF – Memuat Gambar

Pertama-tama: kita perlu memberi mesin OCR sesuatu untuk dibaca. Pembantu `ImageStream.FromFile` memuat file ke dalam stream yang dapat diproses oleh Aspose.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **Pro tip:** Jaga resolusi gambar Anda setidaknya 300 dpi atau lebih; akurasi OCR turun drastis pada pemindaian beresolusi rendah.

## Langkah 2: Mengenali Teks dari Gambar dan Menambahkan Lapisan Teks OCR

Sekarang kami membuat mesin OCR dan memberitahukannya untuk mengenali teks. Keajaiban terjadi ketika kami menggabungkan hasil pengenalan dengan `PdfSaveOptions` yang memiliki `IncludeTextLayer = true`. Bendera itu memaksa Aspose menyematkan karakter yang diekstrak sebagai lapisan teks tak terlihat, yang membuat PDF dapat dicari.

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

Mengapa PDF/A‑2b? Itu adalah format arsip standar ISO yang menjamin preservasi jangka panjang dan, yang penting bagi kami, memaksa PDF berisi lapisan teks yang dapat dicari. Jika Anda tidak memerlukan kepatuhan arsip, Anda dapat menghilangkan `PdfCompliance` sepenuhnya, tetapi mempertahankannya tidak menambah biaya apa pun.

## Langkah 3: Menulis Byte PDF ke File – Menyimpan Hasil

Dengan mesin siap dan opsi sudah diatur, kami menjalankan pengenalan dan segera meminta Aspose memberikan PDF sebagai `byte[]`. Kemudian kami menuliskan byte tersebut ke disk menggunakan `File.WriteAllBytes`. Sederhana, namun kuat.

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

Baris `Console.WriteLine` itu opsional, tetapi memberi Anda umpan balik instan saat menjalankan program dari terminal.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan. Salin‑tempel ke proyek konsol baru, ganti `YOUR_DIRECTORY` dengan jalur yang sebenarnya, dan tekan **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### Output yang Diharapkan

- File bernama `output.pdf` muncul di folder yang Anda tentukan.  
- Buka di Adobe Acrobat Reader atau penampil PDF apa pun dan coba pilih teks—jika Anda dapat menyalin kata, Anda telah berhasil **membuat PDF yang dapat dicari**.  
- Dokumen juga akan lulus alat validasi PDF/A‑2b karena kami menggunakan flag kepatuhan yang tepat.

## Pertanyaan Umum & Kasus Tepi

**Bagaimana jika gambar saya berisi beberapa halaman?**  
Bungkus setiap halaman dalam `ImageStream` masing‑masing dan beri mereka secara berurutan ke `OcrEngine`. Aspose secara otomatis akan menggabungkan halaman‑halaman tersebut menjadi satu PDF.

**Bisakah saya mengubah bahasa OCR?**  
Tentu saja. Set `ocrEngine.Language = Language.English;` (atau bahasa lain yang didukung) sebelum memanggil `Recognize`.

**Bagaimana dengan penggunaan memori untuk file besar?**  
Jika Anda memproses pemindaian berskala gigabyte, pertimbangkan untuk menstream hasil langsung ke `FileStream` alih‑alih menyimpan seluruh `byte[]` di memori:

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**Apakah saya memerlukan lisensi?**  
Aspose menawarkan percobaan gratis tanpa watermark. Untuk penggunaan produksi, beli lisensi untuk menghapus banner evaluasi dan membuka semua fitur.

## Tips untuk Akurasi OCR yang Lebih Baik

- **Pre‑process** gambar: perbaiki kemiringan, hilangkan bintik, dan tingkatkan kontras.  
- **Gunakan format lossless** seperti PNG; artefak kompresi JPEG dapat membingungkan mesin.  
- **Hindari latar belakang berwarna**; latar belakang putih polos memberikan hasil terbaik.

## Langkah Selanjutnya

Sekarang Anda dapat **membuat PDF yang dapat dicari**, Anda mungkin ingin:

- **Proses batch** folder gambar menggunakan `Directory.GetFiles`.  
- **Ekstrak teks tersembunyi** nanti dengan API `PdfDocument` untuk pengindeksan.  
- **Gabungkan OCR dengan tanda tangan digital** untuk membuat arsip yang tahan manipulasi.  

Semua ini dibangun di atas pola inti yang sama yang kami bahas: muat, kenali, konfigurasikan, simpan.

---

*Siap mengubah arsip yang dipindai menjadi PDF yang dapat dicari? Ambil kode, arahkan ke gambar Anda, dan biarkan Aspose melakukan pekerjaan berat. Selamat coding!*

![Contoh PDF yang dapat dicari](/images/create-searchable-pdf.png "Ilustrasi PDF yang dapat dicari yang dihasilkan dari sebuah gambar")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}