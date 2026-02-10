---
category: general
date: 2026-02-09
description: Cara menggunakan OCR di C# untuk mengenali teks dari gambar, mengekstrak
  teks, dan mengubah gambar menjadi teks dengan Aspose OCR. Panduan lengkap langkah
  demi langkah.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- load image stream
language: id
og_description: Cara menggunakan OCR di C# untuk mengenali teks dari gambar, mengekstrak
  teks, dan mengubah gambar menjadi teks dengan Aspose OCR. Panduan lengkap dengan
  kode.
og_title: Cara Menggunakan OCR di C# – Mengenali Teks dari Gambar
tags:
- C#
- Aspose OCR
- Image Processing
title: Cara Menggunakan OCR di C# – Mengenali Teks dari Gambar
url: /id/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di C# – Mengenali Teks dari Gambar

Pernah bertanya-tanya **cara menggunakan OCR** untuk mengubah tangkapan layar menjadi teks yang dapat diedit? Anda tidak sendirian. Banyak pengembang menemui kendala ketika mereka perlu *mengenali teks dari gambar* tetapi tidak memiliki contoh yang jelas dan siap dijalankan.  

Dalam tutorial ini kami akan membahas seluruh proses—memuat lisensi, membuat engine, memberi aliran gambar, dan akhirnya mengekstrak teks polos. Pada akhir tutorial Anda akan dapat **mengekstrak teks dari gambar**, **mengonversi gambar ke teks**, dan bahkan memahami nuansa penanganan **load image stream**.

> **Apa yang akan Anda dapatkan:** program C# lengkap yang dapat dijalankan menggunakan Aspose.OCR, penjelasan tiap langkah, serta tips untuk menghindari jebakan umum.

---

## Prasyarat

- .NET 6.0 atau yang lebih baru (API ini juga bekerja dengan .NET Framework 4.6+)
- Paket NuGet Aspose.OCR untuk .NET (`Aspose.OCR`) terpasang
- File lisensi Aspose OCR yang valid (`Aspose.OCR.lic`) – versi percobaan gratis tetap dapat dipakai tetapi akan menambahkan watermark.
- Sebuah gambar (`sample.jpg`) yang berisi teks jelas yang dapat dibaca mesin.

> **Tip:** Jika Anda menggunakan Visual Studio, perintah konsol NuGet adalah  
> `Install-Package Aspose.OCR -Version 23.10` (ganti dengan versi terbaru).

---

## Cara Menggunakan OCR: Memuat Lisensi dan Menginisialisasi Engine

Hal pertama yang harus Anda lakukan adalah memberi tahu Aspose bahwa Anda memiliki lisensi. Melewatkan langkah ini tetap akan menjalankan program, tetapi watermark akan muncul pada output dan Anda akan membuang waktu pemrosesan pada pemeriksaan mode percobaan.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // Step 1 – Load the Aspose OCR license (replace with your .lic file path)
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Step 2 – Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

**Mengapa ini penting:** Objek `License` menonaktifkan watermark percobaan dan membuka semua fitur lengkap, termasuk model dengan akurasi lebih tinggi serta dukungan multi‑bahasa.  

> **Pro tip:** Simpan file lisensi di luar repositori kontrol sumber Anda. Gunakan variabel lingkungan atau vault yang aman untuk menyuntikkan path pada saat runtime.

---

## Langkah 2 – Memuat Image Stream (dan Mengapa Lebih Baik Daripada Path File)

Ketika Anda *load image stream* alih‑alih memberikan path file mentah, Anda mendapatkan fleksibilitas: gambar dapat berasal dari basis data, permintaan web, atau array byte di memori.  

```csharp
// Step 3 – Load the image you want to recognize
// Using ImageStream.FromFile is the simplest way for local files.
ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

// Alternative: load from a byte array (e.g., when the image is uploaded via HTTP)
// byte[] imageBytes = ... // get from request
// ImageStream imageStream = ImageStream.FromBytes(imageBytes);
```

**Penjelasan:** `ImageStream` mengabstraksi sumber yang mendasarinya, memungkinkan engine OCR memperlakukan semuanya secara seragam. Jika Anda kemudian beralih ke bucket penyimpanan cloud, Anda hanya perlu mengubah cara pembuatan `ImageStream`; sisanya tetap tidak berubah.

---

## Langkah 3 – Mengenali Teks dari Gambar

Sekarang masuk ke inti masalah: **mengenali teks dari gambar**. Metode `OcrEngine.Recognize` menjalankan model jaringan saraf yang dibundel dengan Aspose dan mengembalikan objek `OcrResult` yang berisi beberapa properti berguna.

```csharp
// Step 4 – Run the OCR process on the image
OcrResult ocrResult = ocrEngine.Recognize(imageStream);
```

**Apa yang ada di dalam `OcrResult`?**  
- `PlainText` – satu string berisi semua karakter yang terdeteksi.  
- `Words` – koleksi objek kata dengan kotak pembatas (berguna untuk menyorot).  
- `Lines` – pengelompokan tingkat baris, membantu mempertahankan jeda paragraf.

Jika Anda hanya membutuhkan teks mentah, `PlainText` adalah jalur tercepat. Untuk skenario yang lebih maju (misalnya menampilkan hasil di atas gambar asli), jelajahi `Words` dan `Lines`.

---

## Langkah 4 – Menampilkan atau Menyimpan Teks yang Dikeluarkan

Akhirnya, mari keluarkan teks yang dikenali ke konsol. Pada aplikasi nyata Anda mungkin menulis ke basis data, file, atau mengirimnya melalui API.

```csharp
// Step 5 – Display the recognized plain text (watermark omitted with a full license)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.PlainText);
Console.WriteLine("==================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
```

**Output yang diharapkan:**  
Jika `sample.jpg` berisi kalimat *“Hello World!”*, Anda akan melihat:

```
=== OCR Output ===
Hello World!
==================
```

Saat menggunakan lisensi percobaan, output akan menyertakan watermark kecil “Aspose OCR Demo” di akhir teks. Dengan lisensi penuh, watermark tersebut hilang sepenuhnya.

---

## Contoh Lengkap yang Siap Dijalankan (Copy‑Paste Ready)

Berikut seluruh program, siap untuk dikompilasi. Ganti path dengan lokasi Anda sendiri dan Anda siap meluncur.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // 1️⃣ Load license – required for production use
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // 2️⃣ Create OCR engine – the core processing object
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Load image – you can also use ImageStream.FromBytes for in‑memory data
        ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

        // 4️⃣ Recognize text – this is where the magic happens
        OcrResult ocrResult = ocrEngine.Recognize(imageStream);

        // 5️⃣ Output the plain text – perfect for further processing
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.PlainText);
        Console.WriteLine("==================");

        // Optional: persist the result
        System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
    }
}
```

> **Ingat:** Kode di atas **mengekstrak teks dari gambar** dan **mengonversi gambar ke teks** dalam satu panggilan. Tanpa loop tambahan, tanpa penanganan piksel manual—Aspose melakukan semua pekerjaan berat.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika gambar saya blur atau kontras rendah?

Aspose OCR menyertakan opsi pra‑pemrosesan (misalnya `ocrEngine.ImagePreprocessor`). Anda dapat mengaktifkan binarisasi atau deskew sebelum pengenalan:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Binarization = true,
    Deskew = true
};
```

### Bagaimana cara menangani banyak bahasa?

Setel properti `Language` pada engine:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Engine kemudian akan mencoba mendeteksi kedua bahasa secara otomatis.

### Bisakah saya memproses PDF alih‑alih JPEG?

Ya—Aspose OCR dapat membaca PDF secara langsung, tetapi Anda memerlukan pustaka Aspose.PDF untuk mengekstrak tiap halaman sebagai gambar terlebih dahulu, lalu memberi aliran gambar tersebut ke engine OCR.

### Bagaimana dengan pemrosesan batch besar?

Bungkus logika pengenalan dalam loop dan gunakan kembali instance `OcrEngine` yang sama. Membuat engine baru untuk tiap gambar menambah overhead yang tidak perlu.

---

## Pro Tips untuk OCR Siap Produksi

- **Cache objek lisensi**: Muat sekali saat aplikasi mulai, bukan per permintaan.  
- **Reuse `OcrEngine`**: Engine menyimpan buffer internal; penggunaan kembali mengurangi tekanan GC.  
- **Batasi ukuran gambar**: Gambar sangat besar (>5 MP) meningkatkan waktu pemrosesan secara dramatis. Turunkan resolusi ke 150‑300 DPI bila resolusi tinggi tidak diperlukan.  
- **Validasi output**: OCR tidak sempurna; terapkan pemeriksaan kepercayaan sederhana (`ocrResult.Words.Average(w => w.Confidence)`) dan tandai hasil dengan kepercayaan rendah untuk peninjauan manual.  
- **Keamanan thread**: `OcrEngine` tidak thread‑safe. Buat instance terpisah per thread atau gunakan pola pool.

---

## Kesimpulan

Kami telah membahas **cara menggunakan OCR** di C# mulai dari memuat lisensi hingga mengekstrak teks yang bersih dan dapat dicari. Dengan mengikuti langkah‑langkah di atas Anda dapat **mengenali teks dari gambar**, **mengekstrak teks dari gambar**, dan dengan mudah **mengonversi gambar ke teks** sambil menguasai pola **load image stream** yang membuat kode Anda fleksibel untuk sumber data masa depan.

Siap untuk tantangan berikutnya? Coba tambahkan pemotongan region‑of‑interest, integrasikan dengan Azure Blob storage, atau alirkan output OCR ke pipeline pemrosesan bahasa alami. Langit adalah batasnya, dan kini Anda memiliki fondasi yang kuat untuk membangunnya.

---

![Diagram showing the OCR flow: load license → create engine → load image stream → recognize → output text](image-placeholder.png "how to use OCR to recognize text from image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}