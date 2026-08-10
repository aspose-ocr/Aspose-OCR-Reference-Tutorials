---
category: general
date: 2026-06-25
description: Akselerasi GPU OCR di Java memungkinkan Anda mengenali teks dari gambar
  dengan cepat. Pelajari cara mengekstrak teks dari JPG, mengatur batas memori GPU,
  dan memproses gambar dengan OCR.
draft: false
keywords:
- ocr gpu acceleration
- recognize text from image
- extract text from jpg
- set gpu memory limit
- process image with OCR
language: id
og_description: Akselerasi GPU OCR di Java membantu Anda mengenali teks dari gambar
  dengan cepat. Temukan cara mengekstrak teks dari JPG, mengatur batas memori GPU,
  dan memproses gambar dengan OCR.
og_title: Akselerasi GPU OCR di Java – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: OCR GPU acceleration in Java lets you recognize text from image quickly.
    Learn to extract text from jpg, set GPU memory limit, and process image with OCR.
  headline: OCR GPU Acceleration in Java – Complete Programming Guide
  type: TechArticle
- description: OCR GPU acceleration in Java lets you recognize text from image quickly.
    Learn to extract text from jpg, set GPU memory limit, and process image with OCR.
  name: OCR GPU Acceleration in Java – Complete Programming Guide
  steps:
  - name: Point to the Image You Want to Process
    text: '```java // Step 1 – Specify the image file (can be a JPG, PNG, BMP, etc.)
      String imagePath = "YOUR_DIRECTORY/sample.jpg"; ```'
  - name: Build an OCR Configuration with GPU Support
    text: '```java // Step 2 – Create OCR configuration and turn on GPU acceleration
      OcrConfig ocrConfig = new OcrConfig() .setGpuSettings(new GpuSettings() .setEnabled(true)
      // <-- enable GPU usage .setDeviceId(0) // first GPU in the system .setMemoryLimitMb(4096));
      // optional: set GPU memory limit ```'
  - name: Instantiate the OCR Engine
    text: '```java // Step 3 – Create the OCR engine with the GPU‑enabled configuration
      AsposeOCR ocrEngine = new AsposeOCR(ocrConfig); ```'
  - name: Run the Recognition
    text: '```java // Step 4 – Perform text recognition on the chosen image ImageRecognitionResult
      result = ocrEngine.recognizeImage(imagePath); ```'
  - name: Output the Recognized Text
    text: '```java // Step 5 – Print the extracted text to the console System.out.println("Recognized
      text:

      " + result.getText()); ```'
  type: HowTo
tags:
- Java
- OCR
- GPU
title: Akselerasi GPU OCR di Java – Panduan Pemrograman Lengkap
url: /id/java/advanced-ocr-techniques/ocr-gpu-acceleration-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Akselerasi GPU OCR di Java – Panduan Pemrograman Lengkap

Pernah bertanya-tanya bagaimana **ocr gpu acceleration** dapat mengurangi beberapa detik dari pipeline ekstraksi teks Anda? Jika Anda pernah secara manual menggulir halaman PDF yang dipindai atau berjuang dengan OCR hanya CPU yang lambat, Anda tidak sendirian. Dengan beberapa baris Java, Anda dapat **recognize text from image** file dalam sekejap, bahkan ketika mereka adalah JPG besar.

Dalam tutorial ini kami akan membahas contoh dunia nyata yang menunjukkan cara **extract text from jpg**, mengkonfigurasi batas memori dengan **set gpu memory limit**, dan akhirnya **process image with OCR** menggunakan Java SDK dari Aspose. Pada akhir tutorial, Anda akan memiliki program siap salin‑tempel yang dapat dijalankan pada mesin apa pun dengan GPU yang didukung.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

| Prerequisite | Why it matters |
|--------------|----------------|
| Java 17 (or newer) | Perpustakaan Aspose OCR menargetkan JDK modern. |
| Maven or Gradle | Untuk mengambil dependensi `aspose-ocr`. |
| A CUDA‑compatible GPU (NVIDIA) with at least 4 GB VRAM | Mengaktifkan **ocr gpu acceleration**; jika tidak, SDK akan beralih ke CPU. |
| An image file (`sample.jpg`) you want to read | Kami akan **extract text from jpg** dalam demo. |

Jika ada yang tidak ada, kode tetap akan berjalan—tetapi harapkan kinerja yang lebih lambat.

## Akselerasi GPU OCR – Menyiapkan Lingkungan

Pertama-tama, tambahkan perpustakaan Aspose OCR ke proyek Anda. Dengan Maven tampilannya seperti ini:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the latest version -->
</dependency>
```

> **Pro tip:** Jaga nomor versi tetap terbaru; rilis yang lebih baru seringkali membawa dukungan GPU yang lebih baik dan perbaikan bug.

Setelah dependensi teratasi, Anda siap mengaktifkan **ocr gpu acceleration**.

## Mengenali Teks dari Gambar Menggunakan Aspose OCR

Inti solusi terletak pada empat langkah sederhana. Mari kita uraikan.

### Langkah 1: Arahkan ke Gambar yang Ingin Diproses

```java
// Step 1 – Specify the image file (can be a JPG, PNG, BMP, etc.)
String imagePath = "YOUR_DIRECTORY/sample.jpg";
```

> **Why?** Mesin OCR membutuhkan jalur file yang konkret; jalur relatif juga dapat digunakan, selama JVM dapat menemukan file tersebut.

### Langkah 2: Bangun Konfigurasi OCR dengan Dukungan GPU

```java
// Step 2 – Create OCR configuration and turn on GPU acceleration
OcrConfig ocrConfig = new OcrConfig()
        .setGpuSettings(new GpuSettings()
                .setEnabled(true)          // <-- enable GPU usage
                .setDeviceId(0)            // first GPU in the system
                .setMemoryLimitMb(4096));  // optional: set GPU memory limit
```

* `setEnabled(true)` adalah saklar yang memberi tahu Aspose untuk menggunakan GPU alih-alih CPU.  
* `setDeviceId(0)` memilih GPU pertama; ubah indeks jika Anda memiliki beberapa kartu.  
* `setMemoryLimitMb(4096)` **set gpu memory limit** ke 4 GB, mencegah crash out‑of‑memory pada gambar besar. Sesuaikan nilai ini berdasarkan perangkat keras Anda.

### Langkah 3: Membuat Instance Mesin OCR

```java
// Step 3 – Create the OCR engine with the GPU‑enabled configuration
AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);
```

Mesin kini mengetahui bahwa ia harus mengalihkan beban berat ke GPU, yang menghasilkan waktu pengenalan lebih cepat—terutama untuk foto beresolusi tinggi.

### Langkah 4: Jalankan Pengenalan

```java
// Step 4 – Perform text recognition on the chosen image
ImageRecognitionResult result = ocrEngine.recognizeImage(imagePath);
```

Di balik layar, SDK mengalirkan gambar ke GPU, menjalankan jaringan saraf konvolusional, dan mengembalikan objek hasil yang berisi transkripsi teks biasa.

### Langkah 5: Keluarkan Teks yang Dikenali

```java
// Step 5 – Print the extracted text to the console
System.out.println("Recognized text:\n" + result.getText());
```

**Expected output** (dipotong untuk singkat):

```
Recognized text:
Hello, world!
This is a sample image containing text.
```

Jika GPU tidak tersedia, Aspose secara otomatis beralih ke mode CPU dan mencetak peringatan—sehingga program Anda tidak pernah crash.

## Ekstrak Teks dari JPG – Menangani Jalur File

Saat menangani **extract text from jpg**, seringkali muncul masalah pengkodean jalur di Windows. Pendekatan aman adalah menggunakan `java.nio.file.Paths`:

```java
import java.nio.file.Paths;

// Convert a possibly relative path to an absolute one
String absolutePath = Paths.get(imagePath).toAbsolutePath().toString();
ImageRecognitionResult result = ocrEngine.recognizeImage(absolutePath);
```

Penyesuaian kecil ini menghilangkan kejutan “file not found”, terutama ketika Anda menjalankan program dari IDE dibandingkan baris perintah.

## Atur Batas Memori GPU untuk Kinerja Stabil

Anda mungkin bertanya-tanya mengapa kami menggunakan `setMemoryLimitMb`. GPU modern mengalokasikan memori sesuai permintaan, dan pekerjaan OCR yang tidak terkendali dapat dengan mudah menghabiskan seluruh VRAM, menyebabkan proses berhenti. Dengan membatasi alokasi:

```java
.setMemoryLimitMb(2048) // limit to 2 GB if your GPU is modest
```

Anda melindungi sisa sistem Anda dari kekurangan sumber daya grafis. Jika batas terlalu rendah, SDK akan otomatis beralih ke RAM sistem, yang lebih lambat tetapi tetap berfungsi.

> **Watch out for:** Menetapkan batas lebih rendah daripada buffer yang dibutuhkan gambar dapat menyebabkan `GpuMemoryException`. Dalam kasus itu, tingkatkan batas atau perkecil gambar sebelum OCR.

## Proses Gambar dengan OCR – Contoh End‑to‑End Lengkap

Menggabungkan semuanya, berikut kelas lengkap yang siap dijalankan:

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.config.GpuSettings;
import com.aspose.ocr.config.OcrConfig;
import com.aspose.ocr.ImageRecognitionResult;
import java.nio.file.Paths;

public class GpuExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Specify the image to be processed
        String imagePath = "YOUR_DIRECTORY/sample.jpg";

        // 2️⃣ Build OCR configuration with GPU acceleration enabled
        OcrConfig ocrConfig = new OcrConfig()
                .setGpuSettings(new GpuSettings()
                        .setEnabled(true)          // enable GPU usage
                        .setDeviceId(0)            // select the first GPU device
                        .setMemoryLimitMb(4096));  // optional memory limit

        // 3️⃣ Create the OCR engine using the configured settings
        AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);

        // 4️⃣ Convert to absolute path (helps when extracting text from jpg)
        String absolutePath = Paths.get(imagePath).toAbsolutePath().toString();

        // 5️⃣ Perform text recognition on the image
        ImageRecognitionResult recognitionResult = ocrEngine.recognizeImage(absolutePath);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + recognitionResult.getText());
    }
}
```

**Menjalankan program**:

```bash
$ mvn compile exec:java -Dexec.mainClass=GpuExample
```

Anda akan melihat dump konsol dari teks yang terdapat dalam `sample.jpg`. Jika Anda memperhatikan proses memakan waktu lebih lama dari beberapa detik, periksa kembali bahwa driver GPU Anda terbaru dan bahwa flag `setGpuSettings().setEnabled(true)` dihormati (log akan berisi baris seperti *“GPU acceleration enabled – device 0”*).

## Pertanyaan Umum & Kasus Tepi

| Question | Answer |
|----------|--------|
| **Bagaimana jika saya tidak memiliki GPU?** | SDK dengan elegan beralih ke mode CPU. Anda masih dapat menggunakan kode yang sama; cukup set `setEnabled(false)` atau hapus blok `GpuSettings`. |
| **Gambar saya beresolusi 8 K – apakah masih akan bekerja?** | Ya, tetapi Anda mungkin perlu meningkatkan nilai `setMemoryLimitMb` atau memperkecil gambar untuk menghindari `GpuMemoryException`. |
| **Bisakah saya memproses batch gambar?** | Bungkus panggilan pengenalan dalam loop. Menggunakan kembali instance `AsposeOCR` yang sama lebih efisien karena konteks GPU tetap hidup. |
| **Apakah ada cara untuk mendapatkan skor kepercayaan?** | `ImageRecognitionResult` menyediakan `getConfidence()` untuk setiap blok yang dikenali; Anda dapat mencatat atau menyaring hasil dengan kepercayaan rendah. |
| **Bagaimana cara beralih ke perangkat GPU yang berbeda?** | Ubah `setDeviceId(1)` (atau indeks apa pun yang cocok dengan kartu kedua Anda). Gunakan `nvidia-smi` untuk melihat daftar ID. |

## Tips untuk Penyebaran Siap Produksi

1. **Warm‑up the GPU** – Jalankan gambar dummy kecil sekali saat startup; ini menghindari lonjakan latensi panggilan pertama.  
2. **Thread safety** – Instance `AsposeOCR` bersifat thread‑safe setelah inisialisasi, sehingga Anda dapat membagikannya di seluruh a

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [mengenali teks gambar dengan Aspose OCR – Tutorial OCR Java Lengkap](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Ekstrak Teks dari Gambar Java dengan Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}