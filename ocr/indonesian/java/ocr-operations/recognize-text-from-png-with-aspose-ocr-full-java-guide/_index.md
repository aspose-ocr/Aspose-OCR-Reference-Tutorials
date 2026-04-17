---
category: general
date: 2026-03-28
description: Pelajari cara mengenali teks dari PNG menggunakan Aspose OCR di Java.
  Termasuk mengekstrak teks dari gambar dan mengaktifkan deteksi bahasa otomatis untuk
  bahasa campuran.
draft: false
keywords:
- recognize text from png
- extract text from image
- enable auto language detection
language: id
og_description: Mengenali teks dari PNG secara instan. Panduan ini menunjukkan cara
  mengekstrak teks dari gambar dan mengaktifkan deteksi bahasa otomatis untuk PDF
  campuran bahasa.
og_title: Mengenali teks dari PNG dengan Aspose OCR – Tutorial Java Lengkap
tags:
- Aspose OCR
- Java
- Image Processing
title: Mengenali teks dari PNG dengan Aspose OCR – Panduan Java Lengkap
url: /id/java/ocr-operations/recognize-text-from-png-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali teks dari PNG dengan Aspose OCR – Tutorial Java Lengkap

Pernah membutuhkan untuk **mengenali teks dari png** file tetapi tidak yakin perpustakaan mana yang dapat menangani bahasa campuran dengan baik? Anda tidak sendirian—banyak pengembang mengalami hal yang sama ketika aplikasi mereka harus membaca struk, paspor, atau tanda multilingual.  

Kabar baiknya, Aspose OCR membuatnya sangat mudah: dengan hanya beberapa baris kode Anda dapat **extract text from image**, mengubah PNG menjadi data yang dapat dicari, dan bahkan **enable auto language detection** sehingga mesin memilih skrip yang tepat secara otomatis.  

Dalam tutorial ini kami akan membahas semua yang Anda perlukan untuk memulai: prasyarat, kode langkah‑demi‑langkah, mengapa setiap pengaturan penting, dan cara memverifikasi output. Pada akhir tutorial, Anda akan memiliki program Java yang dapat dijalankan yang dapat membaca PNG yang berisi teks dalam bahasa Inggris, Rusia, dan Mandarin—semua tanpa harus mengganti paket bahasa secara manual.

---

## Apa yang Anda Butuhkan

- **Java Development Kit (JDK) 8+** – kode dapat dikompilasi dengan JDK terbaru apa pun.
- **Aspose.OCR for Java** library (versi terbaru per 2026). Anda dapat mengunduhnya dari Maven Central atau situs web Aspose.
- File gambar (misalnya `mixed-lang.png`) yang berisi teks dalam beberapa bahasa.
- IDE yang layak (IntelliJ IDEA, Eclipse, atau bahkan VS Code) – namun editor teks sederhana juga dapat digunakan.

> **Pro tip:** Jika Anda menggunakan Maven, tambahkan dependensi di bawah ini; jika tidak, unduh JAR dan tambahkan ke classpath Anda.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the newest version -->
</dependency>
```

---

## Langkah 1: Inisialisasi OCR Engine untuk mengenali teks dari png

Sebelum engine dapat melakukan apa pun, Anda memerlukan sebuah instance dari `OcrEngine`. Objek ini menyimpan semua opsi konfigurasi dan melakukan pekerjaan berat.

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine – this is the entry point for all operations
        OcrEngine ocrEngine = new OcrEngine();

        // --------------------------------------------------------------
        // Step 2 and 3 are configured here (see next sections)
        // --------------------------------------------------------------

        // Recognize the image and get the result object
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Print the extracted text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Mengapa ini penting:** `OcrEngine` mengabstraksi algoritma OCR yang mendasarinya. Menginstansiasinya sekali dan menggunakannya kembali pada banyak gambar lebih efisien daripada membuat engine baru untuk setiap file.

---

## Langkah 2: Aktifkan deteksi bahasa otomatis

Jika Anda melewatkan langkah ini, engine akan mengasumsikan satu bahasa default (biasanya Inggris), yang menyebabkan karakter menjadi kacau untuk skrip Cyrillic atau Chinese. Mengaktifkan deteksi otomatis memungkinkan Aspose memindai gambar dan secara otomatis memilih model bahasa terbaik.

```java
// Enable automatic language detection – the engine will sniff the script
ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);
```

> **Apa yang terjadi di balik layar?** Aspose OCR menjalankan pra‑analisis ringan yang memeriksa frekuensi karakter dan rentang Unicode. Ketika menemukan bahasa dominan, ia mengganti dengan model bahasa yang sesuai sebelum proses OCR utama.

---

## Langkah 3: (Opsional) Batasi deteksi ke bahasa yang mungkin – tingkatkan kecepatan

Ketika Anda mengetahui kumpulan bahasa yang diharapkan, Anda dapat memberi petunjuk kepada engine. Ini mempersempit ruang pencarian, mengurangi penggunaan CPU, dan sering menghasilkan hasil yang lebih cepat.

```java
// Suggest candidate languages – only English, Russian, and Chinese will be considered
ocrEngine.getRecognitionSettings()
         .setCandidateLanguages(new String[] { "en", "ru", "zh" });
```

> **Tip:** Jika Anda melewatkan langkah ini, engine tetap akan berfungsi, tetapi akan mengevaluasi semua bahasa yang didukung, yang dapat menambah beberapa detik pada batch besar.

---

## Langkah 4: Kenali PNG dan ekstrak teks dari gambar

Setelah engine dikonfigurasi, panggil `recognizeImage`. Metode ini menerima jalur file, `java.io.File`, atau bahkan `java.io.InputStream`, memberi Anda fleksibilitas untuk unggahan web atau penyimpanan cloud.

```java
// Perform OCR on the specified PNG file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

// The result object holds the raw text, confidence scores, and layout info
String extractedText = ocrResult.getText();
```

> **Kasus khusus:** Jika gambar diputar, Aspose OCR dapat auto‑rotate. Anda juga dapat secara manual mengatur `setDetectOrientation(true)` jika Anda melihat output yang tidak sejajar.

---

## Langkah 5: Tampilkan hasil – verifikasi output

Mencetak ke konsol sudah cukup untuk demo cepat, tetapi dalam aplikasi nyata Anda mungkin menyimpan teks di basis data, mengirimkannya ke indeks pencarian, atau mengembalikannya melalui REST API. Di bawah ini adalah cuplikan verifikasi minimal.

```java
System.out.println("=== Recognized Text ===");
System.out.println(extractedText);
```

### Output konsol yang diharapkan

Asumsikan `mixed-lang.png` berisi tiga baris:

```
Hello world!
Привет мир!
你好，世界！
```

Anda akan melihat sesuatu seperti:

```
=== Recognized Text ===
Hello world!
Привет мир!
你好，世界！
```

Jika output terlihat kacau, periksa kembali bahwa `setAutoDetectLanguage(true)` diaktifkan dan bahwa daftar bahasa kandidat mencakup skrip yang Anda butuhkan.

---

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabungkan)

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);

        // Step 3: (Optional) Limit detection to likely languages
        ocrEngine.getRecognitionSettings()
                 .setCandidateLanguages(new String[] { "en", "ru", "zh" });

        // Step 4: Recognize the PNG image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Step 5: Output the recognized text
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Jalankan:** Kompilasi dengan `javac MixedLangExample.java` dan eksekusi `java MixedLangExample`. Pastikan JAR Aspose OCR berada di classpath Anda (misalnya, `-cp aspose-ocr-23.12.jar;.` di Windows atau `-cp aspose-ocr-23.12.jar:.` di Linux/macOS).

---

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika gambar saya JPEG bukan PNG?** | Metode `recognizeImage` yang sama bekerja untuk JPEG, BMP, TIFF, dll. Cukup ubah ekstensi file. |
| **Bisakah saya memproses aliran dari permintaan HTTP?** | Tentu saja. Gunakan `recognizeImage(InputStream)` dan alirkan input stream permintaan secara langsung. |
| **Seberapa akurat deteksi bahasa otomatis untuk skrip yang mirip (misalnya Serbian Cyrillic vs Russian)?** | Biasanya sangat akurat, tetapi Anda dapat memaksa bahasa dengan menambahkannya ke `candidateLanguages` dan menghapus yang lain. |
| **Apakah saya memerlukan lisensi untuk Aspose OCR?** | Lisensi evaluasi gratis cukup untuk pengujian, tetapi penggunaan produksi memerlukan lisensi berbayar untuk menghapus watermark dan membuka semua fitur. |
| **Bagaimana dengan kinerja pada batch besar?** | Gunakan kembali satu instance `OcrEngine` dan proses gambar secara berurutan atau dalam thread pool. Engine ini thread‑safe untuk operasi read‑only. |

---

## Langkah Selanjutnya & Topik Terkait

- **Extract text from image** dalam file PDF – gabungkan Aspose PDF dengan OCR untuk dokumen yang dipindai.
- **Batch processing** – gunakan `ExecutorService` Java untuk memparallelkan ribuan PNG.
- **Post‑processing** – terapkan pemeriksaan ejaan atau tokenisasi khusus bahasa setelah ekstraksi.
- **Integrate with cloud storage** – baca PNG secara langsung dari AWS S3 atau Azure Blob Storage menggunakan stream.

Silakan bereksperimen: coba tambahkan `setDetectOrientation(true)` jika Anda memiliki pemindaian yang diputar, atau ganti daftar bahasa kandidat untuk menyertakan Jepang (`"ja"`) atau Arab (`"ar"`). API ini cukup fleksibel untuk sebagian besar proyek yang berfokus pada OCR.

---

## Kesimpulan

Anda kini memiliki contoh lengkap yang solid yang menunjukkan cara **recognize text from png** menggunakan Aspose OCR, **extract text from image**, dan **enable auto language detection** untuk konten berbahasa campuran. Kode lengkap, penjelasan mencakup baik “bagaimana” maupun “mengapa”, dan Anda telah melihat output yang diharapkan sehingga dapat memverifikasi semuanya berjalan di mesin Anda.

Memiliki kasus penggunaan lain? Tinggalkan komentar, bagikan temuan Anda, atau jelajahi langkah selanjutnya di atas. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}