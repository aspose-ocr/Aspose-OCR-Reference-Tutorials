---
category: general
date: 2025-12-27
description: Buat logger konsol di C# dan aktifkan unduhan otomatis ke tabel yang
  benar menggunakan AsposeAI. Pelajari cara menampilkan output tabel yang telah dikoreksi
  dalam beberapa langkah saja.
draft: false
keywords:
- create console logger
- enable auto download
- how to correct tables
- setup console logger
- display corrected table
language: id
og_description: Buat logger konsol di C# dan aktifkan unduhan otomatis ke tabel yang
  benar menggunakan AsposeAI. Ikuti panduan ini untuk menampilkan output tabel yang
  telah diperbaiki dengan cepat.
og_title: Buat logger konsol dan perbaiki tabel dengan AsposeAI
tags:
- AsposeAI
- C#
- OCR
- Table processing
title: Buat logger konsol dan perbaiki tabel dengan AsposeAI
url: /id/net/ocr-optimization/create-console-logger-and-correct-tables-with-asposeai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat console logger dan memperbaiki tabel dengan AsposeAI

Pernah perlu **membuat console logger** untuk pipeline AI C# tetapi tidak tahu harus mulai dari mana? Dalam panduan ini kami akan membahas seluruh proses—cara membuat console logger, mengaktifkan auto download untuk file model, dan akhirnya **cara memperbaiki tabel** yang dihasilkan oleh OCR. Pada akhir tutorial Anda akan dapat **menampilkan hasil tabel yang telah diperbaiki** di console hanya dengan beberapa baris kode.

Kami akan mencakup semuanya mulai dari pengaturan logger awal hingga pembersihan akhir, sehingga Anda tidak perlu mencari-cari dokumentasi yang tersebar. Tidak diperlukan pengalaman sebelumnya dengan AsposeAI; pemahaman dasar tentang C# dan .NET sudah cukup. Sepanjang jalan kami akan menyelipkan tips tentang **setup console logger** yang terbaik, membahas kasus tepi, dan menunjukkan seperti apa output yang diharapkan.

---

## Prerequisites

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut:

- .NET 6.0 atau lebih baru (kode menggunakan fitur bahasa modern)
- Visual Studio 2022 atau IDE apa pun yang mendukung proyek C#
- Paket NuGet **Aspose.AI** terpasang (`Install-Package Aspose.AI`)
- Paket NuGet **Aspose.OCR** terpasang (`Install-Package Aspose.OCR`)
- Sebuah objek hasil OCR contoh (`ocrResult`) dari pemanggilan Aspose.OCR sebelumnya

Jika ada yang belum ada, berhentilah sejenak dan siapkan dulu—Anda akan berterima kasih nanti.

---

## Step 1: Create console logger and initialise AsposeAI

Hal pertama yang kita perlukan adalah logger yang menulis langsung ke console. Ini memudahkan debugging dan memberi umpan balik secara real‑time saat mesin AI berjalan.

```csharp
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

// Step 1: Create a logger that writes to the console
ILogger consoleLogger = new ConsoleLogger();

// Step 2: Initialise the AsposeAI engine with the logger
AsposeAI asposeAI = new AsposeAI(consoleLogger);
```

**Mengapa ini penting:**  
`ConsoleLogger` mengimplementasikan antarmuka `ILogger`, sehingga semua pesan internal dari AsposeAI (pemuatan model, status post‑processor, error) muncul seketika di terminal Anda. Ini cara paling sederhana untuk **setup console logger** tanpa harus menambahkan framework logging eksternal.

> **Pro tip:** Jika nanti Anda membutuhkan logging ke file, cukup ganti `ConsoleLogger` dengan logger kustom yang mengimplementasikan `ILogger`—sisa kode tetap tidak berubah.

---

## Step 2: Enable auto download for AI models

AsposeAI dapat mengambil file model yang diperlukan secara otomatis. Mengaktifkan fitur ini menghindarkan Anda dari mengunduh binary berukuran besar secara manual.

```csharp
// Step 3: (Optional) Configure automatic model download and set the model directory
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,               // <‑‑ enable auto download
    DirectoryModelPath = "YOUR_DIRECTORY"   // change to a writable folder
};
```

**Apa yang bisa salah?**  
Jika `DirectoryModelPath` mengarah ke lokasi yang hanya‑baca, auto‑download akan gagal dan Anda akan melihat exception di console. Pastikan folder tersebut ada dan aplikasi Anda memiliki izin menulis.

---

## Step 3: Create a table post‑processor (how to correct tables)

Tabel yang diekstrak dari OCR sering berantakan—sel yang digabung, border yang hilang, atau teks yang tidak rata. `TableAIProcessor` dari AsposeAI dapat membersihkannya secara otomatis.

```csharp
// Step 4: Create a table post‑processor that lets the engine decide when to run correction
TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);
```

**Mengapa mode AUTO?**  
`AITableDetectionMode.AUTO` memungkinkan mesin memeriksa output OCR dan memutuskan apakah koreksi diperlukan. Jika Anda lebih suka kontrol manual, Anda dapat menggunakan `MANUAL` dan memanggil `RunCorrection()` sendiri.

---

## Step 4: Attach the post‑processor and its configuration

Sekarang kita mengikat semuanya—logger, konfigurasi model, dan processor tabel.

```csharp
// Step 5: Attach the post‑processor and its configuration to the AI engine
asposeAI.SetPostProcessor(tableProcessor, modelConfig);
```

Pada titik ini mesin AI tahu *di mana* menyimpan model, *bagaimana* melakukan logging, dan *apa* post‑processing yang harus diterapkan. Ini pemisahan kepedulian yang bersih sehingga perubahan di masa depan menjadi mudah.

---

## Step 5: Run the post‑processor on your OCR result

Dengan asumsi Anda sudah memiliki `ocrResult` dari Aspose.OCR, cukup serahkan ke mesin.

```csharp
// Step 6: Run the post‑processor on the OCR result returned by Aspose.OCR
asposeAI.RunPostprocessor(ocrResult);
```

**Peringatan kasus tepi:**  
Jika `ocrResult` tidak mengandung tabel, processor akan melewatkan koreksi secara diam‑diam. Anda dapat memeriksa `tableProcessor.GetResult().Count` setelahnya untuk memastikan ada yang diproses.

---

## Step 6: Retrieve and **display corrected table** output

Akhirnya, mari ambil teks tabel yang sudah dibersihkan dan cetak ke console.

```csharp
// Step 7: Retrieve and display the corrected table text
Console.WriteLine("Corrected table output:");
Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
```

Output akan terlihat kira‑kira seperti ini (tergantung pada gambar sumber):

```
Corrected table output:
| Item   | Quantity | Price |
|--------|----------|-------|
| Apple  | 10       | $1.20 |
| Banana | 5        | $0.80 |
```

Jika yang muncul adalah string kosong, periksa kembali apakah OCR memang mendeteksi tabel dan apakah `AllowAutoDownload` berhasil.

---

## Step 7: Clean up resources

Menjadi warga yang baik berarti membuang objek berat setelah selesai.

```csharp
// Step 8: Release resources used by the AI engine
asposeAI.Dispose();
```

Melewatkan langkah ini dapat meninggalkan handle file terbuka, terutama di Windows dimana file model tetap terkunci.

---

## Full Working Example

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek console baru. Ganti `"YOUR_DIRECTORY"` dengan path yang nyata dan pastikan `ocrResult` terisi sebelum memanggil `RunPostprocessor`.

```csharp
using System;
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

namespace AsposeAITableCorrection
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a console logger
            ILogger consoleLogger = new ConsoleLogger();

            // 2️⃣ Initialise AsposeAI with the logger
            AsposeAI asposeAI = new AsposeAI(consoleLogger);

            // 3️⃣ Configure auto‑download (optional but recommended)
            AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
            {
                AllowAutoDownload = true,
                DirectoryModelPath = @"C:\AsposeModels" // <-- change this
            };

            // 4️⃣ Create the table processor (auto‑detect mode)
            TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);

            // 5️⃣ Attach processor and config
            asposeAI.SetPostProcessor(tableProcessor, modelConfig);

            // 6️⃣ Obtain OCR result (replace with your own OCR call)
            // Example placeholder – you should have this from Aspose.OCR already
            OcrResult ocrResult = GetOcrResultSomehow();

            // 7️⃣ Run post‑processor on the OCR output
            asposeAI.RunPostprocessor(ocrResult);

            // 8️⃣ Display corrected table
            Console.WriteLine("Corrected table output:");
            if (tableProcessor.GetResult().Count > 0)
            {
                Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
            }
            else
            {
                Console.WriteLine("No tables were detected or corrected.");
            }

            // 9️⃣ Clean up
            asposeAI.Dispose();
        }

        // Dummy method – replace with your actual OCR logic
        static OcrResult GetOcrResultSomehow()
        {
            // For illustration only
            OcrEngine engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample-table.png");
            return engine.Recognize();
        }
    }
}
```

**Output console yang diharapkan** (misalkan gambar tabel sederhana):

```
Corrected table output:
| Name   | Age | City      |
|--------|-----|-----------|
| Alice  | 30  | New York  |
| Bob    | 25  | Seattle   |
```

---

## Common Questions & Answers

- **Apakah saya memerlukan koneksi internet untuk auto download?**  
  Ya. Pada pemanggilan pertama model, AsposeAI akan menghubungi CDN-nya. Setelah file berada di `DirectoryModelPath`, run selanjutnya dapat dilakukan secara offline.

- **Bagaimana jika tabel saya memiliki sel yang digabung?**  
  Model AI berusaha memisahkan sel yang digabung berdasarkan petunjuk visual. Jika hasilnya tidak memuaskan, pertimbangkan pra‑pemrosesan gambar (tingkatkan kontras, luruskan rotasi) sebelum OCR.

- **Bisakah saya memproses banyak tabel sekaligus?**  
  Tentu. `tableProcessor.GetResult()` mengembalikan list; iterasi list tersebut untuk mencetak tiap tabel.

- **Apakah `ConsoleLogger` thread‑safe?**  
  Ia menulis langsung ke `System.Console`, yang thread‑safe untuk penulisan sederhana. Untuk skenario multi‑thread berat, logger kustom dengan sinkronisasi mungkin lebih cocok.

---

## Next Steps & Related Topics

Setelah Anda menguasai **cara memperbaiki tabel**, Anda mungkin ingin:

- **Mengaktifkan auto download** untuk model AsposeAI lain (misalnya terjemahan bahasa).
- **Setup console logger** dengan level log yang berbeda (Info, Warning, Error) untuk kontrol yang lebih halus.
- Menjelajahi **display corrected table** di GUI (WinForms atau WPF) alih‑alih console.
- Menggabungkan koreksi tabel dengan **data extraction** untuk langsung memasukkan ke database.

Masing‑masing topik ini dibangun di atas fondasi yang baru saja kita buat, jadi silakan bereksperimen.

---

## Conclusion

Kami telah menelusuri seluruh siklus hidup **membuat console logger**, mengaktifkan auto download, dan **memperbaiki tabel** dengan AsposeAI, selesai dengan cara bersih untuk **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}