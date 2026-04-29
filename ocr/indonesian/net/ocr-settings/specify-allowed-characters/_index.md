---
description: Pelajari cara menentukan karakter yang diizinkan pada OCR dengan Aspose.OCR
  untuk .NET dan mengenali gambar digit secara efisien. Ikuti panduan langkah demi
  langkah untuk membatasi OCR hanya pada digit.
linktitle: Specify Allowed Characters OCR – Using Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Tentukan Karakter yang Diizinkan OCR – Menggunakan Aspose.OCR untuk .NET
url: /id/net/ocr-settings/specify-allowed-characters/
weight: 13
---

 final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tentukan Karakter yang Diizinkan OCR – Menggunakan Aspose.OCR untuk .NET

Dalam tutorial ini, Anda akan belajar cara **specify allowed characters ocr** dengan Aspose.OCR untuk .NET, memungkinkan Anda membatasi output OCR hanya pada karakter yang Anda butuhkan. Ini sangat berguna ketika Anda perlu **recognize digits image** file seperti nomor seri, ID faktur, atau string mirip barcode. Kami akan membahas pengaturan, kode, dan beberapa skenario praktis sehingga Anda dapat langsung menerapkan teknik ini.

## Jawaban Cepat
- **Apa yang dilakukan “specify allowed characters ocr”?** Ini membatasi OCR pada sekumpulan karakter yang telah ditentukan, meningkatkan akurasi untuk data yang ditargetkan.  
- **Karakter apa yang dapat saya izinkan?** Kombinasi apa pun yang Anda butuhkan—digit, huruf, atau simbol khusus (mis., “0123456789”).  
- **Mengapa membatasi karakter?** Mengurangi pengenalan yang salah dan mempercepat pemrosesan ketika set karakter yang diharapkan diketahui.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Versi .NET mana yang didukung?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Apa itu “specify allowed characters ocr”?
Saat OCR memindai sebuah gambar, ia mencoba mencocokkan setiap pola visual dengan seluruh alfabet karakter yang mungkin. Dengan **specify allowed characters ocr**, Anda memberi tahu mesin untuk mengabaikan semua yang berada di luar daftar putih Anda, yang secara dramatis meningkatkan akurasi pengenalan untuk kumpulan data yang terbatas.

## Mengapa menggunakan Aspose.OCR untuk mengenali gambar digit?
Aspose.OCR menyediakan API yang bersih dan fluently untuk pengembang .NET. Opsi `AllowedCharacters` bawaan memungkinkan Anda fokus pada skenario hanya digit tanpa menulis logika pasca‑pemrosesan khusus. Ini sempurna untuk:
- Membaca pembacaan meter, nomor faktur, atau kode produk.  
- Memvalidasi data yang dimasukkan pengguna yang diambil dari formulir yang dipindai.  
- Mempercepat pemrosesan batch di mana set karakter sudah diketahui sebelumnya.

## Prasyarat

Sebelum menyelam ke kode, pastikan Anda memiliki:

- Pengetahuan yang cukup tentang pengembangan .NET.  
- **Aspose.OCR for .NET** library. Anda dapat mengunduhnya [di sini](https://releases.aspose.com/ocr/net/).  
- Visual Studio (atau IDE .NET pilihan lainnya).  

## Impor Namespace

Dalam proyek .NET Anda, impor namespace yang diperlukan untuk memanfaatkan fungsionalitas Aspose.OCR:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Cara menentukan karakter yang diizinkan OCR – Panduan langkah demi langkah

### Langkah 1: Tetapkan jalur ke folder gambar Anda

Pertama, tentukan di mana gambar contoh Anda disimpan.

```csharp
string dataDir = "Your Document Directory";
```

### Langkah 2: Inisialisasi Aspose.OCR dengan daftar putih hanya digit

Buat instance `AsposeOcr` dan berikan karakter yang ingin Anda izinkan—dalam hal ini, semua digit.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Langkah 3: Kenali satu baris yang berisi digit

Gunakan metode `RecognizeLine` untuk mengekstrak teks dari gambar yang hanya berisi angka.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Langkah 4: Keluarkan digit yang dikenali

Cetak hasil ke konsol sehingga Anda dapat memverifikasi output.

```csharp
Console.WriteLine(result);
```

### Langkah 5: Gunakan RecognitionSettings untuk kontrol lebih

Jika Anda memerlukan kontrol yang lebih halus—seperti memaksa pengenalan satu baris—Anda dapat menggunakan overload yang menerima `RecognitionSettings`.

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

Dengan mengikuti langkah-langkah ini, Anda telah belajar cara **specify allowed characters ocr** dan secara efisien **recognize digits image** konten menggunakan Aspose.OCR untuk .NET.

## Masalah umum dan pemecahan masalah

- **Hasil kosong:** Pastikan kualitas gambar cukup (kontras jelas, noise minimal).  
- **Karakter yang salah dikembalikan:** Periksa kembali bahwa string whitelist persis cocok dengan karakter yang Anda harapkan.  
- **File tidak ditemukan:** Verifikasi bahwa `dataDir` mengarah ke folder yang benar dan nama file cocok dengan sensitivitas huruf.

## Pertanyaan yang Sering Diajukan

### Q1: Apakah Aspose.OCR untuk .NET cocok untuk pemula maupun pengembang berpengalaman?  
**A:** Tentu saja! API ini dirancang agar intuitif bagi pemula sekaligus menawarkan opsi lanjutan untuk pengguna berpengalaman.

### Q2: Bisakah saya menggunakan Aspose.OCR untuk .NET untuk mengenali karakter dalam banyak bahasa?  
**A:** Ya, Aspose.OCR mendukung berbagai bahasa. Anda dapat menggabungkan paket bahasa dengan fitur allowed‑characters untuk skenario multibahasa.

### Q3: Seberapa sering Aspose.OCR untuk .NET diperbarui?  
**A:** Pembaruan dirilis secara reguler untuk menambahkan fitur baru, meningkatkan akurasi, dan memastikan kompatibilitas. Periksa [dokumentasi](https://reference.aspose.com/ocr/net/) untuk detail versi terbaru.

### Q4: Apakah tersedia versi percobaan gratis untuk Aspose.OCR untuk .NET?  
**A:** Ya, Anda dapat menjelajahi kemampuannya dengan mengunduh [free trial](https://releases.aspose.com/).

### Q5: Di mana saya dapat mencari bantuan atau terhubung dengan komunitas untuk dukungan?  
**A:** Kunjungi [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk mengajukan pertanyaan, berbagi pengalaman, dan mendapatkan bantuan dari insinyur Aspose serta pengembang lainnya.

---

**Terakhir Diperbarui:** 2026-02-15  
**Diuji Dengan:** Aspose.OCR 24.11 untuk .NET  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}