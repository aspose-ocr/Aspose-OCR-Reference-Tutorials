---
date: 2026-04-29
description: Tingkatkan akurasi OCR dan pelajari cara mengenali teks dari gambar menggunakan
  Aspose OCR untuk .NET, memanfaatkan pemeriksaan ejaan dan dukungan bahasa untuk
  memperbaiki kesalahan ejaan serta menyesuaikan kamus.
keywords:
- improve ocr accuracy
- recognize text from image
- Aspose OCR spell checking
- custom OCR dictionary
linktitle: Tingkatkan Akurasi OCR dengan Pemeriksaan Ejaan pada Gambar
second_title: Aspose.OCR .NET API
title: Tingkatkan Akurasi OCR dengan Pemeriksaan Ejaan pada Gambar
url: /id/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tingkatkan Akurasi OCR dengan Pemeriksaan Ejaan pada Gambar

Saat Anda bekerja dengan Optical Character Recognition (OCR), tujuan utama adalah untuk **meningkatkan akurasi OCR** sehingga teks yang diekstrak cocok dengan gambar asli secara sempurna. Kata yang salah eja merupakan sumber kesalahan yang umum, terutama ketika gambar sumber berisik atau menggunakan font yang tidak biasa. Aspose.OCR untuk .NET menawarkan kemampuan pemeriksaan ejaan bawaan yang tidak hanya memperbaiki kesalahan tersebut tetapi juga memungkinkan Anda memperluas mesin dengan kamus khusus. Dalam tutorial ini Anda akan belajar cara menggunakan pemeriksaan ejaan untuk meningkatkan hasil OCR, melihat output sebelum‑dan‑sesudah, serta menemukan cara menyesuaikan proses koreksi sesuai kebutuhan bahasa Anda.

## Jawaban Cepat
- **Apa yang dilakukan pemeriksaan ejaan untuk OCR?** Itu secara otomatis mendeteksi kata yang salah eja dalam output OCR dan menggantinya dengan alternatif yang paling mungkin benar.  
- **Perpustakaan mana yang menyediakan fitur ini?** Aspose.OCR untuk .NET menyertakan API pemeriksaan ejaan siap pakai.  
- **Apakah saya memerlukan koneksi internet?** Tidak, mesin pemeriksaan ejaan bekerja sepenuhnya offline.  
- **Bisakah saya menambahkan terminologi saya sendiri?** Ya, Anda dapat menyediakan kamus pengguna khusus untuk menangani kata‑kata khusus domain.  
- **Bagaimana ini membantu saya mengenali teks dari gambar?** Dengan memperbaiki kesalahan yang dihasilkan OCR, teks akhir menjadi bersih dan siap untuk pemrosesan lanjutan.

## Apa Itu Pemeriksaan Ejaan dalam OCR?
Pemeriksaan ejaan memeriksa teks mentah yang dikembalikan oleh mesin OCR, mengidentifikasi token yang tidak cocok dengan kata‑kata yang dikenal dalam kamus bahasa yang dipilih, dan menyarankan atau menerapkan koreksi. Langkah ini penting untuk **meningkatkan akurasi OCR**, terutama saat memproses dokumen yang dipindai, kwitansi, atau formulir di mana OCR dapat salah menafsirkan karakter.

## Mengapa Menggunakan Dukungan Bahasa Aspose OCR?
Aspose.OCR dilengkapi dengan paket bahasa yang luas dan memungkinkan Anda menambahkan kamus tambahan. Memanfaatkan **aspose ocr language support** berarti Anda dapat menangani dokumen multibahasa tanpa menulis parser khusus, dan Anda mendapatkan akses ke aturan bahasa‑spesifik yang lebih meningkatkan kualitas pengenalan.

## Kapan meningkatkan akurasi OCR paling penting?
- **Dokumen hukum dan kepatuhan** di mana satu typo dapat mengubah makna.  
- **Pipeline ekstraksi data** yang mengalirkan hasil OCR ke analitik atau model AI.  
- **Aplikasi yang berhadapan dengan pelanggan** seperti pemindai seluler yang harus mengembalikan teks yang dapat dibaca secara instan.  

## Prasyarat

Sebelum kita menyelami keajaiban pemeriksaan ejaan, pastikan Anda memiliki prasyarat berikut:

- Aspose.OCR untuk .NET Library: Unduh dan instal pustaka Aspose.OCR dari [halaman rilis](https://releases.aspose.com/ocr/net/).
- Direktori Dokumen: Pastikan Anda memiliki direktori yang ditentukan untuk dokumen Anda. Ganti `"Your Document Directory"` dalam potongan kode dengan jalur yang sebenarnya.

## Impor Namespace

Mari kita mulai dengan mengimpor namespace yang diperlukan dalam proyek .NET Anda:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Langkah 1: Inisialisasi Aspose.OCR

Inisialisasi sebuah instance Aspose.OCR untuk memulai proses OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Langkah 2: Kenali Gambar

Selanjutnya, kenali teks dalam sebuah gambar menggunakan Aspose.OCR. Berikut contoh potongan kode yang menunjukkan proses ini:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Langkah 3: Sebelum Koreksi

Ambil hasil OCR sebelum koreksi untuk dibandingkan dengan versi yang telah dikoreksi.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Langkah 4: Setelah Koreksi

Terapkan pemeriksaan ejaan untuk mendapatkan hasil yang telah dikoreksi. Potongan kode berikut menggambarkan langkah ini:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Langkah 5: Kata yang Salah Eja dan Saran

Dapatkan daftar kata yang salah eja beserta saran koreksinya menggunakan kode berikut:

```csharp
// Get list of misspelled words with suggestions
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
    Console.Write("Word:" + word.Word);
    Console.Write(" StartPosition:" + word.StartPosition);
    Console.WriteLine(" Length:" + word.Length);
    Console.WriteLine("SuggestedWords:");
    foreach (var suggest in word.SuggestedWords)
    {
        Console.Write(suggest.Word + " ");
    }
    Console.WriteLine();
}
```

## Langkah 6: Koreksi Teks Pengguna

Koreksi teks yang diberikan pengguna secara spesifik menggunakan pustaka Aspose.OCR:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Langkah 7: Koreksi dengan Kamus Pengguna

Tingkatkan koreksi lebih lanjut dengan mengintegrasikan kamus pengguna khusus:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Masalah Umum dan Solusinya

| Masalah | Mengapa Terjadi | Cara Memperbaiki |
|-------|----------------|------------|
| Tidak ada saran yang dikembalikan | Paket bahasa tidak dimuat atau teks terlalu pendek. | Pastikan `RecognitionSettings(Language.Eng)` sesuai dengan bahasa gambar sumber dan hasil OCR berisi cukup karakter. |
| Kamus khusus tidak diterapkan | Path atau format file tidak benar. | Verifikasi bahwa `dictionary.txt` ada di lokasi yang ditentukan dan menggunakan satu kata per baris. |
| Pemeriksa ejaan memperlambat dokumen besar | Memproses setiap kata secara individual menambah beban. | Proses halaman secara batch atau tingkatkan alokasi memori jika berjalan di .NET Core. |

## Pertanyaan yang Sering Diajukan

**Q1: Bisakah saya menggunakan Aspose.OCR untuk bahasa selain Inggris?**  
A1: Ya, Aspose.OCR mendukung banyak bahasa. Sesuaikan pengaturan bahasa sesuai kebutuhan.

**Q2: Bagaimana cara mengintegrasikan Aspose.OCR ke dalam proyek .NET saya?**  
A2: Lihat [dokumentasi](https://reference.aspose.com/ocr/net/) untuk langkah‑langkah integrasi detail.

**Q3: Apakah ada versi percobaan yang tersedia untuk Aspose.OCR?**  
A3: Ya, Anda dapat menjelajahi fitur dengan [versi percobaan gratis](https://releases.aspose.com/).

**Q4: Bisakah saya mengunggah kamus khusus untuk pemeriksaan ejaan?**  
A4: Tentu saja! Tutorial ini menunjukkan cara meningkatkan koreksi menggunakan kamus yang disediakan pengguna.

**Q5: Di mana saya dapat mencari dukungan untuk Aspose.OCR?**  
A5: Kunjungi [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan komunitas dan panduan.

---

**Terakhir Diperbarui:** 2026-04-29  
**Diuji Dengan:** Aspose.OCR untuk .NET versi terbaru  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}