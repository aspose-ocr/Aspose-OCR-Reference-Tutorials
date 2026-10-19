---
category: general
date: 2026-10-19
description: Pelajari cara mengaktifkan GPU dalam kode Aspose OCR Java untuk mengekstrak
  teks dari gambar. Mengonversi foto menjadi teks dan mengenali teks dari foto secara
  efisien.
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert photo to text
- how to extract text
- recognize text from photo
lastmod: 2026-10-19
og_description: Mengaktifkan GPU untuk OCR di Java memungkinkan Anda mengekstrak teks
  dari gambar dengan cepat, memotong waktu pemrosesan hingga 90% pada GPU modern.
  Pelajari langkah‑demi‑langkah penyiapan, cuplikan kode, dan tips pemecahan masalah.
og_image_alt: Diagram illustrating how to enable GPU in Aspose OCR Java code – how
  to enable gpu
og_title: Cara mengaktifkan GPU untuk OCR di Java – ekstraksi teks cepat
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: Learn how to enable GPU in Aspose OCR Java code to extract text from
    image. Convert photo to text and recognize text from photo efficiently.
  headline: How to Enable GPU for OCR in Java – Extract Text from Image
  type: TechArticle
- questions:
  - answer: Yes, as long as you have a Metal‑compatible GPU and the appropriate Aspose
      OCR binary for macOS. The same `setUseGpu(true)` call applies.
    question: Does this work on macOS?
  - answer: The Community Edition includes CPU‑only inference. To unlock GPU you need
      a licensed version (or a trial that includes GPU support).
    question: Can I use the free Community Edition?
  - answer: Call `ocrEngine.getConfig().setLanguage("spa")` for Spanish, `"fra"` for
      French, etc. Language packs are bundled with the library.
    question: What if I need to **recognize text from photo** in a language other
      than English?
  - answer: Yes—`ocrResult.getWords()` returns a collection where each `Word` object
      has a `getConfidence()` method.
    question: Is there a way to get confidence scores for each word?
  - answer: After creating the engine, invoke `ocrEngine.getConfig().setRequireGpu(true)`.
      The library will throw an exception if no compatible GPU is found, preventing
      silent CPU fallback.
    question: How can I enforce a strict GPU‑only mode?
  type: FAQPage
tags:
- OCR
- Java
- GPU
- Aspose
title: Cara Mengaktifkan GPU untuk OCR di Java – Ekstrak Teks dari Gambar
url: /id/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengaktifkan GPU untuk OCR di Java – mengekstrak teks dari gambar

Pernah bertanya-tanya **bagaimana cara mengaktifkan GPU** saat menjalankan OCR pada foto beresolusi tinggi? Anda tidak sendirian. Banyak pengembang Java menemui kendala ketika pipeline OCR mereka melambat pada konfigurasi CPU‑only, terutama ketika ukuran gambar melebihi beberapa megapiksel. Kabar baiknya? Mengaktifkan percepatan GPU dengan Aspose OCR sangat mudah, dan memungkinkan Anda **mengekstrak teks dari file gambar** dalam sebagian kecil waktu.

Dalam tutorial ini kami akan membahas seluruh proses: mulai dari menyiapkan pustaka Aspose OCR, mengaktifkan flag GPU, memberi gambar berukuran besar, hingga **mengonversi foto menjadi teks**. Pada akhir tutorial Anda akan tahu **cara mengaktifkan GPU** secara andal, dan juga melihat cara **mengenali teks dari foto** pada mesin dengan banyak GPU. Tidak memerlukan referensi eksternal—semua yang Anda butuhkan ada di sini.

## Jawaban cepat
- **Apa yang dilakukan “enable GPU”?** Itu memindahkan inferensi jaringan saraf OCR ke kartu grafis, mengurangi waktu pemrosesan hingga 90 % pada perangkat keras modern.  
- **Apakah saya memerlukan lisensi khusus?** Ya, dukungan GPU hanya tersedia dalam edisi berlisensi Aspose OCR untuk Java (atau versi percobaan yang menyertakan kernel GPU).  
- **GPU mana yang didukung?** GPU NVIDIA dengan CUDA 12.x (kemampuan komputasi 3.5+) dan GPU AMD dengan ROCm 5.x (kemampuan komputasi 6.0+).  
- **Apakah saya dapat kembali ke CPU secara otomatis?** Pustaka mendeteksi GPU yang hilang atau tidak kompatibel dan secara transparan beralih ke CPU, namun Anda dapat memaksa mode GPU‑only yang ketat.  
- **Apakah kode ini kompatibel dengan Java 17?** Tentu—Aspose OCR 23.x menargetkan Java 11+ dan berfungsi mulus dengan Java 17.

## Apa itu percepatan GPU untuk OCR?

Percepatan GPU untuk OCR adalah proses menggunakan prosesor grafis untuk menjalankan model deep‑learning yang mengenali karakter, alih‑alih CPU. Ini mempercepat ekstraksi teks secara dramatis, terutama untuk gambar besar atau yang diproses secara batch. Dengan memindahkan lapisan konvolusional yang berat ke GPU, latensi menurun dan throughput meningkat, menjadikan pemrosesan waktu‑nyata memungkinkan untuk foto beresolusi tinggi.

## Mengapa menggunakan mode GPU Aspose OCR?

Aspose OCR mendukung **lebih dari 50 format input** (JPEG, PNG, BMP, TIFF, PDF, dll.) dan dapat memproses gambar 20‑MP dalam kurang dari satu detik pada RTX 3080, dibandingkan dengan 8 detik pada CPU kelas atas. Pustaka ini juga menyediakan fallback bawaan, paket bahasa untuk lebih dari 30 bahasa, dan API Java sederhana yang hanya memerlukan satu flag untuk mengaktifkan GPU.

## Prasyarat

- Java 17 atau lebih baru terpasang.  
- GPU NVIDIA atau AMD yang didukung dengan driver terbaru (CUDA 12.x untuk NVIDIA, ROCm 5.x untuk AMD).  
- JAR Aspose OCR untuk Java – unduh rilis 23.x terbaru dari situs Aspose.  
- Maven atau Gradle untuk mengelola dependensi (kami akan menunjukkan contoh Maven).  
- Gambar beresolusi tinggi (misalnya `high-res-photo.jpg`) yang ingin Anda proses.

Jika ada yang belum tersedia, kode tetap akan terkompilasi, namun flag GPU akan diabaikan dan Anda akan kembali ke pemrosesan CPU.

## Bagaimana cara mengaktifkan GPU untuk OCR di Java?

Muat mesin OCR, panggil `setUseGpu(true)`, dan jalankan gambar Anda melalui metode `recognize`. Baris tunggal itu mengaktifkan kernel GPU yang menjalankan jaringan saraf konvolusional. **`setUseGpu(true)` mengaktifkan pemrosesan GPU untuk mesin OCR.** Mesin OCR adalah instance dari `com.aspose.ocr.OcrEngine` yang melakukan pengenalan teks.

## Langkah 1 – tambahkan Aspose OCR ke build Anda (cara mengaktifkan GPU)

Pertama-tama: beri tahu proyek Anda di mana menemukan pustaka OCR. Pada Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **Tip profesional:** Jika Anda menggunakan Gradle, setaraannya adalah `implementation 'com.aspose:aspose-ocr:23.10'`. Menjaga pustaka tetap terbaru memastikan Anda mendapatkan kernel GPU terbaru dan perbaikan bug.

Setelah pustaka berada di classpath, kita dapat **mengaktifkan GPU** pada mesin OCR.

## Langkah 2 – buat mesin OCR dan nyalakan GPU (cara mengaktifkan GPU)

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Instantiate the OCR engine – this is the core object.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration.
        // This is the line that answers the question "how to enable gpu".
        ocrEngine.getConfig().setUseGpu(true);

        // Optional: If your system has more than one GPU, pick the one you want.
        // The device ID is zero‑based, so 0 refers to the first GPU.
        // ocrEngine.getConfig().setGpuDeviceId(0);

        // Step 2.3: Process the image and get the result.
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/high-res-photo.jpg");

        // Step 2.4: Print the recognized text – now you have converted photo to text.
        System.out.println(ocrResult.getText());
    }
}
```

> **Mengapa ini penting:** Menetapkan `setUseGpu(true)` memberi tahu pustaka native di bawahnya untuk memindahkan pekerjaan jaringan saraf konvolusional yang berat ke GPU. Pada RTX 3080 modern, gambar yang memakan 8 detik di CPU dapat diproses dalam kurang dari 1 detik. Jika Anda melewatkan langkah ini, Anda masih **mengenali teks dari foto**, namun tidak akan merasakan peningkatan performa.

## Langkah 3 – verifikasi GPU memang sedang digunakan

Anda mungkin bertanya, “Apakah GPU benar‑benar melakukan pekerjaan?” Cara termudah adalah melihat output konsol pustaka Aspose OCR saat Anda mengaktifkan logging debug:

```java
// Enable verbose logging – helpful for confirming GPU usage.
ocrEngine.getConfig().setLogLevel(com.aspose.ocr.Config.LogLevel.DEBUG);
```

Saat menjalankan program, Anda akan melihat baris seperti:

```
[DEBUG] Using GPU device 0 (NVIDIA GeForce RTX 3080) for OCR processing.
```

Jika pesan tersebut tidak muncul, periksa kembali instalasi driver Anda dan pastikan GPU memenuhi kemampuan komputasi minimum (3.5 untuk NVIDIA, 6.0 untuk AMD).

## Langkah 4 – menangani banyak GPU dan kasus tepi

### Memilih GPU yang berbeda

Jika workstation Anda memiliki lebih dari satu GPU (misalnya, GPU terintegrasi Intel dan kartu NVIDIA khusus), Anda dapat menargetkan yang lebih cepat:

```java
ocrEngine.getConfig().setGpuDeviceId(1); // 1 = second GPU in the system
```

### Bagaimana jika tidak ada GPU yang terdeteksi?

Aspose OCR secara elegan beralih ke CPU ketika tidak dapat menemukan GPU yang cocok. Untuk menghindari fallback diam‑diam, Anda dapat menambahkan guard. **`setRequireGpu(true)` memaksa pustaka menggunakan GPU dan melemparkan pengecualian jika tidak ada yang ditemukan.** Ini memastikan Anda sadar ketika GPU tidak tersedia.

```java
if (!ocrEngine.getConfig().isGpuAvailable()) {
    throw new IllegalStateException("No compatible GPU found – cannot enable GPU acceleration.");
}
```

### Gambar besar dan batas memori

Memproses gambar 100 MP masih dapat menghabiskan memori GPU. Trik praktis adalah menurunkan skala gambar **sebanyak yang diperlukan** agar tetap dalam batas memori sambil mempertahankan kejelasan teks:

```java
ocrEngine.getConfig().setMaxImageDimension(4096); // caps width/height to 4096px
```

### Format gambar yang didukung

Aspose OCR memahami JPEG, PNG, BMP, TIFF, dan bahkan PDF. Jika Anda perlu **mengekstrak teks dari file gambar** yang disimpan dalam format lain, konversikan terlebih dahulu menggunakan pustaka seperti ImageIO.

## Langkah 5 – output yang diharapkan dan verifikasi

Saat program selesai, konsol akan mencetak teks OCR mentah. Untuk foto struk tipikal, Anda mungkin melihat:

```
Store: Coffee Corner
Date: 2026-02-25
Items:
  - Latte $4.50
  - Croissant $2.75
Total: $7.25
```

Jika output terlihat berantakan, pertimbangkan:

* Pastikan gambar cukup terang dan tidak terlalu terkompresi.  
* Sesuaikan opsi `setLanguage` jika teks bukan bahasa Inggris.  
* Verifikasi bahwa versi kernel GPU cocok dengan driver Anda (versi yang tidak cocok dapat menyebabkan artefak halus).

**`ocrResult.getWords()` mengembalikan koleksi objek `Word`, masing‑masing menyediakan skor kepercayaan melalui `getConfidence()`.** Ini memungkinkan Anda menyaring hasil dengan kepercayaan rendah.

## Langkah 6 – melampaui: pemrosesan batch dan pemanggilan asynchronous

Proyek dunia nyata sering memerlukan **mengekstrak teks dari kumpulan gambar**. Anda dapat membungkus logika di atas dalam loop atau menggunakan `CompletableFuture` Java untuk menjalankan beberapa pekerjaan OCR secara paralel, masing‑masing pada aliran GPU terpisah (jika perangkat keras Anda mendukung). Berikut sketsa singkatnya:

```java
import java.util.concurrent.*;
import java.nio.file.*;

public class BatchGpuOcr {
    public static void main(String[] args) throws Exception {
        ExecutorService pool = Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors());

        Files.list(Paths.get("photos/"))
             .filter(p -> p.toString().endsWith(".jpg"))
             .forEach(path -> pool.submit(() -> {
                 OcrEngine engine = new OcrEngine();
                 engine.getConfig().setUseGpu(true);
                 OcrResult result = engine.processImage(path.toString());
                 System.out.println("Result for " + path.getFileName() + ":\n" + result.getText());
             }));

        pool.shutdown();
        pool.awaitTermination(1, TimeUnit.HOURS);
    }
}
```

Pendekatan ini memungkinkan Anda **mengonversi foto menjadi teks** secara skala besar sambil tetap memanfaatkan percepatan GPU.

## Pertanyaan yang sering diajukan (FAQ)

**T: Apakah ini bekerja di macOS?**  
J: Ya, selama Anda memiliki GPU yang kompatibel dengan Metal dan binary Aspose OCR yang tepat untuk macOS. Panggilan `setUseGpu(true)` tetap berlaku.

**T: Bisakah saya menggunakan Community Edition gratis?**  
J: Community Edition hanya menyediakan inferensi CPU‑only. Untuk membuka GPU Anda memerlukan versi berlisensi (atau percobaan yang menyertakan dukungan GPU).

**T: Bagaimana jika saya perlu **mengenali teks dari foto** dalam bahasa selain Inggris?**  
J: Panggil `ocrEngine.getConfig().setLanguage("spa")` untuk bahasa Spanyol, `"fra"` untuk Prancis, dll. Paket bahasa sudah disertakan dalam pustaka.

**T: Apakah ada cara mendapatkan skor kepercayaan untuk setiap kata?**  
J: Ya—`ocrResult.getWords()` mengembalikan koleksi di mana setiap objek `Word` memiliki metode `getConfidence()`.

**T: Bagaimana cara memaksa mode GPU‑only yang ketat?**  
J: Setelah membuat mesin, panggil `ocrEngine.getConfig().setRequireGpu(true)`. Pustaka akan melempar pengecualian jika tidak ada GPU yang kompatibel, mencegah fallback ke CPU secara diam‑diam.

## Kesimpulan

Kami telah membahas **cara mengaktifkan GPU** untuk Aspose OCR di Java, menelusuri contoh lengkap yang dapat dijalankan, dan mengeksplorasi jebakan umum ketika Anda ingin **mengekstrak teks dari gambar**, **mengonversi foto menjadi teks**, atau **mengenali teks dari foto**. Dengan mengubah satu flag dan memastikan driver Anda terbaru, Anda dapat menghemat detik pada setiap panggilan OCR dan menskalakan ke batch gambar besar tanpa kesulitan.

Siap untuk langkah selanjutnya? Cobalah mengalirkan output OCR ke pipeline pemrosesan bahasa alami, atau bereksperimen dengan filter pra‑pemrosesan gambar berbeda untuk meningkatkan akurasi. Langit adalah batasnya ketika Anda menggabungkan OCR berbasis GPU dengan alat Java modern.

---

![Diagram showing how to enable GPU in Aspose OCR Java code – how to enable gpu](gpu-ocr-diagram.png)

[Diagram showing how to enable GPU in Aspose OCR Java code – how to enable gpu](gpu-ocr-diagram.png)

*Teks alt gambar:* "Diagram yang menggambarkan cara mengaktifkan GPU dalam kode Aspose OCR Java – cara mengaktifkan gpu"

---

**Terakhir diperbarui:** 2026-10-19  
**Diuji dengan:** Aspose OCR untuk Java 23.10  
**Penulis:** Aspose  






```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

## Tutorial Terkait

- [Cara Mengonfigurasi GPU untuk OCR Mengenali Teks Dari Gambar](/ocr/java/advanced-ocr-techniques/how-to-configure-gpu-for-ocr-recognize-text-from-image/)
- [Mengenali Teks Gambar Menggunakan Aspose OCR GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [Mengekstrak Teks Dari Gambar dengan Panduan Aspose OCR Java](/ocr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}