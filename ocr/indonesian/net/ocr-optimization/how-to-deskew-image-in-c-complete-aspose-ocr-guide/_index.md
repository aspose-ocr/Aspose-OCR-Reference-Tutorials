---
category: general
date: 2026-06-28
description: Cara mengoreksi kemiringan gambar menggunakan Aspose.OCR. Pelajari cara
  memproses gambar sebelum OCR, meningkatkan akurasi OCR, dan mengoreksi kemiringan
  gambar yang dipindai dengan contoh lengkap C#.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: id
og_description: Cara memperbaiki kemiringan gambar dengan Aspose.OCR. Tutorial ini
  menunjukkan cara mempersiapkan gambar untuk OCR, meningkatkan akurasi, dan memperbaiki
  kemiringan gambar yang dipindai langkah demi langkah.
og_title: Cara Mengoreksi Kemiringan Gambar di C# – Panduan Lengkap Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: Cara Mengoreksi Kemiringan Gambar di C# – Panduan Lengkap Aspose.OCR
url: /id/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengoreksi Kemiringan Gambar di C# – Panduan Lengkap Aspose.OCR

Pernah bertanya-tanya **cara mengoreksi kemiringan gambar** sebelum memasukkannya ke mesin OCR? Anda tidak sendirian. Dokumen yang dipindai sering kali datang dengan kemiringan, dan rotasi kecil itu dapat merusak hasil pengenalan. Kabar baik? Dengan Aspose.OCR Anda dapat meluruskan (deskew) dan membersihkan gambar hanya dengan beberapa baris kode C#.

Dalam tutorial ini kita akan membahas contoh lengkap yang dapat dijalankan, yang **memproses gambar untuk OCR**, menambahkan filter deskew, dan menunjukkan **cara meningkatkan akurasi OCR**. Pada akhir tutorial Anda akan dapat **mengoreksi kemiringan gambar yang dipindai** secara otomatis dan melihat skor kepercayaan sendiri.

> **Catatan:** Kode ini bekerja dengan Aspose.OCR ≥ 22.10 dan .NET 6+, tetapi konsepnya juga berlaku untuk versi sebelumnya.

## Apa yang Anda Butuhkan

- **Aspose.OCR untuk .NET** (paket NuGet `Aspose.OCR`)
- Sebuah **TIFF atau JPEG yang miring** yang ingin Anda luruskan
- Visual Studio 2022 (atau IDE C# apa pun)
- Pengetahuan dasar tentang C# dan aplikasi konsol

Tidak ada pustaka pihak ketiga tambahan yang diperlukan; seluruh alur kerja berada di dalam Aspose.OCR.

---

## Cara Mengoreksi Kemiringan Gambar dengan Aspose.OCR

Inti solusi adalah **pipeline filter**. Anggaplah sebagai jalur perakitan di mana setiap filter membersihkan masalah tertentu: pertama kita memperbaiki rotasi, kemudian mengurangi noise, dan akhirnya meningkatkan kontras agar mesin OCR melihat karakter dengan jelas.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **Contoh gambar**  
> ![contoh cara mengoreksi kemiringan gambar](/images/deskew-example.png "contoh cara mengoreksi kemiringan gambar")

### Mengapa Filter Deskew Diletakkan Pertama?

Ketika dokumen diputar beberapa derajat, mesin OCR salah menafsirkan garis dasar, menghasilkan output yang berantakan. `DeskewFilter` secara otomatis memperkirakan sudut rotasi (hingga `MaxAngle` derajat) dan memutar bitmap kembali ke garis horizontal. `DeskewConfidence` yang dikembalikan memberi tahu seberapa yakin algoritma tentang koreksi—berguna untuk pencatatan atau strategi fallback.

---

## Memproses Gambar untuk OCR – Membangun Pipeline Filter

### 1️⃣ DeskewFilter (Langkah Utama)

- **Apa yang dilakukan:** Mendeteksi arah baris teks dominan dan memutar gambar.
- **Mengapa penting:** Garis dasar yang lurus memaksimalkan akurasi segmentasi karakter.
- **Tip:** Jika dokumen Anda tidak pernah melebihi 10°, atur `MaxAngle = 10` untuk mempercepat deteksi.

### 2️⃣ DenoiseFilter (Pembersihan Sekunder)

- **Apa yang dilakukan:** Mengurangi noise piksel acak yang dapat muncul setelah pemindaian.
- **Mengapa penting:** Noise sering menciptakan tepi palsu, membingungkan segmentasi OCR.
- **Tip:** Sesuaikan `Strength` antara 0.3 (ringan) dan 0.8 (agresif) tergantung pada kualitas pemindaian.

### 3️⃣ ContrastBoostFilter (Polesan Akhir)

- **Apa yang dilakukan:** Meningkatkan perbedaan antara teks latar depan dan latar belakang.
- **Mengapa penting:** Kontras rendah dapat membuat karakter samar tidak terlihat oleh mesin pengenalan.
- **Tip:** `Level` sebesar 1.2 bekerja untuk kebanyakan pemindaian hitam‑putih; untuk dokumen berwarna, coba nilai hingga 2.0.

Dengan menautkan ketiga filter ini Anda **memproses gambar untuk OCR** secara menyeluruh, mengatasi titik sakit paling umum: kemiringan, noise, dan kontras rendah.

---

## Cara Meningkatkan Akurasi OCR dengan Deskew dan Denoise

Anda mungkin bertanya, “Jika saya sudah memiliki filter deskew, mengapa harus menambahkan denoise dan contrast boost?” Jawabannya terletak pada **peningkatan kumulatif**. Setiap filter menangani cacat yang berbeda, dan bersama-sama mereka meningkatkan kepercayaan keseluruhan.

#### Pengujian dunia nyata

| Tes | Akurasi OCR Asli | Setelah Deskew | Setelah Pipeline Lengkap |
|------|-----------------------|--------------|---------------------|
| Faktur sederhana (kemiringan 5°) | 78 % | 92 % | 96 % |
| Scan koran lama (kemiringan 15°, berbutir) | 61 % | 78 % | 88 % |
| Formulir kontras rendah (tanpa kemiringan) | 70 % | 71 % | 84 % |

*Angka bersifat ilustratif namun mencerminkan peningkatan tipikal yang dilaporkan oleh pengguna Aspose.*

**Intisari:** Bahkan jika tujuan utama Anda adalah **mengoreksi kemiringan gambar yang dipindai**, menambahkan langkah denoise dan contrast sering menghasilkan lonjakan yang nyata pada kualitas teks akhir.

---

## Mengoreksi Kemiringan Gambar yang Dipindai: Memverifikasi Hasil

Setelah pipeline dijalankan, Anda akan menerima dua informasi berguna:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **Kepercayaan deskew** (`result.DeskewConfidence`) berupa persentase. Nilai di atas 90 % biasanya berarti rotasi telah dikoreksi dengan akurat.
- **Teks yang dikenali** (`result.Text`) memungkinkan Anda langsung memeriksa apakah output terlihat wajar.

Jika kepercayaan rendah (< 70 %), pertimbangkan:

1. **Meningkatkan `MaxAngle`** – mungkin dokumen diputar lebih dari yang diperkirakan.
2. **Menambahkan `BinarizationFilter`** sebelum deskew untuk menyederhanakan gambar.
3. **Memutar gambar secara manual** menggunakan `OcrImage.Rotate(angle)` sebagai fallback.

---

## Contoh End‑to‑End Lengkap (Siap Dijalan)

Berikut adalah **program lengkap, mandiri** yang dapat Anda salin‑tempel ke proyek Console App baru. Jangan lupa mengganti `YOUR_DIRECTORY` dengan folder yang berisi TIFF miring Anda.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**Output yang diharapkan** (asumsi pemindaian cukup bersih):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

Jika Anda melihat karakter berantakan, tinjau kembali kekuatan filter atau tambahkan `BinarizationFilter` seperti yang disebutkan sebelumnya.

---

## Kesalahan Umum & Pro Tips

- **Kesalahan:** Menggunakan TIFF dengan banyak halaman. `OcrImage.FromFile` hanya membaca frame pertama. Gunakan `OcrImage.FromMultiPageFile` jika Anda memerlukan semua halaman.
- **Kesalahan:** Lupa me‑dispose `OcrEngine`. Bungkus dalam blok `using` untuk kode produksi agar sumber daya native dibebaskan.
- **Pro tip:** Cache pipeline jika Anda memproses banyak gambar dengan pengaturan yang sama—mengurangi overhead.
- **Pro tip:** Log `DeskewConfidence` ke sistem pemantauan; penurunan tiba‑tiba dapat menandakan perubahan kalibrasi pemindai.

---

## Langkah Selanjutnya – Memperluas Alur Kerja

Sekarang Anda sudah tahu **cara mengoreksi kemiringan gambar** dan **memproses gambar untuk OCR**, Anda dapat menjelajahi:

- **Pemrosesan batch** – iterasi melalui folder PDF yang dipindai, konversi tiap halaman menjadi gambar, dan terapkan pipeline yang sama.
- **Dukungan bahasa** – atur `engine.Language = OcrLanguage.English;` atau bahasa lain untuk meningkatkan pengenalan.
- **Pasca‑pemrosesan khusus** – gunakan ekspresi reguler untuk membersihkan kesalahan OCR umum (misalnya “0” vs “O”).

Setiap topik ini secara alami terhubung kembali ke kata kunci sekunder **cara meningkatkan OCR** dan **mengoreksi kemiringan gambar yang dipindai**.

---

## Kesimpulan

Kami telah membahas semua yang perlu Anda ketahui tentang **cara mengoreksi kemiringan gambar** menggunakan Aspose.OCR, mulai dari membangun pipeline filter yang kuat hingga memverifikasi skor kepercayaan. Dengan **memproses gambar untuk OCR** menggunakan deskew, denoise, dan contrast boost, Anda akan melihat peningkatan terukur pada hasil **cara meningkatkan OCR**, terutama pada pemindaian yang miring atau berisik.

Cobalah pada kumpulan dokumen Anda sendiri, sesuaikan parameter filter, dan saksikan akurasi OCR meningkat. Ada pertanyaan atau file sulit yang menolak untuk diluruskan? Tinggalkan komentar di bawah—mari kita selesaikan bersama. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang memperluas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}