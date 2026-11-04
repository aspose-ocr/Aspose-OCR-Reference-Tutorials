---
category: general
date: 2026-01-13
description: tutorial c# ocr yang menunjukkan cara mengekstrak teks dari gambar, memuat
  gambar untuk ocr, dan memformat output json menggunakan Aspose OCR. Pelajari cara
  menyerialisasi objek ke json.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: id
og_description: tutorial c# ocr yang memandu Anda melalui ekstraksi teks dari gambar,
  memuat gambar untuk ocr, dan memformat output JSON dengan Aspose OCR.
og_title: Tutorial OCR C# – Ekstrak Teks & Format JSON
tags:
- OCR
- C#
- JSON
title: tutorial OCR c# – Ekstrak Teks dari Gambar dan Dapatkan JSON Terformat
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Ekstrak Teks dari Gambar dan Format Output JSON

Pernah bertanya-tanya bagaimana cara **mengekstrak teks dari gambar** dalam proyek C# tanpa harus berurusan dengan pemrosesan piksel tingkat rendah? Itulah masalah yang diselesaikan oleh *c# ocr tutorial* ini. Dalam beberapa menit Anda akan melihat cara **memuat gambar untuk ocr**, menjalankan Aspose OCR, dan **memformat output json** sehingga Anda dapat langsung mengirim data ke API atau basis data Anda.

Kami akan menelusuri setiap baris kode, menjelaskan mengapa setiap bagian penting, dan bahkan menunjukkan JSON tepat yang harus Anda harapkan. Pada akhir tutorial, Anda akan memiliki aplikasi console siap‑jalankan yang mengubah file PNG faktur menjadi JSON bersih dan terindentasi. Tanpa basa‑basi, hanya solusi praktis yang dapat Anda sisipkan ke proyek .NET 6+ mana pun.

## Apa yang Dibahas dalam c# ocr tutorial Ini

- Menginstal paket NuGet Aspose.OCR  
- Memuat file gambar untuk pemrosesan OCR  
- Mengenali teks bahasa Inggris (atau bahasa lain yang didukung)  
- **Menyerialkan hasil OCR ke JSON** dengan pretty‑printing  
- Menampilkan JSON di console dan menyimpannya jika diinginkan  

Anda hanya memerlukan pemahaman dasar tentang C# dan .NET SDK terbaru. Tidak ada yang lain. Jika Anda penasaran tentang cara **mengekstrak teks dari gambar** untuk faktur, kwitansi, atau formulir yang dipindai, teruskan membaca.

---

## Langkah 1: Siapkan Lingkungan c# ocr tutorial

Sebelum menulis kode apa pun, pastikan Anda memiliki alat yang tepat:

1. **.NET 6 SDK atau lebih baru** – Anda dapat mengunduhnya dari Microsoft.  
2. **Visual Studio 2022** (Community sudah cukup) atau editor pilihan Anda.  
3. **Paket NuGet Aspose.OCR** – jalankan `dotnet add package Aspose.OCR` di folder proyek Anda.

> **Pro tip:** Jika Anda menggunakan pipeline CI, tambahkan referensi paket ke file `.csproj` Anda sehingga proses build akan otomatis meng‑restore‑nya.

---

## Langkah 2: Memuat Gambar untuk OCR

Langkah nyata pertama dalam tutorial kami adalah mengambil gambar yang ingin Anda proses. Aspose OCR bekerja dengan format umum seperti PNG, JPEG, dan TIFF.

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **Mengapa ini penting:** Memuat gambar sebagai `OcrImage` memberi mesin akses ke data bitmap dan informasi DPI, yang meningkatkan akurasi pengenalan. Melewatkan langkah ini atau memberi file yang rusak akan menyebabkan pengecualian runtime.

---

## Langkah 3: Mengekstrak Teks dari Gambar

Sekarang kami menjalankan mesin OCR. Metode `Recognize` mengembalikan objek `OcrResult` yang kaya, berisi teks mentah, skor kepercayaan, dan detail tata letak.

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **Kasus khusus:** Jika Anda perlu memproses dokumen multibahasa, panggil `Recognize` dua kali dengan nilai `OcrLanguage` yang berbeda dan gabungkan hasilnya. Mesin ini thread‑safe, sehingga Anda bahkan dapat memparallelkan batch besar.

---

## Langkah 4: Menyerialkan Objek ke JSON – Format Output JSON

Objek `OcrResult` adalah kelas C# biasa, yang berarti kita dapat menyerahkannya ke `System.Text.Json`. Dengan mengaktifkan `WriteIndented`, output menjadi mudah dibaca manusia.

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **Apa yang Anda dapatkan:** String JSON yang terindentasi dengan rapi, mencakup teks yang dikenali, kepercayaan, dan tata letak halaman. Ini sempurna untuk logging, mengirim ke layanan web, atau menyimpan di basis data NoSQL.

---

## Langkah 5: Menampilkan dan (Opsional) Menyimpan JSON yang Diformat

Akhirnya, kami menampilkan JSON di console. Anda juga dapat menuliskannya ke file dengan `File.WriteAllText` jika lebih suka.

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**Output console yang diharapkan (dipotong untuk singkat):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

Jika mesin OCR tidak menemukan teks apa pun, bidang `Text` akan berisi string kosong dan `Confidence` akan bernilai `0`. Itu menjadi sinyal yang baik untuk memeriksa kembali kualitas gambar.

---

## Langkah 6: Contoh Kerja Lengkap

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel ke aplikasi console baru:

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

Jalankan program (`dotnet run` dari folder proyek) dan saksikan console mencetak representasi JSON yang terformat rapi dari faktur yang dipindai.

---

## Kesulitan Umum & Tips (Ekstra c# ocr tutorial)

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Bidang `Text` kosong** | Gambar berkontras rendah atau diputar. | Praproses gambar (tingkatkan kontras, deskew) atau gunakan `OcrEngine.ImagePreprocess`. |
| **`System.DllNotFoundException`** | Biner native Aspose OCR tidak ditemukan. | Pastikan paket NuGet ter‑restore dengan benar dan arsitektur runtime (x64/x86) cocok dengan OS Anda. |
| **Lag performa pada PDF besar** | OCR memproses setiap halaman secara berurutan. | Parallelkan dengan membuat instance `OcrEngine` terpisah per halaman (mesin thread‑safe). |
| **JSON terlalu besar** | Anda menyerialkan semua detail, termasuk bounding box. | Gunakan DTO yang hanya berisi `Text` dan `Confidence` sebelum serialisasi. |

> **Ingat:** Tujuan tutorial ini adalah menunjukkan alur bersih dari ujung‑ke‑ujung. Anda selalu dapat memotong JSON atau menambahkan metadata lain nanti.

---

## Kesimpulan

Anda baru saja menyelesaikan **c# ocr tutorial** yang memuat gambar, **mengekstrak teks dari gambar**, dan menghasilkan **format json output** dengan **menyerialkan objek ke json**. Langkah‑langkahnya sederhana, kodenya siap dijalankan, dan JSON‑nya terindentasi sempurna untuk konsumsi selanjutnya.

Apa selanjutnya? Coba ganti `OcrLanguage.English` dengan `OcrLanguage.French` atau proses folder berisi kwitansi dalam sebuah loop. Anda juga dapat mengeksplorasi penyimpanan JSON langsung ke Azure Blob Storage atau mengirimnya ke model machine‑learning.

Jika Anda menemui kendala, periksa kembali bahwa path gambar sudah benar dan lisensi Aspose OCR (jika Anda memilikinya) sudah dimuat sebelum memanggil `Recognize`. Selamat coding, semoga hasil OCR Anda selalu tajam! 

--- 

*Image illustrating the OCR flow (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}