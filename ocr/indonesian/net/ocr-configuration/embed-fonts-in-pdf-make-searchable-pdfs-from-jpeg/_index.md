---
category: general
date: 2026-03-05
description: Menyematkan font dalam PDF saat mengonversi JPEG menjadi PDF yang dapat
  dicari menggunakan Aspose OCR. Pelajari cara mengenali teks dari JPEG dan menyematkan
  font untuk kepatuhan PDF/A‑2b.
draft: false
keywords:
- embed fonts in pdf
- recognize text from jpeg
- how to create searchable pdf
- convert image to searchable pdf
- perform ocr on image
language: id
og_description: Sematkan font dalam PDF sambil mengubah JPEG menjadi PDF yang dapat
  dicari. Panduan langkah demi langkah ini menunjukkan cara mengenali teks dari JPEG
  dan membuat file yang sesuai dengan standar PDF/A‑2b.
og_title: Sematkan Font dalam PDF – Buat PDF yang Dapat Dicari dari JPEG
tags:
- Aspose OCR
- PDF generation
- C#
- .NET
title: Sematkan Font dalam PDF – Buat PDF yang Dapat Dicari dari JPEG
url: /id/net/ocr-configuration/embed-fonts-in-pdf-make-searchable-pdfs-from-jpeg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyematkan Font dalam PDF – Membuat PDF yang Dapat Dicari dari JPEG

Pernahkah Anda perlu **menyematkan font dalam PDF** yang dihasilkan dari gambar yang dipindai? Anda bukan satu-satunya. Kebanyakan pengembang mengalami masalah di mana PDF yang dihasilkan terlihat baik di mesin mereka tetapi menampilkan teks yang hilang saat dibuka di tempat lain karena font tidak disematkan.  

Kabar baik? Dengan Aspose OCR Anda dapat **mengenali teks dari JPEG**, menyematkan font yang diperlukan, dan menghasilkan dokumen PDF/A‑2b yang sepenuhnya dapat dicari hanya dengan beberapa baris C#. Dalam tutorial ini kami akan membahas setiap langkah—mengapa setiap pengaturan penting, cara menghindari jebakan umum, dan seperti apa PDF akhir seharusnya.

Pada akhir panduan ini Anda akan dapat **mengonversi gambar menjadi PDF yang dapat dicari**, menyematkan font dengan benar, dan memahami cara **melakukan OCR pada file gambar** secara programatik.

---

## Apa yang Anda Butuhkan

- **Aspose.OCR for .NET** (versi terbaru, misalnya 23.10) – perpustakaan yang melakukan pekerjaan berat.
- File lisensi **Aspose OCR** yang valid (`Aspose.OCR.lic`). Versi percobaan gratis berfungsi, tetapi versi berlisensi menghapus watermark evaluasi.
- Gambar JPEG (`input.jpg`) yang berisi teks cetak atau ketik.
- Lingkungan pengembangan .NET (Visual Studio, Rider, atau VS Code dengan ekstensi C#).

Tidak diperlukan paket NuGet tambahan; mesin OCR sudah menyertakan utilitas pembuatan PDF.

## Langkah 1: Siapkan Mesin OCR dan Terapkan Lisensi *(Menyematkan Font dalam PDF)*

Sebelum Anda dapat menjalankan pengenalan apa pun, Anda harus membuat instance `OcrEngine` dan memberi tahu mesin lisensi mana yang akan digunakan. Melewatkan langkah lisensi akan menyebabkan mesin berjalan dalam mode evaluasi, yang menambahkan overlay “Powered by Aspose” pada setiap halaman.

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Apply your license – replace the path with the actual location of your .lic file
ocrEngine.SetLicense("Aspose.OCR.lic");
```

**Mengapa ini penting:** Lisensi tidak hanya menghapus watermark tetapi juga membuka opsi kepatuhan PDF/A yang akan kita perlukan nanti untuk menyematkan font.

## Langkah 2: Muat Gambar JPEG yang Ingin Anda Proses *(Mengenali Teks dari JPEG)*

Mesin OCR bekerja dengan properti `Image` yang menerima `ImageStream`. Arahkan ke JPEG yang ingin Anda konversi.

```csharp
// Load the source JPEG image
ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");
```

**Tip:** Jika gambar Anda berada dalam stream (misalnya, diunggah melalui API), Anda dapat menggunakan `ImageStream.FromStream(yourStream)` alih-alih `FromFile`.

## Langkah 3: Konfigurasikan Opsi Penyimpanan PDF untuk PDF yang Dapat Dicari

Ini adalah inti dari kebutuhan “menyematkan font dalam PDF”. Kami akan menggunakan `PdfSaveOptions` untuk:

1. Menargetkan **PDF/A‑2b** (standar arsip yang diterima secara luas).
2. **Menyematkan semua font yang digunakan** sehingga PDF ditampilkan sama di mana saja.
3. Menerapkan **kompresi Flate lossless** untuk menjaga ukuran file tetap wajar.
4. Menjaga JPEG asli sebagai lapisan latar belakang, yang mempertahankan kesetiaan visual.

```csharp
// Set up PDF export options
var pdfSaveOptions = new PdfSaveOptions
{
    // Produce a PDF/A‑2b compliant document
    PdfAStandard = PdfAStandard.PdfA2b,

    // Ensure every font used by the OCR text is embedded
    EmbedFonts = true,

    // Use lossless compression for the text and graphics streams
    Compression = PdfCompression.Flate,

    // Keep the original image behind the OCR layer (makes the PDF searchable)
    RenderOriginalImage = true
};
```

**Mengapa pengaturan ini?**  
- **PdfAStandard.PdfA2b** menjamin preservasi jangka panjang dan memaksa penyematan font.  
- **EmbedFonts = true** adalah flag eksplisit yang memenuhi tujuan kata kunci utama.  
- **Compression.Flate** mengurangi ukuran tanpa mengorbankan kualitas.  
- **RenderOriginalImage** mempertahankan tampilan visual halaman yang dipindai sementara lapisan OCR tersembunyi menyediakan teks yang dapat dicari.

## Langkah 4: Jalankan Pengenalan OCR pada Gambar *(Melakukan OCR pada Gambar)*

Dengan semua persiapan selesai, jalankan pengenalan. Mesin akan menganalisis JPEG, mengekstrak karakter, dan secara internal membuat lapisan teks.

```csharp
// Execute OCR – this populates the internal text layer
ocrEngine.Recognize();
```

**Pertanyaan umum:** *Apakah saya perlu menentukan bahasa atau kamus?*  
Jika dokumen Anda bukan bahasa Inggris, atur `ocrEngine.Language = OcrLanguage.French;` (atau bahasa lain yang didukung) sebelum memanggil `Recognize()`. Defaultnya adalah bahasa Inggris.

## Langkah 5: Simpan Output sebagai PDF yang Dapat Dicari dengan Font yang Disematkan

Akhirnya, tulis hasilnya ke disk. Metode `Save` menerima jalur target dan `PdfSaveOptions` yang telah kita definisikan sebelumnya.

```csharp
// Save the searchable PDF with embedded fonts
ocrEngine.Save(@"C:\MyImages\output.pdf", pdfSaveOptions);
```

When Anda membuka `output.pdf` di Adobe Acrobat atau penampil PDF apa pun, Anda harus dapat:

- **Mencari** kata apa pun yang muncul di JPEG asli.
- Melihat **tidak ada peringatan font yang hilang** (berkat `EmbedFonts = true`).
- Memverifikasi bahwa file mematuhi **PDF/A‑2b** (File → Properties → PDF/A).

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke dalam proyek Console App baru, sesuaikan jalur file, dan tekan **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

namespace ImageToSearchablePdf
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine and apply license
            var ocrEngine = new OcrEngine();
            ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // 2️⃣ Load JPEG image
            ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");

            // 3️⃣ Configure PDF save options (embed fonts, PDF/A‑2b, etc.)
            var pdfSaveOptions = new PdfSaveOptions
            {
                PdfAStandard = PdfAStandard.PdfA2b,
                EmbedFonts = true,
                Compression = PdfCompression.Flate,
                RenderOriginalImage = true
            };

            // 4️⃣ Run OCR recognition
            ocrEngine.Recognize();

            // 5️⃣ Save searchable PDF with embedded fonts
            string outputPath = @"C:\MyImages\output.pdf";
            ocrEngine.Save(outputPath, pdfSaveOptions);

            Console.WriteLine($"✅ PDF created at: {outputPath}");
            Console.WriteLine("Open it in any PDF viewer and try searching for words from the original JPEG.");
        }
    }
}
```

**Output yang diharapkan:**  
Konsol mencetak pesan sukses, dan `output.pdf` muncul di folder target. Membuka PDF dan menggunakan kotak pencarian penampil harus menemukan kata apa pun yang ada di `input.jpg`.

## Pertanyaan yang Sering Diajukan & Kasus Tepi

### 1. “Bagaimana jika JPEG saya adalah TIFF multi‑halaman?”

Aspose OCR memperlakukan setiap halaman secara terpisah. Konversi TIFF menjadi serangkaian JPEG (atau gunakan `ImageStream.FromFile` pada setiap halaman) dan lakukan loop proses OCR, menambahkan setiap hasil ke PDF yang sama dengan menggunakan kembali instance `OcrEngine` yang sama.

### 2. “Bisakah saya mengontrol DPI atau pra‑pemrosesan gambar?”

Ya. Sebelum memanggil `Recognize()`, Anda dapat menyesuaikan resolusi gambar:

```csharp
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;
ocrEngine.Image.AutoRotate = true; // auto‑rotate for landscape scans
```

DPI yang lebih tinggi sering menghasilkan akurasi pengenalan yang lebih baik, terutama untuk font kecil.

### 3. “PDF saya masih menunjukkan font yang hilang di Adobe Reader—apa yang salah?”

Pastikan Anda menargetkan **PDF/A‑2b** dan `EmbedFonts` diatur ke `true`. Jika Anda secara manual mengubah `PdfAStandard` menjadi `None`, langkah validasi PDF/A dilewati, dan beberapa font mungkin tetap tidak disematkan.

### 4. “Apakah lapisan OCR dapat dicari di perangkat seluler?”

Tentu saja. Lapisan teks tersembunyi merupakan bagian dari spesifikasi PDF, sehingga penampil PDF apa pun yang mendukung ekstraksi teks (termasuk iOS Files, Android PDF Viewer, dll.) akan memungkinkan pengguna mencari.

### 5. “Bagaimana saya menangani bahasa kanan‑ke‑kiri seperti Arab?”

Atur bahasa sebelum pengenalan:

```csharp
ocrEngine.Language = OcrLanguage.Arabic;
ocrEngine.Recognize();
```

Aspose OCR secara otomatis mengubah arah teks dan menyematkan font yang sesuai ketika `EmbedFonts` bernilai true.

## Tips Pro & Jebakan Umum

- **Tips pro:** Jika gambar sumber Anda adalah foto berwarna, pertimbangkan untuk mengonversinya ke grayscale terlebih dahulu (`ocrEngine.Image.ConvertToGrayscale();`). Ini mengurangi ukuran file tanpa mengurangi akurasi OCR.
- **Waspadai:** Menggunakan lisensi percobaan gratis dengan gambar **besar** dapat menyebabkan mesin memotong teks OCR. Tingkatkan ke lisensi penuh untuk beban kerja produksi.
- **Tips performa:** Menggunakan kembali instance `OcrEngine` yang sama pada beberapa gambar menghindari overhead memuat ulang DLL OCR secara berulang.
- **Catatan keamanan:** File PDF/A‑2b bersifat **hanya‑baca** secara desain, yang membantu mencegah injeksi skrip tidak sengaja—bonus yang bagus untuk lingkungan dengan kepatuhan tinggi.

## Kesimpulan

Kami telah membahas seluruh alur kerja untuk **menyematkan font dalam PDF** sambil **mengenali teks dari JPEG** dan menghasilkan **PDF yang dapat dicari** yang memenuhi standar PDF/A‑2b. Prosesnya dapat diringkas menjadi:

1. Inisialisasi `OcrEngine` dan terapkan lisensi Anda.  
2. Muat gambar JPEG.  
3. Konfigurasikan `PdfSaveOptions` (menyematkan font, PDF/A‑2b, kompresi).  
4. Jalankan `Recognize()`.  
5. Simpan dengan opsi yang telah dikonfigurasi.

Sekarang Anda dapat mengintegrasikan alur ini ke dalam layanan web, utilitas desktop, atau pekerjaan batch yang perlu **mengonversi gambar menjadi PDF yang dapat dicari** secara langsung. Selanjutnya, Anda mungkin ingin menjelajahi **cara membuat PDF yang dapat dicari** dari PDF multi‑halaman atau PDF yang dihasilkan

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}