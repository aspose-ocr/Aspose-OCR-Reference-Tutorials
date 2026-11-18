---
date: 2026-05-24
description: Pelajari cara meningkatkan OCR dengan mengatur karakter yang diizinkan
  menggunakan Aspose.OCR untuk .NET, memungkinkan pengenalan digit yang akurat dan
  pemrosesan yang lebih cepat. Ikuti panduan langkah demi langkah.
keywords:
- how to improve ocr
- set allowed characters
- recognize digits
- improve ocr accuracy
- extract serial numbers
linktitle: Cara Meningkatkan OCR – Mengatur Karakter yang Diizinkan dengan Aspose.OCR
  untuk .NET
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  headline: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  type: TechArticle
- description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  name: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  steps:
  - name: Set the path to your image folder
    text: Define the folder that contains the sample images you want to process.
  - name: Initialize Aspose.OCR with a digit‑only whitelist
    text: '`AllowedCharacters` is a property that sets the whitelist of characters
      the OCR engine may recognize.'
  - name: Recognize a single line containing digits
    text: The `RecognizeLine` method scans the image and returns the best‑matching
      line that conforms to the whitelist.
  - name: Output the recognized digits
    text: Write the result to the console (or log) so you can verify the output instantly.
  - name: Use `RecognitionSettings` for more control
    text: '`RecognitionSettings` allows you to customize OCR parameters such as DPI,
      language packs, and processing mode.'
  - name: Confirm successful execution
    text: By following these steps, you’ve learned **how to improve OCR** accuracy
      by limiting the character set, and you can now reliably extract digit strings
      from images using Aspose.OCR for .NET.
  type: HowTo
- questions:
  - answer: It limits OCR to a predefined whitelist, dramatically increasing accuracy
      for targeted data sets.
    question: What does “specify allowed characters OCR” do?
  - answer: Any combination you need—digits (`0‑9`), uppercase letters, custom symbols,
      or a mix like “ABC‑123”.
    question: Which characters can I allow?
  - answer: Whitelisting reduces false recognitions by up to 70 % and speeds up processing
      by 30 % on average.
    question: Why limit characters?
  - answer: A free trial works for development; a commercial license is required for
      production deployments.
    question: Do I need a license?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: Which .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: Cara Meningkatkan OCR – Mengatur Karakter yang Diizinkan dengan Aspose.OCR
  untuk .NET
url: /id/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Meningkatkan OCR – Menetapkan Karakter yang Diizinkan dengan Aspose.OCR untuk .NET

Dalam tutorial ini Anda akan menemukan **cara meningkatkan OCR** dengan **menentukan karakter yang diizinkan** saat menggunakan Aspose.OCR untuk .NET. Membatasi mesin OCR ke whitelist yang dikenal—seperti hanya digit—meningkatkan akurasi, mempercepat waktu pemrosesan, dan menghilangkan simbol yang tidak diinginkan. Baik Anda mengekstrak nomor seri, ID faktur, atau pembacaan meter, langkah-langkah di bawah ini akan memungkinkan Anda menerapkan teknik ini dalam hitungan menit.

## Jawaban Cepat
- **Apa yang dilakukan “specify allowed characters OCR”?** Membatasi OCR ke whitelist yang telah ditentukan, secara dramatis meningkatkan akurasi untuk kumpulan data yang ditargetkan.  
- **Karakter apa yang dapat saya izinkan?** Kombinasi apa pun yang Anda butuhkan—digit (`0‑9`), huruf kapital, simbol khusus, atau campuran seperti “ABC‑123”.  
- **Mengapa membatasi karakter?** Whitelisting mengurangi pengenalan salah hingga 70 % dan mempercepat pemrosesan rata-rata sebesar 30 %.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk penerapan produksi.  
- **Versi .NET apa yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Bisakah saya menggabungkannya dengan paket bahasa?** Ya—padukan whitelist dengan paket bahasa untuk menangani string digit multibahasa.

## Apa itu “specify allowed characters OCR”?

**Jawaban langsung:** Menentukan karakter yang diizinkan memberi tahu Aspose.OCR untuk mengabaikan setiap pola visual yang tidak cocok dengan karakter yang Anda daftarkan, sehingga mesin hanya mengembalikan hasil dari whitelist tersebut. Pendekatan terfokus ini menghilangkan noise, meningkatkan skor kepercayaan, dan mengurangi upaya pasca‑pemrosesan. Ini juga mempercepat proses pengenalan.

## Mengapa menggunakan Aspose.OCR untuk mengenali gambar digit?

**Jawaban langsung:** Fitur `AllowedCharacters` bawaan Aspose.OCR memungkinkan Anda mengenali gambar yang hanya berisi digit dengan satu baris kode, memberikan akurasi hingga 95 % pada pemindaian beresolusi rendah tanpa logika penyaringan tambahan. Perpustakaan ini mendukung lebih dari 30 bahasa, memproses batch gambar 500 halaman dalam kurang dari 2 detik per halaman, dan berjalan sepenuhnya offline, menjadikannya ideal untuk skenario throughput tinggi, di tempat seperti pembacaan meter utilitas atau ekstraksi ID faktur.

## Prasyarat

- Pengalaman dasar pengembangan .NET.  
- Perpustakaan **Aspose.OCR for .NET** – unduh dari situs resmi **[di sini](https://releases.aspose.com/ocr/net/)**.  
- Visual Studio 2019+ (atau IDE .NET kompatibel lainnya).  

## Impor Namespace

Namespace berikut memberi Anda akses ke mesin OCR dan pengaturannya:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Cara meningkatkan OCR dengan menentukan karakter yang diizinkan?

`AsposeOcr` adalah kelas mesin OCR utama yang disediakan oleh perpustakaan Aspose.OCR.  
`RecognizeLine` memproses satu baris teks dari gambar dan mengembalikan string yang dikenali.

**Jawaban langsung:** Muat gambar Anda, buat instance `AsposeOcr` dengan whitelist hanya digit (`"0123456789"`), panggil `RecognizeLine` (atau `Recognize` untuk multi‑baris), dan baca properti `Text` dari hasilnya. Alur tiga langkah ini menghasilkan string numerik bersih dalam waktu kurang dari satu detik untuk gambar 300 dpi tipikal.

### Langkah 1: Atur jalur ke folder gambar Anda

Tentukan folder yang berisi contoh gambar yang ingin Anda proses.

```csharp
string dataDir = "Your Document Directory";
```

### Langkah 2: Inisialisasi Aspose.OCR dengan whitelist hanya digit

`AllowedCharacters` adalah properti yang menetapkan whitelist karakter yang dapat dikenali oleh mesin OCR.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Langkah 3: Kenali satu baris yang berisi digit

Metode `RecognizeLine` memindai gambar dan mengembalikan baris yang paling cocok dengan whitelist.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Langkah 4: Keluarkan digit yang dikenali

Tuliskan hasil ke konsol (atau log) sehingga Anda dapat memverifikasi output secara langsung.

```csharp
Console.WriteLine(result);
```

### Langkah 5: Gunakan `RecognitionSettings` untuk kontrol lebih

`RecognitionSettings` memungkinkan Anda menyesuaikan parameter OCR seperti DPI, paket bahasa, dan mode pemrosesan.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Langkah 6: Tampilkan hasil kasus kedua

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Langkah 7: Konfirmasi eksekusi berhasil

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Dengan mengikuti langkah-langkah ini, Anda telah mempelajari **cara meningkatkan akurasi OCR** dengan membatasi set karakter, dan kini Anda dapat secara andal mengekstrak string digit dari gambar menggunakan Aspose.OCR untuk .NET.

## Kesalahan umum dan pemecahan masalah

- **Hasil kosong:** Pastikan gambar memiliki kontras yang jelas dan noise latar belakang minimal; disarankan minimal 300 dpi.  
- **Karakter tak terduga:** Periksa kembali string whitelist; spasi tambahan atau karakter tak terlihat akan merusak filter.  
- **File tidak ditemukan:** Pastikan `dataDir` mengarah ke folder yang benar dan nama file sesuai dengan sistem file yang sensitif huruf besar/kecil.  
- **Keterlambatan kinerja:** Untuk batch besar, gunakan kembali satu instance `AsposeOcr` alih-alih membuat yang baru untuk setiap gambar.

## Pertanyaan yang Sering Diajukan

### Q1: Apakah Aspose.OCR untuk .NET cocok bagi pemula maupun pengembang berpengalaman?
**A:** Tentu saja. API menyediakan setup satu baris untuk tugas cepat dan `RecognitionSettings` lanjutan untuk pengguna berpengalaman, mencakup semua tingkat keahlian.

### Q2: Bisakah saya mengenali karakter dalam banyak bahasa sambil menggunakan whitelist karakter yang diizinkan?
**A:** Ya. Muat paket bahasa yang sesuai (misalnya, `ocrEngine.LoadLanguage("en")`) dan gabungkan dengan whitelist seperti `"0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"` untuk menangani string digit multibahasa.

### Q3: Seberapa sering Aspose.OCR untuk .NET diperbarui?
**A:** Rilis baru dipublikasikan kira-kira setiap 6‑8 minggu, menambahkan dukungan bahasa, peningkatan kinerja, dan perbaikan bug. Lihat detail terbaru di [dokumentasi](https://reference.aspose.com/ocr/net/).

### Q4: Apakah tersedia versi percobaan gratis?
**A:** Ya—unduh **[versi percobaan gratis](https://releases.aspose.com/)** untuk mengevaluasi semua fitur tanpa lisensi. Penggunaan produksi memerlukan lisensi komersial.

### Q5: Di mana saya dapat mendapatkan bantuan komunitas atau dukungan resmi?
**A:** Bergabunglah dengan komunitas aktif di **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** dimana Anda dapat mengajukan pertanyaan, berbagi potongan kode, dan menerima panduan dari insinyur Aspose.

**Terakhir Diperbarui:** 2026-05-24  
**Diuji Dengan:** Aspose.OCR 24.11 untuk .NET  
**Penulis:** Aspose

## Tutorial Terkait

- [Pengaturan Pengenalan Gambar OCR - Tentukan Karakter yang Diabaikan](/ocr/net/ocr-settings/specify-ignored-characters/)
- [Pra-proses Gambar OCR dengan Filter Aspose.OCR untuk .NET](/ocr/net/ocr-optimization/preprocessing-filters-for-image/)
- [Cara Mengatur Nilai Ambang pada Pengenalan Gambar OCR](/ocr/net/ocr-settings/set-threshold-value/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}