---
category: general
date: 2026-04-03
description: Pelajari cara melakukan OCR di C# dan mengekstrak teks dari gambar menggunakan
  Aspose OCR, dengan pemeriksaan ejaan untuk bahasa Rusia.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: id
og_description: Pelajari cara melakukan OCR di C# dan mengekstrak teks dari gambar
  menggunakan Aspose OCR, dengan pemeriksaan ejaan untuk bahasa Rusia.
og_title: Cara Melakukan OCR di C# – Ekstrak Teks dari Gambar
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: Cara Melakukan OCR di C# – Ekstrak Teks dari Gambar
url: /id/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di C# – Ekstrak Teks dari Gambar

Pernah bertanya‑tanya **cara melakukan OCR** pada foto catatan tulisan tangan? Mungkin Anda memiliki struk yang dipindai, tanda dalam bahasa asing, atau halaman PDF yang tidak dapat disalin‑tempel. Kabar baiknya? Dengan beberapa baris C# dan pustaka Aspose OCR Anda dapat mengubah gambar tersebut menjadi teks yang dapat diedit dalam sekejap.  

Dalam panduan ini kami tidak hanya akan menunjukkan **cara melakukan OCR**, tetapi juga akan membahas **ekstrak teks dari gambar**, **konversi gambar ke teks**, dan bahkan **cara memeriksa ejaan** hasilnya ketika Anda menangani dokumen berbahasa Rusia. Kedengarannya banyak? Tetap di sini – kami akan menjelaskan semuanya langkah demi langkah.

## Apa yang Akan Anda Pelajari

Pada akhir tutorial ini Anda akan dapat:

* Menyiapkan Aspose OCR untuk dukungan bahasa Rusia.  
* Memuat file gambar dan menjalankan optical character recognition untuk **ekstrak teks dari gambar**.  
* Menggunakan pemeriksa ejaan bawaan untuk secara otomatis memperbaiki kata yang salah eja – jawaban sempurna untuk “**cara memeriksa ejaan**” output OCR.  
* Mencetak string yang sudah dibersihkan ke konsol, siap untuk diproses lebih lanjut atau disimpan.

**Prasyarat** – Anda memerlukan:

* .NET 6.0 atau yang lebih baru (kode ini juga bekerja dengan .NET Framework 4.8).  
* Lisensi Aspose OCR yang valid atau kunci evaluasi sementara.  
* File gambar yang berisi teks berbahasa Rusia (untuk demo kami akan menyebutnya `russian_note.jpg`).  

Jika ada yang belum familiar, jangan khawatir. Langkah‑langkah di bawah ini mencakup perintah NuGet yang tepat untuk mengunduh Aspose OCR, dan kode sepenuhnya mandiri.

![contoh cara melakukan OCR](/images/ocr-demo.png "contoh cara melakukan OCR di C#")

## Langkah 1 – Instal Aspose OCR dan Tambahkan Namespace

Hal pertama yang harus dilakukan adalah mendapatkan pustaka. Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.OCR
```

Perintah itu mengunduh versi stabil terbaru (per April 2026 versi 22.9). Setelah paket dipulihkan, tambahkan directive `using` yang diperlukan di bagian atas file C# Anda:

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*Tip pro:* Jika Anda menggunakan Visual Studio, IDE akan menyarankan penambahan ini secara otomatis setelah Anda mengetik nama kelas pertama.

## Langkah 2 – Inisialisasi OCR Engine untuk Bahasa Rusia

Bagian **cara melakukan OCR** dimulai dengan membuat instance `OcrEngine`. Dengan menentukan `OcrLanguage.Russian` kami memberi tahu engine untuk memuat set karakter Cyrillic dan heuristik khusus bahasa.

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

Mengapa ini penting? Tanpa mengatur bahasa, engine secara default menggunakan bahasa Inggris dan akan salah menafsirkan banyak karakter Cyrillic, menghasilkan output yang berantakan. Mengonfigurasi bahasa secara eksplisit meningkatkan akurasi secara dramatis.

## Langkah 3 – Muat Gambar dan **Konversi Gambar ke Teks**

Sekarang kami memuat gambar ke memori. Metode `Image.FromFile` bekerja dengan sebagian besar format umum (JPG, PNG, BMP). Setelah dimuat, kami memanggil `Recognize` untuk **konversi gambar ke teks**.

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

Variabel `rawText` kini berisi output OCR mentah, yang mungkin masih mengandung typo atau karakter yang salah dikenali. Anda dapat mencetaknya untuk melihat apa yang ditangkap engine:

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## Langkah 4 – **Cara Memeriksa Ejaan** Hasil OCR

OCR bahasa Rusia dapat berisik, terutama pada pemindaian beresolusi rendah. Aspose menyediakan kelas `SpellChecker` yang memahami kamus Rusia secara bawaan. Berikut cara menggunakannya:

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

Metode `CheckAndCorrect` mengembalikan string baru di mana kata yang salah eja diganti dengan alternatif yang paling mungkin benar. Metode ini juga menghormati tanda baca, sehingga Anda tidak mendapatkan teks yang berantakan.

*Kasus khusus:* Jika output OCR kosong (misalnya gambar sepenuhnya putih), `CheckAndCorrect` hanya akan mengembalikan string kosong. Sebaiknya Anda menambahkan pengecekan jika berencana menulis hasil ke file.

## Langkah 5 – Tampilkan Hasil yang Sudah Dibersihkan

Akhirnya, kami mencetak string yang telah dikoreksi. Dalam aplikasi dunia nyata Anda mungkin menulisnya ke basis data, API JSON, atau dokumen Word. Untuk demo ini, cukup menampilkan di konsol:

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

Perhatikan bagaimana pemeriksa ejaan mengubah “Привeт” (e Latin ‘e’) menjadi Cyrillic yang tepat “Привет”. Itulah keajaiban **cara memeriksa ejaan** output OCR.

## Contoh Lengkap yang Dapat Dijalankan

Berikut adalah program lengkap yang dapat dijalankan, menggabungkan semua langkah. Salin‑tempel ke proyek konsol baru dan tekan **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### Output yang Diharapkan

Menjalankan program dengan foto tulisan tangan Rusia yang jelas dan beresolusi tinggi biasanya menghasilkan kalimat yang bersih dan dapat dibaca manusia. Jika gambar blur, Anda mungkin masih mendapatkan kata‑kata yang sebagian benar, tetapi pemeriksa ejaan akan memperbaiki sebagian besar kesalahan yang jelas.

## Masalah Umum & Tips

| Masalah | Mengapa Terjadi | Cara Memperbaiki / Menghindari |
|---------|-----------------|-------------------------------|
| **Karakter sampah** | DPI rendah atau latar belakang berisik | Praproses gambar (tingkatkan kontras, ubah ukuran menjadi ≥300 dpi) sebelum memberi ke `Recognize`. |
| **Output kosong** | Path file salah atau format tidak didukung | Verifikasi path, dan gunakan `Image.FromFile` dalam blok `try/catch` untuk menampilkan error. |
| **Pemeriksa ejaan tidak menemukan kesalahan** | Kata langka tidak ada di kamus | Perluas kamus dengan memuat daftar kata khusus via `spellChecker.AddUserDictionary("mywords.txt")`. |
| **Lag performa pada batch besar** | OCR memakan CPU | Jalankan OCR pada thread latar belakang atau gunakan `Parallel.ForEach` untuk banyak gambar. |
| **Pengecualian lisensi** | Menggunakan versi evaluasi melewati masa percobaan | Beli lisensi dan panggil `License license = new License(); license.SetLicense("Aspose.Total.lic");` sebelum membuat `OcrEngine`. |

## Langkah Selanjutnya – Melampaui OCR Sederhana

Setelah Anda menguasai **cara melakukan OCR**, pertimbangkan ekstensi berikut:

* **Pemrosesan batch** – Loop melalui folder gambar dan tulis setiap teks yang telah dikoreksi ke file `.txt`.  
* **Konversi PDF** – Gunakan Aspose PDF untuk menyematkan teks yang diekstrak kembali ke PDF yang dapat dicari.  
* **Deteksi bahasa** – Jika Anda harus menangani banyak bahasa, periksa hasil OCR terlebih dahulu dan ubah `OcrLanguage` sesuai kebutuhan.  
* **Integrasi dengan Azure Cognitive Services** – Bandingkan hasil Aspose dengan API OCR Microsoft untuk pendekatan hibrida.

Semua topik tersebut secara alami melibatkan kata kunci sekunder **extract text from image**, **convert image to text**, dan **how to spell check**, jadi

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}