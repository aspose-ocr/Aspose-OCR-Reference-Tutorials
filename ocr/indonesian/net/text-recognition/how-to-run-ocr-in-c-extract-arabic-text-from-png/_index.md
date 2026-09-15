---
category: general
date: 2026-01-10
description: Cara menjalankan OCR dengan cepat dan mengekstrak teks Arab dari gambar.
  Pelajari cara mengonversi gambar menjadi teks, membaca teks dari PNG, dan lihat
  cara mengekstrak teks dengan Aspose OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: id
og_description: Cara menjalankan OCR di C# dan mengekstrak teks Arab dari gambar PNG.
  Panduan ini menunjukkan cara mengubah gambar menjadi teks dan membaca teks dari
  PNG langkah demi langkah.
og_title: Cara Menjalankan OCR di C# – Ekstrak Teks Arab dari PNG
tags:
- OCR
- C#
- Aspose
title: Cara Menjalankan OCR di C# – Mengekstrak Teks Arab dari PNG
url: /id/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menjalankan OCR di C# – Ekstrak Teks Arab dari PNG

Pernah bertanya-tanya **bagaimana menjalankan OCR** pada gambar yang berisi karakter Arab? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mereka perlu **mengekstrak teks Arab** dari PNG tetapi tidak tahu perpustakaan mana yang dapat menangani skrip kanan‑ke‑kiri tanpa masalah.  

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui untuk **mengonversi gambar menjadi teks**, **membaca teks dari PNG**, dan akhirnya **cara mengekstrak teks** menggunakan Aspose.OCR dalam aplikasi konsol C# yang bersih. Pada akhir tutorial Anda akan memiliki program siap‑jalankan yang mencetak string Arab langsung ke terminal Anda.

## Apa yang Akan Anda Pelajari

- Menginstal dan mereferensikan paket NuGet Aspose.OCR.  
- Mengonfigurasi mesin OCR untuk dukungan bahasa Arab.  
- Memuat gambar PNG dan menjalankan proses pengenalan.  
- Mengambil dan menampilkan teks yang diekstrak.  
- Menyesuaikan pengaturan untuk akurasi yang lebih baik dan menangani jebakan umum.

Tidak diperlukan pengalaman sebelumnya dengan OCR, cukup pemahaman dasar tentang C# dan lingkungan pengembangan .NET (Visual Studio, Rider, atau `dotnet` CLI sudah cukup).

---

## Cara Menjalankan OCR – Menyiapkan Aspose OCR

### Langkah 1: Tambahkan Paket NuGet Aspose.OCR

Hal pertama yang kita butuhkan adalah perpustakaan OCR itu sendiri. Aspose.OCR adalah produk komersial, tetapi menawarkan percobaan gratis yang berfungsi sempurna untuk tujuan pembelajaran.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Sebagai alternatif, buka **NuGet Package Manager** di Visual Studio, cari **Aspose.OCR**, dan klik **Install**.

> **Pro tip:** Jika Anda berencana menggunakan perpustakaan ini dalam pipeline CI, tambahkan flag `-v` untuk mengunci versi, misalnya, `dotnet add package Aspose.OCR -v 23.10`.

### Langkah 2: Buat Proyek Konsol Baru (jika Anda belum memilikinya)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Sekarang Anda memiliki file `Program.cs` baru yang siap untuk kode kami.

---

## Ekstrak Teks Arab – Menulis Kode OCR

Berikut adalah program lengkap yang siap‑jalankan. Simpan sebagai `Program.cs` (atau ganti file yang dihasilkan secara otomatis).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Mengapa Setiap Baris Penting

- **`OcrEngine`**: Kelas pusat yang mengkoordinasikan pemuatan gambar, pemilihan bahasa, dan pengenalan.  
- **`Language = OcrLanguage.Arabic`**: Bahasa Arab menggunakan skrip kanan‑ke‑kiri dan glyph unik; mengatur bahasa memberi tahu mesin untuk menerapkan model karakter yang tepat.  
- **`ImageStream.FromFile`**: Menangani PNG, JPEG, BMP, dan banyak format lainnya. Jika Anda perlu membaca dari `MemoryStream` (misalnya, file yang diunggah), ganti pemanggilan ini sesuai kebutuhan.  
- **`Recognize()`**: Melakukan pekerjaan berat—analisis piksel, segmentasi, dan klasifikasi karakter.  
- **`ocrEngine.Text`**: String Unicode akhir, siap untuk pemrosesan lebih lanjut, penyimpanan, atau tampilan.

### Output yang Diharapkan

Jika `arabic_sample.png` berisi frasa “مرحبا بالعالم” (Hello World), konsol akan mencetak:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Jika output terlihat berantakan, periksa kembali bahwa gambar jelas, bahasa sudah diatur ke Arab, dan versi mesin OCR cocok dengan dokumentasi.

---

## Mengonversi Gambar ke Teks – Menyesuaikan Akurasi

Meskipun pengaturan default bekerja untuk sebagian besar pemindaian bersih, gambar dunia nyata sering membutuhkan sedikit penyesuaian tambahan.

| Pengaturan | Apa yang Dilakukan | Kapan Digunakan |
|------------|--------------------|-----------------|
| `ocrEngine.Config.Preprocess = true` | Mengaktifkan binarisasi otomatis dan penghilangan noise. | Dokumen yang dipindai dengan bayangan. |
| `ocrEngine.Config.Deskew = true` | Memutar gambar untuk memperbaiki kemiringan ringan. | Foto yang diambil dengan sudut. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Menganggap seluruh gambar sebagai satu blok teks. | Keterangan sederhana atau label satu baris. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Membatasi pengenalan hanya pada karakter Arab. | Mengurangi hasil positif palsu pada halaman berbahasa campuran. |

Anda dapat menambahkan baris-baris ini tepat setelah membuat mesin:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Membaca Teks dari PNG – Menangani Berbagai Sumber Gambar

Kadang PNG berada di dalam basis data atau datang dari permintaan web. Berikut varian cepat yang membaca dari `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

Sisa alur tetap identik, yang berarti **cara mengekstrak teks** tetap konsisten terlepas dari sumbernya.

---

## Cara Mengekstrak Teks – Opsi Lanjutan & Kasus Tepi

### 1. PDF atau TIFF Multi‑Halaman

Jika Anda perlu melakukan OCR pada dokumen multi‑halaman, lakukan loop pada setiap halaman:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Catatan:** Anda akan membutuhkan paket `Aspose.PDF` untuk potongan kode ini.

### 2. Mendeteksi Bahasa Secara Otomatis

Aspose.OCR juga menawarkan deteksi otomatis, tetapi lebih lambat. Jika Anda tidak yakin apakah gambar berisi bahasa Arab atau skrip lain, aktifkan fitur ini:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

### 3. Tips Kinerja

- **Gunakan kembali objek `OcrEngine`** untuk beberapa gambar; membuat instance baru setiap kali menambah beban.  
- **Jalankan secara paralel** hanya jika Anda memiliki instance mesin terpisah per thread—berbagi satu instance menyebabkan kondisi balapan.

---

## Kesimpulan

Kami telah membahas **cara menjalankan OCR** di C# dari awal hingga akhir, menunjukkan cara **mengekstrak teks Arab**, **mengonversi gambar ke teks**, **membaca teks dari PNG**, dan menjawab **cara mengekstrak teks** dalam berbagai skenario. Kode contoh lengkap, mandiri, dan siap Anda tempel ke proyek konsol .NET mana pun.

Langkah selanjutnya? Coba ganti `OcrLanguage.Arabic` dengan bahasa Korea atau Cyrillic Serbia untuk melihat kemampuan multibahasa perpustakaan. Bereksperimenlah dengan flag preprocessing untuk meningkatkan akurasi pada pemindaian berisik, atau integrasikan rutin OCR ke dalam API web sehingga pengguna dapat mengunggah gambar dan mendapatkan hasil teks secara instan.

Selamat coding, semoga hasil OCR Anda selalu jernih seperti kristal!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}