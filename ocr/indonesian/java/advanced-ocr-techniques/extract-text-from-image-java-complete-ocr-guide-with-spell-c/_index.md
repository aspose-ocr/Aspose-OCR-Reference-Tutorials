---
category: general
date: 2026-11-17
description: 'Contoh Aspose OCR Java: mengekstrak teks dari gambar dengan koreksi
  ejaan. Pelajari cara memuat gambar, mengaktifkan koreksi ejaan, dan mengambil teks
  yang bersih dan dapat dicari dalam tutorial Java OCR yang singkat.'
draft: false
keywords:
- aspose ocr java example
- how to extract text from image java
- java ocr tutorial
- spell correction ocr
- load image for ocr
lastmod: 2026-11-17
og_description: Contoh Aspose OCR Java menunjukkan cara mengekstrak teks dari gambar,
  mengaktifkan koreksi ejaan, dan mendapatkan hasil yang akurat di Java. Ikuti panduan
  langkah demi langkah untuk output OCR yang bersih.
og_image_alt: Screenshot of console output showing corrected OCR text in Java
og_title: Contoh Aspose OCR Java – mengekstrak teks dari gambar
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: 'Aspose OCR Java example: extract text from image with spell correction.
    Learn how to load an image, enable spell‑correction, and retrieve clean searchable
    text in a concise Java OCR tutorial.'
  headline: 'Aspose OCR Java example: extract text from image'
  type: TechArticle
- description: 'Aspose OCR Java example: extract text from image with spell correction.
    Learn how to load an image, enable spell‑correction, and retrieve clean searchable
    text in a concise Java OCR tutorial.'
  name: 'Aspose OCR Java example: extract text from image'
  steps:
  - name: '**Batch processing** – Loop over a directory of images, collect results
      into a CSV, and feed them to downstream analytics.'
    text: '**Batch processing** – Loop over a directory of images, collect results
      into a CSV, and feed them to downstream analytics.'
  - name: '**Language detection** – Use `ocrEngine.getRecognitionSettings().setLanguage(Language.AUTO_DETECT);`
      for multilingual documents.'
    text: '**Language detection** – Use `ocrEngine.getRecognitionSettings().setLanguage(Language.AUTO_DETECT);`
      for multilingual documents.'
  - name: '**Region‑based OCR** – If you only need a specific area (e.g., a barcode
      region), define a rectangle via `ocrEngine.setRectangle(new Rectangle(x, y,
      width, height));`.'
    text: '**Region‑based OCR** – If you only need a specific area (e.g., a barcode
      region), define a rectangle via `ocrEngine.setRectangle(new Rectangle(x, y,
      width, height));`.'
  - name: '**Integrate with PDF** – Convert scanned PDFs to images first, then run
      the same pipeline; Aspose PDF for Java can render pages as PNGs.'
    text: '**Integrate with PDF** – Convert scanned PDFs to images first, then run
      the same pipeline; Aspose PDF for Java can render pages as PNGs.'
  type: HowTo
- questions:
  - answer: Yes. You need a valid Aspose license for production use; a free trial
      is available for evaluation.
    question: Can I use the Aspose OCR Java example in a commercial application?
  - answer: Absolutely. Set `ocrEngine.getRecognitionSettings().setLanguage(Language.SPANISH);`
      (or any supported language) and provide the appropriate language data files.
    question: Does the engine support languages other than English?
  - answer: The engine streams data and can process images up to 500 MP without loading
      the entire file into memory, though you may need to increase the JVM heap for
      very large files.
    question: How large of an image can the engine handle?
  - answer: Yes. You can disable it via `ocrEngine.getRecognitionSettings().setEnableSpellCheck(false);`
      if you prefer raw OCR output.
    question: Is spell‑correction optional?
  - answer: All Java 8+ runtimes are supported, including Java 11, Java 17, and newer
      LTS releases.
    question: What Java versions are supported?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: 'Contoh Aspose OCR Java: mengekstrak teks dari gambar'
url: /id/java/advanced-ocr-techniques/extract-text-from-image-java-complete-ocr-guide-with-spell-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Contoh Aspose OCR Java: ekstrak teks dari gambar

Pernah membutuhkan **extract text from image java** tetapi outputnya penuh dengan typo? Anda tidak sendirian. Resi yang dipindai, screenshot berisik, dan PDF beresolusi rendah semuanya menghasilkan hasil yang berantakan, dan kebanyakan pengembang akhirnya membersihkan teks secara manual.  

Dalam tutorial ini kami akan membahas **java ocr tutorial** yang menunjukkan secara tepat cara **load image for OCR**, mengaktifkan koreksi ejaan, dan mendapatkan teks yang bersih serta dapat dicari—semua dengan Aspose OCR untuk Java. Pada akhir tutorial Anda akan memiliki program siap‑jalan yang dapat Anda masukkan ke dalam proyek apa pun.

## Jawaban Cepat
- **Apa yang dilakukan contoh Aspose OCR Java?** Ia memuat gambar, mengaktifkan koreksi ejaan, menjalankan pengenalan, dan mengembalikan output teks polos yang telah dikoreksi.  
- **Perpustakaan apa yang diperlukan?** Aspose OCR untuk Java (versi terbaru tersedia di Maven Central).  
- **Apakah saya memerlukan lisensi?** Lisensi evaluasi gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya memproses banyak gambar?** Ya – bungkus kode dalam loop atau gunakan batch API.  
- **Versi Java apa yang didukung?** JDK 8 dan yang lebih baru.

## Apa itu contoh Aspose OCR Java?
Contoh **Aspose OCR Java** memperlihatkan cara menggunakan kelas `OcrEngine` untuk membaca teks dari gambar raster dan secara otomatis memperbaiki kesalahan pengenalan umum. Dengan memuat gambar, mengonfigurasi pengaturan bahasa dan koreksi ejaan, serta memanggil `recognize()`, Anda memperoleh string Unicode yang bersih siap untuk diindeks, disimpan, atau dianalisis lebih lanjut. Contoh singkat ini ideal bagi pengembang yang membutuhkan OCR yang dapat diandalkan tanpa ketergantungan native.

## Mengapa menggunakan Aspose OCR untuk Java?
Aspose OCR mendukung **lebih dari 50 format gambar input** (PNG, JPEG, TIFF, BMP, GIF, halaman yang dirender dari PDF, dll.) dan dapat memproses dokumen hingga **500 MP** tanpa memuat seluruh file ke memori, berkat arsitektur streaming-nya. Benchmark menunjukkan **peningkatan kecepatan 30 %** dibandingkan perpustakaan lain pada pemindaian berisik ketika koreksi ejaan diaktifkan, menjadikannya pilihan berperforma tinggi untuk beban kerja perusahaan.

## Apa yang Anda perlukan

Sebelum kita mulai, pastikan Anda memiliki:

- **Java Development Kit (JDK) 8+** – kode ini menggunakan API Java standar.  
- **Perpustakaan Aspose OCR untuk Java** (versi terbaru per 2026). Anda dapat mengambilnya dari Maven Central atau mengunduh JAR secara langsung.  
- Sebuah file gambar yang ingin Anda proses – untuk panduan ini kami akan menggunakan `noisy‑scan.png` yang ditempatkan dalam folder bernama `YOUR_DIRECTORY`.  
- IDE yang memadai (IntelliJ IDEA, Eclipse, atau VS Code) – apa saja dapat digunakan, tetapi IntelliJ memudahkan penanganan Maven.  

Itu saja. Tidak ada kerangka kerja tambahan, tidak ada ketergantungan native yang berat.

![Ekstrak teks dari gambar contoh Java](extract-text-from-image-java.png "ekstrak teks dari gambar contoh java")

Lihat gambar contoh: [Ekstrak teks dari gambar contoh Java](extract-text-from-image-java.png "ekstrak teks dari gambar contoh java")

## Apa langkah pertama untuk menambahkan Aspose OCR ke proyek Java?
Tambahkan perpustakaan Aspose OCR ke konfigurasi build Anda sehingga kelas-kelas tersedia saat kompilasi. Untuk Maven, sisipkan dependensi ke dalam `pom.xml`; untuk Gradle, tambahkan ke `build.gradle`. Menggunakan manajer paket memastikan Anda menerima pembaruan otomatis dan dependensi transitif.

## Langkah 1 – tambahkan Aspose OCR ke proyek Anda

Hal pertama yang harus dilakukan. Kita membutuhkan mesin OCR di classpath. Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the newest version -->
</dependency>
```

Jika Anda lebih suka Gradle, yang setara adalah:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

*Pro tip:* Selalu periksa kembali nomor versi; rilis yang lebih baru mungkin menyertakan penyesuaian kinerja untuk gambar berisik.

## Langkah 2 – inisialisasi mesin OCR

Sekarang perpustakaan tersedia, kita dapat membuat instance `OcrEngine`. Anggap objek ini sebagai otak yang akan membaca gambar Anda.

```java
import com.aspose.ocr.*;

public class SpellCorrectionTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

Mengapa kita menginstansiasi mesin terlebih dahulu? `OcrEngine` menyimpan pengaturan konfigurasi (seperti bahasa, DPI, dan koreksi ejaan) yang memengaruhi setiap panggilan pengenalan berikutnya. Membuatnya di awal membuat kode rapi dan memungkinkan kita menyesuaikan pengaturan di satu tempat.

## Langkah 3 – muat gambar untuk OCR

Langkah logis berikutnya adalah mengarahkan mesin ke file yang ingin Anda proses. Di sinilah bagian **load image for OCR** terjadi.

```java
        // Step 3: Load the image you want to extract text from
        ocrEngine.setImage("YOUR_DIRECTORY/noisy-scan.png");
```

Jika gambar berada di tempat lain (misalnya, URL atau `InputStream`), Aspose OCR juga menerima overload tersebut – cukup ganti string path dengan pemanggilan metode yang sesuai.  

*Edge case:* Saat menangani gambar sangat besar (> 5 MB), pertimbangkan untuk mengubah ukuran terlebih dahulu agar penggunaan memori tetap wajar. Mesin OCR dapat menangani resolusi tinggi, tetapi JVM mungkin kehabisan heap space jika tidak.

## Langkah 4 – aktifkan koreksi ejaan

Tanpa koreksi ejaan, OCR akan mereproduksi apa yang “dilihat” secara akurat, bahkan jika karakter salah diidentifikasi. Aktifkan fitur ini dan biarkan mesin membersihkan kesalahan umum.

```java
        // Step 4: Enable spell‑correction to improve accuracy
        ocrEngine.getRecognitionSettings().setSpellCorrectionEnabled(true);
```

Di balik layar, mesin menjalankan pemeriksaan kamus ringan. Ini sangat berguna untuk teks bahasa Inggris, tetapi Aspose juga mendukung bahasa lain – cukup atur properti `Language` sesuai.

## Langkah 5 – kenali teks dan ambil hasil

Sekarang kita akhirnya meminta mesin melakukan tugasnya. Metode `recognize()` mengembalikan objek `OcrResult` yang berisi string yang diekstrak dan, opsional, informasi kotak pembatas.

```java
        // Step 5: Perform recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 6: Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Output yang diharapkan** (asumsi gambar contoh berisi frasa “Invoice #1234” dengan beberapa bintik):

```
Corrected text:
Invoice #1234
Date: 2025-11-30
Total: $1,250.00
```

Perhatikan bagaimana mesin OCR memperbaiki “I” yang awalnya terbaca sebagai “1” dan menghapus titik-titik yang tidak diinginkan. Itulah keajaiban koreksi ejaan.

## Langkah 6 – jebakan umum & cara menghindarinya

- **Data bahasa hilang** – Jika Anda mendapatkan karakter kacau, pastikan paket bahasa untuk bahasa target Anda terpasang. Aspose menyertakan bahasa Inggris secara default; bahasa lain memerlukan unduhan tambahan.  
- **Pengaturan DPI tidak tepat** – Gambar beresolusi rendah (< 100 DPI) sering menghasilkan hasil yang buram. Anda dapat meningkatkan akurasi dengan memanggil `ocrEngine.getRecognitionSettings().setDpi(300);` sebelum pengenalan.  
- **Masalah jalur file** – Jalur relatif diselesaikan terhadap direktori kerja. Menggunakan jalur absolut atau `Paths.get(...).toAbsolutePath()` menghilangkan kejutan “file tidak ditemukan”.  
- **Kebocoran memori** – `OcrEngine` mengimplementasikan `AutoCloseable`. Dalam layanan yang berjalan lama, bungkus mesin dalam blok try‑with‑resources untuk memastikan sumber daya native dilepaskan:

```java
try (OcrEngine ocrEngine = new OcrEngine()) {
    // configure and recognize...
}
```

## Contoh lengkap, siap‑jalan

Berikut adalah program lengkap, salin‑tempel ke dalam file bernama `SpellCorrectionTutorial.java`, sesuaikan jalur gambar, dan jalankan dengan `mvn exec:java` atau konfigurasi run IDE Anda.

```java
import com.aspose.ocr.*;

public class SpellCorrectionTutorial {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        try (OcrEngine ocrEngine = new OcrEngine()) {

            // Load the image you want to extract text from
            ocrEngine.setImage("YOUR_DIRECTORY/noisy-scan.png");

            // Enable spell‑correction for cleaner output
            ocrEngine.getRecognitionSettings().setSpellCorrectionEnabled(true);

            // (Optional) Boost accuracy for low‑resolution scans
            ocrEngine.getRecognitionSettings().setDpi(300);

            // Perform the recognition
            OcrResult ocrResult = ocrEngine.recognize();

            // Show the corrected text
            System.out.println("Corrected text:");
            System.out.println(ocrResult.getText());
        }
    }
}
```

Jalankan, dan Anda akan melihat teks yang telah dikoreksi dicetak ke konsol—tepat seperti yang ditargetkan oleh **java ocr tutorial** biasa.

## Apa langkah selanjutnya setelah mengekstrak teks?
Setelah mengekstrak teks Anda dapat memperluas solusi dengan memproses banyak file, mendeteksi bahasa secara otomatis, menargetkan wilayah tertentu, atau mengintegrasikan output ke alur kerja PDF. Peningkatan ini memungkinkan Anda membangun pipeline batch, menambahkan dukungan multibahasa, memfokuskan OCR pada area yang diminati, dan menggabungkan Aspose OCR dengan produk Aspose lainnya untuk pemrosesan dokumen end‑to‑end.

1. **Pemrosesan batch** – Loop melalui direktori gambar, kumpulkan hasil ke dalam CSV, dan berikan ke analitik hilir.  
2. **Deteksi bahasa** – Gunakan `ocrEngine.getRecognitionSettings().setLanguage(Language.AUTO_DETECT);` untuk dokumen multibahasa.  
3. **OCR berbasis wilayah** – Jika Anda hanya membutuhkan area tertentu (misalnya, wilayah barcode), definisikan persegi panjang melalui `ocrEngine.setRectangle(new Rectangle(x, y, width, height));`.  
4. **Integrasi dengan PDF** – Konversi PDF yang dipindai menjadi gambar terlebih dahulu, lalu jalankan pipeline yang sama; Aspose PDF untuk Java dapat merender halaman sebagai PNG.  

Setiap topik ini terkait kembali ke langkah inti yang kami bahas, sehingga transisinya akan mulus.

## Pertanyaan yang sering diajukan

**Q: Bisakah saya menggunakan contoh Aspose OCR Java dalam aplikasi komersial?**  
A: Ya. Anda memerlukan lisensi Aspose yang valid untuk penggunaan produksi; percobaan gratis tersedia untuk evaluasi.

**Q: Apakah mesin mendukung bahasa selain Inggris?**  
A: Tentu saja. Atur `ocrEngine.getRecognitionSettings().setLanguage(Language.SPANISH);` (atau bahasa lain yang didukung) dan sediakan file data bahasa yang sesuai.

**Q: Seberapa besar gambar yang dapat ditangani mesin?**  
A: Mesin melakukan streaming data dan dapat memproses gambar hingga 500 MP tanpa memuat seluruh file ke memori, meskipun Anda mungkin perlu meningkatkan heap JVM untuk file yang sangat besar.

**Q: Apakah koreksi ejaan opsional?**  
A: Ya. Anda dapat menonaktifkannya melalui `ocrEngine.getRecognitionSettings().setEnableSpellCheck(false);` jika lebih suka output OCR mentah.

**Q: Versi Java apa yang didukung?**  
A: Semua runtime Java 8+ didukung, termasuk Java 11, Java 17, dan rilis LTS yang lebih baru.

## TL;DR

- **Tujuan utama:** *extract text from image java* menggunakan Aspose OCR.  
- **Tindakan kunci:** muat gambar untuk OCR, aktifkan koreksi ejaan, jalankan `recognize()`.  
- **Hasil:** teks bersih yang dapat dicari siap untuk diindeks atau diproses lebih lanjut.  

Cobalah dengan pemindaian Anda sendiri, sesuaikan DPI, dan bereksperimen dengan paket bahasa. Kekuatan OCR di Java ada di ujung jari Anda—selamat coding!

---

**Terakhir Diperbarui:** 2026-11-17  
**Diuji Dengan:** Aspose OCR for Java 24.11  
**Penulis:** Aspose

## Tutorial Terkait

- [Mengenali Teks Dari Gambar Di Java Lengkap Aspose Ocr Spell](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-aspose-ocr-spell/)
- [Contoh Java Ocr Muat Gambar Dan Kenali Teks Dengan Aspose](/ocr/java/ocr-basics/java-ocr-example-load-image-and-recognize-text-with-aspose/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}