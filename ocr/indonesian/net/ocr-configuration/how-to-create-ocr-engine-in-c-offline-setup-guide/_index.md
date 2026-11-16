---
category: general
date: 2026-03-04
description: Pelajari cara membuat OCR di C# tanpa internet. Panduan langkah demi
  langkah ini juga menunjukkan cara menjalankan OCR secara offline menggunakan sumber
  daya lokal.
draft: false
keywords:
- how to create OCR
- how to run OCR
- offline OCR C#
- local OCR resources
- OcrEngine setup
language: id
og_description: Cara membuat OCR di C# tanpa panggilan jaringan. Ikuti panduan ini
  untuk mempelajari cara menjalankan OCR secara lokal menggunakan LocalResourceProvider.
og_title: Cara Membuat Mesin OCR di C# – Pengaturan Offline
tags:
- OCR
- C#
- Offline Processing
title: Cara Membuat Mesin OCR di C# – Panduan Pengaturan Offline
url: /id/net/ocr-configuration/how-to-create-ocr-engine-in-c-offline-setup-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat Mesin OCR di C# – Panduan Penyiapan Offline

Pernah bertanya‑tanya **bagaimana cara membuat OCR** yang tidak pernah terhubung ke internet? Mungkin Anda sedang membangun aplikasi desktop yang aman, atau Anda sekadar tidak suka panggilan jaringan yang tidak stabil. Bagaimanapun, Anda menginginkan mesin OCR yang sepenuhnya berada di mesin klien.  

Kabar baik? Ini cukup sederhana. Dalam tutorial ini kami akan membahas **bagaimana cara membuat OCR** langkah demi langkah, lalu menunjukkan **bagaimana cara menjalankan OCR** dalam mode offline menggunakan `LocalResourceProvider`. Pada akhir tutorial Anda akan memiliki potongan kode C# yang berdiri sendiri dan dapat disisipkan ke proyek .NET mana pun—tanpa layanan eksternal.

## Apa yang Akan Anda Pelajari

- Prasyarat minimal untuk penyiapan OCR offline.  
- Cara menginstansiasi `OcrEngine` dan menunjukannya ke folder sumber daya lokal.  
- Mengapa menggunakan penyedia lokal menghilangkan latensi jaringan dan meningkatkan privasi.  
- Jebakan umum (file yang hilang, jalur yang salah) dan cara menghindarinya.  

Semua kode yang Anda butuhkan sudah disertakan, plus langkah verifikasi cepat sehingga Anda dapat melihat mesin beraksi segera setelah menyalin‑tempel.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

1. **.NET 6.0 atau lebih baru** – perpustakaan OCR yang akan kita gunakan menargetkan .NET Standard 2.0, jadi runtime terbaru mana pun dapat dipakai.  
2. **Folder dengan sumber daya OCR** – paket bahasa, file data terlatih, dan biner pendukung lainnya. Jika belum memilikinya, unduh paket yang sesuai dari bundel offline vendor dan ekstrak ke `C:\MyApp\OcrResources`.  
3. **Visual Studio 2022** (atau IDE lain yang Anda sukai).  

Itu saja—tidak ada paket NuGet yang mengakses internet saat runtime.

![Diagram showing offline OCR flow – how to create OCR engine without network calls](offline-ocr-diagram.png)

*Teks alt gambar: diagram cara membuat mesin OCR offline*

---

## Langkah 1: Tambahkan Referensi Perpustakaan OCR

Pertama, tambahkan referensi assembly SDK OCR ke proyek Anda. Jika Anda memiliki file `.dll` dari vendor, klik kanan **References → Add Reference** dan telusuri ke `OcrSdk.dll`. Alternatifnya, jika SDK tersedia sebagai paket NuGet yang mendukung mode offline, jalankan:

```bash
dotnet add package OcrSdk --version 3.2.1
```

> **Tips pro:** Kunci nomor versi. Memperbarui nanti dapat memperkenalkan perubahan yang memecah kompatibilitas pada jalur sumber daya offline.

---

## Langkah 2: Buat Instance Mesin OCR  

Sekarang kita akan benar‑benarnya **bagaimana cara membuat OCR** dengan membangun objek `OcrEngine`. Objek ini adalah titik masuk untuk semua tugas pengenalan.

```csharp
using OcrSdk;               // Namespace provided by the OCR library
using OcrSdk.Resources;    // Contains LocalResourceProvider

// ...

// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Mengapa kita memerlukan mesin khusus? `OcrEngine` menyimpan konfigurasi, cache model bahasa, dan mengelola pool thread. Menginstansiasinya sekali dan menggunakannya kembali pada banyak pemindaian jauh lebih efisien daripada membuat objek baru untuk setiap gambar.

---

## Langkah 3: Arahkan Mesin ke Folder Sumber Daya Lokal  

Berikut bagian krusial yang memungkinkan Anda **bagaimana cara menjalankan OCR** tanpa menyentuh web. Kami menetapkan `LocalResourceProvider` yang membaca data bahasa dari direktori di disk.

```csharp
// Step 3: Configure the engine to use offline resources
string resourcePath = @"C:\MyApp\OcrResources";
ocrEngine.ResourceProvider = new LocalResourceProvider(resourcePath);
```

**Apa yang terjadi di balik layar?** `LocalResourceProvider` mengimplementasikan antarmuka yang sama dengan penyedia berbasis cloud default, tetapi membaca file `.dat` dari `resourcePath`. Trik ini menjamin semua panggilan OCR berikutnya tetap lokal.

> **Waspada:** Jika jalurnya salah atau folder tidak berisi file yang diperlukan (`eng.traineddata`, `ocr_config.xml`, dll.), mesin akan melempar `ResourceNotFoundException`. Selalu validasi folder sebelum menetapkannya.

---

## Langkah 4: Verifikasi Mesin Siap  

Pemeriksaan cepat menyelamatkan Anda dari debugging di kemudian hari. Panggil `IsReady` (atau properti setara) dan tampilkan hasilnya.

```csharp
// Step 4: Verify the engine can locate its resources
if (ocrEngine.IsReady)
{
    Console.WriteLine("✅ OCR engine is ready – offline mode confirmed.");
}
else
{
    Console.WriteLine("❌ OCR engine failed to load resources. Check the path and files.");
    return;
}
```

Anda seharusnya melihat tanda centang hijau di konsol. Jika yang muncul tanda silang merah, periksa kembali bahwa `resourcePath` mengarah ke folder yang berisi paket bahasa.

---

## Langkah 5: Jalankan OCR pada Gambar Contoh  

Akhirnya, mari **bagaimana cara menjalankan OCR** pada sebuah gambar. Letakkan gambar bernama `sample.png` di folder sumber daya yang sama (atau lokasi yang dapat diakses) dan berikan ke mesin.

```csharp
// Step 5: Perform OCR on a local image
string imagePath = Path.Combine(resourcePath, "sample.png");

// Load the image (the SDK may provide its own Image class)
var ocrImage = OcrImage.FromFile(imagePath);

// Run recognition – this call is completely offline
OcrResult result = ocrEngine.Recognize(ocrImage);

// Output the recognized text
Console.WriteLine("🖋️ Recognized Text:");
Console.WriteLine(result.Text);
```

**Output yang diharapkan** (asumsi `sample.png` berisi frasa “Hello OCR!”):

```
🖋️ Recognized Text:
Hello OCR!
```

Jika hasilnya kosong, pastikan gambar jelas dan model bahasa untuk Inggris (`eng`) ada di `OcrResources`.

---

## Kasus Tepi & Jebakan Umum  

| Situasi | Apa yang Terjadi | Cara Memperbaikinya |
|-----------|--------------|---------------|
| **File bahasa hilang** | `ResourceNotFoundException` pada langkah 3 | Pastikan `eng.traineddata` (atau bahasa target Anda) ada di folder. |
| **Gambar rusak** | `OcrException` dengan pesan “Unsupported format” | Konversi gambar ke PNG atau BMP sebelum memberikannya ke mesin. |
| **Banyak thread** | Kondisi balapan jika Anda membuat banyak mesin | Gunakan satu instance `OcrEngine` saja; ia thread‑safe untuk panggilan `Recognize` bersamaan. |
| **Jalur mengandung spasi** | Mesin gagal menemukan sumber daya | Gunakan string verbatim (`@"C:\Path With Spaces\OcrResources"`) atau escape backslash. |

---

## Contoh Lengkap yang Berfungsi  

Berikut program konsol siap‑jalankan yang menggabungkan semua langkah. Salin kode ke proyek `.csproj` baru dan tekan **F5**.

```csharp
// File: Program.cs
using System;
using System.IO;
using OcrSdk;
using OcrSdk.Resources;

namespace OfflineOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Point to local resources (offline mode)
            string resourcePath = @"C:\MyApp\OcrResources";
            ocrEngine.ResourceProvider = new LocalResourceProvider(resourcePath);

            // 3️⃣ Verify the engine can load resources
            if (!ocrEngine.IsReady)
            {
                Console.WriteLine("❌ Engine failed to initialize. Check your resource folder.");
                return;
            }
            Console.WriteLine("✅ Engine initialized successfully.");

            // 4️⃣ Load a test image
            string imagePath = Path.Combine(resourcePath, "sample.png");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            var ocrImage = OcrImage.FromFile(imagePath);

            // 5️⃣ Run OCR – entirely offline
            OcrResult result = ocrEngine.Recognize(ocrImage);

            // 6️⃣ Show the result
            Console.WriteLine("\n🖋️ Recognized Text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

**Menjalankan program** akan mencetak pesan konfirmasi dan teks yang diekstrak, membuktikan bahwa Anda kini tahu **bagaimana cara membuat OCR** dan **bagaimana cara menjalankan OCR** tanpa pernah meninggalkan mesin.

---

## Kesimpulan  

Kami telah membahas semua yang perlu Anda ketahui tentang **bagaimana cara membuat OCR** dalam proyek C# dan mendemonstrasikan **bagaimana cara menjalankan OCR** sepenuhnya offline. Dengan mengonfigurasi `LocalResourceProvider`, Anda menghilangkan latensi jaringan, melindungi data sensitif, dan memperoleh kontrol penuh atas siklus hidup OCR.  

Siap untuk tantangan berikutnya? Coba ganti model bahasa Inggris dengan bahasa lain, atau bereksperimen dengan langkah pra‑pemrosesan gambar yang berbeda (konversi ke grayscale, deskewing) untuk meningkatkan akurasi. Pola yang sama tetap berlaku—cukup arahkan mesin ke folder sumber daya yang berbeda.

Jika Anda menemui kendala, tinjau kembali tabel kasus tepi di atas atau tinggalkan komentar; selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}