---
category: general
date: 2026-03-13
description: Cara melakukan OCR di C# dan mengekstrak teks dari gambar menggunakan
  OcrEngine. Pelajari cara mengubah gambar menjadi teks dengan cepat melalui panduan
  lengkap langkah demi langkah.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: id
og_description: Bagaimana melakukan OCR di C#? Panduan ini menunjukkan cara mengekstrak
  teks dari gambar, mengonversi gambar menjadi teks, dan membaca teks dari gambar
  menggunakan OcrEngine.
og_title: Cara Melakukan OCR di C# – Ekstrak Teks dari Gambar
tags:
- OCR
- C#
- Image Processing
title: Cara Melakukan OCR di C# – Ekstrak Teks dari Gambar
url: /id/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Ekstrak Teks dari Gambar

Cara melakukan OCR di C# adalah pertanyaan umum bagi pengembang yang perlu **membaca teks dari file gambar**. Dalam panduan ini kami akan menunjukkan cara mengekstrak teks dari gambar menggunakan pustaka `OcrEngine`, mengubah foto menjadi string yang dapat dicari hanya dengan beberapa baris kode.  

Jika Anda pernah menatap faktur yang dipindai, catatan tulisan tangan, atau tangkapan layar dan bertanya *“bagaimana cara mengekstrak teks?”*, Anda berada di tempat yang tepat. Kami juga akan membahas cara mengonversi gambar ke teks untuk pemrosesan batch, sehingga Anda dapat mengotomatisasi seluruh alur kerja.

---

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

- **.NET 6.0 atau lebih baru** (API yang kami gunakan bekerja dengan .NET Standard 2.0+)
- Paket NuGet **OcrEngine** (atau pustaka OCR kompatibel lain yang menyediakan properti `Language`, `Image`, `Recognize`, dan `Text`)
- File gambar contoh, misalnya `hindi_page.jpg`, ditempatkan di folder yang dapat direferensikan dari kode
- Pemahaman dasar tentang sintaks C# – tidak memerlukan trik lanjutan

Itu saja. Tanpa layanan eksternal, tanpa kunci API, hanya pustaka lokal yang melakukan pekerjaan berat.

---

## Implementasi Langkah‑per‑Langkah

Di bawah ini kami membagi proses menjadi bagian‑bagian logis. Setiap bagian memiliki judul yang jelas, cuplikan kode singkat, dan penjelasan **mengapa** langkah tersebut penting—bukan hanya **apa** yang dilakukannya.

### Cara Melakukan OCR – Langkah Inti

Alur keseluruhan dapat diringkas dalam lima tindakan:

1. **Buat** instance mesin OCR
2. **Pilih** bahasa yang ingin dikenali
3. **Muat** gambar yang berisi teks
4. **Jalankan** algoritma pengenalan
5. **Baca** teks yang diekstrak

Itulah kerangka dasarnya; bagian‑bagian berikut akan mengembangkannya.

---

### Ekstrak Teks dari Gambar – Buat Mesin

Pertama, kita memerlukan objek yang dapat berkomunikasi dengan mesin OCR.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*Mengapa ini penting:* Menginstansiasi `OcrEngine` mengalokasikan semua buffer internal dan memuat DLL native yang diperlukan untuk analisis gambar. Melewatkan langkah ini akan membuat Anda tidak memiliki pengenal yang dapat dipanggil nanti.

> **Tip pro:** Jika Anda berencana memproses banyak gambar secara berurutan, pertahankan instance `ocrEngine` yang sama tetap hidup. Ia akan menggunakan kembali model bahasa dan mempercepat pemanggilan berikutnya.

---

### Konversi Gambar ke Teks – Pilih Bahasa

Akurasi OCR sangat bergantung pada model bahasa yang Anda berikan. Untuk Hindi, Tamil, atau skrip lain, atur properti `Language` sesuai.

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*Mengapa ini penting:* Mesin menggunakan set karakter dan model statistik khusus bahasa. Memberikan bahasa yang salah biasanya menghasilkan output yang berantakan, terutama untuk skrip non‑Latin.

> **Kasus khusus:** Jika Anda memerlukan dukungan multi‑bahasa, beberapa pustaka memungkinkan Anda menetapkan daftar fallback, misalnya `ocrEngine.Language = Language.Multilingual;`.

---

### Baca Teks dari Gambar – Muat Gambar Sumber

Sekarang kami mengarahkan mesin ke file yang berisi teks visual.

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*Mengapa ini penting:* `ImageStream.FromFile` mengubah file mentah menjadi format bitmap yang dapat dipahami inti OCR. Memberikan file yang rusak atau format yang tidak didukung (seperti SVG) akan menyebabkan pengecualian.

> **Waspada:** Gambar berukuran besar dapat mengonsumsi banyak memori. Jika Anda memproses pemindaian resolusi tinggi, pertimbangkan menurunkan skala dengan `Image.Resize` sebelum mengirimkannya ke mesin.

---

### Konversi Gambar ke Teks – Jalankan Pengenalan

Dengan mesin siap dan gambar dimuat, kami akhirnya memanggil proses OCR.

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*Mengapa ini penting:* `Recognize` memicu serangkaian langkah internal—pra‑pemrosesan, segmentasi, klasifikasi karakter, dan pasca‑pemrosesan. Pemanggilan ini bersifat blocking, artinya thread menunggu hingga teks siap.

> **Catatan kinerja:** Pada desktop biasa, mengenali halaman 300 dpi memakan < 1 detik. Pada server, Anda mungkin ingin menjalankannya dalam tugas latar belakang agar UI tidak membeku.

---

### Cara Ekstrak Teks – Ambil Hasil

Setelah pengenalan selesai, mesin menyimpan output teks polos di properti `Text`.

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*Mengapa ini penting:* Properti `Text` memberikan string UTF‑8 bersih yang dapat Anda tulis ke file, masukkan ke basis data, atau teruskan ke pipeline NLP selanjutnya.

> **Output yang diharapkan:** Untuk contoh halaman Hindi, Anda mungkin melihat sesuatu seperti  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> (Output sebenarnya tergantung pada kualitas gambar dan model bahasa.)

---

## Pertimbangan Tambahan untuk Proyek Dunia Nyata

Berikut beberapa skenario “bagaimana jika” yang kemungkinan akan Anda temui saat **mengekstrak teks dari gambar** dalam produksi.

### Menangani Banyak Gambar dalam Loop

Jika Anda perlu **mengonversi gambar ke teks** untuk puluhan file, bungkus langkah‑langkah tersebut dalam loop `foreach` dan gunakan kembali `ocrEngine` yang sama:

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### Menghadapi Scan Berkualitas Rendah

- **Pra‑proses** dengan binarisasi (`Image.Binarize()`), penghilangan noise, atau deskewing.
- **Tingkatkan DPI** saat memindai (300 dpi adalah patokan aman).
- **Pilih model bahasa** yang mendukung ligatur skrip (misalnya Devanagari untuk Hindi).

### Membaca Teks dari Gambar di Web

Ketika gambar berasal dari URL, unduh terlebih dahulu ke stream memori:

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### Keamanan Thread dan Paralelisme

Sebagian besar pustaka OCR **tidak** thread‑safe secara default. Jika Anda berencana **membaca teks dari gambar** secara bersamaan, buat instance `OcrEngine` terpisah per thread, atau gunakan antrian produsen‑konsumen untuk menyerialkan akses.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut aplikasi konsol siap‑jalankan yang mendemonstrasikan **cara melakukan OCR**, **mengekstrak teks dari gambar**, dan **membaca teks dari gambar** dalam satu program terpadu.

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**Apa yang akan Anda lihat:** Konsol mencetak kalimat Hindi yang diekstrak dari `hindi_page.jpg`, diikuti konfirmasi bahwa file teks telah dibuat. Jika gambar bersih, output akan hampir identik dengan teks tercetak aslinya.

---

## Kesimpulan

Anda kini tahu **cara melakukan OCR** di C# dari awal hingga akhir, cara **mengekstrak teks dari gambar**, **mengonversi gambar ke teks**, dan **membaca teks dari gambar** menggunakan alur kerja `OcrEngine` yang sederhana. Pola lima langkah—buat, atur bahasa, muat, kenali, baca—mencakup mayoritas kasus penggunaan, dan tip tambahan membantu Anda menangani pekerjaan batch, scan berkualitas rendah, serta sumber berbasis web.

Siap untuk tantangan berikutnya? Coba ganti bahasa ke Inggris, gunakan halaman PDF yang dirender sebagai gambar, atau sambungkan output OCR ke pipeline indeks pencarian. Langit adalah batasnya setelah Anda menguasai dasar‑dasar OCR di C#.

Punya pertanyaan atau gambar sulit yang tidak mau bekerja? Tinggalkan komentar di bawah, dan mari kita selesaikan bersama. Selamat coding!  

![contoh cara melakukan OCR](images/ocr-example.png "contoh cara melakukan OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}