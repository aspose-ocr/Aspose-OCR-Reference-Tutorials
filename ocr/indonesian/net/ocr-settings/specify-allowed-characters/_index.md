---
date: 2025-12-27
description: Pelajari cara menggunakan konversi gambar ke teks OCR dengan Aspose.OCR
  untuk .NET, menentukan karakter yang diizinkan, dan menyetel pengaturan pengenalan
  OCR secara detail. Termasuk kode untuk mengenali gambar angka.
linktitle: 'ocr image to text: Specify Allowed Characters in OCR'
second_title: Aspose.OCR .NET API
title: 'ocr gambar ke teks: Tentukan Karakter yang Diizinkan dalam OCR'
url: /id/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to text: Tentukan Karakter yang Diizinkan dalam OCR

## Pendahuluan

Dalam lanskap teknologi yang terus berkembang, Optical Character Recognition (OCR) – atau konversi **ocr image to text** – telah muncul sebagai alat transformatif, memungkinkan mesin memahami teks dari gambar. Aspose.OCR untuk .NET menonjol sebagai solusi yang kuat, menyediakan integrasi mulus bagi pengembang yang mencari kemampuan OCR yang handal dalam aplikasi .NET mereka.

## Jawaban Cepat
- **Apa yang dilakukan “Specify Allowed Characters”?** Itu membatasi output OCR ke sekumpulan simbol yang ditentukan, seperti hanya digit.  
- **Metode mana yang mengekstrak satu baris teks?** `RecognizeLine` mengembalikan baris pertama yang terdeteksi.  
- **Bisakah saya mengubah pengaturan pengenalan OCR secara dinamis?** Ya – gunakan `RecognitionSettings` untuk menyesuaikan opsi seperti `AllowedCharacters`.  
- **Apakah versi percobaan tersedia?** Tentu saja, unduh trial gratis dari situs Aspose.  
- **Versi .NET mana yang didukung?** Semua versi .NET Framework modern dan .NET Core/5/6.

## Prasyarat

Sebelum memulai tutorial, pastikan Anda memiliki prasyarat berikut:

- Pengetahuan kerja tentang pengembangan .NET.  
- Perpustakaan Aspose.OCR untuk .NET. Anda dapat mengunduhnya [di sini](https://releases.aspose.com/ocr/net/).  
- Familiaritas dengan Visual Studio atau lingkungan pengembangan .NET lain yang Anda sukai.

## Impor Namespace

Di proyek .NET Anda, impor namespace yang diperlukan untuk memanfaatkan fungsionalitas Aspose.OCR untuk .NET secara efektif:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Sekarang, mari kita uraikan tutorial menjadi serangkaian langkah komprehensif:

## Langkah 1: Tentukan Karakter yang Diizinkan dalam ocr image to text

Untuk memulai, atur jalur ke direktori dokumen Anda:

```csharp
string dataDir = "Your Document Directory";
```

## Langkah 2: Inisialisasi Aspose.OCR dengan Simbol yang Diizinkan (mengenali gambar digit)

Buat instance `AsposeOcr`, menentukan simbol yang diizinkan. Dalam kasus ini, kami hanya mengizinkan digit (0‑9):

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## Langkah 3: Kenali Gambar

Manfaatkan instance `AsposeOcr` untuk mengenali teks dari sebuah gambar:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## Langkah 4: Tampilkan Teks yang Dikenali

Cetak teks yang dikenali ke konsol:

```csharp
Console.WriteLine(result);
```

## Langkah 5: Kasus Kedua – Kenali Gambar dengan Pengaturan Pengenalan OCR Spesifik

Inisialisasi instance `AsposeOcr` lain, kali ini dengan pengaturan yang lebih spesifik yang menunjukkan penggunaan **ocr recognition settings**:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## Langkah 6: Tampilkan Teks yang Dikenali pada Kasus Kedua

Cetak teks yang dikenali dari kasus kedua ke konsol:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## Langkah 7: Eksekusi Berhasil

Akhirnya, konfirmasikan eksekusi berhasil dari tutorial **SpecifyAllowedCharacters**:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Dengan mengikuti langkah‑langkah ini, Anda telah membuka kemampuan untuk **menentukan karakter yang diizinkan** dalam pengenalan gambar OCR menggunakan Aspose.OCR untuk .NET, memungkinkan konversi **ocr image to text** yang tepat untuk skenario hanya digit.

## Mengapa Menggunakan Penyaringan Karakter yang Diizinkan?

- **Akurasi Lebih Tinggi:** Membatasi set karakter mengurangi pengenalan palsu, terutama pada gambar berisik.  
- **Peningkatan Kinerja:** Mesin OCR melewatkan glyph yang tidak relevan, mempercepat proses.  
- **Kepatuhan:** Menegakkan format data (mis., nomor faktur, kode seri) langsung pada tahap OCR.

## Kesalahan Umum & Tips

- **Kesalahan:** Menyediakan string kosong untuk karakter yang diizinkan menonaktifkan penyaringan.  
  **Tips:** Selalu berikan string yang tidak kosong atau gunakan enum `CharactersAllowedType`.  
- **Kesalahan:** Menggunakan `RecognizeLine` pada dokumen multi‑baris dapat melewatkan data.  
  **Tips:** Beralih ke `RecognizeImage` dengan `RecognizeSingleLine = false` untuk ekstraksi seluruh halaman.  
- **Kesalahan:** Lupa menggabungkan jalur direktori dengan benar dapat menyebabkan `FileNotFoundException`.  
  **Tips:** Gunakan `Path.Combine(dataDir, "file.jpg")` untuk jalur yang independen platform.

## Pertanyaan yang Sering Diajukan

**T: Apakah Aspose.OCR untuk .NET cocok untuk pemula maupun pengembang berpengalaman?**  
J: Tentu saja! API ini intuitif bagi pemula sekaligus menawarkan pengaturan lanjutan bagi pengguna tingkat lanjut.

**T: Bisakah saya menggunakan Aspose.OCR untuk .NET untuk mengenali karakter dalam banyak bahasa?**  
J: Ya, Aspose.OCR mendukung berbagai bahasa; Anda juga dapat menggabungkan paket bahasa untuk proyek multibahasa.

**T: Seberapa sering Aspose.OCR untuk .NET diperbarui?**  
J: Pembaruan dirilis secara reguler untuk mengikuti rilis .NET terbaru dan peningkatan OCR. Periksa [dokumentasi](https://reference.aspose.com/ocr/net/) untuk versi terkini.

**T: Apakah ada trial gratis tersedia untuk Aspose.OCR untuk .NET?**  
J: Ya, Anda dapat menjelajahi kemampuan dengan mengunduh [trial gratis](https://releases.aspose.com/).

**T: Di mana saya dapat mencari bantuan atau terhubung dengan komunitas untuk dukungan?**  
J: Kunjungi [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk berinteraksi dengan pakar dan sesama pengembang.

---

**Terakhir Diperbarui:** 2025-12-27  
**Diuji Dengan:** Aspose.OCR 24.11 untuk .NET  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}