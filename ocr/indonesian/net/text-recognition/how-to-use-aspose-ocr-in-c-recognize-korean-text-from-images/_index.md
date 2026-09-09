---
category: general
date: 2025-12-29
description: Cara menggunakan Aspose OCR untuk mengonversi teks gambar dan mengekstrak
  teks Korea. Panduan langkah demi langkah untuk mengekstrak teks gambar dan mengenali
  teks Korea dalam C#.
draft: false
keywords:
- how to use aspose
- convert image text
- extract text image
- extract korean text
- recognize korean text
language: id
og_description: Pelajari cara menggunakan Aspose OCR untuk mengonversi teks gambar,
  mengekstrak teks Korea, dan mengenali teks Korea dari foto dengan contoh lengkap
  C#.
og_title: Cara Menggunakan Aspose OCR – Mengenali Teks Korea dalam C#
tags:
- Aspose
- OCR
- C#
- Image Processing
title: Cara Menggunakan Aspose OCR di C# – Mengenali Teks Korea dari Gambar
url: /id/net/text-recognition/how-to-use-aspose-ocr-in-c-recognize-korean-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Aspose OCR di C# – Mengenali Teks Korea dari Gambar

Pernah bertanya-tanya **bagaimana cara menggunakan Aspose** untuk mengambil karakter Korea dari sebuah foto? Mungkin Anda memiliki screenshot tanda jalan, kwitansi yang dipindai, atau meme yang perlu diubah menjadi teks yang dapat dicari. Kabar baiknya, Aspose OCR membuat ini sangat mudah, dan Anda tidak perlu berurusan dengan trik pemrosesan gambar tingkat‑rendah.

Dalam tutorial ini kami akan menelusuri **contoh lengkap yang dapat dijalankan** yang menunjukkan cara **mengonversi teks gambar**, **mengekstrak teks gambar**, dan secara khusus **mengekstrak teks Korea** menggunakan pustaka Aspose OCR. Pada akhirnya Anda akan memiliki aplikasi konsol yang mencetak string Korea yang dikenali, dan Anda akan memahami mengapa setiap baris penting.

## Apa yang Anda Butuhkan

- **.NET 6+** (semua SDK .NET terbaru dapat digunakan – Visual Studio, Rider, atau `dotnet` CLI)
- **Aspose.OCR for .NET** paket NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- File gambar yang berisi karakter Korea (misalnya `korean_sign.jpg`).  
- Sedikit pengetahuan C# – jika Anda pernah menulis “Hello World” sebelumnya, Anda siap melanjutkan.

> **Pro tip:** Aspose OCR mendukung lebih dari 50 bahasa secara bawaan. Kami akan fokus pada Korea karena skrip Hangul‑nya sering membuat mesin OCR umum gagal.

## Langkah 1 – Instal dan Referensikan Aspose OCR

Pertama, tambahkan pustaka ke proyek Anda. Perintah NuGet di atas melakukan pekerjaan berat, tetapi jika Anda lebih suka UI, cukup cari *Aspose.OCR* di NuGet Package Manager.

```csharp
// No code needed here – the package reference is enough.
// The using directives below will bring the types into scope.
using Aspose.OCR;
using Aspose.OCR.Models;
```

> **Mengapa ini penting:** Pernyataan `using` memberi Anda akses ke `OcrEngine`, `Language`, dan kelas pembantu `Image`. Tanpa mereka, kompiler akan mengeluh tentang tipe yang tidak dikenal.

## Langkah 2 – Muat Gambar yang Ingin Diproses

Aspose OCR bekerja dengan pembungkus `Image` miliknya, yang dapat membaca JPEG, PNG, BMP, dan banyak format lainnya. Arahkan ke file yang berisi teks Korea.

```csharp
// Step 2: Load the image containing Korean characters
var imagePath = Path.Combine(Environment.CurrentDirectory, "korean_sign.jpg");
var image = Image.Load(imagePath);
```

Jika file tidak berada di folder yang sama dengan executable Anda, sesuaikan pathnya. Pemanggilan `Image.Load` melakukan **mengonversi teks gambar** menjadi representasi internal yang dapat dipahami mesin OCR.

![contoh penggunaan aspose OCR](/images/aspose-ocr-korean.png "cara menggunakan aspose OCR untuk mengenali teks Korea")

*Teks alt gambar: “contoh penggunaan aspose OCR yang menampilkan tanda jalan Korea.”*

## Langkah 3 – Konfigurasikan Mesin OCR untuk Bahasa Korea

Mesin perlu mengetahui bahasa apa yang harus dicari; jika tidak, secara default akan menggunakan bahasa Inggris dan akan melewatkan karakter Hangul.

```csharp
// Step 3: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // Tell Aspose we want to recognize Korean (Hangul)
    Language = Language.Korean
};
```

> **Mengapa ini penting:** Menetapkan `Language = Language.Korean` memberi tahu mesin untuk memuat paket bahasa Korea, yang secara dramatis meningkatkan akurasi untuk glyph Hangul. Melewatkan langkah ini sering menghasilkan output yang berantakan.

## Langkah 4 – Jalankan Proses Pengenalan

Sekarang kami benar‑benar meminta Aspose membaca gambar. Metode `Recognize` mengembalikan objek `OcrResult` yang berisi string yang diekstrak dan skor kepercayaan.

```csharp
// Step 4: Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(image);
```

Jika Anda perlu **mengekstrak teks gambar** dari foto yang lebih besar (misalnya screenshot dengan banyak elemen UI), Anda dapat memotong wilayah yang diinginkan terlebih dahulu menggunakan `image.Crop(...)` sebelum memanggil `Recognize`. Itu trik yang berguna ketika Anda hanya peduli pada bagian tertentu dari gambar.

## Langkah 5 – Tampilkan Teks Korea yang Dikenali

Akhirnya, tampilkan hasilnya. Dalam aplikasi dunia nyata Anda mungkin menyimpannya ke basis data atau mengirimkannya ke API terjemahan, tetapi untuk tutorial ini menulis ke konsol cukup sederhana.

```csharp
// Step 5: Print the recognized Korean text
Console.WriteLine("Recognized Korean text:");
Console.WriteLine(ocrResult.Text);
```

### Output yang Diharapkan

```
Recognized Korean text:
서울특별시 강남구 테헤란로 123
```

Output aktual Anda tentu akan mencerminkan karakter Korea apa pun yang ada di `korean_sign.jpg`.

## Contoh Lengkap yang Berfungsi

Berikut adalah **program lengkap** yang dapat Anda salin‑tempel ke proyek konsol baru (`dotnet new console`). Pastikan file gambar berada di samping `.exe` yang telah dikompilasi atau sesuaikan pathnya.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet before running this code.

        // 2️⃣ Load the image that contains Korean text.
        var imagePath = Path.Combine(Environment.CurrentDirectory, "korean_sign.jpg");
        var image = Image.Load(imagePath);

        // 3️⃣ Create the OCR engine and set it to recognize Korean.
        var ocrEngine = new OcrEngine
        {
            Language = Language.Korean   // 👈 This enables Hangul support.
        };

        // 4️⃣ Run the OCR process.
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted Korean string.
        Console.WriteLine("Recognized Korean text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Jalankan program dengan `dotnet run` dan saksikan karakter Korea muncul di konsol Anda.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika OCR mengembalikan karakter yang berantakan?

- **Periksa pengaturan bahasa.** Lupa menambahkan `Language.Korean` adalah kesalahan paling umum.
- **Tingkatkan kualitas gambar.** Gambar yang lebih tajam, DPI lebih tinggi, dan pencahayaan yang tepat meningkatkan akurasi.
- **Pra‑proses gambar.** Aspose OCR menawarkan filter bawaan (`image.Binarize()`, `image.Deskew()`) yang dapat membersihkan pemindaian yang berisik.

### Bisakah saya **mengonversi teks gambar** secara massal?

Tentu saja. Bungkus langkah‑langkah di atas dalam loop `foreach` yang mengiterasi folder berisi gambar. Berikut cuplikan singkatnya:

```csharp
foreach (var file in Directory.GetFiles(@"C:\KoreanImages", "*.jpg"))
{
    var img = Image.Load(file);
    var result = ocrEngine.Recognize(img);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

Skrip ini **mengekstrak teks gambar** dari setiap file dan menulis file `.txt` berdampingan.

### Bagaimana cara menangani banyak bahasa dalam satu gambar?

Aspose OCR dapat mendeteksi bahasa secara otomatis jika Anda menetapkan `Language = Language.Auto`. Namun, deteksi otomatis mungkin lebih lambat dan sedikit kurang akurat dibandingkan menentukan bahasa secara tepat. Jika Anda tahu gambar berisi Korea dan Inggris, Anda dapat menjalankan dua kali—pertama dengan `Language.Korean`, kemudian dengan `Language.English`—dan menggabungkan hasilnya.

## Tips untuk OCR Siap Produksi

- **Cache OcrEngine.** Membuat mesin baru untuk setiap permintaan menambah beban. Simpan sebagai singleton jika Anda memproses banyak gambar.
- **Batasi ukuran gambar.** Gambar besar mengonsumsi memori; skala turun ke lebar ~1500 px sebelum memberi ke mesin.
- **Tangani pengecualian.** Bungkus pemanggilan `Recognize` dalam try/catch untuk menangani file rusak secara elegan.

## Kesimpulan

Kami baru saja membahas **cara menggunakan Aspose** untuk **mengonversi teks gambar**, **mengekstrak teks gambar**, dan secara khusus **mengekstrak teks Korea** dengan beberapa baris kode C#. Langkah‑langkahnya sederhana:

1. Instal Aspose OCR.  
2. Muat gambar Anda.  
3. Konfigurasikan mesin untuk Korea.  
4. Jalankan `Recognize`.  
5. Tampilkan hasilnya.

Sekarang Anda dapat menyematkan potongan kode ini ke alur kerja yang lebih besar—pemrosesan batch, pengarsipan dokumen, atau bahkan aplikasi terjemahan waktu nyata. Ingin melangkah lebih jauh? Coba tambahkan metode `Image.Preprocess()` dari Aspose, bereksperimen dengan bahasa lain, atau integrasikan output dengan Azure Cognitive Services untuk terjemahan.

Masih ada pertanyaan tentang **mengenali teks Korea** atau fitur Aspose lainnya? Tinggalkan komentar, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}