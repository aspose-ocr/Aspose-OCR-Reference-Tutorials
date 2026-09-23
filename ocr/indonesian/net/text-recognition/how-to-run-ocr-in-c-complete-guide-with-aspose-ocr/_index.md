---
category: general
date: 2026-01-10
description: Cara menjalankan OCR pada gambar menggunakan Aspose OCR di C#. Pelajari
  cara mengekstrak teks dari gambar, menjalankan OCR pada gambar, dan memuat gambar
  untuk OCR dengan percepatan GPU.
draft: false
keywords:
- how to run OCR
- extract text from image
- run OCR on image
- load image for OCR
- Aspose OCR tutorial
language: id
og_description: Cara menjalankan OCR pada gambar menggunakan Aspose OCR. Tutorial
  ini menunjukkan cara mengekstrak teks dari gambar, menjalankan OCR pada gambar,
  dan memuat gambar untuk OCR secara efisien.
og_title: Cara Menjalankan OCR di C# – Panduan Langkah demi Langkah Lengkap
tags:
- OCR
- C#
- Aspose
title: Cara Menjalankan OCR di C# – Panduan Lengkap dengan Aspose OCR
url: /id/net/text-recognition/how-to-run-ocr-in-c-complete-guide-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menjalankan OCR di C# – Panduan Lengkap dengan Aspose OCR

Pernah bertanya-tanya **bagaimana cara menjalankan OCR** pada foto dan mengambil teksnya tanpa membuat Anda stres? Anda bukan satu-satunya. Baik Anda mendigitalkan faktur, memindai kwitansi, atau hanya mencoba membuat PDF yang dapat dicari, kemampuan mengekstrak teks dari gambar adalah kebutuhan harian bagi banyak pengembang.  

Dalam tutorial ini kami akan membahas contoh praktis, end‑to‑end yang menunjukkan **cara menjalankan OCR pada gambar** menggunakan pustaka Aspose OCR, lengkap dengan akselerasi GPU untuk kecepatan. Pada akhir tutorial Anda akan tahu persis cara memuat gambar untuk OCR, menyesuaikan penggunaan memori, dan mendapatkan hasil teks bersih—semua dalam beberapa menit kode.

## Apa yang Akan Anda Pelajari

- Cara menginisialisasi mesin Aspose OCR di C#  
- Cara **memuat gambar untuk OCR** dari disk atau stream  
- Cara mengaktifkan akselerasi GPU dan membatasi memori GPU  
- Cara **mengekstrak teks dari gambar** dan memverifikasi outputnya  
- Kesulitan umum (modul GPU tidak ada, batas memori) dan solusi cepat  

Tidak diperlukan pengalaman sebelumnya dengan Aspose OCR; cukup dengan lingkungan .NET yang berfungsi dan sebuah gambar contoh.

---

## Cara Menjalankan OCR pada Gambar dengan Aspose OCR

Hal pertama yang Anda butuhkan adalah cuplikan kode yang jelas dan dapat dijalankan yang melakukan seluruh pekerjaan. Di bawah ini adalah program lengkap yang dapat Anda salin, tempel, dan jalankan segera.

```csharp
// ------------------------------------------------------------
// Complete C# program: How to Run OCR with Aspose OCR
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Config;
using System.Drawing;          // For Image handling (optional)

// 1️⃣ Initialize the OCR engine
var ocrEngine = new OcrEngine();

// 2️⃣ Enable GPU acceleration (requires the Aspose OCR GPU module)
//    This speeds up recognition dramatically on supported hardware.
ocrEngine.Config.EnableGpuAcceleration = true;

// 3️⃣ (Optional) Limit GPU memory usage to 1024 MB to avoid OOM errors
ocrEngine.Config.GpuMemoryLimit = 1024;

// 4️⃣ Load the image you want to process
//    Replace the path with your own image file.
string imagePath = "YOUR_DIRECTORY/sample_skewed.jpg";
ocrEngine.Image = ImageStream.FromFile(imagePath);

// 5️⃣ Run the OCR recognition
ocrEngine.Recognize();

// 6️⃣ Retrieve the plain‑text result and display it
string recognizedText = ocrEngine.Text;
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

**Output yang diharapkan** (asumsi gambar contoh berisi frasa “Hello World”):

```
=== OCR Result ===
Hello World
```

> **Pro tip:** Jika Anda tidak melihat teks apa pun, periksa kembali apakah modul GPU terpasang dan jalur gambar sudah benar. Metode `ImageStream.FromFile` akan melempar pengecualian yang jelas jika file tidak dapat ditemukan.

---

## Ekstrak Teks dari Gambar Menggunakan Akselerasi GPU

Mengapa repot-repot menggunakan GPU? OCR hanya CPU berfungsi, tetapi dapat sangat lambat pada gambar berukuran besar atau beresolusi tinggi. Mengaktifkan akselerasi GPU (langkah 2 di atas) menyerahkan beban berat ke kartu grafis Anda, yang dapat memproses ribuan piksel per detik.

### Kapan Menggunakan GPU

- **Pemrosesan batch** – memindai puluhan faktur sekaligus.  
- **Pemindaian resolusi tinggi** – apa pun di atas 300 dpi.  
- **Aplikasi real‑time** – seperti pemindai seluler yang membutuhkan umpan balik instan.  

Jika lingkungan Anda tidak memiliki GPU yang kompatibel, cukup setel `EnableGpuAcceleration = false;` dan mesin akan otomatis beralih ke mode CPU.

---

## Jalankan OCR pada Gambar – Memuat Gambar dengan Benar

Memuat gambar adalah langkah **memuat gambar untuk OCR** yang sering membuat orang kebingungan. Aspose OCR mengharapkan sebuah `ImageStream`, yang dapat dibuat dari file, memory stream, atau bahkan URL. Berikut beberapa variasinya:

```csharp
// Load from file (as shown earlier)
ocrEngine.Image = ImageStream.FromFile("path/to/file.jpg");

// Load from a byte array (useful for web uploads)
byte[] imageBytes = File.ReadAllBytes("uploaded_image.png");
ocrEngine.Image = ImageStream.FromBytes(imageBytes);

// Load from a remote URL (requires internet)
ocrEngine.Image = ImageStream.FromUrl("https://example.com/image.tif");
```

**Kasus khusus:** Beberapa gambar mengandung saluran alfa (transparansi) yang membingungkan mesin OCR. Menghapus alfa sangat mudah:

```csharp
using (var bitmap = new Bitmap(imagePath))
{
    var nonAlpha = new Bitmap(bitmap.Width, bitmap.Height, System.Drawing.Imaging.PixelFormat.Format24bppRgb);
    using (var g = Graphics.FromImage(nonAlpha))
    {
        g.DrawImage(bitmap, 0, 0, bitmap.Width, bitmap.Height);
    }
    ocrEngine.Image = ImageStream.FromBitmap(nonAlpha);
}
```

Sekarang Anda telah mencakup cara paling umum untuk **memuat gambar untuk OCR**, memastikan mesin menerima format yang bersih dan didukung setiap saat.

---

## Tips Memuat Gambar untuk OCR Secara Efisien

1. **Ubah ukuran gambar besar** – OCR tidak memerlukan foto 4 K; memperkecil hingga lebar ~1500 px mempercepat proses tanpa mengurangi akurasi.  
2. **Konversi ke skala abu‑abu** – mengurangi noise dan dapat meningkatkan pengenalan pada pemindaian kontras rendah.  
3. **Pra‑proses dengan deskew** – jika gambar Anda miring, deskew bawaan Aspose OCR dapat diaktifkan melalui `ocrEngine.Config.EnableDeskew = true;`.  

Penyesuaian ini sangat berguna ketika Anda **mengekstrak teks dari gambar** secara massal.

---

## Kesulitan Umum & Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| `System.DllNotFoundException: Aspose.OCR.Gpu.dll` | Modul GPU tidak terpasang | Instal paket Aspose OCR GPU atau nonaktifkan GPU (`EnableGpuAcceleration = false`). |
| Output kosong | Jalur gambar salah atau format tidak didukung | Verifikasi jalur `ImageStream.FromFile`; coba muat dari byte untuk memastikan file dibaca dengan benar. |
| Kesalahan kehabisan memori | Batas memori GPU terlalu rendah untuk batch besar | Tingkatkan `GpuMemoryLimit` (mis., 2048) atau proses gambar dalam potongan lebih kecil. |
| Karakter kacau | Gambar memiliki noise berat atau kontras rendah | Pra‑proses: binarisasi, despeckle, atau tingkatkan DPI sebelum OCR. |

---

## Contoh Lengkap yang Berfungsi – Gabungkan Semua

Di bawah ini adalah aplikasi konsol ringkas yang menggabungkan praktik terbaik yang kami bahas: akselerasi GPU, pembatasan memori, pra‑proses gambar, dan penanganan error.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Config;

class Program
{
    static void Main()
    {
        try
        {
            // Initialize OCR engine
            var ocr = new OcrEngine();

            // Enable GPU (set false if no GPU)
            ocr.Config.EnableGpuAcceleration = true;
            ocr.Config.GpuMemoryLimit = 1024;          // 1 GB limit
            ocr.Config.EnableDeskew = true;            // Auto‑deskew

            // Load and optionally preprocess image
            string path = "YOUR_DIRECTORY/sample_skewed.jpg";
            using (var original = new Bitmap(path))
            {
                // Resize if too large
                const int maxWidth = 1500;
                Bitmap processed = original.Width > maxWidth
                    ? new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width))
                    : new Bitmap(original);

                // Convert to grayscale (optional but often helpful)
                var gray = new Bitmap(processed.Width, processed.Height, System.Drawing.Imaging.PixelFormat.Format24bppRgb);
                using (var g = Graphics.FromImage(gray))
                {
                    var cm = new System.Drawing.Imaging.ColorMatrix(
                        new float[][]{
                            new float[]{0.3f,0.3f,0.3f,0,0},
                            new float[]{0.59f,0.59f,0.59f,0,0},
                            new float[]{0.11f,0.11f,0.11f,0,0},
                            new float[]{0,0,0,1,0},
                            new float[]{0,0,0,0,1}});
                    var ia = new System.Drawing.Imaging.ImageAttributes();
                    ia.SetColorMatrix(cm);
                    g.DrawImage(processed, new Rectangle(0,0,processed.Width,processed.Height),
                                0,0,processed.Width,processed.Height, GraphicsUnit.Pixel, ia);
                }

                // Feed the processed bitmap into OCR
                ocr.Image = ImageStream.FromBitmap(gray);
            }

            // Run recognition
            ocr.Recognize();

            // Output result
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocr.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR: {ex.Message}");
        }
    }
}
```

Menjalankan program ini akan mencetak teks bersih yang diekstrak dari gambar Anda, menunjukkan cara yang kuat untuk **mengekstrak teks dari gambar** bahkan ketika sumbernya tidak sempurna.

---

## Kesimpulan

Kami telah membahas **cara menjalankan OCR** pada gambar menggunakan Aspose OCR, mulai dari menginisialisasi mesin hingga memuat gambar, mengaktifkan akselerasi GPU, dan menangani kasus khusus. Anda kini memiliki referensi yang kuat dan dapat dijadikan acuan yang dapat Anda salin‑tempel ke proyek .NET apa pun dan mulai **mengekstrak teks dari gambar** segera.

Langkah selanjutnya? Coba proses halaman PDF, bereksperimen dengan bahasa berbeda (set `ocrEngine.Config.Language = "spa"` untuk bahasa Spanyol), atau integrasikan alur ini ke dalam API web yang memproses unggahan secara langsung. Langit adalah batasnya, dan dengan alat yang kami bahas, Anda siap menghadapi tantangan OCR apa pun.

Selamat coding, semoga teks Anda selalu bersih dan OCR Anda cepat!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}