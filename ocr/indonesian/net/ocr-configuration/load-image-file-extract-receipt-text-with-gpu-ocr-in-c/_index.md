---
category: general
date: 2026-02-14
description: Muat file gambar dan ekstrak teks dari struk menggunakan mesin Aspose
  OCR GPU. Pelajari cara mengatur memori GPU maksimum, mengonfigurasi memori GPU,
  dan menjalankan OCR pada gambar secara efisien.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: id
og_description: Muat file gambar dan ekstrak teks dari struk menggunakan mesin OCR
  GPU Aspose. Panduan ini menunjukkan cara mengatur memori maksimum GPU dan menjalankan
  OCR pada gambar di C#.
og_title: Muat File Gambar & Ekstrak Teks Resi dengan OCR GPU di C#
tags:
- C#
- OCR
- Aspose
- GPU
title: Muat File Gambar & Ekstrak Teks Resi dengan OCR GPU di C#
url: /id/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Muat File Gambar & Ekstrak Teks Resi dengan GPU OCR di C#

Pernah perlu **load image file** dan mengambil teks tepat dari sebuah resi tetapi terhambat pada langkah OCR? Anda bukan satu-satunya. Dalam banyak aplikasi dunia nyata—pelacak pengeluaran, sistem inventaris, atau bahkan bot pemindaian resi sederhana—kemampuan untuk dengan cepat membaca gambar resi dapat menjadi pengubah permainan.  

Berita baiknya? Dengan mesin yang dipercepat GPU milik Aspose.OCR Anda dapat **load image file**, **set max GPU memory**, dan **run OCR on image** semuanya dalam beberapa baris kode C# yang rapi. Di bawah ini kami akan menjelaskan seluruh proses, mulai dari mengonfigurasi GPU hingga mencetak teks polos yang diekstrak.

## Apa yang Akan Anda Pelajari

* **Load image file** dari disk menggunakan `ImageStream` milik Aspose.
* **Configure GPU memory** sehingga mesin tidak pernah menghabiskan RAM lebih dari yang Anda izinkan.
* **Run OCR on image** dan mengambil setiap karakter pada resi.
* Menangani jebakan umum—seperti kesalahan out‑of‑memory atau pemindaian yang buram.
* Memverifikasi output dan menyesuaikan pengaturan untuk akurasi yang lebih baik.

Tidak ada layanan eksternal, tidak ada trik tersembunyi—hanya kode C# murni yang dapat Anda masukkan ke dalam proyek .NET 6+ apa pun.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* .NET 6 SDK atau yang lebih baru terpasang.
* Lisensi Aspose.OCR yang valid (atau Anda dapat menggunakan mode evaluasi gratis).
* Paket NuGet `Aspose.OCR` dan `Aspose.OCR.Gpu` telah ditambahkan ke proyek Anda.
* Sebuah contoh gambar resi (`receipt.png`) siap di disk.

Jika ada yang belum familiar, jeda sejenak dan instal paket-paketnya:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Itu saja—tidak diperlukan pustaka native tambahan karena dukungan GPU sudah terintegrasi langsung dalam paket NuGet.

---

## Muat File Gambar dan Siapkan Mesin GPU

Hal pertama yang harus Anda lakukan adalah **load image file** ke dalam `ImageStream`. Objek ini mengabstraksi detail sistem file dan memberikan mesin OCR representasi bersih dalam memori.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Mengapa ini penting:**  
*Loading the image file* melalui `ImageStream.FromFile` menjamin bahwa mesin melihat data piksel yang tepat, mempertahankan DPI dan kedalaman warna. Melewatkan langkah ini atau memberi aliran yang rusak akan menyebabkan OCR kehilangan karakter atau melemparkan pengecualian.

> **Pro tip:** Jika Anda menangani file yang diunggah pengguna, bungkus pemanggilan `FromFile` dalam blok try‑catch dan validasi ukuran file terlebih dahulu. Gambar besar dapat membebani memori GPU jika Anda belum **configure GPU memory** dengan benar.

---

## Atur Memori GPU Maksimum untuk Kinerja Optimal

Sumber daya GPU sangat berharga, terutama pada server bersama atau laptop dengan VRAM terbatas. Properti `MaxDeviceMemory` memberi tahu Aspose berapa banyak memori GPU yang dapat dialokasikan dengan aman.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

Saat Anda **set max GPU memory**, mesin secara otomatis akan beralih ke pemrosesan CPU jika tidak dapat memenuhi permintaan—mencegah crash. Ini adalah cara paling aman untuk **configure GPU memory** tanpa mengkodekan batas perangkat secara khusus.

**Kapan harus disesuaikan:**  
* Jika Anda melihat `OutOfMemoryException` selama pemrosesan batch berat, turunkan batasnya.  
* Jika resi Anda beresolusi tinggi (300 DPI+), naikkan menjadi 2 GB untuk menjaga kecepatan tetap tinggi.

---

## Jalankan OCR pada Gambar untuk Mengekstrak Teks dari Resi

Sekarang bagian yang menyenangkan—sebenarnya **run OCR on image** dan mengambil teks resi. Metode `Recognize` mengembalikan objek `OcrResult` yang berisi properti `Text` dengan output teks polos.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

Konsol akan menampilkan sesuatu seperti:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Mengapa ini berhasil:**  
Mesin GPU menjalankan model deep‑learning yang telah dilatih pada berbagai tata letak dokumen. Dengan memberi gambar yang bersih dan dimuat dengan benar, Anda memberi model peluang terbaik untuk **extract text from receipt** secara akurat.

---

## Verifikasi Output dan Jebakan Umum

Bahkan dengan mesin yang kuat, OCR bukan sihir. Berikut beberapa hal yang perlu diwaspadai:

| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| Karakter berantakan | Kontras rendah atau gambar buram | Pra‑proses dengan `ImageProcessor` milik Aspose untuk meningkatkan kontras |
| Baris hilang | Gambar terpotong terlalu ketat | Pastikan resi sepenuhnya berada dalam batas gambar |
| Kesalahan out‑of‑memory | `MaxDeviceMemory` terlalu rendah untuk ukuran gambar | Tingkatkan `MaxDeviceMemory` atau perkecil gambar terlebih dahulu |
| Bahasa salah | Resi berisi teks non‑English | Set `gpuEngine.Language = OcrLanguage.Spanish;` (atau yang sesuai) |

Jika Anda mengalami salah satu masalah ini, solusi cepatnya adalah mengubah ukuran gambar menjadi kurang dari 2000 px pada sisi terpanjang—ini secara dramatis mengurangi beban GPU tanpa mengorbankan keterbacaan untuk kebanyakan resi.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah seluruh program, siap untuk dikompilasi. Ganti jalur file dengan lokasi resi Anda sendiri.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output konsol yang diharapkan** (tentu saja resi Anda akan berbeda):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Jalankan program dengan `dotnet run`. Jika Anda melihat teks tercetak, selamat—Anda telah berhasil **load image file**, **set max GPU memory**, dan **run OCR on image** untuk **extract text from receipt**.

---

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja pada mesin tanpa GPU khusus?**  
A: Ya. Aspose.OCR akan dengan elegan beralih ke mode CPU jika tidak ada GPU yang kompatibel terdeteksi. Anda masih dapat **load image file** dan **run OCR on image**, hanya sedikit lebih lambat.

**Q: Bisakah saya memproses banyak resi sekaligus dalam batch?**  
A: Tentu saja. Bungkus kode pengenalan dalam loop `foreach`, tetapi ingat untuk menggunakan kembali instance `GpuEngine` yang sama—ini menghindari inisialisasi ulang sumber daya GPU untuk setiap file.

**Q: Bagaimana jika resi saya dalam bahasa selain Inggris?**  
A: Atur bahasa sebelum memanggil `Recognize`:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

---

## Langkah Selanjutnya & Topik Terkait

Sekarang Anda telah menguasai dasar-dasarnya, pertimbangkan untuk mengeksplorasi:

* **Fine‑tuning OCR accuracy** – bereksperimen dengan `gpuEngine.RecognitionOptions` seperti `EnableDeskew` atau `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}