---
category: general
date: 2026-09-23
description: Pelajari cara melakukan OCR pada gambar di Java menggunakan Aspose OCR,
  mengekstrak teks dari gambar, dan mengaktifkan spell correction dengan custom dictionary.
draft: false
keywords:
- how to perform ocr
- how to extract text from image
- java ocr maven dependency
- java image to text conversion
- aspose ocr java
lastmod: 2026-09-23
og_description: Cara melakukan OCR pada gambar di Java dengan Aspose OCR. Panduan
  ini menunjukkan cara memuat gambar, mengekstrak teks dari gambar, dan menambahkan
  spell correction untuk hasil yang akurat.
og_image_alt: 'Aspose OCR Java tutorial: extracting text from images with spell correction'
og_title: Cara melakukan OCR pada gambar dengan Aspose OCR di Java
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  headline: How to perform OCR on images with Aspose OCR in Java
  type: TechArticle
- description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  name: How to perform OCR on images with Aspose OCR in Java
  steps:
  - name: set up the project and import dependencies
    text: Add the Aspose OCR Maven dependency to your `pom.xml`. This single line
      pulls in the core OCR engine and all required transitive libraries. > **Pro
      tip:** Verify the version number on Maven Central; newer releases add language
      packs and performance improvements.
  - name: load the image for OCR
    text: '`OcrEngine` works with any `InputStream`. Use `ImageStream` to wrap a file
      path, byte array, or URL. **Definition anchor:** `ImageStream` is Aspose OCR’s
      lightweight wrapper that reads image data from various sources without converting
      it to a `BufferedImage` first.'
  - name: enable spell‑correction (optional but powerful)
    text: Turn on the built‑in spell‑correction flag to automatically fix common OCR
      mis‑recognitions such as “l” vs “1”. Spell‑correction can improve accuracy by
      up to **80 %** on low‑contrast scans, turning “Inv0ice” into “Invoice” without
      extra code.
  - name: provide a custom dictionary (tailor the engine)
    text: Supply a plain‑text dictionary for industry‑specific terminology—medical
      codes, legal terms, product SKUs, etc. **Definition anchor:** `CustomDictionary`
      loads a UTF‑8 word list that the OCR engine consults during post‑processing
      to prefer your domain vocabulary.
  - name: run the OCR process
    text: Invoke `process()` to get an `OcrResult` containing the recognized text,
      confidence scores, and optional layout data. If an error occurs, `ocrResult.getErrorMessage()`
      returns a detailed description you can log or display.
  - name: output the recognized (and corrected) text
    text: 'Print the extracted string to the console or write it to a file. For quick
      testing, a simple `System.out.println` is sufficient. Running the program should
      produce clean, searchable text similar to: If you notice stray characters, revisit
      your custom dictionary and consider pre‑processing the image '
  type: HowTo
- questions:
  - answer: No. The library runs entirely offline; all recognition happens locally
      on your JVM.
    question: Does Aspose OCR require an internet connection?
  - answer: Aspose OCR supports Java 8 through Java 21, including both standard and
      OpenJDK distributions.
    question: Which Java versions are supported?
  - answer: Yes. The engine streams data and can handle images up to 500 MB, limited
      only by available heap memory.
    question: Can I process images larger than 10 MB?
  - answer: Purchase a commercial license from the Aspose store and set the license
      file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: How do I license Aspose OCR for production?
  - answer: Aspose OCR includes a handwriting mode that can be enabled via `ocrEngine.getEngineOptions().setHandwriting(true);`,
      improving accuracy on cursive scripts.
    question: Is there built‑in support for handwritten text?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- image to text
- OCR Maven dependency
title: Cara melakukan OCR pada gambar dengan Aspose OCR di Java
url: /id/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada gambar – tutorial Java lengkap

Jika Anda mencari cara yang andal untuk **how to perform OCR** pada file gambar menggunakan Java, Anda berada di tempat yang tepat. Dengan Aspose OCR untuk Java Anda dapat mengekstrak teks dari aset gambar dalam beberapa baris kode, meningkatkan akurasi dengan kamus khusus, dan mengaktifkan koreksi ejaan untuk membersihkan pemindaian yang berisik. Tutorial ini memandu Anda melalui setiap langkah—dari memuat gambar untuk OCR hingga mencetak teks yang telah dikoreksi—sehingga Anda dapat mengintegrasikan konversi gambar‑ke‑teks ke dalam aplikasi Anda hari ini.

## Jawaban Cepat
- **What is the main class to start OCR?** `OcrEngine` adalah kelas inti Aspose OCR yang melakukan pengenalan karakter optik.
- **Which Maven artifact adds OCR support?** Tambahkan `com.aspose:aspose-ocr` ke `pom.xml` Anda.
- **Do I need a license for development?** Lisensi sementara gratis berfungsi untuk pengujian; lisensi komersial diperlukan untuk produksi.
- **Can I improve accuracy on low‑quality scans?** Ya—aktifkan koreksi ejaan dan sediakan kamus khusus.
- **Is multi‑page support built‑in?** Proses setiap gambar halaman dalam loop; mesin ini thread‑safe untuk eksekusi bersamaan.

## Apa itu how to perform OCR?
Frasa **how to perform OCR** mengacu pada proses mengubah teks cetak atau tulisan tangan dalam sebuah gambar menjadi karakter digital yang dapat diedit dan dicari menggunakan teknologi pengenalan karakter optik. Aspose OCR mengimplementasikan proses ini dengan mesin satu‑lalu‑lulus yang mendukung lebih dari 20 format raster dan lebih dari 50 bahasa.

## Mengapa menggunakan Aspose OCR untuk Java?
Aspose OCR mendukung **20+ format gambar** (termasuk PNG, JPEG, TIFF, BMP, dan GIF) dan dapat memproses **batch ratusan halaman** tanpa memuat seluruh dokumen ke memori, menghasilkan hingga **300 halaman per menit** pada server 4‑core tipikal. Fitur koreksi ejaan bawaan dan kamus khususnya mengurangi tingkat kesalahan OCR tipikal dari 12 % menjadi di bawah 2 % pada faktur yang berisik.

## Prasyarat
- **Java Development Kit (JDK) 8+** – runtime Java standar.
- **Aspose OCR for Java** library – dapatkan JAR terbaru dari Maven Central atau portal unduhan Aspose.
- File gambar (misalnya `invoice.png`) yang ingin Anda proses.
- (Opsional) `custom_dict.txt` – file teks UTF‑8 yang berisi kata‑kata spesifik domain, satu per baris.

Itu saja yang Anda butuhkan—tanpa layanan eksternal atau kerangka kerja berat.

## Cara melakukan OCR pada gambar di Java?
Muat gambar Anda, aktifkan koreksi ejaan, secara opsional sediakan kamus khusus, jalankan mesin, dan baca hasilnya. Pendekatan ini bekerja untuk file satu‑halaman maupun pemrosesan batch, dan mesin secara otomatis menangani dekode gambar, deteksi bahasa, dan penilaian kepercayaan, memberikan output teks yang dapat diandalkan siap untuk pemrosesan lebih lanjut. Bagian‑bagian berikut memecah setiap langkah dengan penjelasan jelas dan kode tepat yang perlu Anda salin.

### Langkah 1: siapkan proyek dan impor dependensi

Tambahkan dependensi Maven Aspose OCR ke `pom.xml` Anda. Baris tunggal ini menarik mesin OCR inti dan semua pustaka transitive yang diperlukan.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Pro tip:** Verifikasi nomor versi di Maven Central; rilis terbaru menambahkan paket bahasa dan peningkatan kinerja.

### Langkah 2: muat gambar untuk OCR

`OcrEngine` bekerja dengan semua `InputStream`. Gunakan `ImageStream` untuk membungkus jalur file, array byte, atau URL.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Definition anchor:** `ImageStream` adalah pembungkus ringan Aspose OCR yang membaca data gambar dari berbagai sumber tanpa mengonversinya ke `BufferedImage` terlebih dahulu.

### Langkah 3: aktifkan koreksi ejaan (opsional namun kuat)

Aktifkan flag koreksi ejaan bawaan untuk secara otomatis memperbaiki kesalahan pengenalan OCR umum seperti “l” vs “1”.

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Koreksi ejaan dapat meningkatkan akurasi hingga **80 %** pada pemindaian kontras rendah, mengubah “Inv0ice” menjadi “Invoice” tanpa kode tambahan.

### Langkah 4: sediakan kamus khusus (sesuaikan mesin)

Sediakan kamus teks biasa untuk terminologi spesifik industri—kode medis, istilah hukum, SKU produk, dll.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

**Definition anchor:** `CustomDictionary` memuat daftar kata UTF‑8 yang dikonsultasikan mesin OCR selama pasca‑pemrosesan untuk memprioritaskan kosakata domain Anda.

### Langkah 5: jalankan proses OCR

Panggil `process()` untuk mendapatkan `OcrResult` yang berisi teks yang dikenali, skor kepercayaan, dan data tata letak opsional.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Jika terjadi error, `ocrResult.getErrorMessage()` mengembalikan deskripsi detail yang dapat Anda log atau tampilkan.

### Langkah 6: keluarkan teks yang dikenali (dan dikoreksi)

Cetak string yang diekstrak ke konsol atau tulis ke file. Untuk pengujian cepat, `System.out.println` sederhana sudah cukup.

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Menjalankan program harus menghasilkan teks bersih dan dapat dicari serupa dengan:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Jika Anda melihat karakter yang tidak diinginkan, tinjau kembali kamus khusus Anda dan pertimbangkan pra‑pemrosesan gambar (tingkatkan kontras, hilangkan noise, atau konversi ke grayscale).

## Cara mengekstrak teks dari gambar menggunakan kamus khusus?
Muat kamus sebelum pemrosesan, lalu panggil `ocrEngine.setCustomDictionary(customDict)`. Mesin akan memprioritaskan kata‑kata dari daftar, secara dramatis mengurangi false positive untuk kosakata khusus. Dengan menyediakan istilah spesifik domain, Anda membantu post‑processor OCR menyelesaikan karakter ambigu, seperti membedakan antara huruf “O” dan angka “0”, yang meningkatkan akurasi keseluruhan pada dokumen teknis.

## Cara menambahkan dependensi Maven OCR Java dengan benar?
Tambahkan potongan berikut ke `pom.xml` Anda di dalam bagian `<dependencies>`. Dependensi ini menarik pustaka inti Aspose OCR beserta semua komponen transitive yang diperlukan, memastikan mesin OCR dapat diinstansiasi tanpa konfigurasi tambahan. Pastikan menjalankan `mvn clean install` setelah memperbarui file agar Maven menyelesaikan versi terbaru dari repositori pusat.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

## Pertanyaan umum & kasus tepi

### Bagaimana jika gambar berada dalam format berbeda (PDF, TIFF, dll.)?
Aspose OCR menangani format raster secara langsung. Untuk PDF, ekstrak setiap halaman sebagai gambar terlebih dahulu—Aspose PDF untuk Java menyediakan `PdfExtractor` untuk melakukan ini secara efisien. Setelah Anda memiliki `BufferedImage` atau aliran byte, panggilan `setImage` yang sama berfungsi. Pendekatan ini memungkinkan Anda memproses dokumen multi‑halaman tanpa mengonversi seluruh PDF ke memori, menjaga alur kerja cepat dan skalabel.

### Bagaimana saya menangani dokumen multi‑halaman?
Iterasi setiap gambar halaman, buat instance baru `OcrEngine` (atau reset yang ada), dan gabungkan nilai `OcrResult.getText()`. Pendekatan ini menjaga konteks pemeriksaan ejaan tetap independen per halaman. Dengan memproses halaman secara berurutan atau dalam thread paralel, Anda dapat mempertahankan throughput tinggi sambil memastikan setiap halaman mendapat manfaat dari kamus dan pengaturan koreksi ejaan yang sama.

### Bisakah saya membatasi bahasa atau set karakter?
Ya. Panggil `ocrEngine.getEngineOptions().setLanguage(Language.English)` (atau bahasa yang didukung) untuk mempersempit ruang lingkup pengenalan, yang mempercepat pemrosesan hingga **30 %**. Membatasi bahasa mengurangi set karakter yang harus dipertimbangkan mesin, mengurangi ambiguitas dan meningkatkan kecepatan serta akurasi, terutama untuk dokumen yang hanya berisi karakter Latin.

### Bagaimana dengan kinerja pada batch besar?
Mesin ini thread‑safe untuk operasi hanya‑baca. Buat pool thread dan tugaskan setiap gambar ke instance `OcrEngine` masing‑masing. Pada mesin 4‑core, Anda dapat mencapai **≈250 halaman/menit** dengan eksekusi paralel. Pastikan memori heap yang cukup dialokasikan dan pantau penggunaan CPU untuk menghindari bottleneck saat memproses ribuan gambar resolusi tinggi.

## Tips untuk akurasi lebih baik

- **Pre‑process the image**: tingkatkan kontras, terapkan filter median, atau konversi ke grayscale sebelum OCR.
- **Gunakan pemindaian 300 dpi atau lebih tinggi**; resolusi lebih rendah meningkatkan tingkat kesalahan secara dramatis.
- **Keep the custom dictionary focused**: kata‑kata tidak terkait yang berlebihan dapat membingungkan pemeriksa ejaan.
- **Post‑process with regex**: validasi tanggal, angka, atau ID setelah ekstraksi untuk menangkap anomali yang tersisa.

## Langkah selanjutnya

Sekarang Anda tahu **how to perform OCR** pada gambar dan **how to extract text from image** file, Anda dapat menjelajahi:

- Menyimpan output OCR sebagai PDF yang dapat dicari dengan lapisan teks tersembunyi.
- Menyimpan data faktur yang diekstrak langsung ke basis data relasional.
- Menerapkan model machine‑learning untuk lebih membersihkan catatan tulisan tangan.
- Mengekspos alur kerja OCR sebagai layanan web RESTful untuk gambar yang diunggah pengguna.

Setiap ekstensi ini dibangun di atas langkah inti yang dibahas di atas, sehingga Anda akan menemukan transisi yang mulus.

---

**Last Updated:** 2026-09-23  
**Tested With:** Aspose OCR 24.12 for Java  
**Author:** Aspose  

## Pertanyaan yang sering diajukan

**Q: Apakah Aspose OCR memerlukan koneksi internet?**  
A: Tidak. Perpustakaan ini berjalan sepenuhnya offline; semua pengenalan terjadi secara lokal pada JVM Anda.

**Q: Versi Java mana yang didukung?**  
A: Aspose OCR mendukung Java 8 hingga Java 21, termasuk distribusi standar dan OpenJDK.

**Q: Bisakah saya memproses gambar lebih besar dari 10 MB?**  
A: Ya. Mesin ini melakukan streaming data dan dapat menangani gambar hingga 500 MB, hanya dibatasi oleh memori heap yang tersedia.

**Q: Bagaimana cara melisensikan Aspose OCR untuk produksi?**  
A: Beli lisensi komersial dari toko Aspose dan atur file lisensi dengan `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

**Q: Apakah ada dukungan bawaan untuk teks tulisan tangan?**  
A: Aspose OCR mencakup mode tulisan tangan yang dapat diaktifkan melalui `ocrEngine.getEngineOptions().setHandwriting(true);`, meningkatkan akurasi pada skrip kursif.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

## Tutorial Terkait

- [Lakukan OCR pada Gambar dengan Panduan Langkah demi Langkah Aspose OCR Java](/ocr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/)
- [Pra‑proses Gambar OCR di Java untuk Meningkatkan Akurasi Ekstrak Teks](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [Cara Mengaktifkan GPU untuk OCR di Java Mengenali Teks dari Gambar](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}