---
category: general
date: 2026-08-22
description: Cara mengaktifkan GPU dalam OCR Java untuk mengenali teks dari gambar
  dengan cepat. Pelajari cara mengekstrak teks dari PNG, mengatur opsi gambar, dan
  mengenali teks secara efisien menggunakan Aspose OCR.
draft: false
keywords:
- how to enable gpu
- recognize text image java
- aspose ocr java tutorial
- extract text from png
- set image options
lastmod: 2026-08-22
og_description: Cara mengaktifkan GPU dalam OCR Java untuk mengenali teks dari gambar
  dengan cepat. Panduan ini menunjukkan cara mengekstrak teks dari PNG, mengatur opsi
  gambar, dan mengenali teks secara efisien menggunakan Aspose OCR.
og_image_alt: Java OCR GPU example code snippet showing Aspose OCR usage
og_title: Cara mengaktifkan GPU untuk OCR di Java – ekstraksi teks cepat
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  headline: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  type: TechArticle
- description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  name: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  steps:
  - name: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
    text: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
  - name: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
    text: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
  - name: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
    text: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR trial includes full GPU support; you just need to
      enable it in code.
    question: Does the free trial support GPU acceleration?
  - answer: Aspose OCR can rasterize PDF pages internally, but for best performance
      convert to high‑resolution PNG first.
    question: Can I process PDFs directly without converting to images?
  - answer: CUDA 11.2 or newer is recommended; older versions may work but are not
      officially tested.
    question: What CUDA version is required?
  - answer: Validate file size and type before processing, and run the OCR in a sandboxed
      thread to mitigate risks.
    question: Is it safe to run OCR on untrusted user uploads?
  - answer: Set `ocrEngine.setDebugMode(true)`; the console will list the selected
      GPU device and memory statistics.
    question: How do I enable logging to verify GPU usage?
  type: FAQPage
tags:
- OCR
- Java
- GPU
title: Cara Mengaktifkan GPU untuk OCR di Java – Mengenali Teks dari Gambar dengan
  Cepat
url: /id/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengaktifkan GPU untuk OCR di Java – Mengenali Teks dari Gambar dengan Cepat

Mengaktifkan percepatan GPU dalam aplikasi OCR Java dapat memotong waktu pemrosesan secara dramatis, terutama ketika Anda perlu mengekstrak teks dari gambar besar atau batch ber‑volume tinggi. Dalam tutorial ini Anda akan belajar **cara mengaktifkan GPU**, cara **mengenali teks dari gambar** file, dan langkah‑langkah tepat untuk **mengekstrak teks dari PNG** menggunakan pustaka Aspose OCR. Kami juga akan membahas opsi pra‑pemrosesan gambar yang meningkatkan akurasi dan menjawab pertanyaan umum “cara mengenali teks” sepanjang jalan.

## Jawaban Cepat
- **Apa peningkatan kecepatan terbesar?** Hingga 5× lebih cepat pada RTX 2060 menengah dibandingkan OCR hanya CPU.  
- **Apakah saya memerlukan lisensi khusus?** Lisensi Aspose OCR standar berfungsi untuk GPU; cukup aktifkan flag GPU.  
- **Versi Java apa yang diperlukan?** Java 17 atau lebih baru disarankan untuk kinerja optimal.  
- **Bisakah saya menjalankannya di dalam Docker?** Ya – cukup tambahkan flag `--gpus all` dan instal driver NVIDIA di dalam container.  
- **Apakah kode kompatibel dengan format gambar lain?** API yang sama bekerja untuk JPEG, TIFF, BMP, dan PNG tanpa perubahan.

## Apa yang Anda Butuhkan

Anda memerlukan mesin yang mendukung GPU, pustaka Aspose OCR untuk Java, dan lingkungan pengembangan Java 17 (atau lebih baru). Setup tipikal mencakup NVIDIA RTX 3060 atau kartu yang kompatibel dengan CUDA, JAR Aspose OCR terbaru dari Maven Central, dan contoh faktur PNG untuk benchmarking.

**Jawaban langsung (40‑70 kata):** Untuk memulai Anda harus menginstal Java 17, menambahkan dependensi Aspose OCR ke proyek Anda, memverifikasi bahwa JVM dapat melihat setidaknya satu perangkat CUDA, dan menyiapkan gambar uji. Setelah prasyarat tersebut terpenuhi, Anda dapat mengaktifkan GPU pada mesin OCR dan mulai memproses gambar dengan kecepatan GPU.

- **Java 17** (atau lebih baru) – kode dapat dikompilasi dengan versi sebelumnya tetapi 17 memberikan dukungan API terbaik.  
- **Aspose OCR untuk Java** – dapatkan JAR terbaru dari situs Aspose atau Maven Central.  
- **GPU yang kompatibel dengan CUDA** – misalnya, NVIDIA RTX 3060, RTX 2070, atau kartu modern apa pun dengan driver yang tepat.  
- **Gambar uji** – faktur PNG berformat besar cocok untuk mengukur kinerja.

> **Tip pro:** Pada laptop dengan grafis terintegrasi dan terpisah, paksa JVM menggunakan GPU terpisah melalui panel kontrol driver; jika tidak, pustaka secara diam-diam kembali ke CPU.

![contoh cara mengaktifkan gpu](image.png "contoh cara mengaktifkan gpu")
[contoh cara mengaktifkan gpu](image.png "contoh cara mengaktifkan gpu")

*Teks alternatif: contoh cara mengaktifkan gpu menampilkan potongan kode Java.*

## Langkah 1 – Instal Aspose OCR dan Verifikasi Ketersediaan GPU

GpuSettings adalah kelas yang mengontrol penggunaan GPU untuk mesin Aspose OCR.

Add the Maven dependency (or drop the JAR into `libs/`):

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check for the latest version -->
</dependency>
```

Run the sanity‑check snippet to list available devices:

```java
import com.aspose.ocr.GpuSettings;

public class GpuCheck {
    public static void main(String[] args) {
        GpuSettings settings = new GpuSettings();
        System.out.println("GPU enabled? " + settings.getEnable());
        System.out.println("Detected GPU count: " + settings.getDeviceCount());
    }
}
```

Jika output menunjukkan jumlah perangkat non‑nol, JVM Anda melihat GPU. Jika melaporkan nol, periksa kembali instalasi driver dan pastikan variabel lingkungan `CUDA_PATH` sudah diset.

## Langkah 2 – Cara Mengaktifkan GPU di Aspose OCR

**Jawaban langsung (40‑70 kata):** Aktifkan GPU dengan membuat objek `GpuSettings`, mengatur `setEnable(true)`, secara opsional menentukan ID perangkat, dan meneruskan objek pengaturan ini ke konstruktor `AsposeOCR`. Setelah itu, semua panggilan OCR berikutnya akan dijalankan pada GPU yang dipilih, memberikan peningkatan kecepatan seperti yang dijelaskan di bagian kinerja.

Kelas `GpuSettings` memungkinkan Anda mengaktifkan atau menonaktifkan penggunaan GPU dan memilih perangkat tertentu ketika ada beberapa GPU.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.GpuSettings;
import com.aspose.ocr.ImageProcessingOptions;
import com.aspose.ocr.RecognitionLanguage;
import com.aspose.ocr.OcrResult;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // 2️⃣ Enable GPU processing (auto‑detects available device)
        GpuSettings gpuSettings = new GpuSettings();
        gpuSettings.setEnable(true);          // turn GPU on
        gpuSettings.setDeviceId(0);           // first GPU (change if you have multiple)
        ocrEngine.setGpuSettings(gpuSettings);

        // 3️⃣ Optimize image preprocessing for GPU performance
        ImageProcessingOptions imgOpts = new ImageProcessingOptions();
        imgOpts.setAutoDeskew(true);
        imgOpts.setBinarization(true);
        ocrEngine.setImageProcessingOptions(imgOpts);

        // 4️⃣ Recognize text from an image file (PNG in this case)
        OcrResult result = ocrEngine.recognizeImage(
                "YOUR_DIRECTORY/large_invoice.png",
                RecognitionLanguage.ENGLISH);

        // 5️⃣ Output the detected text
        System.out.println("Detected text:\n" + result.getText());
    }
}
```

### Mengapa Mengaktifkan GPU?

Akselerasi GPU memindahkan pekerjaan perkalian matriks berat yang dilakukan model OCR ke ribuan inti paralel. Dalam praktiknya Anda akan melihat **peningkatan kecepatan 2‑5×** pada RTX 2060 yang sederhana, dan bahkan lebih pada kartu yang lebih baru. Trade‑off‑nya adalah jejak memori yang sedikit lebih tinggi, namun biasanya bukan masalah untuk PNG berukuran faktur tipikal.

## Langkah 3 – Mengenali Teks Gambar Java – Praktik Terbaik

Metode `recognizeImage` memproses file gambar yang diberikan dan mengembalikan teks yang diekstrak.

**Jawaban langsung (40‑70 kata):** Panggil `ocrEngine.recognizeImage(filePath)` setelah GPU diaktifkan; metode ini secara otomatis mendeteksi format file, menjalankan model OCR pada GPU, dan mengembalikan teks yang diekstrak. Untuk akurasi terbaik, pastikan gambar telah dibinarisasi dan diluruskan sebelum pemanggilan.

The code above already does it, but here’s a distilled version that isolates the OCR call:

```java
// Assuming ocrEngine is already configured with GPU
String imagePath = "sample.png";
OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.ENGLISH);
String extractedText = ocrResult.getText();

System.out.println("Extracted text from PNG:");
System.out.println(extractedText);
```

**Apa yang akan Anda perhatikan:** Metode `recognizeImage` secara otomatis mendeteksi jenis file, sehingga Anda dapat memberikan JPEG, TIFF, atau PNG tanpa flag tambahan. Itulah mengapa **mengekstrak teks dari PNG** berfungsi langsung.

### Menangani File Besar

If your PNG is larger than 5 MB, consider scaling it down before OCR:

```java
imgOpts.setResizeFactor(0.5); // shrink to 50 % of original dimensions
ocrEngine.setImageProcessingOptions(imgOpts);
```

Down‑sampling mengurangi penggunaan memori GPU dan sering meningkatkan akurasi karena model melihat tepi yang lebih bersih.

## Langkah 4 – Cara Mengatur Opsi Gambar untuk Akurasi Lebih Baik

ImageOptions adalah objek konfigurasi yang memungkinkan Anda menyesuaikan langkah pra‑pemrosesan seperti pelurusan dan binarisasi sebelum OCR.

**Jawaban langsung (40‑70 kata):** Gunakan objek `ImageOptions` untuk mengaktifkan auto‑deskew, binarisasi, dan pengubahan ukuran opsional sebelum mengirim gambar ke mesin OCR. Nilai tipikal adalah `setAutoDeskew(true)`, `setBinarization(true)`, dan faktor ubah ukuran antara 0.5 dan 0.8 untuk pemindaian besar. Pengaturan ini meningkatkan kontras dan penyelarasan, yang membantu jaringan saraf mengenali karakter lebih akurat, terutama pada dokumen yang berisik atau miring.

Frasa **cara mengatur gambar** muncul secara alami ketika kita membicarakan pra‑pemrosesan. Aspose OCR menawarkan beberapa pengaturan:

| Opsi                     | Apa yang dilakukannya                               | Nilai tipikal |
|----------------------------|--------------------------------------------|---------------|
| `setAutoDeskew(true)`      | Meluruskan baris teks yang miring              | true          |
| `setBinarization(true)`    | Mengubah menjadi hitam‑putih untuk kontras   | true          |
| `setResizeFactor(x)`       | Mengubah skala gambar (0 < x ≤ 1)               | 0.5‑0.8       |
| `setContrastAdjustment(y)` | Meningkatkan kontras (0‑100)                    | 30            |

Anda dapat menggabungkannya dalam urutan apa pun; pustaka menerapkannya secara berurutan sebelum memberi gambar ke jaringan saraf. Eksperimen adalah kunci—faktur yang berbeda mungkin memerlukan ambang batas yang berbeda.

## Langkah 5 – Cara Mengenali Teks dalam Kasus Tepi

Kelas `GpuExample` menunjukkan alur kerja OCR end‑to‑end lengkap menggunakan Aspose OCR dengan percepatan GPU.

**Jawaban langsung (40‑70 kata):** Untuk pemindaian resolusi rendah, pertama perbesar gambar atau minta sumber dengan dpi lebih tinggi; untuk catatan tulisan tangan, beralih ke model yang dilatih khusus; dan untuk dokumen multibahasa, berikan daftar dipisah koma ke `RecognitionLanguage`. Penyesuaian ini memastikan mesin yang dipercepat GPU tetap memberikan hasil yang dapat diandalkan.

Even with GPU power, certain scenarios trip up OCR:

1. **Pemindaian resolusi rendah (< 150 dpi).** Perbesar terlebih dahulu atau minta pengguna untuk pemindaian resolusi lebih tinggi.  
2. **Catatan tulisan tangan.** Model default fokus pada teks cetak; Anda memerlukan model yang dilatih khusus untuk tulisan sambung.  
3. **Banyak bahasa.** Berikan daftar dipisah koma ke `RecognitionLanguage`, misalnya, `RecognitionLanguage.ENGLISH_FRENCH`.

```java
ocrEngine.recognizeImage("multilang.png",
        RecognitionLanguage.ENGLISH_FRENCH);
```

## Output yang Diharapkan

Running the full `GpuExample` class against `large_invoice.png` should print something like:

```
Detected text:
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
...
```

Jika Anda melihat karakter tidak terbaca, periksa kembali bahwa `gpuSettings.setEnable(true)` benar‑benar diterapkan (konsol akan menampilkan perangkat GPU jika Anda mengaktifkan logging debug).

## Kesalahan Umum & Tips Pro

- **Lupa mengatur ID perangkat GPU.** Pada rig multi‑GPU, `setDeviceId(1)` mungkin diperlukan.  
- **Menjalankan di dalam Docker tanpa runtime NVIDIA.** Tambahkan `--gpus all` ke perintah `docker run`.  
- **Mencampur jalur kode CPU‑only dan GPU‑enabled.** Pertahankan satu instance `AsposeOCR` per thread untuk menghindari benturan status.  
- **Memory leak.** Panggil `ocrEngine.dispose()` saat selesai, terutama pada layanan yang berjalan lama.

## Pertanyaan yang Sering Diajukan

**T: Apakah percobaan gratis mendukung percepatan GPU?**  
J: Ya, percobaan Aspose OCR mencakup dukungan GPU penuh; Anda hanya perlu mengaktifkannya dalam kode.

**T: Bisakah saya memproses PDF langsung tanpa mengonversi ke gambar?**  
J: Aspose OCR dapat meraster halaman PDF secara internal, tetapi untuk kinerja terbaik konversi ke PNG beresolusi tinggi terlebih dahulu.

**T: Versi CUDA apa yang diperlukan?**  
J: CUDA 11.2 atau lebih baru disarankan; versi lama mungkin berfungsi tetapi tidak diuji secara resmi.

**T: Apakah aman menjalankan OCR pada unggahan pengguna yang tidak dipercaya?**  
J: Validasi ukuran dan tipe file sebelum diproses, dan jalankan OCR dalam thread yang di‑sandbox untuk mengurangi risiko.

**T: Bagaimana cara mengaktifkan logging untuk memverifikasi penggunaan GPU?**  
J: Atur `ocrEngine.setDebugMode(true)`; konsol akan menampilkan perangkat GPU yang dipilih dan statistik memori.

## Kesimpulan

Kami telah membahas **cara mengaktifkan GPU** untuk Aspose OCR di Java, menunjukkan cara **mengenali teks dari gambar**, mendemonstrasikan cara paling sederhana untuk **mengekstrak teks dari PNG**, menjelaskan **cara mengatur gambar** opsi pemrosesan, dan membahas nuansa **cara mengenali teks** dalam file dunia nyata. Dengan GPU diaktifkan, pipeline OCR Anda akan terasa jauh lebih cepat, menjadikannya cocok untuk skenario throughput tinggi seperti pemrosesan faktur batch atau pemindaian dokumen secara langsung.

Siap untuk langkah selanjutnya? Coba ganti model bahasa Inggris default dengan model multibahasa, atau bereksperimen dengan pipeline pra‑pemrosesan khusus untuk kwitansi berisik. Langit adalah batasnya—terutama ketika Anda memiliki GPU yang melakukan pekerjaan berat.

---

**Terakhir Diperbarui:** 2026-08-22  
**Diuji Dengan:** Aspose OCR for Java 24.10  
**Penulis:** Aspose

## Tutorial Terkait

- [Mengenali Teks Gambar dengan Aspose OCR Tutorial Java Ocr Lengkap](/ocr/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Cara Mengatur Lisensi Aspose OCR dan Memverifikasinya di Java](/ocr/java/ocr-basics/set-license/)
- [Mengekstrak Teks dari Gambar Java dengan Aspose.OCR Mode Deteksi Area](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}