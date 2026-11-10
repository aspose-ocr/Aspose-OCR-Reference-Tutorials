---
category: general
date: 2026-06-22
description: Lakukan OCR pada gambar menggunakan Aspose.OCR di C#. Pelajari cara mengekstrak
  teks dari PNG, mengonversi gambar menjadi teks, dan mengenali teks dari PNG termasuk
  bahasa Rusia.
draft: false
keywords:
- perform ocr on image
- extract text from png
- convert image to text
- recognize text from png
- read russian text
language: id
og_description: Lakukan OCR pada gambar di C# dengan Aspose.OCR. Panduan ini menunjukkan
  cara mengekstrak teks dari PNG, mengonversi gambar menjadi teks, dan membaca teks
  Rusia secara efisien.
og_title: Lakukan OCR pada Gambar dengan Aspose.OCR – Tutorial C#
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Aspose.OCR in C#. Learn to extract text
    from png, convert image to text, and recognize text from png including Russian
    language.
  headline: Perform OCR on Image with Aspose.OCR – Complete C# Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Lakukan OCR pada Gambar dengan Aspose.OCR – Panduan Lengkap C#
url: /id/net/text-recognition/perform-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar dengan Aspose.OCR – Panduan Lengkap C#

Pernah bertanya-tanya bagaimana cara **perform OCR on image** file tanpa menghabiskan berjam‑jam mencari pustaka yang tepat? Menurut pengalaman saya, Aspose.OCR membuat seluruh proses terasa seperti berjalan di taman, terutama ketika Anda perlu **extract text from png** file yang ditulis dalam alfabet Sirilik.  

Dalam tutorial ini kita akan menelusuri contoh dunia nyata yang tidak hanya **convert image to text** tetapi juga menunjukkan cara **recognize text from png** dan **read Russian text** secara andal. Pada akhir tutorial Anda akan memiliki aplikasi konsol siap‑jalankan yang mencetak hasil OCR langsung ke konsol.

---

![diagram alur melakukan OCR pada gambar](image-placeholder.png "diagram alur melakukan OCR pada gambar")

## Lakukan OCR pada Gambar – Implementasi Langkah‑per‑Langkah

Berikut adalah kode lengkap yang dapat dijalankan. Silakan salin‑tempel ke proyek konsol baru, tekan F5, dan saksikan keajaibannya.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load your Aspose.OCR license (if you have one)
        var license = new License();
        // license.SetLicense("Aspose.OCR.lic");   // uncomment and provide the path to your license file

        // Step 2: Create an OCR engine (CPU mode is the default)
        var ocrEngine = new OcrEngine();

        // Step 3: Specify the language to recognize – Russian (Cyrillic)
        ocrEngine.Language = OcrLanguage.Russian;

        // Step 4: (Optional) Set a download timeout for language resources, in seconds
        ocrEngine.ResourceDownloadTimeout = 120;

        // Step 5: Perform OCR on the image file
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/sample_russian.png");

        // Step 6: Output the recognized plain‑text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Menjalankan program akan mencetak sesuatu seperti:

```
Привет, мир!
Это тестовое изображение.
```

Output tersebut membuktikan bahwa kita berhasil **perform OCR on image** dan **read Russian text** sekaligus.

---

## Extract Text from PNG – Memuat File

Sebelum mesin dapat bekerja, ia memerlukan bitmap untuk diproses. Metode `RecognizeImage` menerima path ke format raster yang didukung, PNG menjadi yang paling umum untuk screenshot lossless.  

> **Mengapa PNG?** Karena PNG mempertahankan setiap piksel, yang berarti mesin OCR melihat data persis seperti yang Anda tangkap—tidak ada artefak kompresi yang membingungkan pengenalan.

Jika Anda menggunakan JPEG atau BMP, panggilan yang sama tetap berlaku; cukup ganti ekstensi file. Bagian pentingnya adalah file tersebut ada dan aplikasi Anda memiliki izin baca.

---

## Convert Image to Text – Mengenali Konten

Inti tutorial terletak pada langkah 5, di mana kita **convert image to text**. Di balik layar, Aspose.OCR memuat gambar, menjalankannya melalui jaringan saraf yang dilatih pada glif Sirilik, dan mengembalikan string teks biasa.  

Beberapa tips praktis:

* **Tip:** Jika Anda melihat karakter yang kacau, tingkatkan `ResourceDownloadTimeout` atau unduh paket bahasa terlebih dahulu untuk menghindari gangguan jaringan.
* **Tip:** Untuk PDF multi‑halaman, Anda dapat melakukan loop pada setiap gambar halaman dan menggabungkan hasilnya—masih menggunakan panggilan **perform OCR on image** per halaman.

---

## Read Russian Text – Menetapkan Bahasa

Anda mungkin bertanya, “Apakah saya harus menyebutkan bahasa Rusia secara manual?” Jawaban singkatnya: **yes**, jika Anda menginginkan akurasi optimal. Dengan menetapkan `ocrEngine.Language = OcrLanguage.Russian;` kami memberi tahu mesin untuk memuat set karakter Sirilik dan model bahasa.  

Jika Anda melewatkan langkah ini, mesin akan default ke bahasa Inggris, dan karakter Rusia Anda akan berubah menjadi tanda tanya atau sampah. Jadi selalu **read Russian text** dengan secara eksplisit menetapkan bahasa.

---

## Recognize Text from PNG – Menangani Timeout dan Sumber Daya

Latensi jaringan dapat menjadi masalah ketika mesin OCR harus mengunduh sumber daya bahasa untuk pertama kalinya. Properti `ResourceDownloadTimeout` (langkah 4) memberikan jaring pengaman.  

* **Kapan menyesuaikan:** Jika Anda berada di VPN korporat yang lambat, naikkan timeout menjadi 180 detik.
* **Kapan tidak perlu:** Untuk paket bahasa yang sudah terpasang secara lokal, nilai default 120 detik sudah lebih dari cukup.

---

## Extract Text from PNG – Manajemen Lisensi (Opsional)

Aspose.OCR berfungsi langsung dalam mode percobaan, tetapi lisensi menghilangkan watermark dan membuka seluruh API. Untuk **perform OCR on image** tanpa batas, hapus komentar pada baris lisensi dan arahkan ke file `.lic` Anda.  

```csharp
var license = new License();
license.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

---

## Convert Image to Text – Daftar Periksa Proyek Lengkap

| ✅ | Item |
|---|------|
| 1 | Instal **Aspose.OCR** via NuGet (`Install-Package Aspose.OCR`) |
| 2 | Tambahkan `using Aspose.OCR;` dan `using Aspose.OCR.Models;` |
| 3 | (Opsional) Terapkan lisensi Anda |
| 4 | Buat instance `OcrEngine` |
| 5 | Set `Language = OcrLanguage.Russian` untuk **read russian text** |
| 6 | Sesuaikan `ResourceDownloadTimeout` bila diperlukan |
| 7 | Panggil `RecognizeImage(@"path\to\file.png")` untuk **perform OCR on image** |
| 8 | Cetak `ocrResult.Text` – Anda baru saja **extract text from png**! |

---

## Pertanyaan Umum & Kasus Tepi

**Bagaimana jika PNG saya berisi bahasa Inggris dan Rusia sekaligus?**  
Anda dapat menetapkan `ocrEngine.Language = OcrLanguage.Multilingual;` yang memuat model gabungan. Mesin tetap akan **recognize text from png** dengan akurat, meskipun ukuran paket bahasa sedikit bertambah.

**Bisakah saya memproses seluruh folder gambar?**  
Tentu saja. Bungkus panggilan `RecognizeImage` dalam loop `foreach (var file in Directory.GetFiles(folder, "*.png"))`. Setiap iterasi **performs OCR on image** dan Anda dapat menuliskan hasilnya ke file `.txt`.

**Bagaimana dengan gambar beresolusi rendah?**  
Kualitas OCR menurun di bawah 72 dpi. Jika screenshot Anda blur, pertimbangkan untuk memperbesar ukuran dengan pustaka grafis sebelum memberi ke Aspose.OCR. Pustaka itu sendiri tidak akan secara ajaib meningkatkan kualitas piksel.

---

## Pro Tips untuk OCR Siap Produksi

* **Cache hasil:** Simpan teks biasa ke dalam basis data untuk menghindari menjalankan OCR berulang pada file yang tidak berubah.
* **Validasi output:** Gunakan regex sederhana untuk mendeteksi apakah hasil kosong—jika iya, coba lagi dengan timeout yang lebih tinggi.
* **Paralelisasi:** Untuk pemrosesan massal, jalankan beberapa instance `OcrEngine` pada thread terpisah; Aspose.OCR aman untuk thread selama tiap thread memiliki engine masing‑masing.

---

## Kesimpulan

Kami baru saja **performed OCR on image** file menggunakan Aspose.OCR, memperlihatkan cara **extract text from png**, **convert image to text**, dan **recognize text from png** sambil **reading Russian text** dengan sempurna. Solusi lengkap ini muat dalam satu metode `Main`, namun dapat diskalakan ke skenario perusahaan dengan beberapa penyesuaian.

Siap untuk tantangan berikutnya? Coba tambahkan pra‑pemrosesan gambar (deskew, penghilangan noise) dengan pustaka seperti **ImageSharp**, atau eksperimen mengekspor hasil OCR ke JSON untuk analitik lanjutan. Langit adalah batasnya ketika Anda menguasai dasar‑dasar OCR di C#.

Selamat coding, semoga gambar Anda selalu dapat dibaca!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang memperluas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}