---
category: general
date: 2026-11-17
description: Cara mengaktifkan GPU di Java OCR untuk mengekstrak teks dari gambar
  dengan cepat. Pelajari cara mengkonfigurasi GPU, mengekstrak teks, dan mengenali
  teks java dengan Aspose OCR.
draft: false
keywords:
- how to enable gpu
- high resolution ocr
- aspose ocr java
- extract text image java
- gpu acceleration ocr
lastmod: 2026-11-17
og_description: Cara mengaktifkan GPU untuk Java OCR dengan cepat. Panduan ini menunjukkan
  cara mengkonfigurasi GPU, mengekstrak teks dari gambar, dan mengenali teks java
  menggunakan Aspose OCR.
og_image_alt: 'Developer guide: Enable GPU for Java OCR using Aspose OCR library'
og_title: Cara mengaktifkan GPU untuk Java OCR – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: How to enable GPU in Java OCR to extract text from image fast. Learn
    how to configure GPU, extract text and recognize text java with Aspose OCR.
  headline: How to enable GPU for Java OCR – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes, you can pass a PDF file directly to `setImage`; the library rasterizes
      each page before OCR.
    question: Does Aspose OCR support PDF input?
  - answer: Use `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` to
      improve recognition of specialized vocabulary.
    question: How do I add custom dictionaries for domain‑specific terms?
  - answer: Currently only CUDA‑compatible NVIDIA GPUs on Windows and Linux are supported;
      macOS users fall back to CPU.
    question: Is GPU acceleration available on macOS?
  - answer: Absolutely—`OcrResult` includes a `getConfidence()` method for each `OcrWord`
      object.
    question: Can I retrieve the confidence score for each recognized word?
  - answer: A commercial Aspose OCR license is required for production deployments;
      a free evaluation license works for development and testing.
    question: What license is required for production use?
  type: FAQPage
tags:
- gpu ocr
- java ocr
- aspose ocr
- high resolution ocr
- java image processing
title: Cara mengaktifkan GPU untuk Java OCR – panduan langkah demi langkah
url: /id/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengaktifkan GPU untuk OCR Java – panduan langkah demi langkah

Jika Anda mencari **cara mengaktifkan GPU** saat mengekstrak teks dari gambar dengan Java, Anda berada di tempat yang tepat. Akselerasi GPU dapat memotong waktu pemrosesan OCR dari beberapa detik menjadi sebagian detik, terutama pada pemindaian resolusi tinggi. Dalam panduan ini kami akan menjelaskan cara menginstal Aspose OCR, mengkonfigurasi perangkat GPU, dan menjalankan program ekstraksi teks lengkap yang berfungsi andal baik pada mesin dengan GPU maupun hanya CPU.

## Jawaban Cepat
- **Apa versi Java minimum?** Java 17 atau lebih baru.  
- **Jenis GPU apa yang diperlukan?** GPU NVIDIA yang kompatibel dengan CUDA (CUDA 11+).  
- **Apakah saya memerlukan lisensi untuk menjalankan contoh?** Lisensi percobaan gratis cukup untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Seberapa cepat OCR dengan GPU?** Hingga 5× lebih cepat pada gambar 4 MP dibandingkan dengan CPU.  
- **Apakah saya dapat kembali ke CPU secara otomatis?** Ya—Aspose OCR beralih ke CPU jika tidak ada GPU yang terdeteksi.

## Apa itu percepatan GPU untuk OCR?
Percepatan GPU untuk OCR berarti menjalankan langkah‑langkah inferensi jaringan saraf pada prosesor grafis alih‑alih CPU, memungkinkan ribuan operasi paralel. Ini secara dramatis mengurangi latensi inferensi, terutama untuk gambar resolusi tinggi di mana CPU biasanya menjadi bottleneck.

## Mengapa menggunakan Aspose OCR untuk Java?
Aspose OCR mendukung **lebih dari 50 format input** (termasuk PNG, JPEG, TIFF, PDF) dan dapat memproses dokumen ratusan halaman tanpa harus memuat seluruh file ke memori. API Java‑nya menyediakan satu kelas `OcrEngine` yang menyembunyikan panggilan CUDA tingkat rendah, sehingga Anda dapat fokus pada logika bisnis.

## Prasyarat
- JDK Java 17+ terinstal.  
- Maven 3.6+ atau Gradle 7+ untuk manajemen dependensi.  
- GPU NVIDIA yang kompatibel dengan CUDA dengan driver yang cocok dengan CUDA 11.x atau lebih baru.  
- Akses internet untuk mengunduh pustaka Aspose OCR.

## Cara mengaktifkan GPU untuk OCR Java?
Muat pustaka Aspose OCR, buat sebuah `OcrEngine`, dan aktifkan dukungan GPU hanya dalam beberapa baris kode. Mesin secara otomatis mendeteksi perangkat yang tersedia; Anda juga dapat menentukan ID perangkat untuk menargetkan GPU tertentu dalam lingkungan multi‑GPU.

## Bagaimana cara kerja OcrEngine?
`OcrEngine` adalah kelas pusat yang mengatur pra‑pemrosesan gambar, inferensi jaringan saraf, dan agregasi hasil. Ia menerima gambar sebagai jalur file, objek `java.io.File`, atau instance `java.awt.image.BufferedImage`, memberi Anda fleksibilitas dalam cara memasukkan data ke dalam alur kerja.

## Cara mengkonfigurasi percepatan GPU (cara mengkonfigurasi GPU)
Di sinilah Anda memberi tahu Aspose OCR untuk menggunakan GPU dan memilih perangkat yang akan dipakai.

Untuk mengaktifkan percepatan GPU Anda membuat sebuah instance `GpuConfiguration`, panggil `setEnable(true)`, opsional pilih perangkat dengan `setDeviceId(int)`, dan lampirkan ke `OcrEngine` melalui `setGpuConfiguration`. Konfigurasi ini juga memungkinkan Anda menentukan strategi fallback, seperti kembali ke CPU ketika perangkat yang diminta tidak tersedia, memastikan aplikasi tetap stabil.  

```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

Mengapa mengaktifkan GPU? Pipeline OCR menjalankan beberapa jaringan saraf konvolusional. Menjalankan jaringan tersebut pada GPU memanfaatkan ribuan inti paralel, memotong waktu inferensi dari 3–5 detik pada CPU menjadi kurang dari 1 detik pada RTX 3080 modern untuk gambar 4 MP. Jika perangkat yang ditentukan tidak ada, Aspose secara diam‑diam beralih ke CPU, mencegah crash.

### Penanganan Kasus Tepi

Aplikasi yang kuat perlu memverifikasi bahwa driver CUDA terinstal sebelum mencoba pekerjaan GPU.

```java
        // Verify that a GPU was actually engaged
        if (!gpuConfig.isEnabled() || !gpuConfig.isDeviceAvailable()) {
            System.out.println("GPU not detected – falling back to CPU. " +
                               "Performance will be slower.");
        }
```

## Langkah 1 – Instal Aspose OCR dan siapkan gambar Anda (cara mengaktifkan GPU)

Pertama, tambahkan dependensi Aspose OCR ke proyek Anda. Jika Anda menggunakan Maven, tambahkan:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

Pengguna Gradle dapat menambahkan:

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

Letakkan file resolusi tinggi (misalnya `sample-highres.png`) di folder yang dapat Anda referensikan dari kode. Gambar harus setidaknya 300 dpi untuk akurasi OCR terbaik.

> **Tips Pro:** Jika Anda menguji pada laptop tanpa GPU terpisah, Anda tetap dapat menjalankan kode; mesin akan otomatis beralih ke CPU.

![ilustrasi cara mengaktifkan gpu](placeholder.png "Diagram yang menunjukkan pipeline OCR Java dengan percepatan GPU – cara mengaktifkan gpu")
[ilustrasi cara mengaktifkan gpu](placeholder.png "Diagram yang menunjukkan pipeline OCR Java dengan percepatan GPU – cara mengaktifkan gpu")

## Langkah 2 – Buat mesin OCR dan muat gambar (ekstrak teks dari gambar)

Kelas `OcrEngine` adalah objek tingkat atas yang mewakili satu sesi OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.*;

public class GpuOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to process
        // Replace with the absolute or relative path to your PNG/JPEG/TIFF
        ocrEngine.setImage("YOUR_DIRECTORY/sample-highres.png");
```

Metode `setImage` menerima jalur file, objek `java.io.File`, atau `java.awt.image.BufferedImage`. Menyediakan sumber beresolusi tinggi memastikan GPU memiliki cukup piksel untuk menjaga semua inti tetap sibuk, yang diterjemahkan menjadi peningkatan kecepatan yang nyata.

## Langkah 3 – Konfigurasikan percepatan GPU (cara mengkonfigurasi GPU)

Objek `GpuConfiguration` memungkinkan Anda mengaktifkan penggunaan GPU, memilih perangkat, dan mendefinisikan perilaku fallback untuk mesin OCR.

```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

## Langkah 4 – Lakukan pengenalan teks (recognize text java)

Dengan mesin dan GPU siap, Anda akhirnya dapat mengekstrak karakter.

Metode `recognize()` menjalankan pipeline OCR dan mengembalikan sebuah `OcrResult` yang berisi teks polos, skor kepercayaan, dan data kotak pembatas opsional.  

```java
        // Step 4: Perform the recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
Recognized text:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Jika gambar Anda berisi beberapa bahasa, Anda dapat menambahkan paket bahasa sebelum memanggil `recognize()`:

```java
ocrEngine.getLanguage().add(OcrLanguage.FRENCH);
ocrEngine.getLanguage().add(OcrLanguage.SPANISH);
```

## Langkah 5 – Tinjau output dan langkah selanjutnya

Jalankan program dengan:

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrTutorial
```

Pada mesin dengan GPU yang memadai, OCR selesai **dalam kurang dari satu detik untuk gambar 4 MP**, dibandingkan dengan 3–5 detik pada CPU saja. Peningkatan kecepatan ini sangat berharga dalam skenario pemrosesan batch atau pipeline ingest dokumen real‑time.

### Pertanyaan umum

* **Bagaimana jika saya mendapatkan error “CUDA driver version is insufficient”?**  
  Perbarui driver NVIDIA Anda ke versi terbaru yang cocok dengan toolkit CUDA yang dibundel dengan Aspose (biasanya CUDA 11.x pada 2026).

* **Apakah saya dapat memproses batch gambar?**  
  Ya. Gunakan kembali satu instance `OcrEngine` di dalam loop untuk menghindari pembuatan konteks GPU berulang, yang meningkatkan throughput.

* **Apakah ada batas memori?**  
  Penggunaan memori GPU skala dengan ukuran gambar; untuk TIFF sangat besar, bagi gambar menjadi ubin sebelum memberi ke mesin agar tetap dalam batas memori GPU tipikal 8 GB.

### Tips Pro

* **Pin GPU** – pada server multi‑GPU, setel `gpuConfig.setDeviceId(1)` untuk memesan GPU kedua bagi OCR sementara GPU pertama menangani beban kerja lain.  
* **Warm‑up** – panggil `ocrEngine.recognize()` pada gambar dummy kecil sekali saat startup; ini memuat jaringan saraf ke GPU, menghilangkan latensi panggilan pertama.  
* **Keamanan Thread** – setiap thread harus memiliki instance `OcrEngine` masing‑masing; kelas ini tidak thread‑safe, sehingga berbagi antar thread dapat menyebabkan kondisi balapan.

## Pertanyaan yang Sering Diajukan

**T: Apakah Aspose OCR mendukung input PDF?**  
J: Ya, Anda dapat langsung memberikan file PDF ke `setImage`; pustaka akan meraster setiap halaman sebelum OCR.

**T: Bagaimana cara menambahkan kamus khusus untuk istilah domain‑spesifik?**  
J: Gunakan `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` untuk meningkatkan pengenalan kosakata khusus.

**T: Apakah percepatan GPU tersedia di macOS?**  
J: Saat ini hanya GPU NVIDIA yang kompatibel dengan CUDA pada Windows dan Linux yang didukung; pengguna macOS kembali ke CPU.

**T: Bisakah saya mengambil skor kepercayaan untuk setiap kata yang dikenali?**  
J: Tentu—`OcrResult` menyertakan metode `getConfidence()` untuk setiap objek `OcrWord`.

**T: Lisensi apa yang diperlukan untuk penggunaan produksi?**  
J: Lisensi komersial Aspose OCR diperlukan untuk penyebaran produksi; lisensi evaluasi gratis cukup untuk pengembangan dan pengujian.

---

**Terakhir Diperbarui:** 2026-11-17  
**Diuji Dengan:** Aspose OCR 24.11 for Java  
**Penulis:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

## Tutorial Terkait

- [Contoh Aspose OCR Java Ekstrak Teks Dari Gambar Dengan GPU](/ocr/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/)
- [Mengenali Teks Dari Gambar Java OCR Dengan Akselerasi GPU](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [Tutorial OCR Dipercepat GPU Java Panduan Cepat Gambar ke Teks](/ocr/java/advanced-ocr-techniques/gpu-accelerated-ocr-tutorial-java-guide-to-fast-image-to-tex/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}