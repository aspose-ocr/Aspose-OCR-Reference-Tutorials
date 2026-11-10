---
category: general
date: 2026-06-25
description: Buat objek OCRConfig di Java dan aktifkan mode evaluasi Aspose OCR. Pelajari
  cara mengatur batas halaman, menginisialisasi mesin, dan menjalankan OCR secara
  efisien.
draft: false
keywords:
- create ocrconfig object
- aspose ocr evaluation mode
- java ocr configuration
- set page limit ocr
- asposeocr engine initialization
language: id
og_description: Buat objek OCRConfig di Java, aktifkan mode evaluasi Aspose OCR, dan
  atur batas halaman. Ikuti tutorial langkah demi langkah ini untuk mesin OCR siap
  pakai.
og_title: Buat Objek OCRConfig di Java – Panduan Lengkap Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Create OCRConfig object in Java and enable Aspose OCR evaluation mode.
    Learn to set page limit, initialize the engine, and run OCR efficiently.
  headline: Create OCRConfig Object in Java – Full Aspose OCR Setup Guide
  type: TechArticle
tags:
- Aspose OCR
- Java
- OCR Configuration
title: Buat Objek OCRConfig di Java – Panduan Lengkap Pengaturan Aspose OCR
url: /id/java/advanced-ocr-techniques/create-ocrconfig-object-in-java-full-aspose-ocr-setup-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Objek OCRConfig di Java – Panduan Lengkap Pengaturan Aspose OCR

Pernah perlu **create OCRConfig object** di Java tetapi tidak yakin properti mana yang harus diaktifkan terlebih dahulu? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mencoba mengaktifkan mode evaluasi Aspose OCR sambil tetap mengontrol anggaran pemrosesan.

Begini: dengan `OCRConfig` yang dikonfigurasi dengan benar, Anda dapat memulai mesin AsposeOCR dalam hitungan detik, membatasi jumlah halaman yang akan diproses, dan tetap mendapatkan ekstraksi teks yang dapat diandalkan. Dalam tutorial ini kami akan menelusuri setiap baris yang Anda perlukan, menjelaskan *mengapa* setiap pengaturan penting, dan memberikan contoh lengkap yang dapat dijalankan yang dapat Anda masukkan ke dalam proyek Anda hari ini.

> **What you’ll walk away with**  
> * Sebuah potongan kode Java yang berfungsi yang **creates OCRConfig object** dengan mode evaluasi diaktifkan.  
> * Pengetahuan tentang cara **set page limit OCR** untuk menghindari pemrosesan yang tidak terkendali.  
> * Jalur yang jelas ke **AsposeOCR engine initialization** sehingga Anda dapat mulai mengenali teks segera.  

Tidak ada dokumen eksternal, tidak ada referensi yang samar—hanya kode sederhana, alasan yang kuat, dan beberapa tip profesional yang tidak akan Anda temukan di panduan cepat resmi.

---

## Prasyarat

* Java 17 (atau JDK terbaru apa pun) terpasang di mesin Anda.  
* Artefak Maven Aspose.OCR untuk Java yang ditambahkan ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.11</version> <!-- Use the latest version available -->
</dependency>
```

* IDE atau editor yang Anda nyaman gunakan (IntelliJ IDEA, Eclipse, VS Code…).

Itu saja. Tidak ada pustaka native tambahan, tidak ada masalah lisensi untuk build evaluasi—Aspose menyediakan semua yang Anda butuhkan dalam JAR.

---

## Langkah 1: **Create OCRConfig Object** di Java

Hal pertama yang Anda lakukan saat bekerja dengan Aspose OCR adalah menginstansiasi sebuah `OcrConfig`. Anggaplah itu sebagai panel kontrol untuk seluruh mesin.

```java
// Step 1: Create an OCR configuration object
OcrConfig ocrConfig = new OcrConfig();
```

Mengapa memulai di sini? `OcrConfig` menyimpan semua hal mulai dari paket bahasa hingga penyesuaian kinerja. Jika Anda melewatkan langkah ini, mesin akan kembali ke nilai defaultnya—sering kali cukup untuk demo cepat tetapi tidak ideal untuk beban kerja produksi di mana Anda memerlukan kontrol yang lebih ketat.

> **Pro tip:** Anda dapat menggunakan kembali `OCRConfig` yang sama di beberapa instance `AsposeOCR` jika Anda memproses batch secara paralel. Pastikan Anda tidak mengubahnya setelah mesin dimulai.

---

## Langkah 2: Aktifkan **Aspose OCR Evaluation Mode** dan **Set Page Limit OCR**

Mode evaluasi adalah sandbox yang memungkinkan Anda menguji mesin OCR tanpa mengonsumsi kuota lisensi Anda. Padukan dengan batas halaman, dan Anda tidak akan pernah secara tidak sengaja memproses lebih banyak halaman daripada yang dimaksudkan.

```java
// Step 2: Enable evaluation mode and limit the number of pages processed
EvaluationSettings evalSettings = new EvaluationSettings()
        .setEnabled(true)          // Turn on evaluation mode
        .setPageLimit(100);        // Process at most 100 pages
ocrConfig.setEvaluationSettings(evalSettings);
```

*`setEnabled(true)`* mengaktifkan mode evaluasi. Ketika Anda kemudian memanggil `ocrEngine.recognize(...)`, Aspose akan menghitung halaman terhadap batas 100 halaman yang Anda definisikan dengan `setPageLimit`. Setelah batas tercapai, mesin akan melemparkan pengecualian yang ramah, memungkinkan aplikasi Anda berhenti dengan elegan.

**Mengapa memperhatikan batas halaman?**  
Memproses PDF besar dapat menghabiskan banyak memori. Dengan membatasi jumlah halaman, Anda melindungi server dari error OOM dan menjaga model biaya tetap dapat diprediksi—terutama penting saat Anda beralih dari evaluasi ke lisensi berbayar nanti.

---

## Langkah 3: **AsposeOCR Engine Initialization** dengan Pengaturan yang Dikonfigurasi

Sekarang `OCRConfig` sudah lengkap, kami menyerahkannya ke konstruktor `AsposeOCR`. Di sinilah keajaiban (atau lebih tepatnya, kerja berat) dimulai.

```java
// Step 3: Initialise the AsposeOCR engine with the configured settings
AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);
```

Di balik layar, Aspose membaca `EvaluationSettings` yang Anda berikan, mengalokasikan buffer internal, dan memuat data bahasa sebelumnya. Jika ada yang salah konfigurasi, Anda akan langsung mendapatkan `IllegalArgumentException`—jauh lebih baik daripada kegagalan diam-diam di kemudian hari.

> **Edge case:** Jika Anda menjalankan di lingkungan terkontainer, pastikan JVM memiliki heap yang cukup (`-Xmx` flag). Mesin OCR dapat mengonsumsi hingga 2 GB untuk gambar beresolusi tinggi.

---

## Langkah 4: Jalankan Operasi OCR Setelah Konfigurasi

Dengan mesin siap, Anda kini dapat memanggil metode OCR apa pun. Berikut contoh singkat yang membaca satu file gambar dan mencetak teks yang diekstrak.

```java
// Step 4: Proceed with normal OCR operations using ocrEngine...
String imagePath = "src/main/resources/sample.png";

try {
    String extractedText = ocrEngine.recognize(imagePath);
    System.out.println("Recognized Text:");
    System.out.println(extractedText);
} catch (Exception e) {
    // Handles both evaluation limit breaches and I/O errors
    System.err.println("OCR failed: " + e.getMessage());
}
```

Jika Anda mencapai batas 100 halaman, blok `catch` akan mencetak sesuatu seperti:

```
OCR failed: Evaluation mode page limit of 100 exceeded.
```

Pesan itu sengaja dibuat jelas agar Anda dapat memutuskan apakah akan menghentikan pemrosesan, meminta peningkatan lisensi, atau membagi input menjadi bagian‑bagian yang lebih kecil.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut kelas lengkap yang dapat Anda kompilasi dan jalankan langsung:

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.config.OcrConfig;
import com.aspose.ocr.config.EvaluationSettings;

public class EvalModeTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR configuration object
        OcrConfig ocrConfig = new OcrConfig();

        // Step 2: Enable evaluation mode and limit the number of pages processed
        EvaluationSettings evalSettings = new EvaluationSettings()
                .setEnabled(true)          // Turn on evaluation mode
                .setPageLimit(100);        // Process at most 100 pages
        ocrConfig.setEvaluationSettings(evalSettings);

        // Step 3: Initialise the AsposeOCR engine with the configured settings
        AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);

        // Step 4: Perform OCR on a sample image
        String imagePath = "src/main/resources/sample.png";
        try {
            String extracted = ocrEngine.recognize(imagePath);
            System.out.println("Recognized Text:");
            System.out.println(extracted);
        } catch (Exception e) {
            System.err.println("OCR failed: " + e.getMessage());
        }
    }
}
```

**Expected output** (asumsi `sample.png` berisi kata “Hello”) :

```
Recognized Text:
Hello
```

Jika Anda menjalankan program terhadap PDF multi‑halaman dan melampaui batas, Anda akan melihat peringatan mode evaluasi sebagai gantinya.

---

## Pertanyaan Umum & Pro Tips

| Question | Answer |
|----------|--------|
| *Do I need a license to use evaluation mode?* | Tidak. Mode evaluasi gratis, tetapi membatasi Anda pada batas halaman yang Anda tetapkan. |
| *Can I change the page limit at runtime?* | Ya, cukup panggil `ocrConfig.getEvaluationSettings().setPageLimit(newLimit)` sebelum panggilan OCR apa pun. |
| *What if I want to disable evaluation after testing?* | Set `setEnabled(false)` atau cukup hilangkan blok `EvaluationSettings` saat membuat `OCRConfig`. |
| *Is the OCRConfig thread‑safe?* | Konfigurasi bersifat tidak dapat diubah setelah Anda menyerahkannya ke `AsposeOCR`. Bagikan mesin di antara thread untuk kinerja terbaik. |

---

## Kesimpulan

Anda baru saja mempelajari **how to create OCRConfig object** di Java, mengaktifkan **Aspose OCR evaluation mode**, dan secara aman **set page limit OCR** untuk menjaga proses tetap terkendali. Dengan **AsposeOCR engine** yang sepenuhnya diinisialisasi, Anda kini dapat mengenali teks dari gambar, PDF, atau format lain yang didukung tanpa khawatir tentang penggunaan sumber daya yang tidak terkendali.

Langkah logis berikutnya adalah menjelajahi paket bahasa (`ocrConfig.setLanguage("eng")`), menyesuaikan pengaturan pra‑pemrosesan gambar, atau mengintegrasikan mesin ke endpoint REST Spring Boot. Semua topik tersebut dibangun langsung di atas fondasi yang kami letakkan di sini.

Masih ada pertanyaan? Tinggalkan komentar, coba batas yang berbeda, dan selamat coding! 

![Screenshot showing how to create OCRConfig object in Java](/images/create-ocrconfig-object-java.png "create OCRConfig object Java example")

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Set License and Verify Aspose.OCR License in Java](/ocr/english/java/ocr-basics/set-license/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}