---
category: general
date: 2026-02-09
description: Ekstrak teks dari gambar dengan cepat menggunakan C# dengan mengatur
  paralelisme maksimum untuk OCR batch – pelajari cara mengonversi halaman yang dipindai,
  menangani OCR pada banyak gambar, dan membaca teks PNG secara efisien.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: id
og_description: Ekstrak teks gambar di C# dengan mengatur paralelisme maksimum. Tutorial
  ini menunjukkan cara mengonversi halaman yang dipindai, menjalankan OCR gambar secara
  berganda, dan membaca teks PNG dengan Aspose OCR.
og_title: Ekstrak gambar teks dari PNG dengan C# – Panduan OCR Batch Lengkap
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Ekstrak teks gambar dari PNG dengan C# – OCR batch menggunakan Aspose OCR
url: /id/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ekstrak gambar teks dari PNG dengan C# – Batch OCR menggunakan Aspose OCR

Pernah perlu **mengekstrak gambar teks** dari folder berisi PNG yang dipindai tetapi terhambat pada pertanyaan “bagaimana cara membuatnya cepat?”? Anda tidak sendirian. Dalam banyak proyek dunia nyata, pengembang harus **mengatur max parallelism** sehingga puluhan halaman diproses dalam hitungan detik, bukan menit.  

Dalam panduan ini kami akan menelusuri contoh lengkap yang dapat dijalankan, yang **mengonversi halaman yang dipindai**, menjalankan **OCR pada banyak gambar**, dan akhirnya **membaca teks png** tanpa kesulitan. Tidak ada tautan “lihat dokumentasi” yang samar—hanya kode yang dapat Anda salin‑tempel, penjelasan mengapa setiap baris penting, dan tips untuk menghindari jebakan umum.

> **Pro tip:** Jika Anda sudah menggunakan Aspose OCR di tempat lain, Anda akan melihat kelas `OcrEngine` yang sama muncul di sini, tetapi kami akan menyesuaikan konfigurasinya untuk pemrosesan paralel yang sesungguhnya.

---

## Apa yang Anda Butuhkan

- **.NET 6+** (atau .NET Framework 4.6+). API berfungsi sama, tetapi runtime yang lebih baru memberikan penanganan thread yang lebih baik.  
- **Aspose.OCR for .NET** – instal melalui NuGet: `Install-Package Aspose.OCR`.  
- Sebuah folder yang berisi beberapa PNG hasil pemindaian (`page1.png`, `page2.png`, …).  
- IDE atau editor yang Anda sukai (Visual Studio, Rider, VS Code…).

Itu saja. Tidak ada layanan tambahan, tidak ada kunci cloud, hanya pemrosesan lokal murni.

---

## ekstrak gambar teks – Mengatur Max Parallelism untuk Batch OCR

Saat Anda memicu OCR pada beberapa file, mesin secara default akan menggunakan satu thread. Itu aman tetapi sangat lambat. Dengan mengonfigurasi `MaxDegreeOfParallelism` Anda memberi tahu mesin berapa banyak thread yang boleh dijalankan secara bersamaan.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Mengapa 4?**  
Empat adalah titik optimal pada kebanyakan laptop modern—cukup inti untuk membuat CPU sibuk, tetapi tidak terlalu banyak sehingga proses lain kelaparan sumber daya. Jika Anda menjalankannya di server dengan 16 core, naikkan angka menjadi 12 atau 14 untuk percepatan yang terasa.

---

## Convert scanned pages – Membangun Koleksi Image Stream

Aspose mengharapkan setiap gambar sebagai `ImageStream`. Helper `FromFile` membaca file, menyimpannya di memori, dan menyerahkannya ke mesin OCR. Anda juga dapat memberi `MemoryStream` jika gambar berasal dari basis data atau respons HTTP.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Kasus tepi:** Jika ada file yang hilang atau rusak, `FromFile` akan melempar `FileNotFoundException`. Bungkus konstruksi dalam `try/catch` jika Anda mengharapkan input yang tidak dapat diandalkan.

---

## multiple image ocr – Melakukan Batch OCR

Sekarang pekerjaan berat terjadi. `RecognizeBatch` memunculkan hingga jumlah thread yang Anda atur sebelumnya, memproses setiap gambar, dan mengembalikan daftar objek `OcrResult`.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Di balik layar, setiap thread memuat gambarnya, menjalankan jaringan saraf, dan mengekstrak teks polos. Urutan hasil sesuai dengan urutan daftar input, sehingga Anda dapat dengan aman memetakan halaman 1 → hasil 0, dan seterusnya.

---

## read png text – Menampilkan Konten yang Diekstrak

Akhirnya kami melintasi hasil dan mencetak teks polos ke konsol. Di sinilah Anda dapat menyalurkan output ke file, basis data, atau bahkan layanan NLP downstream.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Output Konsol yang Diharapkan

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Jika Anda melihat bagian kosong, periksa kembali bahwa PNG bukan gambar putih murni—OCR membutuhkan kontras.

---

## Tips Praktis & Jebakan Umum

| Situasi | Apa yang Harus Dilakukan |
|-----------|------------|
| **Tekanan memori** pada batch besar | Proses gambar dalam potongan 10‑20 file, lalu panggil `GC.Collect()` jika Anda melihat lonjakan. |
| **Deteksi bahasa yang salah** | Setel `ocrEngine.Configuration.Language = OcrLanguage.English;` (atau bahasa target Anda) sebelum memanggil `RecognizeBatch`. |
| **Performa lambat meski paralel** | Pastikan SSD Anda tidak membatasi I/O; baca semua file ke memori terlebih dahulu (seperti yang kami lakukan dengan `ImageStream.FromFile`). |
| **Karakter hilang** | Tingkatkan `ocrEngine.Configuration.DPI = 300;` untuk pemrosesan resolusi lebih tinggi. |

---

## Memperluas Contoh – Dari PNG ke PDF atau DOCX

Jika pada akhirnya Anda perlu **mengonversi halaman yang dipindai** menjadi PDF yang dapat dicari, cukup masukkan `ocrResults[i].PlainText` ke dalam perpustakaan PDF (misalnya, Aspose.PDF) dan lapiskan teks sebagai lapisan tak terlihat. Trik paralelisme yang sama juga berlaku di sana.

---

## Kode Sumber Lengkap (Siap Salin‑Tempel)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Simpan sebagai `BatchExample.cs`, jalankan `dotnet run`, dan saksikan konsol Anda terisi dengan teks yang sebelumnya tersembunyi di dalam PNG tersebut.

---

## Ringkasan Visual

![extract text images example](images/ocr-batch.png){alt="contoh ekstrak gambar teks"}

Diagram menunjukkan alur: **File PNG → koleksi ImageStream → OcrEngine (max parallelism) → hasil OCR → Konsol / penyimpanan downstream**.

---

## Kesimpulan

Anda kini memiliki resep menyeluruh, ujung‑ke‑ujung, untuk **mengekstrak gambar teks** di C# sambil **mengatur max parallelism**, **mengonversi halaman yang dipindai**, menangani **OCR pada banyak gambar**, dan **membaca teks png** secara efisien. Kode bersifat mandiri, penjelasan mencakup “bagaimana” dan “mengapa”, serta tips menjaga Anda dari sakit kepala umum.

Apa selanjutnya? Coba ganti daftar PNG dengan loop dinamis `Directory.GetFiles`, bereksperimen dengan jumlah thread yang berbeda, atau alirkan output ke PDF yang dapat dicari. Pola yang sama dapat diskalakan ke ratusan halaman dengan hampir tidak ada tambahan kode.

Punya pertanyaan atau kasus tepi yang rumit? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}