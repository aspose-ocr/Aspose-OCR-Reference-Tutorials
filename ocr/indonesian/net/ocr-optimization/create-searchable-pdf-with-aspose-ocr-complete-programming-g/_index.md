---
category: general
date: 2026-05-21
description: Buat PDF yang dapat dicari menggunakan Aspose OCR sambil meningkatkan
  akurasi OCR dan pelajari cara memuat gambar untuk OCR dalam C#. Tutorial langkah
  demi langkah.
draft: false
keywords:
- create searchable PDF
- improve OCR accuracy
- load image for OCR
- Aspose OCR C#
- PDF output with OCR
language: id
og_description: Buat PDF yang dapat dicari dengan Aspose OCR. Pelajari cara meningkatkan
  akurasi OCR dan memuat gambar untuk OCR dalam satu contoh yang dapat dijalankan.
og_title: Buat PDF yang Dapat Dicari dengan Aspose OCR – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF using Aspose OCR while you improve OCR accuracy
    and learn how to load image for OCR in C#. Step‑by‑step tutorial.
  headline: Create Searchable PDF with Aspose OCR – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- Aspose
- PDF
- C#
title: Buat PDF yang Dapat Dicari dengan Aspose OCR – Panduan Pemrograman Lengkap
url: /id/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat PDF yang Dapat Dicari dengan Aspose OCR – Panduan Pemrograman Lengkap

Pernah perlu **membuat PDF yang dapat dicari** dari gambar yang dipindai tetapi tidak tahu harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami kebingungan saat pertama kali menangani proyek OCR. Kabar baiknya, Aspose OCR membuat seluruh alur kerja—memuat gambar, memperbaiki gambar untuk hasil yang lebih baik, dan akhirnya menyimpan PDF yang dapat dicari—menjadi cukup sederhana.

Dalam panduan ini kami akan menelusuri contoh lengkap dari awal hingga akhir yang tidak hanya menunjukkan cara **membuat PDF yang dapat dicari**, tetapi juga memperlihatkan cara **meningkatkan akurasi OCR** dan cara yang tepat untuk **memuat gambar untuk OCR**. Pada akhir tutorial Anda akan memiliki aplikasi konsol C# yang siap dijalankan dan menghasilkan PDF yang dapat dicari dengan gambar asli tersemat.

## Apa yang Akan Anda Pelajari

- Menyiapkan Aspose OCR (termasuk akselerasi GPU opsional)  
- Mengonfigurasi mesin untuk bahasa Prancis (atau bahasa apa pun) guna **meningkatkan akurasi OCR**  
- **Memuat gambar untuk OCR** dengan benar menggunakan `ImageStream`  
- Membangun pipeline filter untuk membersihkan gambar sebelum pengenalan  
- Menyimpan hasil sebagai PDF yang dapat dicari dengan gambar sumber tersemat  

Tidak ada ketergantungan eksternal selain Aspose OCR, dan kode ini bekerja pada .NET 6+ (atau .NET Framework 4.6+). Mari kita mulai.

---

![Contoh PDF yang dapat dicari yang dihasilkan oleh Aspose OCR – contoh membuat PDF yang dapat dicari](images/searchable-pdf-sample.png "contoh membuat PDF yang dapat dicari")

## Langkah 1: Membuat PDF yang Dapat Dicari – Aktifkan GPU & Atur Path Sumber Daya  

Jika Anda memiliki GPU yang kompatibel, mengaktifkannya dapat mempercepat proses pengenalan secara signifikan. Bahkan jika Anda melewatkan langkah ini, sisa kode tetap berfungsi dengan baik.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// Enable GPU acceleration (optional)
OcrEngine.EnableGpu(true);

// Tell Aspose where to find language data files (offline mode)
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");
```

**Mengapa ini penting:** Akselerasi GPU mengurangi latensi pada batch besar, dan mengatur path sumber daya memastikan mesin dapat bekerja tanpa koneksi internet—sempurna untuk pipeline CI atau lingkungan yang terisolasi.

> **Tip profesional:** Jika Anda berada di server tanpa tampilan (headless), pastikan driver CUDA cocok dengan versi yang disertakan dalam Aspose OCR; versi yang tidak cocok dapat menyebabkan kegagalan tanpa pesan error.

## Langkah 2: Meningkatkan Akurasi OCR – Pilih Bahasa yang Tepat  

Memilih model bahasa yang tepat adalah cara cepat meningkatkan akurasi. Di sini kami memilih bahasa Prancis, tetapi Anda dapat mengganti `OcrLanguage.French` dengan bahasa lain yang didukung.

```csharp
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.French   // improves OCR accuracy for French documents
};
```

**Mengapa ini penting:** Kamus khusus bahasa membantu mesin menyelesaikan karakter yang ambigu (misalnya, “œ” vs “oe”). Jika Anda melewatkan langkah ini, mesin akan menggunakan bahasa Inggris secara default, yang dapat secara drastis menurunkan **meningkatkan akurasi OCR** untuk teks non‑Inggris.

## Langkah 3: Memuat Gambar untuk OCR – Menggunakan ImageStream  

Sekarang kami **memuat gambar untuk OCR**. Helper `ImageStream.FromFile` menyembunyikan penanganan bitmap mentah dan bekerja dengan sebagian besar format umum (JPG, PNG, TIFF).

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

**Mengapa ini penting:** Memuat gambar dengan cara ini menjamin Aspose menerima gambar dalam format yang dapat diproses secara efisien. Jika Anda mencoba memberikan `Bitmap` mentah secara langsung, Anda mungkin akan menghadapi masalah manajemen memori pada file berukuran besar.

## Langkah 4: Membangun Pipeline Filter Gambar untuk Meningkatkan Akurasi  

Gambar yang bersih adalah setengah dari perjuangan. Pipeline di bawah ini melakukan deskew pada gambar dan menghapus noise latar belakang—dua penyebab klasik yang merusak **meningkatkan akurasi OCR**.

```csharp
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());   // corrects rotation
filterPipeline.Add(new DenoiseFilter()); // reduces grainy artifacts

// Apply the pipeline and replace the original image
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);
```

**Mengapa ini penting:** Deskew memastikan baris teks berada secara horizontal, sementara denoising mengurangi blob karakter palsu. Anda dapat menambahkan filter lain (misalnya, `ContrastFilter`) jika pemindaian sumber Anda sangat buruk.

## Langkah 5: Melakukan Pengenalan OCR  

Setelah gambar dipra‑proses, kami akhirnya membiarkan mesin melakukan magisnya.

```csharp
ocrEngine.Recognize();
```

Baris tunggal itu memicu model deep‑learning di balik Aspose OCR. Ia mengisi `ocrEngine.Text` dengan teks biasa dan juga menyiapkan output PDF.

> **Bagaimana jika teks terlihat berantakan?** Periksa kembali pengaturan bahasa pada Langkah 2 dan pertimbangkan menambahkan `BinarizeFilter` ke pipeline.

## Langkah 6: Menyimpan Hasil sebagai PDF yang Dapat Dicari  

Bagian akhir adalah menyimpan **PDF yang dapat dicari** di mana teks yang diekstrak berada di belakang gambar asli—tepat seperti yang Anda butuhkan untuk dokumen hukum atau arsip.

```csharp
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });
```

**Mengapa ini penting:** `EmbedOriginalImage = true` menjaga fidelitas visual pemindaian sekaligus memungkinkan pencarian teks. Jika Anda mengaturnya ke `false`, PDF akan berisi hanya teks yang diekstrak, yang mungkin berguna untuk arsip ringan.

### Opsional: Mencetak Teks yang Dikenali & JSON  

Jika Anda ingin memeriksa output mentah, baris-baris ini akan menampilkan teks biasa dan payload JSON terstruktur.

```csharp
Console.WriteLine(ocrEngine.Text);               // plain text
Console.WriteLine(ocrEngine.GetResultAsJson());  // JSON with layout info
```

**Output yang diharapkan:** Setelah menjalankan program, Anda akan melihat kalimat berbahasa Prancis yang dicetak di konsol, diikuti oleh objek JSON yang berisi kotak pembatas, skor kepercayaan, dan metadata bahasa.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// 1️⃣ Enable GPU (optional) and set resources path
OcrEngine.EnableGpu(true);
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");

// 2️⃣ Create and configure the OCR engine (improve OCR accuracy)
var ocrEngine = new OcrEngine { Language = OcrLanguage.French };

// 3️⃣ Load the source image (load image for OCR)
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");

// 4️⃣ Build filter pipeline (deskew + denoise)
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());
filterPipeline.Add(new DenoiseFilter());
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);

// 5️⃣ Recognize text
ocrEngine.Recognize();

// 6️⃣ Save as searchable PDF (create searchable PDF)
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });

// Optional: output text and JSON
Console.WriteLine(ocrEngine.Text);
Console.WriteLine(ocrEngine.GetResultAsJson());
```

Jalankan program, arahkan `YOUR_DIRECTORY` ke folder yang berisi `input.jpg` dan sumber daya Aspose OCR, dan Anda akan mendapatkan `output.pdf` tepat di sampingnya.

---

## Kesimpulan

Anda kini memiliki resep solid dan siap produksi untuk **membuat PDF yang dapat dicari** dengan Aspose OCR, sambil sekaligus belajar cara **meningkatkan akurasi OCR** dan **memuat gambar untuk OCR** dengan benar. Pipeline—GPU (opsional) → pemilihan bahasa → pemuatan gambar → rangkaian filter → pengenalan → penyimpanan PDF—mencakup setiap langkah penting, sehingga Anda dapat menyesuaikannya untuk bahasa lain, batch yang lebih besar, atau format output yang berbeda.

Apa selanjutnya? Coba ganti `PdfSaveOptions` dengan `DocxSaveOptions` untuk menghasilkan dokumen Word yang dapat dicari, bereksperimen dengan filter tambahan seperti `ContrastFilter`, atau integrasikan kode ini ke dalam API ASP.NET Core untuk menghasilkan PDF secara real‑time. Kemungkinannya tak terbatas, dan dengan fondasi yang telah dibangun di sini, Anda siap menghadapi tantangan OCR apa pun.

Ada pertanyaan atau menemukan kendala? Tinggalkan komentar, dan selamat coding!

## Tutorial Terkait

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}