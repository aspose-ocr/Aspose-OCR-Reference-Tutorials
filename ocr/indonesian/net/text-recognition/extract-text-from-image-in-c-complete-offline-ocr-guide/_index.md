---
category: general
date: 2026-03-18
description: Ekstrak teks dari gambar menggunakan Aspose OCR di C#. Pelajari cara
  mengekstrak teks, menjalankan pengenalan OCR, dan mengenali teks Cyrillic tanpa
  internet.
draft: false
keywords:
- extract text from image
- how to extract text
- run OCR recognition
- recognize cyrillic text
- offline OCR with Aspose
language: id
og_description: Ekstrak teks dari gambar dengan Aspose OCR. Panduan langkah demi langkah
  untuk menjalankan pengenalan OCR, cara mengekstrak teks, dan mengenali teks Cyrillic
  secara offline.
og_title: Ekstrak Teks dari Gambar di C# – Tutorial OCR Offline
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Ekstrak Teks dari Gambar di C# – Panduan OCR Offline Lengkap
url: /id/net/text-recognition/extract-text-from-image-in-c-complete-offline-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar – Panduan OCR Offline Lengkap

Pernahkah Anda perlu **mengekstrak teks dari gambar** tetapi khawatir tentang latensi jaringan atau pembatasan lisensi? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika aplikasi mereka harus bekerja di lingkungan sandbox, namun tetap membutuhkan OCR yang handal. Kabar baik? Dengan Aspose OCR Anda dapat menjalankan seluruh pipeline secara lokal, **mengekstrak teks dari gambar** tanpa pernah menyentuh internet.

Dalam tutorial ini kami akan membahas contoh praktis yang menunjukkan **cara mengekstrak teks**, menyiapkan mesin offline, **menjalankan pengenalan OCR**, dan bahkan **mengenali teks Cyrillic**. Pada akhir tutorial Anda akan memiliki aplikasi konsol C# siap‑jalankan yang mencetak string yang terdeteksi langsung ke konsol.

## Apa yang Anda Butuhkan

- .NET 6.0 SDK (atau versi .NET terbaru apa pun)  
- Visual Studio 2022 atau VS Code – mana pun yang Anda suka  
- Paket NuGet Aspose.OCR untuk .NET  
- Sebuah folder yang berisi file model Aspose OCR (unduh sekali dari portal Aspose)  
- File gambar yang mencakup karakter Bahasa Inggris dan Cyrillic (misalnya `cyrillic_doc.jpg`)

Tidak ada layanan eksternal, tidak ada unduhan tersembunyi saat runtime – semuanya berada di disk Anda.

## Langkah 1: Instal Aspose.OCR dan Siapkan Sumber Daya

Pertama, tambahkan paket NuGet Aspose.OCR ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

Selanjutnya, buat folder bernama `AsposeOCRResources` di suatu tempat pada mesin Anda dan salin file model yang Anda unduh dari Aspose ke dalamnya. Mesin OCR akan mencari paket bahasa di direktori ini, jadi pastikan jalurnya benar.

> **Pro tip:** Simpan folder sumber daya di samping file `.csproj` Anda; ini menyederhanakan penanganan jalur selama pengembangan.

## Langkah 2: Bangun Mesin OCR Offline

Sekarang kami akan menginstansiasi mesin dan mengarahkannya ke folder sumber daya. Ini adalah langkah penting yang memungkinkan kami **menjalankan pengenalan OCR** sepenuhnya secara offline.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell the engine where the language models live
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // 3️⃣ Load the languages you need – English and Cyrillic
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);
```

Mengapa memuat bahasa secara eksplisit? Karena kami memberi tahu mesin untuk tetap offline; ia tidak akan menghubungi server Aspose untuk mengambil paket yang hilang. Jika Anda lupa memuat sebuah bahasa, semua karakter dari skrip tersebut akan diabaikan.

## Langkah 3: Berikan Gambar ke Mesin

Dengan mesin siap, kini kami menyediakan gambar yang ingin diproses. Helper `ImageStream.FromFile` membaca file ke dalam format yang dipahami mesin OCR.

```csharp
        // 4️⃣ Load the target image (make sure the path points to your file)
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");
```

Jika gambar Anda besar, pertimbangkan untuk mengubah ukurannya terlebih dahulu guna meningkatkan kecepatan dan akurasi. Mesin OCR bekerja paling baik dengan DPI sekitar 300.

## Langkah 4: Jalankan Proses Pengenalan

Memanggil `Recognize` melakukan pekerjaan berat. Metode ini mengembalikan objek `OcrResult` yang berisi string yang diekstrak, skor kepercayaan, dan lainnya.

```csharp
        // 5️⃣ Run the OCR recognition
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Di balik layar, Aspose mem-parsing bitmap, menjalankan jaringan saraf khusus bahasa, dan menyatukan karakter-karakter. Karena kami memuat bahasa Inggris dan Cyrillic, dokumen campuran skrip ditangani dengan mulus.

## Langkah 5: Tampilkan Teks yang Diekstrak

Akhirnya, kami menampilkan hasilnya. Dalam aplikasi nyata Anda mungkin menyimpannya di basis data atau mengirimnya ke layanan lain, tetapi untuk demo ini kami hanya akan mencetaknya.

```csharp
        // 6️⃣ Show the extracted text on the console
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Menjalankan program seharusnya menghasilkan sesuatu seperti:

```
=== OCR Output ===
This is an English line.
Это строка на кириллице.
```

Jika Anda melihat karakter yang kacau, periksa kembali bahwa paket bahasa Cyrillic ditempatkan dengan benar di folder sumber daya dan gambar tidak terlalu buram.

![contoh ekstrak teks dari gambar](extract_text_image.png "ekstrak teks dari gambar")

*Teks alt gambar: ekstrak teks dari gambar – hasil OCR menampilkan baris Bahasa Inggris dan Cyrillic.*

## Menangani Masalah Umum

### Paket Bahasa Hilang

Jika Anda mendapatkan pengecualian dengan pesan “Language data not found,” mesin tidak dapat menemukan file model. Verifikasi `ResourcesPath` dan pastikan folder berisi `english.dat` dan `cyrillic.dat` (atau file dengan nama serupa).

### Skor Kepercayaan Rendah

Kadang-kadang mesin OCR akan mengembalikan kepercayaan rendah untuk karakter tertentu, terutama jika gambar memiliki noise. Anda dapat meningkatkan akurasi dengan:

- Mengonversi gambar ke skala abu-abu sebelum memberi ke mesin  
- Menerapkan filter median untuk mengurangi bintik-bintik  
- Memastikan teks ter-align secara horizontal (putar jika diperlukan)

### Gambar Besar

Memproses foto 10 MP dapat menjadi lambat. Turunkan skala ke lebar maksimum 2000 px sambil mempertahankan rasio aspek; mesin tetap akan menangkap sebagian besar karakter dengan akurat.

## Memperluas Contoh

- **Pemrosesan batch:** Bungkus logika pengenalan dalam loop yang mengiterasi semua file dalam sebuah direktori.  
- **Format output:** `OcrResult` juga menyediakan koleksi `TextLines` yang mencakup kotak pembatas—berguna untuk menyorot teks dalam aplikasi UI.  
- **Bahasa tambahan:** Cukup panggil `LoadLanguage` dengan nilai enum lain yang didukung (mis., `Language.French`).  

Semua ekstensi ini tetap mematuhi prinsip **cara mengekstrak teks**—cukup muat paket bahasa yang sesuai dan biarkan mesin melakukan sisanya.

## Ringkasan Kode Sumber Lengkap

Berikut adalah program lengkap yang siap disalin‑tempel. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya pada mesin Anda.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Point the engine to the folder that contains OCR model files
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // Step 3: Load the languages you need (no automatic download will occur)
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);

        // Step 4: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");

        // Step 5: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 6: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Simpan ini sebagai `Program.cs`, jalankan `dotnet run`, dan lihat konsol mencetak teks yang diambil mesin dari gambar Anda. Itu saja—Anda telah berhasil **mengekstrak teks dari gambar** secara offline.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **mengekstrak teks dari gambar** menggunakan Aspose OCR dalam skenario sepenuhnya offline. Panduan ini menunjukkan **cara mengekstrak teks**, mendemonstrasikan **menjalankan pengenalan OCR**, dan membuktikan bahwa Anda dapat **mengenali teks Cyrillic** bersama Bahasa Inggris tanpa panggilan jaringan apa pun.  

Dari menyiapkan paket NuGet hingga menangani kasus tepi seperti paket bahasa yang hilang, Anda kini memiliki fondasi yang kuat untuk membangun fitur berbasis OCR dalam aplikasi .NET apa pun.  

Apa selanjutnya? Coba beri masukan PDF, pindai beberapa halaman, atau integrasikan output dengan indeks pencarian. Langit adalah batasnya setelah Anda menguasai OCR offline.

Selamat coding, dan semoga gambar Anda selalu jernih!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}