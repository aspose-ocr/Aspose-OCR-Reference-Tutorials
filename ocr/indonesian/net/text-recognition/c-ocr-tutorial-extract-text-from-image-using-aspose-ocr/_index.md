---
category: general
date: 2026-03-26
description: Tutorial OCR C# yang menunjukkan cara mengekstrak teks dari gambar, mengenali
  teks dari JPEG, dan memuat gambar untuk OCR – termasuk dukungan Cyrillic.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from jpeg
- load image for ocr
- recognize cyrillic text
language: id
og_description: Tutorial OCR C# yang memandu Anda melalui proses memuat gambar untuk
  OCR, mengenali teks dari JPEG, dan mengekstrak teks Sirilik dalam beberapa langkah
  mudah.
og_title: tutorial OCR c# – Ekstrak Teks dari Gambar dengan Aspose OCR
tags:
- OCR
- C#
- Aspose
- ImageProcessing
title: Tutorial OCR C# – Ekstrak Teks dari Gambar Menggunakan Aspose OCR
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-image-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial c# ocr – Ekstrak Teks dari Gambar Menggunakan Aspose OCR

Pernah membutuhkan **c# ocr tutorial** yang benar‑benar membawa Anda dari JPEG kosong ke teks Unicode yang dapat dibaca? Mungkin Anda sedang membangun alat pengarsipan dokumen, pemindai struk, atau hanya penasaran tentang cara mengambil teks dari gambar. Bagaimanapun, Anda berada di tempat yang tepat. Dalam panduan ini kami akan menunjukkan cara **extract text from image** file, **recognize text from jpeg** aset, dan bahkan menangani skenario **recognize cyrillic text** yang rumit—tanpa panggilan ke cloud.

Kami akan menggunakan Aspose.OCR, sebuah perpustakaan sepenuhnya offline yang menyertakan modul bahasa yang dapat Anda arahkan ke disk. Pada akhir tutorial ini Anda akan memiliki aplikasi konsol mandiri yang memuat gambar untuk OCR, menjalankan mesin, dan mencetak hasilnya ke konsol. Tanpa layanan eksternal, tanpa kunci API—hanya C# murni.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework)
- Visual Studio 2022 atau IDE apa pun yang Anda sukai
- Paket NuGet Aspose.OCR (`Aspose.OCR`) dan folder `Aspose.OCR.Resources` yang cocok
- Gambar JPEG yang berisi karakter Cyrillic (atau bahasa apa pun yang ingin Anda uji)

Jika Anda belum memiliki salah satu dari itu, dapatkan paket NuGet melalui Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

dan unduh sumber daya bahasa dari situs web Aspose, ekstrak ke folder seperti `C:\OCR\Aspose.OCR.Resources`.

Sekarang, mari kita mulai.

## Langkah 1: Muat Sumber Daya OCR – load image for ocr

Hal pertama yang dibutuhkan mesin adalah jalur ke modul bahasa. Anggap saja Anda memberi tahu OCR di mana kamusnya berada.

```csharp
using Aspose.OCR;
using Aspose.OCR.Resources;

// Point to the folder that contains the language modules
ResourceManager.SetLocalResourcesPath(@"C:\OCR\Aspose.OCR.Resources");
```

> **Pro tip:** Gunakan jalur absolut selama pengembangan. Saat Anda mendistribusikan aplikasi, pertimbangkan untuk menyematkan sumber daya atau menyalinnya di samping executable.

## Langkah 2: Pilih Bahasa – recognize cyrillic text

Aspose mendukung puluhan bahasa, tetapi Anda harus memilih yang Anda perlukan. Untuk teks Cyrillic kami menggunakan `OcrLanguage.CyrillicExtended`. Jika Anda hanya membutuhkan karakter Latin, ganti dengan `OcrLanguage.English`.

```csharp
// Create the OCR engine and set the language
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.CyrillicExtended   // This enables Cyrillic recognition
};
```

Mengapa ini penting? Mesin memuat classifier khusus bahasa; memilih yang salah dapat secara dramatis menurunkan akurasi.

## Langkah 3: Muat JPEG – recognize text from jpeg

Sekarang kami benar‑benar memuat gambar yang ingin dipindai. Aspose dapat membaca format umum seperti JPEG, PNG, BMP, dan TIFF.

```csharp
// Load the image file (replace with your own path)
var ocrImage = OcrImage.FromFile(@"C:\OCR\Samples\cyrillic_doc.jpg");
```

Jika gambar berukuran besar, Anda mungkin ingin menurunkan skala sebelum memberikannya ke mesin—ini mempercepat pemrosesan dan mengurangi penggunaan memori.

## Langkah 4: Jalankan Pengenalan – extract text from image

Dengan mesin yang dikonfigurasi dan gambar berada di memori, langkah pengenalan cukup satu baris.

```csharp
// Perform the OCR operation
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

Di balik layar, mesin menjalankan rangkaian pra‑pemrosesan (penghilangan noise, binarisasi) dan kemudian mencocokkan pola visual dengan model bahasa yang dipilih.

## Langkah 5: Tampilkan Hasil – extract text from image

Akhirnya, kami menampilkan string yang dikenali. Dalam aplikasi dunia nyata Anda mungkin menulisnya ke file, basis data, atau memasukkannya ke indeks pencarian.

```csharp
// Print the extracted text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Output yang diharapkan** (asumsi gambar contoh berisi “Привет мир!”):

```
=== OCR Output ===
Привет мир!
```

Jika Anda melihat karakter yang kacau, periksa kembali bahwa Anda telah memilih bahasa yang tepat dan gambar tidak terlalu berisik.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap disalin‑tempel. Simpan sebagai `Program.cs` di dalam proyek konsol baru dan jalankan.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Resources;

class OfflineOcrDemo
{
    static void Main()
    {
        // Step 1: Point the OCR engine to the folder that contains the language modules
        ResourceManager.SetLocalResourcesPath(@"C:\OCR\Aspose.OCR.Resources");

        // Step 2: Create the OCR engine and select the required language (Cyrillic Extended)
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.CyrillicExtended
        };

        // Step 3: Load the image that contains the text to be recognized
        var ocrImage = OcrImage.FromFile(@"C:\OCR\Samples\cyrillic_doc.jpg");

        // Step 4: Perform the recognition operation
        OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 5: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Catatan:** Ganti jalur dengan lokasi sebenarnya di mesin Anda. Program ini bekerja offline; tidak diperlukan koneksi internet setelah sumber daya tersedia.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika gambar saya PNG bukan JPEG?

Aspose.OCR memperlakukan PNG sama seperti JPEG. Cukup ubah ekstensi file di `FromFile`. Langkah **recognize text from jpeg** bekerja untuk format apa pun yang didukung.

### Bagaimana cara meningkatkan akurasi pada pemindaian berkualitas rendah?

- Pra‑proses gambar (tingkatkan kontras, luruskan) menggunakan `ocrImage.AdjustContrast(1.2)` atau metode serupa.
- Gunakan `OcrEngine.PreprocessImage` sebelum memanggil `Recognize`.
- Pilih bahasa yang cocok dengan skrip; untuk campuran Latin/Cyrillic Anda dapat mengatur `Language = OcrLanguage.Multilingual`.

### Bisakah saya mengekstrak hanya angka atau tanggal?

Ya. Setelah Anda memiliki `ocrResult.Text`, terapkan ekspresi reguler untuk menyaring bagian yang Anda butuhkan. OCR itu sendiri mengembalikan string mentah; parsing selanjutnya menjadi tanggung jawab Anda.

### Apakah mungkin menjalankannya di Linux?

Tentu saja. Aspose.OCR bersifat lintas‑platform. Cukup instal runtime .NET di mesin Linux Anda dan arahkan `SetLocalResourcesPath` ke folder yang sesuai.

## Tips Pro untuk Produksi

- **Cache the OcrEngine**: Membuat mesin baru untuk setiap permintaan menambah beban. Simpan sebagai singleton jika Anda memproses banyak gambar.
- **Thread safety**: Mesin tidak thread‑safe secara default. Baik kunci di sekitar `Recognize` atau buat mesin terpisah per thread.
- **Memory management**: Buang objek `OcrImage` setelah digunakan (`ocrImage.Dispose()`) untuk membebaskan buffer native.
- **Logging**: Tangkap `ocrResult.Confidence` (jika tersedia) untuk mendeteksi pemindaian dengan kepercayaan rendah dan memicu fallback.

## Kesimpulan

Anda kini memiliki **c# ocr tutorial** yang memandu Anda melalui setiap langkah untuk **load image for ocr**, **recognize text from jpeg**, **extract text from image**, dan **recognize cyrillic text** menggunakan Aspose.OCR. Kode contoh siap dijalankan, dan penjelasannya menunjukkan mengapa setiap baris penting—bukan hanya bagaimana.

Dari sini Anda dapat bereksperimen dengan bahasa lain, mengintegrasikan OCR ke dalam API web, atau memasukkan string yang diekstrak ke dalam mesin pencari. Kemungkinannya seluas gambar yang Anda berikan.

Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa dokumentasi Aspose untuk opsi konfigurasi yang lebih mendalam. Selamat coding, dan semoga gambar Anda selalu jernih!

![tangkapan layar tutorial c# ocr yang menunjukkan output konsol teks yang diekstrak](/images/ocr-demo.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}