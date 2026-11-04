---
category: general
date: 2026-04-11
description: Pelajari cara menonaktifkan OCR di Aspose OCR untuk C# agar dapat berjalan
  secara offline, mengekstrak teks dari gambar tanpa internet, dan memuat gambar dengan
  benar untuk OCR.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: id
og_description: Cara menonaktifkan OCR di Aspose OCR untuk C# dan menjalankannya secara
  offline, mengekstrak teks dari gambar tanpa memerlukan internet, serta memuat gambar
  untuk OCR dengan mudah.
og_title: Cara Menonaktifkan OCR di C# – Panduan OCR Offline Aspose
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Cara Menonaktifkan OCR di C# – Panduan OCR Offline Aspose
url: /id/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menonaktifkan OCR di C# – Panduan Aspose OCR Offline

Pernah bertanya-tanya **bagaimana cara menonaktifkan OCR** ketika Anda membutuhkan solusi yang benar‑benar offline? Mungkin Anda sedang membangun aplikasi desktop yang aman dan tidak dapat mengandalkan koneksi jaringan, atau Anda hanya ingin menghindari unduhan yang tidak terduga. Bagaimanapun, kabar baiknya adalah Aspose OCR memungkinkan Anda mematikan pengambilan sumber daya otomatisnya, menunjuk ke folder lokal, dan menjaga semuanya tetap di‑lokasi. Dalam tutorial ini Anda juga akan melihat cara **mengekstrak teks dari gambar** dan **memuat gambar untuk OCR** dengan benar tanpa kendala.

Kami akan membimbing Anda melalui contoh lengkap yang siap dijalankan yang menunjukkan setiap langkah—dari menginisialisasi engine hingga mencetak teks Jepang yang dikenali. Tanpa dokumen eksternal, tanpa keajaiban tersembunyi; hanya kode C# biasa yang dapat Anda masukkan ke dalam proyek Anda hari ini. Pada akhir tutorial Anda akan mengerti mengapa menonaktifkan fitur unduhan otomatis penting, cara mengatur jalur sumber daya, dan jebakan‑jebakan apa yang harus diwaspadai.

## Prasyarat

- .NET 6.0 (atau versi .NET terbaru) terpasang di mesin Anda.  
- Paket NuGet Aspose.OCR untuk .NET (`Install-Package Aspose.OCR`).  
- Folder yang sudah berisi sumber daya bahasa yang Anda perlukan (misalnya model Jepang).  
- File gambar (`japan_doc.png`) yang ingin Anda proses dengan OCR.  

Jika Anda belum memiliki paket bahasa, unduh sekali saja dari portal Aspose, ekstrak ke folder seperti `AsposeOCRResources`, dan Anda siap. Tidak ada unduhan lebih lanjut yang akan terjadi setelah Anda menonaktifkan fitur unduhan otomatis.

![How to disable OCR offline](/images/how-to-disable-ocr.png "how to disable OCR illustration")

## Langkah 1 – Buat Instance OCR Engine  

Hal pertama yang Anda lakukan adalah menginstansiasi `OcrEngine`. Anggap objek ini sebagai otak yang akan membaca gambar Anda.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Mengapa ini penting:** Tanpa engine Anda tidak dapat mengonfigurasi apa pun. Objek tersebut menyimpan semua pengaturan, termasuk flag penting yang memberi tahu perpustakaan apakah ia boleh mengakses internet.

## Langkah 2 – Nonaktifkan Unduhan Sumber Daya Otomatis  

Secara default Aspose OCR akan mencoba mengambil file bahasa yang hilang secara otomatis. Untuk menjaga semuanya tetap offline, ubah saklar `AutoDownloadResources` menjadi `false`.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Tips pro:** Mematikan ini tidak hanya menjamin privasi tetapi juga mempercepat proses pengenalan pertama karena engine tidak akan membuang waktu memeriksa pembaruan.

## Langkah 3 – Arahkan ke Folder Sumber Daya Lokal Anda  

Sekarang beri tahu engine di mana paket bahasa yang sudah diunduh sebelumnya berada. Ini adalah jalur yang Anda siapkan pada bagian prasyarat.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **Apa yang bisa salah?** Jika jalur salah atau file bahasa yang diperlukan tidak ada, engine akan melempar `ResourceNotFoundException`. Periksa kembali ejaan folder dan pastikan model Jepang (`jpn.traineddata`) ada.

## Langkah 4 – Pilih Model Bahasa Lokal  

Pilih bahasa yang sebenarnya Anda miliki di disk. Pada contoh kami menggunakan bahasa Jepang, tetapi Anda dapat mengganti `Language.Japanese` dengan bahasa lain yang telah Anda unduh.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Kasus khusus:** Beberapa bahasa memerlukan kamus tambahan (misalnya, bahasa Mandarin). Pastikan file tambahan tersebut juga berada di folder sumber daya yang sama.

## Langkah 5 – Muat Gambar untuk OCR  

Di sinilah kita **memuat gambar untuk OCR**. Metode `ImageStream.FromFile` membaca file ke dalam stream yang dapat diproses oleh Aspose.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Tip:** Format yang didukung meliputi PNG, JPEG, BMP, dan TIFF. Jika Anda perlu menangani PDF, konversi setiap halaman menjadi gambar terlebih dahulu.

## Langkah 6 – Jalankan Proses Pengenalan  

Sekarang engine benar‑benar membaca piksel dan mencoba mengubahnya menjadi teks.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Mengapa langkah ini dapat lambat:** OCR membutuhkan banyak CPU, terutama untuk gambar beresolusi tinggi. Jika kinerja menjadi perhatian, pertimbangkan menurunkan skala gambar sebelum pengenalan.

## Langkah 7 – Keluarkan Teks yang Diekstrak  

Akhirnya, kami **mengekstrak teks dari gambar** dan mencetaknya ke konsol.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Menjalankan program harus menampilkan karakter Jepang yang ada di `japan_doc.png`. Jika semuanya telah diatur dengan benar, Anda akan melihat blok teks Unicode yang bersih di konsol Anda.

### Output yang Diharapkan

```
これはサンプルの日本語テキストです。
```

*(Output sebenarnya akan bergantung pada isi gambar.)*

## Kesalahan Umum & Cara Menghindarinya  

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **File bahasa hilang** | `AutoDownloadResources` bernilai false, sehingga engine tidak dapat mengambilnya. | Pastikan `ResourcesPath` mengarah ke folder yang berisi `jpn.traineddata`. |
| **Jalur gambar tidak tepat** | `ImageStream.FromFile` melempar `FileNotFoundException`. | Gunakan jalur absolut atau pastikan direktori kerja diatur dengan benar. |
| **Format gambar tidak didukung** | Aspose hanya membaca format tertentu. | Konversi gambar Anda ke PNG atau JPEG sebelum memanggil `FromFile`. |
| **Kekurangan memori pada gambar besar** | OCR memuat seluruh gambar ke dalam memori. | Ubah ukuran atau bagi gambar menjadi beberapa bagian, atau tingkatkan batas memori proses. |

## Memperluas Contoh  

- **Pemrosesan batch:** Loop melalui direktori gambar, panggil kode pengenalan yang sama, dan tulis setiap hasil ke file `.txt` terpisah.  
- **Bahasa berbeda:** Ganti `Language.Japanese` dengan `Language.English` (atau bahasa lain) setelah menempatkan file sumber daya yang sesuai.  
- **Pra‑pemrosesan khusus:** Gunakan Aspose.Imaging untuk mengoreksi kemiringan atau meningkatkan kontras sebelum OCR demi akurasi yang lebih baik.

## Kesimpulan  

Sekarang Anda tahu **cara menonaktifkan OCR** di Aspose OCR untuk C# dan menjalankannya sepenuhnya offline. Dengan mengatur `AutoDownloadResources` menjadi `false`, mengarahkan engine ke folder sumber daya lokal, dan **memuat gambar untuk OCR** dengan benar, Anda dapat dengan andal **mengekstrak teks dari gambar** tanpa pernah menyentuh internet. Pendekatan ini ideal untuk lingkungan yang aman, pipeline CI, atau skenario apa pun di mana akses jaringan terbatas.

Siap untuk langkah selanjutnya? Cobalah memproses seluruh folder PDF yang dipindai, bereksperimen dengan paket bahasa yang berbeda, atau integrasikan hasil OCR ke dalam basis data yang dapat dicari. Pengaturan offline yang Anda bangun hari ini merupakan fondasi yang kuat untuk alur kerja pemrosesan dokumen on‑premises apa pun.

Selamat coding, dan jangan ragu meninggalkan komentar jika Anda mengalami kendala!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}