---
category: general
date: 2026-03-28
description: Pelajari cara mengenali teks gambar di Java menggunakan Aspose OCR, mengekstrak
  file PNG berisi teks, dan menggunakan akselerasi GPU untuk OCR cepat pada gambar
  berukuran besar.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: id
og_description: Temukan cara mengenali teks gambar di Java, mengekstrak teks dari
  file PNG, dan menggunakan akselerasi GPU untuk OCR gambar besar.
og_title: Mengenali Teks Gambar dengan Java OCR – Contoh yang Dipercepat GPU
tags:
- OCR
- Java
- GPU
title: Mengenali teks gambar dengan Java OCR – Contoh yang Dipercepat GPU
url: /id/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks gambar dengan Java OCR – Contoh Dipercepat GPU

Pernah perlu **mengenali teks gambar** dari PNG yang sangat besar tetapi menemukan versi CPU berjalan sangat lambat? Anda bukan satu‑satunya. Dalam banyak alur kerja dunia nyata—misalnya pemindaian faktur atau pengarsipan dokumen bersejarah—ukuran gambar dapat membengkak, dan mesin OCR default tidak dapat mengimbanginya.  

Berita baik: Aspose OCR for Java memungkinkan Anda **menggunakan percepatan GPU** untuk mempercepat proses, dan kodenya ternyata sangat ringkas. Dalam tutorial ini Anda akan melihat contoh Java OCR yang lengkap dan dapat dijalankan yang **mengekstrak teks PNG**, memanfaatkan GPU yang mendukung CUDA, dan menangani **gambar OCR besar** dengan hanya beberapa baris kode. Pada akhir tutorial Anda akan tahu persis cara memasukkannya ke dalam proyek Java Anda sendiri dan mengapa setiap pengaturan penting.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan Aspose OCR dalam proyek Maven atau Gradle.  
- Proses langkah‑demi‑langkah untuk **mengenali teks gambar** pada GPU.  
- Mengapa mengonfigurasi jumlah stream GPU dapat meningkatkan throughput.  
- Cara memverifikasi output dan mengatasi masalah umum.  

> **Prasyarat** – Java 17 (atau lebih baru), GPU yang kompatibel dengan CUDA dengan driver terbaru, dan lisensi Aspose OCR for Java yang valid (versi percobaan gratis dapat digunakan untuk evaluasi). Tidak diperlukan pustaka eksternal lainnya.

---

## Langkah 1: Tambahkan Dependensi Aspose OCR

Pertama, masukkan pustaka Aspose OCR ke dalam build Anda. Jika Anda menggunakan **Maven**, tambahkan potongan berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

Untuk **Gradle**, letakkan ini di `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Tips pro:** Versi terbaru (per Maret 2026) mencakup perbaikan kinerja untuk beban kerja GPU, jadi selalu gunakan rilis terbaru.

---

## Langkah 2: Inisialisasi Mesin OCR dan Aktifkan GPU

Membuat mesin OCR sangat sederhana. Bagian pentingnya adalah mengaktifkan flag GPU—jika tidak, mesin akan kembali ke mode CPU.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Mengapa Mengaktifkan GPU?

Saat Anda mengaktifkan `setUseGpu(true)`, Aspose memindahkan perhitungan jaringan saraf konvolusional yang berat ke kartu grafis. Ini dapat mengurangi beberapa detik dari waktu pemrosesan **ocr large image**, terutama ketika gambar melebihi 4000 × 4000 px. Jika lingkungan Anda tidak memiliki GPU yang kompatibel, panggilan tersebut hanya menjadi no‑op dan mesin akan tetap berjalan di CPU—tidak ada crash, hanya kinerja yang lebih lambat.

---

## Langkah 3: Mengenali Gambar PNG dan Mengekstrak Teksnya

Sekarang arahkan mesin ke file yang ingin Anda proses. Contoh ini menggunakan `sample-large.png`, tetapi Anda dapat menggantinya dengan PNG atau JPEG apa pun.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Output tersebut mengonfirmasi operasi **recognize image text** berhasil dan Anda berhasil **extract text png** konten.

---

## Langkah 4: Verifikasi Pemanfaatan GPU (Opsional tetapi Berguna)

Jika Anda penasaran apakah GPU benar‑benar digunakan, buka alat pemantauan GPU sistem Anda (misalnya `nvidia-smi` di Linux). Saat proses Java berjalan, Anda harus melihat lonjakan kecil pada penggunaan memori dan pemanfaatan komputasi.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Jika Anda tidak melihat aktivitas apa pun, periksa kembali bahwa:

1. Driver CUDA cocok dengan model GPU.  
2. Panggilan `setUseGpu(true)` tidak ditimpa kemudian dalam kode.  
3. File lisensi Anda (jika ada) tidak membatasi penggunaan GPU.

---

## Langkah 5: Menangani Kasus Pinggir Umum

### Gambar Besar Melebihi Memori GPU

Ketika gambar sangat besar (misalnya 8000 × 8000 px), GPU mungkin kehabisan memori. Solusi cepat adalah memperkecil skala gambar sebelum memberikannya ke Aspose:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Kemudian berikan `"sample-resized.png"` ke `recognizeImage`. Ini menjaga akurasi OCR sambil tetap berada dalam batas memori GPU.

### PDF Multi‑Halaman

Aspose OCR juga dapat menangani PDF halaman‑per‑halaman. Loop setiap halaman, konversi menjadi gambar, dan berikan ke mesin. Flag **use gpu acceleration** yang sama berlaku, memberi Anda pipeline PDF‑to‑text yang cepat.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah kelas Java lengkap, siap untuk dikompilasi dan dijalankan. Ganti `YOUR_DIRECTORY` dengan jalur ke file PNG Anda.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Output yang diharapkan** – representasi teks biasa dari semua yang dapat dibaca mesin dari gambar. Jika gambar berisi tabel, Anda akan mendapatkan isi sel yang digabungkan dengan jeda baris; Aspose tidak mempertahankan tata letak, tetapi Anda dapat memproses ulang string tersebut jika diperlukan.

---

## Pertanyaan yang Sering Diajukan

| Question | Answer |
|----------|--------|
| **Apakah saya memerlukan lisensi berbayar?** | Versi percobaan berfungsi hingga 200 halaman dan menonaktifkan watermark untuk OCR. Untuk produksi, lisensi menghapus batasan dan membuka seluruh stack GPU. |
| **Bagaimana jika GPU saya lebih lama (misalnya GTX 750)?** | GPU yang lebih lama masih dapat berfungsi tetapi dengan kecepatan yang berkurang; pastikan Anda memiliki setidaknya Compute Capability 3.0. |
| **Apakah saya dapat memproses file JPG atau BMP?** | Tentu saja—`recognizeImage` menerima format apa pun yang didukung oleh Java ImageIO. |
| **Apakah ada cara untuk memproses banyak gambar secara batch?** | Bungkus panggilan OCR dalam loop, dan pertimbangkan meningkatkan `setGpuStreams` untuk mencocokkan jumlah stream bersamaan yang Anda inginkan. |
| **Bagaimana jika saya perlu mempertahankan tata letak?** | Gunakan `LayoutOptions` Aspose OCR untuk mendapatkan bounding box; ini di luar cakupan panduan singkat ini tetapi didokumentasikan dalam API. |

---

## Kesimpulan

Anda kini memiliki **contoh java ocr** yang singkat dan menyeluruh yang **recognize image text**, **extract text png**, dan **use GPU acceleration** untuk mempercepat pemrosesan **ocr large image**. Dengan menyesuaikan jumlah stream GPU dan, bila perlu, memperkecil skala gambar yang terlalu besar, Anda dapat menyesuaikan solusi ini untuk hampir semua konfigurasi perangkat keras.

Siap untuk langkah selanjutnya? Cobalah memasukkan folder berisi kwitansi yang dipindai ke dalam pipeline yang sama, atau bereksperimen dengan API `TextRegion` Aspose untuk mempertahankan tata letak asli. Dan jika Anda mengalami kendala, forum Aspose dan Javadoc adalah sumber daya yang sangat baik—ingat saja dasar‑dasar yang telah kami bahas di sini.

Selamat coding, semoga OCR Anda secepat kilat!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}