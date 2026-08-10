---
category: general
date: 2026-02-19
description: tutorial c# ocr – pelajari cara mengekstrak teks dari gambar, membaca
  teks gambar, mengonversi gambar menjadi teks, dan mengenali teks gambar menggunakan
  Aspose.OCR dalam hitungan menit.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- read image text
- convert image to text
- recognize image text
language: id
og_description: Tutorial OCR c# menunjukkan cara mengekstrak teks dari gambar, membaca
  teks gambar, mengonversi gambar menjadi teks, dan mengenali teks gambar menggunakan
  Aspose OCR.
og_title: tutorial OCR c# – Ekstrak Teks dari Gambar dengan Aspose OCR
tags:
- OCR
- C#
- Aspose
title: 'Tutorial OCR C#: Ekstrak Teks dari Gambar dengan Aspose OCR'
url: /id/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial c# ocr – Ekstrak Teks dari Gambar dengan Aspose OCR

Pernah bertanya-tanya bagaimana cara **mengambil teks dari gambar** sambil tetap berada dalam lingkungan C# murni? Itulah yang diselesaikan oleh **tutorial c# ocr** ini. Dalam beberapa langkah saja Anda akan belajar membaca teks gambar, mengonversi gambar ke teks, dan bahkan mengenali teks gambar dalam berbagai bahasa menggunakan pustaka Aspose.OCR.

Dalam panduan ini kami akan membahas semua yang Anda perlukan: mulai dari menginstal paket NuGet hingga menangani lisensi, mengatur bahasa, dan mencetak hasil. Pada akhir panduan Anda akan memiliki aplikasi konsol siap‑jalankan yang mengubah gambar apa pun—seperti faktur yang dipindai atau tangkapan layar—menjadi teks yang dapat dicari.

## Apa yang Anda Butuhkan

- .NET 6.0 SDK atau yang lebih baru (kode ini juga bekerja pada .NET Framework 4.7+)  
- Visual Studio 2022 (atau editor apa pun yang Anda sukai)  
- File lisensi Aspose.OCR *opsional* – pustaka ini berfungsi dalam mode evaluasi, tetapi lisensi menghilangkan watermark.  
- Gambar contoh (misalnya `cyrillic_sample.jpg`) yang ditempatkan di suatu tempat pada disk.

Tidak ada alat pihak ketiga lain yang diperlukan; Aspose.OCR menangani semua proses berat di balik layar.

---

![c# ocr tutorial sample image showing Cyrillic text](/images/ocr-sample.jpg "c# ocr tutorial – sample image for OCR")

## tutorial c# ocr – Menyiapkan Aspose OCR

Pertama, tambahkan paket Aspose.OCR ke proyek Anda:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, Anda juga dapat klik kanan proyek → **Manage NuGet Packages** dan cari *Aspose.OCR*.

### Mengapa lisensi penting

Aspose.OCR berjalan dalam mode evaluasi 30‑hari tanpa lisensi. Kelas `License` hanya menunjuk ke file `.lic` Anda; setelah diatur, mesin berhenti menyisipkan footer evaluasi ke dalam output.

```csharp
// Optional: apply your Aspose.OCR license to unlock full features
// new License().SetLicense("Aspose.OCR.lic");
```

Jika Anda melewatkan baris ini selama pengembangan, OCR tetap berfungsi—hanya ingat pemberitahuan evaluasi akan muncul dalam teks yang diekstrak.

## Ekstrak teks dari gambar – Membuat OCR Engine

Inti dari setiap **tutorial c# ocr** adalah objek `OcrEngine`. Objek ini mengabstraksi seluruh pipeline pengenalan.

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Step 1: (Optional) Apply your license – see above
        // new License().SetLicense("Aspose.OCR.lic");

        // Step 2: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 3: Choose the language you want to recognize
        // For this demo we use Cyrillic, but you can pick English, Arabic, etc.
        ocrEngine.Language = Language.Cyrillic;

        // Step 4: Run OCR on the target picture
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/cyrillic_sample.jpg");

        // Step 5: Output the recognized text to the console
        Console.WriteLine("Recognized text:");
        Console.WriteLine(result.Text);
    }
}
```

### Apa yang sebenarnya dilakukan kode ini

- **Menginstansiasi `OcrEngine`** membuat konteks pemrosesan baru.  
- **Mengatur `Language`** memberi tahu Aspose set karakter apa yang diharapkan; ini secara dramatis meningkatkan akurasi karena mesin dapat menerapkan heuristik khusus bahasa.  
- **`RecognizeImage`** memuat file, menjalankan serangkaian langkah pra‑pemrosesan gambar (deskew, binarisasi, penghilangan noise) dan akhirnya menjalankan pengenalan jaringan saraf.  
- **`result.Text`** menyimpan representasi teks polos—sempurna untuk skenario **convert image to text**.

## Baca teks gambar – Menangani Berbagai Jenis File

Aspose.OCR tidak terbatas pada JPEG. Ia mendukung PNG, BMP, TIFF, dan bahkan halaman PDF (sebagai gambar). Jika Anda perlu memproses batch, bungkus pemanggilan dalam loop sederhana:

```csharp
string[] files = Directory.GetFiles(@"YOUR_DIRECTORY", "*.*", SearchOption.TopDirectoryOnly)
                          .Where(f => f.EndsWith(".jpg") || f.EndsWith(".png") || f.EndsWith(".tif"))
                          .ToArray();

foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(res.Text);
}
```

### Kasus tepi: Gambar kosong atau rusak

Jika `RecognizeImage` menerima file null atau tidak dapat dibaca, ia melempar `ArgumentException`. Guard singkat menjaga **tutorial c# ocr** Anda tetap kuat:

```csharp
if (!File.Exists(file))
{
    Console.WriteLine($"File not found: {file}");
    continue;
}
```

## Kenali teks gambar – Penyetelan Halus untuk Akurasi

Kadang pengaturan default melewatkan beberapa karakter, terutama pada pemindaian kontras rendah. Aspose.OCR menyediakan beberapa pengaturan yang dapat Anda sesuaikan:

| Properti               | Apa yang dilakukan                              | Kasus penggunaan umum |
|------------------------|-------------------------------------------|------------------|
| `ocrEngine.PreprocessingOptions.Deskew` | Memutar gambar untuk memperbaiki kemiringan | Dokumen yang dipindai |
| `ocrEngine.PreprocessingOptions.NoiseRemoval` | Menghilangkan bintik-bintik | Foto lama |
| `ocrEngine.Language`   | Model bahasa (Cyrillic, English, dll.) | OCR multibahasa |

Contoh mengaktifkan deskew:

```csharp
ocrEngine.PreprocessingOptions.Deskew = true;
```

Penyesuaian ini membantu Anda **mengambil teks dari gambar** yang tidak teralign dengan sempurna, meningkatkan tingkat keberhasilan operasi **baca teks gambar** Anda.

## Output yang Diharapkan

Menjalankan kode contoh terhadap `cyrillic_sample.jpg` (yang berisi frasa “Привет мир”) menghasilkan sesuatu seperti:

```
Recognized text:
Привет мир
```

Jika Anda berada dalam mode evaluasi, Anda juga akan melihat baris tambahan:

```
--- Evaluation version. Use a licensed copy for production. ---
```

Baris tersebut menghilang begitu Anda menyediakan file lisensi yang valid.

---

## Kesalahan Umum & Cara Menghindarinya

1. **Pengaturan bahasa yang salah** – Menggunakan `Language.English` pada teks Cyrillic akan menghasilkan karakter acak. Selalu sesuaikan bahasa dengan sumber.  
2. **Gambar besar** – Memproses foto 10 MP dapat lambat. Turunkan skala gambar terlebih dahulu (`Bitmap.Resize`) jika kecepatan lebih penting daripada akurasi pixel‑sempurna.  
3. **Ketergantungan yang hilang** – Aspose.OCR menyertakan binary native; pastikan folder output Anda berisi `Aspose.OCR.Native.dll` (NuGet menangani ini, tetapi pipeline build khusus mungkin memerlukan langkah penyalinan).

## Langkah Selanjutnya – Melampaui Dasar

- **Konversi batch**: Gabungkan loop yang ditunjukkan sebelumnya dengan `Task.Run` asynchronous untuk mempercepat folder besar.  
- **Ekspor ke PDF**: Setelah Anda **convert image to text**, masukkan string ke generator PDF (misalnya Aspose.PDF) untuk membuat PDF yang dapat dicari.  
- **Integrasikan dengan Azure Functions**: Ubah logika OCR menjadi endpoint serverless yang memproses unggahan secara langsung.  

Semua ekstensi ini melanjutkan tema **mengambil teks dari gambar** dan **baca teks gambar** dalam aplikasi dunia nyata.

---

## Kesimpulan

Anda baru saja menyelesaikan **tutorial c# ocr** yang menunjukkan cara membaca teks gambar, mengonversi gambar ke teks, dan mengenali teks gambar menggunakan Aspose.OCR. Contoh lengkap yang dapat dijalankan di atas memperlihatkan setiap langkah—dari lisensi hingga pemilihan bahasa dan penanganan error—sehingga Anda dapat menambahkan kode ini ke proyek .NET mana pun dan mulai mengekstrak teks segera.

Silakan bereksperimen dengan berbagai bahasa, menyesuaikan opsi pra‑pemrosesan, atau menghubungkan output ke basis data untuk arsip yang dapat dicari. Jika Anda menemukan kendala, dokumentasi Aspose adalah referensi yang solid, namun kode di sini seharusnya langsung berfungsi untuk kebanyakan skenario.

Selamat coding, dan semoga gambar Anda selalu dapat dibaca!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}