---
category: general
date: 2026-05-06
description: Pelajari cara melakukan OCR pada file PDF menggunakan Aspose OCR di C#.
  Tutorial ini juga menunjukkan cara mengekstrak teks dari PDF dan memuat PDF untuk
  OCR.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF
- how to extract text from scanned PDF
- load PDF for OCR
language: id
og_description: Temukan cara melakukan OCR pada PDF menggunakan Aspose OCR di C#.
  Kode langkah demi langkah, penjelasan, dan tips untuk mengekstrak teks dari PDF
  secara efisien.
og_title: Lakukan OCR pada PDF dengan Aspose OCR – Panduan Lengkap
tags:
- Aspose OCR
- C#
- PDF processing
title: Lakukan OCR pada PDF dengan Aspose OCR – Panduan Lengkap
url: /id/net/text-recognition/perform-ocr-on-pdf-with-aspose-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada PDF dengan Aspose OCR – Panduan Lengkap

Pernah perlu **melakukan OCR pada PDF** tetapi tidak tahu harus mulai dari mana? Anda tidak sendirian. Dalam banyak proyek dunia nyata—misalnya pemrosesan faktur otomatis atau digitalisasi laporan arsip—kemampuan mengekstrak teks dari PDF yang dipindai sangat penting.  

Dalam tutorial ini kami akan membimbing Anda melalui solusi praktis yang tidak hanya **melakukan OCR pada PDF** menggunakan pustaka Aspose OCR, tetapi juga menunjukkan cara **mengekstrak teks dari PDF**, **memuat PDF untuk OCR**, dan bahkan menangani dokumen multibahasa. Pada akhir tutorial Anda akan memiliki program C# siap jalankan yang mengubah PDF yang dipindai menjadi teks yang dapat dicari dan diedit.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan Aspose OCR dalam proyek .NET.  
- Langkah‑langkah tepat untuk **memuat PDF untuk OCR** dan memberikannya ke mesin.  
- Cara memetakan bahasa yang berbeda ke halaman‑halaman individual—berguna ketika PDF mencampur bahasa Inggris, Prancis, dan Jerman.  
- Cara memverifikasi output dan mengatasi masalah umum.  

> **Pro tip:** Jika Anda bekerja dengan PDF berukuran besar, pertimbangkan memproses halaman secara paralel untuk mengurangi waktu eksekusi beberapa menit. Kami akan membahasnya nanti.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Core dan .NET Framework).  
- Lisensi Aspose OCR yang valid atau kunci evaluasi sementara.  
- Sebuah PDF yang dipindai bernama `multilang.pdf` ditempatkan di folder yang dapat Anda referensikan dari kode.  

Tidak ada paket pihak ketiga lain yang diperlukan.

---

## Langkah 1 – Instal Aspose OCR dan Buat Engine

Pertama, tambahkan paket NuGet Aspose.OCR ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

Setelah paket terpasang, Anda dapat menginstansiasi engine OCR. Objek ini adalah inti dari operasi; ia mengetahui cara membaca gambar, PDF, dan mengubahnya menjadi teks.

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Create an OCR engine instance – this is where we’ll perform OCR on PDF
var ocrEngine = new OcrEngine();
```

> **Mengapa ini penting:** Menginisialisasi engine sekali dan menggunakannya kembali pada setiap halaman mengurangi beban memori dan mempercepat proses.

---

## Langkah 2 – Muat Dokumen PDF untuk OCR

Engine dapat membuka PDF secara langsung, tetapi Anda harus memberi tahu file mana yang akan diproses. Inilah langkah **memuat PDF untuk OCR** yang sering terlewatkan oleh banyak pengembang.

```csharp
// Load the multi‑language PDF document from disk
ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");
```

Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya di mesin Anda. Jika file disematkan sebagai sumber daya, Anda juga dapat memuatnya dari stream.

> **Kasus khusus:** Jika PDF dilindungi kata sandi, panggil `ocrEngine.LoadPdf(path, password)` untuk memberikan kata sandi dekripsi.

---

## Langkah 3 – Pemetaan Bahasa ke Halaman (Opsional namun Kuat)

Seringkali PDF yang dipindai berisi halaman dalam bahasa yang berbeda. Secara default Aspose OCR mengasumsikan bahasa Inggris, yang menghasilkan hasil buruk pada halaman Prancis atau Jerman. Kami akan membuat kamus sederhana yang memberi tahu engine bahasa apa yang digunakan per halaman.

```csharp
// Define a language map: page index → OcrLanguage enum
var languageMap = new Dictionary<int, OcrLanguage>
{
    { 0, OcrLanguage.English }, // Page 1
    { 1, OcrLanguage.French },  // Page 2
    { 2, OcrLanguage.German }   // Page 3
};

// Provide the mapping via a lambda expression
ocrEngine.PageLanguageProvider = pageIndex =>
    languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;
```

> **Mengapa Anda melakukannya:** Menyediakan bahasa yang tepat secara dramatis meningkatkan akurasi, terutama untuk karakter aksen dan tanda baca khusus bahasa.

---

## Langkah 4 – Jalankan OCR dan Tangkap Hasilnya

Sekarang pekerjaan berat terjadi. Memanggil `Recognize()` memproses *semua* halaman sesuai peta bahasa yang baru saja kami tetapkan.

```csharp
// Run OCR on every page and collect the result
var recognitionResult = ocrEngine.Recognize();
```

Objek `recognitionResult` berisi properti `Text` yang menggabungkan teks yang dikenali dari setiap halaman.

---

## Langkah 5 – Keluarkan Teks yang Diekstrak

Akhirnya, kami cukup menuliskan teks gabungan ke konsol—atau Anda dapat menuliskannya ke file, basis data, atau sistem hilir lainnya.

```csharp
// Display the combined OCR output
Console.WriteLine(recognitionResult.Text);
```

Jika Anda lebih suka menyimpan ke file:

```csharp
System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
```

> **Tips verifikasi:** Buka `extracted_text.txt` yang dihasilkan dan cari kata‑kata yang dikenal dari masing‑masing bahasa. Jika aksen Prancis muncul rusak, periksa kembali peta bahasa Anda.

---

## Contoh Program Lengkap

Menggabungkan semua bagian, berikut program lengkap yang siap dijalankan. Salin‑tempel ke proyek konsol baru dan tekan **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑language PDF document
        // Make sure the path points to your actual file
        ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");

        // Step 3: Define which language should be used for each page
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },
            { 1, OcrLanguage.French },
            { 2, OcrLanguage.German }
        };

        // Step 4: Provide the language mapping to the engine
        ocrEngine.PageLanguageProvider = pageIndex =>
            languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;

        // Step 5: Run OCR on all pages
        var recognitionResult = ocrEngine.Recognize();

        // Step 6: Output the combined text from the document
        Console.WriteLine("=== OCR Output Start ===");
        Console.WriteLine(recognitionResult.Text);
        Console.WriteLine("=== OCR Output End ===");

        // Optional: Save to a file for later use
        System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
        Console.WriteLine("Text saved to extracted_text.txt");
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
=== OCR Output Start ===
Page 1 (English):
Invoice #12345
Date: 2024‑04‑30
...

Page 2 (French):
Facture #12345
Date : 30/04/2024
...

Page 3 (German):
Rechnung #12345
Datum: 30.04.2024
...
=== OCR Output End ===
Text saved to extracted_text.txt
```

---

## Menangani PDF Besar dan Penyempurnaan Performa

Jika PDF Anda berisi ratusan halaman, pertimbangkan penyesuaian berikut:

1. **Pemrosesan berkelompok** – Proses 50 halaman sekaligus, lalu tulis hasil menengah ke disk.  
2. **Paralelisme** – Gunakan `Parallel.ForEach` dengan instance `OcrEngine` terpisah (setiap engine aman untuk thread setelah inisialisasi).  
3. **Manajemen memori** – Panggil `ocrEngine.Dispose()` setelah setiap kelompok untuk membebaskan sumber daya native.

```csharp
Parallel.ForEach(pageIndices, pageIdx =>
{
    var localEngine = new OcrEngine();
    localEngine.LoadPdf("multilang.pdf", pageIdx, 1); // Load a single page
    // Apply language mapping as before …
    var result = localEngine.Recognize();
    // Append result.Text to a thread‑safe collection
    localEngine.Dispose();
});
```

---

## Kesalahan Umum & Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Solusi |
|--------|----------------------|--------|
| Karakter rusak pada halaman Prancis | Bahasa yang salah diatur | Pastikan `PageLanguageProvider` mengembalikan `OcrLanguage.French` untuk halaman tersebut. |
| File output kosong | PDF tidak dimuat (jalur salah) | Periksa jalur dan pastikan file tidak terkunci oleh proses lain. |
| Exception out‑of‑memory pada PDF sangat besar | Engine memuat seluruh PDF sekaligus | Gunakan overload `LoadPdf` untuk satu halaman atau proses secara berkelompok. |
| Proses lambat (> 5 menit untuk 100 halaman) | Eksekusi satu‑thread | Aktifkan pemrosesan paralel seperti contoh di atas. |

---

## Langkah Selanjutnya – Lebih dari OCR Dasar

Sekarang Anda dapat **melakukan OCR pada PDF** dan **mengekstrak teks dari PDF**, Anda mungkin ingin:

- **Membuat PDF yang dapat dicari** – Gunakan Aspose.PDF untuk menyematkan teks OCR kembali ke PDF asli, menjadikannya dapat dicari.  
- **Ekstraksi data** – Terapkan ekspresi reguler untuk mengambil nomor faktur, tanggal, atau total dari teks yang diekstrak.  
- **Integrasi dengan AI** – Kirim output OCR ke model bahasa (misalnya Azure OpenAI) untuk rangkuman atau klasifikasi.  

Semua ekstensi ini tetap bergantung pada kemampuan inti **memuat PDF untuk OCR**, jadi fondasinya sudah Anda miliki.

---

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **melakukan OCR pada PDF** menggunakan Aspose OCR dalam C#. Dari instalasi pustaka, memuat PDF, menetapkan bahasa per halaman, menjalankan engine pengenalan, hingga akhirnya **mengekstrak teks dari PDF** dan menyimpannya, tutorial ini memberikan solusi mandiri yang siap produksi.  

Silakan bereksperimen dengan pemrosesan paralel, kombinasi bahasa berbeda, atau bahkan menggabungkan teks OCR dengan pustaka pemrosesan dokumen lainnya. Jika Anda menemui kendala, periksa tabel pemecahan masalah di atas atau tinggalkan komentar—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}