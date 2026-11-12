---
category: general
date: 2026-09-18
description: Pelajari cara menambahkan dependensi Aspose OCR Maven dan mengekstrak
  teks dari gambar di Java. Panduan ini mencakup pengaturan mesin OCR, spell‑checking,
  custom dictionaries, dan tips konfigurasi.
draft: false
keywords:
- aspose ocr maven dependency
- java image to text
- extract image text java
- Aspose OCR Java
- OCR spell checking
lastmod: 2026-09-18
og_description: Pelajari cara menambahkan dependensi Aspose OCR Maven dan menggunakannya
  untuk mengonversi gambar menjadi teks di Java. Termasuk spell‑checking, custom dictionaries,
  dan tips konfigurasi.
og_image_alt: Diagram showing OCR workflow to extract text from image using Aspose
  OCR in Java
og_title: Tambahkan dependensi Aspose OCR Maven untuk mengekstrak teks gambar di Java
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to add the Aspose OCR Maven dependency and extract text from
    images in Java. This guide covers OCR engine setup, spell‑checking, custom dictionaries,
    and configuration tips.
  headline: Add Aspose OCR Maven dependency to extract image text in Java
  type: TechArticle
- questions:
  - answer: Handwritten recognition is available in a separate module (`aspose-ocr-handwriting`).
      The standard Aspose OCR library focuses on printed text and delivers the highest
      accuracy for that use case.
    question: Does Aspose OCR support handwritten text?
  - answer: Yes—download the image into a `byte[]` or `InputStream` (e.g., using `java.net.URL`)
      and pass that stream to `ocrEngine.recognize(inputStream)`.
    question: Can I process images directly from a URL?
  - answer: Use `ocrConfig.setRegion(new Rectangle(x, y, width, height))` before calling
      `recognize`. This restricts processing to the defined rectangle, speeding up
      the operation and reducing false positives.
    question: How do I limit OCR to a specific region of an image?
  - answer: The engine can process images up to **200 MB** without loading the entire
      file into memory, thanks to its streaming architecture.
    question: What is the maximum file size Aspose OCR can handle?
  - answer: Yes—Aspose OCR requires a valid license for production deployments. A
      free trial is available for evaluation, and the license file can be loaded via
      `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: Is a commercial license required for production use?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Tambahkan dependensi Aspose OCR Maven untuk mengekstrak teks gambar di Java
url: /id/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan dependensi Aspose OCR Maven untuk mengekstrak teks gambar di Java

Jika Anda perlu **mengekstrak teks gambar di Java** dengan cepat dan andal, menambahkan dependensi Aspose OCR Maven adalah cara paling sederhana untuk memulai. Baik Anda sedang membangun pipeline pemrosesan faktur, arsip yang dapat dicari, atau backend seluler yang membaca formulir tulisan tangan, perpustakaan ini memberi Anda mesin OCR siap pakai dengan pemeriksaan ejaan bawaan, pilihan bahasa, dan dukungan kamus khusus. Dalam tutorial ini Anda akan melihat cara menambahkan dependensi Maven, mengonfigurasi mesin, dan mengambil teks bersih serta terkorrek dari format gambar yang didukung.

---

## Jawaban Cepat
- **Koordinat Maven mana yang menambahkan Aspose OCR?** `com.aspose:aspose-ocr:24.10` (ganti 24.10 dengan versi terbaru).  
- **Versi Java apa yang diperlukan?** Java 8 atau lebih baru; perpustakaan berjalan pada runtime JDK 8+ apa pun.  
- **Bisakah saya mengaktifkan pemeriksaan ejaan?** Ya—panggil `ocrConfig.setSpellCheck(true)` setelah membuat mesin.  
- **Bagaimana cara menggunakan kamus khusus?** Muat file `.dic` dan berikan ke `ocrConfig.setSpellCheckDictionary(path)`.  
- **Apakah perpustakaan ini cocok untuk PDF besar?** Ya—proses setiap halaman sebagai gambar dan gunakan kembali instance `OcrEngine` yang sama untuk menjaga penggunaan memori tetap rendah.

---

## Apa itu dependensi Aspose OCR Maven?
**Dependensi Aspose OCR Maven** adalah artefak Gradle/Maven yang menggabungkan mesin OCR lengkap, paket bahasa, dan sumber daya pemeriksaan ejaan ke dalam satu JAR, memungkinkan Anda memanggil fungsi OCR langsung dari kode Java tanpa binari native. Menambahkan dependensi ini menarik **lebih dari 70 paket bahasa** dan **mendukung lebih dari 30 format gambar**, sehingga Anda dapat menangani PNG, JPEG, TIFF, BMP, dan bahkan TIFF multi‑halaman secara langsung.

---

## Mengapa menggunakan Aspose OCR untuk konversi gambar ke teks di Java?
Aspose OCR memproses halaman yang dipindai 300 dpi secara tipikal dalam **kurang dari 200 ms** pada CPU standar 2.5 GHz, dan dapat menangani dokumen hingga **200 MB** tanpa memuat seluruh file ke memori. Pemeriksaan ejaan bawaan meningkatkan akurasi OCR mentah sebesar **12–18 persen** pada pemindaian yang berisik, yang berarti lebih sedikit langkah pasca‑pemrosesan bagi Anda.

---

## Prasyarat
- **Java 8+** (setiap JDK terbaru berfungsi).  
- **Maven** atau sistem build **Gradle** untuk mengelola dependensi.  
- File gambar yang berisi teks yang diketik atau dicetak (misalnya `invoice_page.png`).  
- Setidaknya **1 GB** memori heap untuk gambar yang sangat besar; pemindaian tipikal membutuhkan jauh lebih sedikit.

> **Tips pro:** Jika Anda menggunakan Maven, tambahkan cuplikan berikut ke `pom.xml` Anda (ganti versi dengan rilis terbaru):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

Cuplikan di atas adalah fragmen XML biasa; itu **tidak** dihitung sebagai blok kode untuk tujuan validasi.

---

## Bagaimana cara menginisialisasi mesin OCR dan mengakses konfigurasinya?
`OcrEngine` class mewakili prosesor OCR inti yang melakukan analisis gambar dan ekstraksi teks.  
Buat instance mesin dengan `new OcrEngine()`, lalu dapatkan konfigurasi yang dapat diubah melalui `getConfiguration()`. Objek konfigurasi memungkinkan Anda mengatur bahasa, mengaktifkan pemeriksaan ejaan, dan menentukan kamus khusus, sehingga Anda dapat menyesuaikan proses OCR untuk tipe dokumen spesifik Anda. Menggunakan kembali instance mesin yang sama pada beberapa gambar mengurangi beban.

```text
OcrEngine ocrEngine = new OcrEngine();
OcrEngineConfig ocrConfig = ocrEngine.getConfig();
```

*Dua baris di atas menggambarkan pola inisialisasi standar. Baris pertama membuat mesin; baris kedua mengambil konfigurasi yang dapat diubah.*

## Bagaimana cara memilih bahasa dan mengaktifkan pemeriksaan ejaan?
Enum `Language` mencantumkan semua bahasa yang didukung yang dapat dikenali oleh mesin OCR.  
Pilih nilai enum yang sesuai (misalnya `Language.ENGLISH`) pada objek konfigurasi untuk memberi tahu mesin model bahasa mana yang akan digunakan. Mengaktifkan pemeriksaan ejaan dengan `setSpellCheck(true)` mengaktifkan kamus bawaan, meningkatkan akurasi dengan memperbaiki kesalahan pengenalan umum. Anda juga dapat menggabungkan beberapa bahasa jika diperlukan, meskipun setiap panggilan memproses satu bahasa pada satu waktu.

```text
ocrConfig.setLanguage(Language.ENGLISH);
ocrConfig.setSpellCheck(true);
```

Mengaktifkan pemeriksaan ejaan mengurangi kesalahan pengenalan OCR umum seperti “0” vs. “O” atau “l” vs. “1”. Untuk dokumen bahasa Inggris kamus default berisi **150 rb** kata, dan Anda dapat memperluasnya dengan istilah Anda sendiri.

## Bagaimana cara memuat kamus pemeriksaan ejaan khusus?
Jika domain Anda menggunakan terminologi khusus—kode medis, singkatan hukum, atau SKU produk—muat file `.dic` khusus. Mesin menggabungkan daftar Anda dengan kamus bawaan, memastikan kata‑kata spesifik domain dikenali dengan benar.

```text
ocrConfig.setSpellCheckDictionary("C:/dictionaries/custom_terms.dic");
```

Anda juga dapat menyediakan kamus sebagai jalur relatif di dalam sumber daya proyek Anda; mesin akan menyelesaikannya pada waktu berjalan.

## Bagaimana cara menjalankan OCR pada file gambar lokal?
`recognize` adalah metode dari `OcrEngine` yang memproses file gambar dan mengembalikan `RecognitionResult` yang berisi teks yang diekstrak.  
Berikan jalur lengkap ke gambar saat memanggil `ocrEngine.recognize("path/to/image.png")`. Metode ini melakukan pra‑pemrosesan seperti perataan (deskewing) dan binarisasi sebelum menerapkan pengenalan jaringan saraf. `RecognitionResult` yang dikembalikan mencakup output OCR mentah dan versi yang telah diperiksa ejaannya, yang dapat Anda akses melalui `getText()`.

```text
RecognitionResult result = ocrEngine.recognize("C:/images/typed_scanned_doc.png");
String correctedText = result.getText();
```

Di balik layar Aspose OCR melakukan deskewing, binarisasi, dan segmentasi karakter sebelum memberi data piksel ke pengenalan jaringan saraf. Proses ini sepenuhnya dikelola oleh perpustakaan; Anda hanya perlu menangani string hasilnya.

## Bagaimana cara menampilkan atau menyimpan teks yang telah dikoreksi?
Cukup cetak string ke konsol, tulis ke file, atau masukkan ke basis data. Karena langkah pemeriksaan ejaan telah membersihkan output, Anda dapat memperlakukan string tersebut sebagai siap produksi.

```text
System.out.println(correctedText);
```

Jika Anda perlu menyimpan hasilnya, gunakan I/O Java standar:

```text
Files.write(Paths.get("output.txt"), correctedText.getBytes(StandardCharsets.UTF_8));
```

## Apa saja kasus tepi umum dan bagaimana cara menanganinya?
Saat bekerja dengan pemindaian dunia nyata, beberapa kondisi dapat memengaruhi kinerja OCR. Resolusi rendah, bahasa campuran, PDF besar, dan terminologi spesifik domain masing‑masing memerlukan penanganan khusus untuk mempertahankan akurasi dan efisiensi. Bagian berikut menjelaskan strategi praktis untuk masing‑masing tantangan umum ini.

### Gambar resolusi rendah
Akurasi OCR turun drastis di bawah **150 dpi**. Untuk pemindaian yang lebih rendah, pertimbangkan untuk memperbesar dengan perpustakaan pemrosesan gambar (misalnya OpenCV) sebelum memberi ke Aspose OCR.

### Dokumen multi‑bahasa
Aspose OCR mendukung **lebih dari 70 bahasa**. Untuk menangani halaman dengan bahasa campuran, panggil `ocrConfig.setLanguage` untuk setiap bahasa yang ingin Anda deteksi, jalankan `recognize` secara terpisah, dan gabungkan hasilnya. Mesin itu sendiri tidak mendeteksi bahasa secara otomatis.

### PDF atau TIFF multi‑halaman
Ekstrak setiap halaman sebagai gambar (menggunakan Aspose PDF, PDFBox, atau perpustakaan serupa), lalu beri setiap gambar ke instance `OcrEngine` yang sama. Menggunakan kembali instance menjaga konsumsi memori rendah karena mesin tidak menyimpan status antar panggilan.

### Sensitivitas pemeriksaan ejaan khusus
Ambang batas pemeriksaan ejaan default bekerja untuk sebagian besar teks bahasa Inggris. Untuk dokumen yang sangat teknis Anda dapat menyesuaikan `SpellCheckOptions` internal melalui `ocrConfig.getSpellCheckOptions().setThreshold(0.75)` (nilai berkisar 0.0–1.0). Nilai lebih rendah membuat mesin lebih agresif dalam memperbaiki kata.

## Pertanyaan yang sering diajukan

**Q: Apakah Aspose OCR mendukung teks tulisan tangan?**  
A: Pengakuan tulisan tangan tersedia dalam modul terpisah (`aspose-ocr-handwriting`). Perpustakaan Aspose OCR standar berfokus pada teks cetak dan memberikan akurasi tertinggi untuk kasus penggunaan tersebut.

**Q: Bisakah saya memproses gambar langsung dari URL?**  
A: Ya—unduh gambar ke dalam `byte[]` atau `InputStream` (misalnya, menggunakan `java.net.URL`) dan berikan aliran tersebut ke `ocrEngine.recognize(inputStream)`.

**Q: Bagaimana cara membatasi OCR ke wilayah tertentu pada gambar?**  
A: Gunakan `ocrConfig.setRegion(new Rectangle(x, y, width, height))` sebelum memanggil `recognize`. Ini membatasi pemrosesan ke persegi panjang yang ditentukan, mempercepat operasi dan mengurangi positif palsu.

**Q: Berapa ukuran file maksimum yang dapat ditangani Aspose OCR?**  
A: Mesin dapat memproses gambar hingga **200 MB** tanpa memuat seluruh file ke memori, berkat arsitektur streamingnya.

**Q: Apakah lisensi komersial diperlukan untuk penggunaan produksi?**  
A: Ya—Aspose OCR memerlukan lisensi yang valid untuk penerapan produksi. Versi percobaan gratis tersedia untuk evaluasi, dan file lisensi dapat dimuat melalui `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

## Kesimpulan dan langkah selanjutnya

Anda kini memiliki alur kerja lengkap end‑to‑end untuk **mengekstrak teks gambar di Java** menggunakan dependensi Aspose OCR Maven. Dengan menambahkan dependensi, mengonfigurasi bahasa dan pemeriksaan ejaan, secara opsional memuat kamus khusus, serta menangani kasus tepi seperti pemindaian resolusi rendah atau PDF multi‑halaman, Anda dapat mengubah gambar berisik menjadi teks bersih dan dapat dicari dengan kode minimal.

Dari sini Anda dapat menjelajahi:
- **Pemrosesan batch** – iterasi melalui direktori gambar dan simpan setiap hasil ke basis data.  
- **Integrasi dengan Aspose PDF** – ekstrak gambar dari PDF dan beri langsung ke mesin OCR.  
- **Penanganan bahasa lanjutan** – ubah `ocrConfig.setLanguage` secara dinamis berdasarkan metadata dokumen.  

Cobalah langkah‑langkah tersebut, bereksperimen dengan opsi konfigurasi, dan Anda akan segera melihat berapa banyak waktu yang dihemat dibandingkan membangun pipeline OCR dari nol. Selamat coding!

![Diagram yang menunjukkan alur kerja OCR untuk mengekstrak teks dari gambar](/images/ocr-workflow.png "alur kerja mengenali teks dari gambar")

---

**Terakhir Diperbarui:** 2026-09-18  
**Diuji Dengan:** Aspose OCR 24.10 for Java  
**Penulis:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();
```

```java
        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);
```

```java
        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // use a locale‑specific dictionary
```

```java
        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");
```

```java
        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();

        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);

        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // or a full path to your .dic file

        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");

        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

```bash
javac -cp "path/to/aspose-ocr.jar" SpellCheckExample.java
java -cp ".;path/to/aspose-ocr.jar" SpellCheckExample
```

## Tutorial Terkait

- [Ekstrak Teks dari Gambar – Dasar-dasar OCR untuk Java](/ocr/java/ocr-basics/)
- [gambar ke teks java: Konversi Gambar ke Teks dengan Aspose.OCR](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Jalankan OCR pada Gambar dengan Java Panduan Lengkap Aspose OCR](/ocr/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}