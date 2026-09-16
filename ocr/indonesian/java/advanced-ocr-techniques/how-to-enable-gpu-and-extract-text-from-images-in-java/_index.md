---
category: general
date: 2026-09-16
description: Pelajari cara mengaktifkan GPU untuk OCR yang lebih cepat di Java, mengenali
  teks dari file gambar, dan mengonversi gambar menjadi teks menggunakan Aspose OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize text from image
- extract text from image
- how to perform ocr
- convert image to text
language: id
lastmod: 2026-09-16
og_description: Cara mengaktifkan GPU untuk OCR di Java, mengenali teks dari file
  gambar, dan mengonversi gambar menjadi teks dengan Aspose OCR – panduan lengkap
  langkah demi langkah.
og_image_alt: Screenshot showing Java code that enables GPU for OCR and extracts text
  from an image
og_title: Cara mengaktifkan GPU dan mengekstrak teks dari gambar di Java
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  headline: How to enable GPU and extract text from images in Java
  type: TechArticle
- description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  name: How to enable GPU and extract text from images in Java
  steps:
  - name: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
    text: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
  - name: '**Segmentation** – locate text lines, words, and characters.'
    text: '**Segmentation** – locate text lines, words, and characters.'
  - name: '**Classification** – match each character against the built‑in language
      model.'
    text: '**Classification** – match each character against the built‑in language
      model.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Cara mengaktifkan GPU dan mengekstrak teks dari gambar di Java
url: /id/java/advanced-ocr-techniques/how-to-enable-gpu-and-extract-text-from-images-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengaktifkan GPU dan mengekstrak teks dari gambar di Java

Jika Anda perlu **how to enable GPU** untuk pengenalan karakter optik, panduan ini menunjukkan langkah‑langkah tepatnya. Dengan mengaktifkan percepatan GPU Anda dapat **recognize text from image** file hingga beberapa kali lebih cepat dibandingkan pemrosesan hanya CPU. Contohnya menggunakan Aspose OCR untuk Java, tetapi konsepnya berlaku untuk perpustakaan OCR yang kompatibel dengan GPU mana pun.

Dalam tutorial ini Anda akan belajar cara:

* Mengaktifkan percepatan GPU di mesin OCR.  
* Memuat sebuah gambar dan **extract text from image** file.  
* **Convert image to text** dengan hanya beberapa baris kode.  

Tidak diperlukan layanan eksternal—semua berjalan secara lokal di mesin Anda. Lingkungan pengembangan Java dasar dan perpustakaan Aspose OCR untuk Java adalah satu‑satunya prasyarat.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

| Requirement | Version / Detail |
|-------------|------------------|
| Java Development Kit (JDK) | 8 atau lebih baru |
| Maven atau Gradle (untuk manajemen dependensi) | Versi terbaru apa pun |
| GPU dengan dukungan CUDA (opsional tetapi disarankan) | GPU NVIDIA dengan driver ≥ 450 |
| Aspose OCR untuk Java library | 23.9 atau lebih baru (unduh dari situs web Aspose) |

Jika Anda tidak memiliki GPU, kode tetap berfungsi; ia hanya akan berjalan di CPU.

## Langkah 1: Tambahkan Aspose OCR ke proyek Anda

Untuk Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

Untuk Gradle, letakkan ini di `build.gradle`:

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

## Langkah 2: Cara mengaktifkan GPU untuk mesin OCR

Tugas utama adalah memberi tahu `OcrEngine` untuk menggunakan GPU. Aspose OCR menyediakan sebuah flag sederhana:

```java
// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the “how to enable gpu” step
ocrEngine.setGpuEnabled(true);
```

**Mengapa ini penting:** Ketika `setGpuEnabled(true)` dipanggil, perpustakaan memuat kernel berbasis CUDA yang memparalelkan tahap pra‑pemrosesan gambar dan segmentasi karakter. Pada kartu NVIDIA modern, Anda dapat melihat peningkatan kecepatan 2‑4× dibandingkan jalur CPU default.

> **Pro tip:** Pastikan GPU Anda terdeteksi dengan menjalankan `SystemInfo.isCudaSupported()` sebelum mengaktifkan flag. Jika metode mengembalikan `false`, mesin akan otomatis kembali ke CPU.

## Langkah 3: Muat gambar yang ingin diproses

Anda dapat memberi mesin OCR format gambar apa pun yang didukung oleh Aspose (JPEG, PNG, BMP, TIFF, dll.). Berikut cara memuat file JPEG:

```java
// Load the image that contains the text to be recognized
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

**Kasus khusus:** Jika gambar berukuran besar (lebih dari 5 MB) pertimbangkan untuk mengubah ukurannya terlebih dahulu guna mengurangi konsumsi memori. Mesin OCR bekerja paling baik dengan gambar sekitar 300 dpi.

## Langkah 4: Lakukan OCR dan **recognize text from image**

Sekarang mesin telah dikonfigurasi dan gambar telah dimuat, Anda dapat menjalankan proses pengenalan:

```java
// Execute OCR – this is the core “how to perform ocr” step
String recognizedText = ocrEngine.recognize();
```

Metode `recognize()` mengembalikan `String` teks biasa. Secara internal, mesin menjalankan beberapa tahap:

1. **Pre‑processing** – menghilangkan kemiringan, binarisasi, dan meningkatkan kontras (dipercepat GPU).  
2. **Segmentation** – menemukan baris teks, kata, dan karakter.  
3. **Classification** – mencocokkan setiap karakter dengan model bahasa bawaan.

Karena GPU aktif, langkah 1 dan 2 paling diuntungkan dari eksekusi paralel.

## Langkah 5: Tampilkan atau simpan teks yang diekstrak

Akhirnya, keluarkan hasil ke konsol, file, atau pemroses hilir apa pun:

```java
// Show the extracted text – this completes the “convert image to text” flow
System.out.println("Recognized text:\n" + recognizedText);

// Optional: write the text to a file
Files.write(Paths.get("output.txt"), recognizedText.getBytes(StandardCharsets.UTF_8));
```

**Output tipikal** (untuk gambar contoh yang berisi “Hello World”):

```
Recognized text:
Hello World
```

Jika OCR gagal mendeteksi karakter apa pun, `recognizedText` akan menjadi string kosong. Dalam kasus tersebut, periksa kembali kualitas gambar atau nonaktifkan GPU untuk membandingkan kinerja.

## Menangani jebakan umum

| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| **GPU not detected** | Driver CUDA tidak ada atau GPU tidak didukung | Instal driver NVIDIA terbaru dan verifikasi dengan `nvidia-smi`. |
| **Incorrect characters** | Kontras rendah atau latar belakang berisik | Pra‑proses gambar (mis., tingkatkan kontras) sebelum memberi ke mesin. |
| **Out‑of‑memory error** | Gambar sangat besar pada memori GPU terbatas | Ubah ukuran gambar menjadi ≤ 2000 px lebar atau proses dalam ubin. |
| **Language mismatch** | Model bahasa default adalah Inggris tetapi teks dalam bahasa lain | Panggil `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (atau enum yang sesuai) sebelum `recognize()`. |

## Contoh lengkap yang dapat dijalankan

Berikut adalah kelas Java mandiri yang menggabungkan semua langkah. Simpan sebagai `GpuEnabledOcrExample.java`, sesuaikan jalur gambar, dan jalankan dengan `javac`/`java` atau melalui IDE Anda.

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class GpuEnabledOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn on GPU acceleration for faster processing
        // This is the core "how to enable gpu" call
        ocrEngine.setGpuEnabled(true);

        // Optional sanity check – ensures CUDA is available
        if (!SystemInfo.isCudaSupported()) {
            System.out.println("CUDA not detected. Falling back to CPU.");
        }

        // Step 3: Load the image that contains the text to be recognized
        // Replace with the absolute path to your image file
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Perform the OCR operation and obtain the recognized text
        // This answers "how to perform ocr" and "recognize text from image"
        String recognizedText = ocrEngine.recognize();

        // Step 5: Display the extracted text – completes "convert image to text"
        System.out.println("Recognized text:\n" + recognizedText);

        // (Optional) Save the result to a text file
        Path output = Paths.get("recognized_output.txt");
        Files.write(output, recognizedText.getBytes());
        System.out.println("Text saved to " + output.toAbsolutePath());
    }
}
```

### Hasil yang diharapkan

Menjalankan program mencetak teks yang diekstrak ke konsol dan menulis konten yang sama ke `recognized_output.txt`. Dengan GPU diaktifkan, total waktu eksekusi untuk gambar 2 MP biasanya di bawah 200 ms pada NVIDIA RTX 3060, dibandingkan ~500 ms pada CPU saja.

## Kesimpulan

Anda kini tahu **how to enable GPU** untuk Aspose OCR di Java, **recognize text from image** file, dan **convert image to text** dengan beberapa baris kode yang sederhana. Dengan memanfaatkan percepatan GPU Anda memperoleh pemrosesan yang lebih cepat, yang penting untuk aplikasi berorientasi batch atau waktu‑nyata seperti pemindaian faktur, pemrosesan kwitansi, dan digitalisasi dokumen.

**Next steps**

* Bereksperimen dengan model bahasa yang berbeda (`ocrEngine.setLanguage`) untuk **extract text from image** file dalam bahasa Prancis, Jerman, atau Mandarin.  
* Gabungkan output OCR dengan Apache Tika untuk secara otomatis mengindeks konten yang diekstrak.  
* Jelajahi streaming PDF besar halaman‑per‑halaman jika Anda perlu **recognize text from image** frame di dalam dokumen PDF.

Silakan sesuaikan contoh, integrasikan ke layanan Anda sendiri, dan bagikan hasilnya. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membaca Teks dari Gambar di Java Menggunakan Aspose OCR – Panduan Lengkap](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [recognize text image with Aspose OCR – Tutorial OCR Java Lengkap](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [gambar ke teks java: Convert Image to Text dengan Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}