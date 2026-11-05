---
category: general
date: 2026-03-23
description: Ekstrak teks dari formulir dengan cepat menggunakan Aspose OCR. Pelajari
  cara mengenali teks dalam area dan menangani bagian OCR dari gambar dengan contoh
  lengkap C#.
draft: false
keywords:
- extract text from form
- recognize text in area
- ocr part of image
- Aspose OCR C#
- region based OCR
language: id
og_description: Ekstrak teks dari formulir menggunakan Aspose OCR. Tutorial ini menunjukkan
  cara mengenali teks dalam area dan memproses bagian OCR gambar dalam C#.
og_title: Ekstrak Teks dari Formulir dengan Aspose OCR – Panduan Lengkap
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Ekstrak Teks dari Formulir dengan Aspose OCR – Panduan Langkah demi Langkah
url: /id/net/text-recognition/extract-text-from-form-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Formulir dengan Aspose OCR – Panduan Langkah‑per‑Langkah

Pernahkah Anda perlu **mengekstrak teks dari formulir** tetapi seluruh halaman berantakan? Anda bukan satu-satunya—para pengembang terus berjuang dengan PDF, faktur yang dipindai, atau survei tulisan tangan di mana hanya satu bidang yang penting. Kabar baiknya? Anda dapat memberi tahu Aspose OCR untuk melihat hanya bagian yang Anda butuhkan, mengabaikan sisanya.  

Dalam panduan ini kami akan menunjukkan secara tepat cara **mengenali teks di area** dari formulir yang dipindai, mengambil nilai yang diperlukan, dan membiarkan sisanya dari gambar tidak tersentuh. Pada akhir tutorial Anda akan memiliki program C# siap‑jalankan yang menangani **bagian ocr gambar** yang Anda butuhkan, tanpa menggunakan layanan eksternal apa pun.

## Apa yang Akan Anda Dapatkan dari Tutorial Ini

- Sebuah aplikasi konsol C# lengkap yang dapat dijalankan dan mengekstrak sebuah bidang dari gambar formulir.  
- Penjelasan jelas mengapa menargetkan persegi panjang lebih cepat dan lebih akurat.  
- Tips untuk menangani hasil kosong, pengaturan DPI yang berbeda, dan formulir multi‑halaman.  
- Daftar periksa cepat agar Anda dapat menyesuaikan kode ke proyek Anda dalam hitungan menit.

**Prasyarat** – Anda memerlukan .NET 6 atau yang lebih baru, Visual Studio 2022 (atau IDE apa pun yang Anda suka), dan koneksi internet pada pertama kali untuk mengunduh paket Aspose.OCR NuGet. Tidak ada pustaka lain yang diperlukan.

---

## Ekstrak Teks dari Formulir – Menyiapkan Proyek

Sebelum kita menyelam ke kode, pastikan lingkungan sudah siap. Langkah-langkahnya sengaja dibuat sederhana, karena keajaiban sesungguhnya terjadi setelah mesin OCR diinstansiasi.

1. **Buat proyek konsol baru**  
   ```bash
   dotnet new console -n FormOcrDemo
   cd FormOcrDemo
   ```

2. **Tambahkan Aspose.OCR via NuGet**  
   ```bash
   dotnet add package Aspose.OCR
   ```

3. **Salin formulir yang dipindai** ke dalam folder proyek dan beri nama `form.png`.  
   (Jika file Anda berupa PDF, ekspor halaman yang Anda butuhkan sebagai PNG terlebih dahulu—Aspose OCR bekerja paling baik dengan gambar raster.)

Itu saja. Sisa tutorial mengasumsikan ketiga langkah tersebut telah selesai.

![extract text from form example](form-region.png "extract text from form example")

*Teks alt gambar: contoh ekstrak teks dari formulir yang menunjukkan area yang disorot pada dokumen yang dipindai.*

---

## Kenali Teks di Area – Mendefinisikan Wilayah yang Diinginkan

Kenapa repot-repot dengan persegi panjang? Bayangkan Anda memiliki pemindaian 2 MB dari seluruh pengembalian pajak. Menjalankan OCR pada seluruh gambar membuang siklus CPU dan dapat menghasilkan positif palsu dari bidang yang tidak terkait. Dengan mempersempit ruang lingkup ke koordinat tepat yang memuat nilai target, Anda:

- **Mengurangi waktu pemrosesan** hingga 80 % untuk gambar besar.  
- **Meningkatkan akurasi** karena mesin mengabaikan grafik yang mengganggu.  
- **Menyederhanakan pasca‑pemrosesan**—Anda tahu persis teks apa yang diharapkan.

Persegi panjang didefinisikan oleh empat angka: `x`, `y`, `width`, dan `height`. Nilai-nilai ini diukur dalam piksel dari sudut kiri‑atas gambar. Jika Anda tidak yakin di mana bidang berada, buka gambar di Paint, arahkan kursor ke sudut kiri‑atas untuk membaca nilai X/Y, lalu seret untuk mengukur lebar dan tinggi.

---

## Bagian OCR Gambar – Memuat Formulir dan Mengonfigurasi Mesin

Setelah wilayah jelas, mari bicarakan mesin itu sendiri. `OcrEngine` adalah inti dari Aspose OCR. Ia secara otomatis mendeteksi bahasa, menangani koreksi kemiringan, dan mengembalikan string teks biasa. Anda juga dapat menyesuaikan propertinya—seperti `Resolution` atau `Language`—jika formulir Anda menggunakan skrip non‑Latin. Untuk kebanyakan formulir berbahasa Inggris, nilai default sudah cukup.

Di bawah ini adalah **program lengkap, mandiri** yang menggabungkan semuanya. Silakan salin‑tempel ke `Program.cs` dan tekan **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing; // for Rectangle

class RegionExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine (using ensures disposal)
        // -------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // -------------------------------------------------
            // Step 2: Load the image that contains the form
            // -------------------------------------------------
            // ImageStream.FromFile reads the file into Aspose's internal format
            // Replace "YOUR_DIRECTORY/form.png" with the actual path if needed
            ocrEngine.Image = ImageStream.FromFile("form.png");

            // -------------------------------------------------
            // Step 3: Define the region that holds the desired field
            // -------------------------------------------------
            // (x, y, width, height) – adjust these numbers for your form
            Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);

            // -------------------------------------------------
            // Step 4: Recognize text only inside the defined region
            // -------------------------------------------------
            bool success = ocrEngine.Recognize(regionOfInterest);
            string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;

            // -------------------------------------------------
            // Step 5: Display the extracted field value
            // -------------------------------------------------
            Console.WriteLine("Field value: " + (string.IsNullOrEmpty(recognizedText)
                ? "[No text detected]"
                : recognizedText));
        }

        // Keep the console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

### Output yang Diharapkan

Jika persegi panjang dengan benar melingkupi bidang yang berisi “Invoice # 12345”, konsol akan mencetak:

```
Field value: Invoice # 12345
```

Jika wilayah kosong atau OCR gagal, Anda akan melihat:

```
Field value: [No text detected]
```

---

## Penelusuran Kode Langkah‑per‑Langkah

Di bawah ini kami memecah program menjadi potongan‑potongan kecil, menjelaskan **alasan** di balik setiap baris, dan menunjukkan bagian yang mungkin perlu Anda sesuaikan.

### Langkah 1: Instal Aspose.OCR via NuGet *(H3)*

```bash
dotnet add package Aspose.OCR
```

*Mengapa?* Paket NuGet mengemas mesin OCR native, file data bahasa, dan wrapper .NET tipis. Tanpanya, kelas `OcrEngine` tidak ada.

### Langkah 2: Inisialisasi OcrEngine *(H3)*

```csharp
using (OcrEngine ocrEngine = new OcrEngine())
```

*Mengapa menggunakan `using`?* `OcrEngine` menyimpan sumber daya tidak terkelola (DLL native, buffer gambar). Pernyataan `using` menjamin mereka dibebaskan, mencegah kebocoran memori pada layanan yang berjalan lama.

### Langkah 3: Muat Gambar Formulir *(H3)*

```csharp
ocrEngine.Image = ImageStream.FromFile("form.png");
```

*Mengapa `ImageStream`?* Ia mengabstraksi I/O file dan secara otomatis mengonversi format umum (PNG, JPEG, TIFF) ke representasi bitmap internal yang diperlukan oleh Aspose OCR.

### Langkah 4: Tentukan Wilayah untuk Mengekstrak Teks *(H3)*

```csharp
Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);
```

*Mengapa `Rectangle`?* Mesin OCR menerima `System.Drawing.Rectangle`. Empat parameter memungkinkan Anda menandai bidang tepat, memotong sisanya dari halaman.

*Tip:* Jika Anda perlu mendukung banyak bidang, simpan setiap persegi panjang dalam `Dictionary<string, Rectangle>` dan lakukan loop di atasnya.

### Langkah 5: Jalankan Pengenalan dan Dapatkan Hasil *(H3)*

```csharp
bool success = ocrEngine.Recognize(regionOfInterest);
string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;
```

*Mengapa memeriksa `success`?* OCR dapat gagal karena berbagai alasan—gambar buram, bahasa tidak didukung, atau wilayah kosong. Memeriksa boolean mencegah Anda bekerja dengan data usang.

### Langkah 6: Tangani Kasus Tepi dan Jebakan Umum *(H3)*

- **DPI Berbeda:** Jika pemindaian beresolusi rendah (< 150 DPI), tingkatkan `ocrEngine.Image.DpiX` dan `ocrEngine.Image.DpiY` sebelum memanggil `Recognize`.  
- **Banyak Halaman:** Untuk PDF multi‑halaman, ekstrak setiap halaman sebagai PNG terpisah dan ulangi logika persegi panjang per halaman.  
- **Teks Non‑Inggris:** Atur `ocrEngine.Language = Language.Thai;` (atau bahasa lain yang didukung) sebelum pengenalan.  
- **Pengurangan Noise:** `ocrEngine.Image.Filters.Add(new GaussianBlurFilter(1.2f));` dapat meningkatkan hasil pada pemindaian berbutir.

---

## Melangkah Lebih Jauh – Variasi Dunia Nyata

### Mengekstrak Banyak Bidang dari Formulir yang Sama

Jika Anda perlu mengambil “Name”, “Date”, dan “Amount” dari satu dokumen, buat koleksi:

```csharp
var fields = new Dictionary<string, Rectangle>
{
    { "Name",   new Rectangle(50, 200, 300, 60) },
    { "Date",   new Rectangle(400, 200, 200, 60) },
    { "Amount", new Rectangle(650, 200, 250, 60) }
};

foreach (var kvp in fields)
{
    bool ok = ocrEngine.Recognize(kvp.Value);
    Console.WriteLine($"{kvp.Key}: {(ok ? ocrEngine.Text.Trim() : "[Not found]")}");
}
```

### Mengintegrasikan dengan Database

Setelah mengekstrak, Anda mungkin ingin menyimpan hasilnya di SQL Server:

```csharp
using (var conn = new SqlConnection(connectionString))
{
    conn.Open();
    var cmd = new SqlCommand(
        "INSERT INTO FormResults (FieldName, FieldValue) VALUES (@name, @value)", conn);
    cmd.Parameters.AddWithValue("@name", "InvoiceNumber");
    cmd.Parameters.AddWithValue("@value", recognizedText);
    cmd.ExecuteNonQuery();
}
```

### Mengotomatisasi di Server

Jika Anda berencana menjalankan ini sebagai layanan latar belakang, bungkus logika dalam metode `async` dan gunakan `Task.Run` untuk menjaga UI tetap responsif. Ingat untuk mengatur `ocrEngine.ParallelProcessing = true;` untuk percepatan multi‑core.

---

## Kesimpulan

Anda kini memiliki cara yang solid dan siap produksi untuk **mengekstrak teks dari formulir** gambar menggunakan Aspose OCR. Dengan memfokuskan pada persegi panjang tertentu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}