---
category: general
date: 2026-05-06
description: Pelajari cara mengenali teks dari gambar menggunakan Aspose OCR di C#.
  Ekstrak teks dari kwitansi, muat gambar untuk OCR, dan lihat contoh lengkap Aspose
  OCR.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for OCR
- Aspose OCR example
language: id
og_description: Pelajari cara mengenali teks dari gambar dengan Aspose OCR, mengekstrak
  teks dari struk, dan memuat gambar untuk OCR dalam panduan singkat langkah demi
  langkah.
og_title: Mengenali teks dari gambar di C# – Tutorial Lengkap Aspose OCR
tags:
- C#
- OCR
- Aspose
title: Mengenali teks dari gambar dalam C# – Tutorial Lengkap Aspose OCR
url: /id/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar di C# – Tutorial Lengkap Aspose OCR

Pernah membutuhkan untuk **recognize text from image** tetapi tidak yakin pustaka mana yang harus dipilih? Anda tidak sendirian—banyak pengembang mengalami hal yang sama ketika mencoba mengambil angka dari struk atau memindai formulir. Kabar baiknya, Aspose OCR membuat seluruh proses menjadi sangat mudah, dan dalam tutorial ini kami akan membimbing Anda melalui **complete Aspose OCR example** yang memungkinkan Anda **extract text from receipt** dalam beberapa baris kode C#.

Dalam beberapa menit ke depan Anda akan belajar cara **load image for OCR**, menentukan wilayah tepat yang berisi total jumlah, menjalankan mesin, dan akhirnya menampilkan hasilnya. Tanpa referensi samar ke dokumen eksternal, tanpa bagian yang hilang—semua yang Anda butuhkan untuk copy‑paste dan jalankan ada di sini. Sedikit pengaturan, beberapa langkah, dan Anda akan dapat mengenali teks dari file gambar secara langsung.

> **Apa yang akan Anda dapatkan**  
> * Aplikasi konsol C# yang dapat dijalankan dan mengenali teks dari file gambar.  
> * Pemahaman mengapa Anda mungkin ingin membatasi OCR pada persegi panjang tertentu (kecepatan dan akurasi).  
> * Tips menangani kasus tepi umum seperti struk yang buram atau pemindaian yang diputar.  

---

## Prerequisites

Sebelum kita mulai, pastikan Anda memiliki:

| Persyaratan | Mengapa penting |
|-------------|----------------|
| .NET 6.0 SDK (atau lebih baru) | Aspose OCR dikirim sebagai pustaka .NET Standard 2.0 / .NET 5+, sehingga runtime terbaru mana pun dapat digunakan. |
| Visual Studio 2022 (atau VS Code) | IDE yang nyaman mempercepat proses debugging, tetapi editor apa pun yang dapat mengompilasi C# sudah cukup. |
| **Aspose.OCR for .NET** NuGet package | Ini adalah pustaka inti yang benar‑benarnya **recognises text from image**. |
| Contoh gambar struk (`receipt.jpg`) | Kami akan menggunakan file ini untuk mendemonstrasikan **extract text from receipt**. |

Anda dapat menginstal paket NuGet dengan perintah berikut:

```bash
dotnet add package Aspose.OCR
```

Setelah selesai, Anda siap untuk mulai **load image for OCR**.

---

## Step 1: Load the image for OCR

Hal pertama yang perlu Anda lakukan adalah mengarahkan mesin ke file yang ingin Anda analisis. Di sinilah kata kunci sekunder **load image for OCR** muncul secara alami.

```csharp
using Aspose.OCR;
using System.Drawing;

// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// Load the receipt image – replace the path with your own file location
ocrEngine.SetImage(@"C:\Images\receipt.jpg");
```

> **Pro tip:** Jika gambar Anda berada di folder proyek, Anda dapat menggunakan path relatif seperti `ocrEngine.SetImage("receipt.jpg");`. Pastikan file tersebut disalin ke direktori output (`Copy to Output Directory = PreserveNewest`).

Metode `SetImage` menerima format apa pun yang dapat didekode oleh System.Drawing (JPEG, PNG, BMP, dll.), sehingga Anda tidak terbatas pada satu jenis file.

---

## Step 2: Define the region of interest – **extract text from receipt**

Memindai seluruh gambar membuang siklus CPU dan dapat menimbulkan noise. Dengan memberi tahu Aspose OCR secara tepat di mana total jumlah berada, Anda meningkatkan kecepatan dan akurasi. Inilah bagian di mana kami **extract text from receipt**.

```csharp
// Define a rectangle that covers the total amount on the receipt
// (x, y, width, height) – adjust these numbers for your own layout
var roi = new Rectangle(150, 500, 300, 80);
ocrEngine.SetRegionOfInterest(roi);
```

> **Mengapa persegi panjang?**  
> Mesin OCR bekerja pada grid piksel. Ketika Anda membatasinya pada wilayah tertentu, ia mengabaikan segala hal lainnya—tidak ada lagi karakter acak dari logo toko atau baris header.

Jika Anda tidak yakin dengan koordinat yang tepat, Anda dapat menggunakan penampil gambar apa pun yang menampilkan posisi piksel (misalnya Paint.NET) untuk memperkirakan angka-angka tersebut.

---

## Step 3: Run the engine – **recognize text from image** (primary keyword)

Sekarang keajaiban terjadi. Anda memberi tahu Aspose untuk benar‑benarnya membaca piksel di dalam persegi panjang yang baru saja Anda definisikan.

```csharp
// Perform the recognition
OcrResult result = ocrEngine.Recognize();
```

`OcrResult` berisi teks mentah, skor kepercayaan, dan bahkan kotak pembatas untuk setiap kata. Untuk demo singkat kami hanya akan mencetak teks biasa.

```csharp
Console.WriteLine("Total amount detected: " + result.Text);
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
Total amount detected: $23.45
```

Jika output terlihat berantakan, periksa kembali koordinat ROI atau coba tingkatkan resolusi gambar.

---

## Step 4: Handling the result – polishing the **Aspose OCR example**

Solusi yang kuat melakukan lebih dari sekadar menumpahkan string ke konsol. Di bawah ini ada helper kecil yang memangkas spasi, menghapus baris baru yang tidak diinginkan, dan memvalidasi bahwa nilai yang diekstrak tampak seperti jumlah uang.

```csharp
static string CleanAmount(string raw)
{
    // Remove any non‑numeric characters except dot and comma
    var cleaned = new string(raw
        .Where(c => char.IsDigit(c) || c == '.' || c == ',')
        .ToArray());

    // Normalize decimal separator to dot
    cleaned = cleaned.Replace(',', '.');

    // If we end up with an empty string, return a friendly message
    return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
}

// ...

string amount = CleanAmount(result.Text);
Console.WriteLine($"Parsed amount: ${amount}");
```

Helper ini menunjukkan **Aspose OCR example** yang realistis yang dapat Anda masukkan ke dalam sistem penagihan yang lebih besar.

---

## Step 5: Full runnable program – the ultimate **extract text from receipt** demo

Menggabungkan semuanya memberi Anda satu file yang dapat langsung di‑copy‑paste. Simpan sebagai `Program.cs` dan jalankan `dotnet run`.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the image for OCR
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage(@"C:\Images\receipt.jpg");   // <-- adjust path

        // 2️⃣ Define the region that holds the total amount
        var roi = new Rectangle(150, 500, 300, 80);
        ocrEngine.SetRegionOfInterest(roi);

        // 3️⃣ Run the engine – recognize text from image
        OcrResult result = ocrEngine.Recognize();

        // 4️⃣ Clean up the output
        string amount = CleanAmount(result.Text);
        Console.WriteLine($"Total amount detected: ${amount}");
    }

    // Helper that sanitises the OCR output
    static string CleanAmount(string raw)
    {
        var cleaned = new string(raw
            .Where(c => char.IsDigit(c) || c == '.' || c == ',')
            .ToArray());

        cleaned = cleaned.Replace(',', '.');
        return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
    }
}
```

**Expected output**

```
Total amount detected: $23.45
```

Jika gambar struk lebih gelap atau teksnya miring, Anda mungkin melihat sesuatu seperti `Total amount detected: 23,45`. Metode `CleanAmount` akan menormalkannya menjadi format desimal standar.

---

## Common pitfalls when you **recognize text from image**

### 1. Koordinat ROI Salah
Jika persegi panjang terlalu kecil, mesin akan memotong karakter; terlalu besar dan Anda memperkenalkan noise kembali. Gunakan alat visual untuk menyetel angka-angka tersebut, atau deteksi batas struk secara programatis dengan pustaka pemrosesan gambar sederhana (misalnya OpenCV).

### 2. Pemindaian resolusi rendah
Akurasi OCR turun drastis di bawah 150 dpi. Jika Anda mengontrol proses pemindaian, targetkan setidaknya 300 dpi. Jika Anda terpaksa menggunakan file beresolusi rendah, coba `ocrEngine.SetResolution(300);` sebelum memanggil `Recognize()`.

### 3. Struk miring atau berputar
Aspose OCR dapat memutar otomatis, tetapi Anda harus mengaktifkannya:

```csharp
ocrEngine.SetAutoRotate(true);
```

### 4. Pengaturan bahasa
Bahasa default adalah Inggris. Jika struk Anda berisi alfabet lain, atur bahasa secara eksplisit:

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
```

---

## Edge cases & variations – extending the **Aspose OCR example**

* **Multiple fields:** Ingin mengambil tanggal dan jumlah pajak juga? Cukup ulangi langkah ROI dengan persegi panjang baru dan panggil `Recognize()` lagi (atau gunakan mesin yang sama setelah mereset ROI).  
* **Batch processing:** Bungkus logika dalam loop `foreach (var file in Directory.GetFiles(@"C:\Receipts"))` untuk menangani puluhan file secara otomatis.  
* **Async execution:** Metode `Recognize` bersifat sinkron, tetapi Anda dapat memindahkannya ke thread latar belakang dengan `Task.Run` jika membangun aplikasi UI.

---

## Visual reference

![recognize text from image example](/images/ocr-demo.png "Screenshot showing Aspose OCR result – recognize text from image")

*Screenshot menunjukkan output konsol setelah menjalankan program lengkap.*

---

## Conclusion

Kami baru saja **recognize text from image** menggunakan Aspose OCR, melewati cara **load image for OCR**, dan membangun alur kerja **extract text from receipt** yang praktis yang dapat Anda masukkan ke proyek .NET mana pun. **Aspose OCR example** lengkap hanya beberapa baris kode, namun mencakup skenario paling umum: pemilihan ROI, pembersihan hasil, dan penanganan jebakan tipikal.

Langkah selanjutnya? Coba ganti persegi panjang dengan rutin deteksi dinamis, bereksperimen dengan bahasa lain, atau integrasikan output ke basis data untuk pelacakan pengeluaran otomatis. Langit adalah batasnya, dan dengan fondasi yang kini Anda miliki, memperluasnya akan menjadi mudah.

Ada pertanyaan atau struk sulit yang menolak bekerja sama?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}