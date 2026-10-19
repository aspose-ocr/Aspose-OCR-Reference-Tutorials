---
category: general
date: 2026-05-25
description: Cara mendapatkan OCR di Java dan mengekstrak teks mentah dari gambar.
  Pelajari cara mematikan koreksi ejaan, mengenali teks tulisan tangan, dan cara memuat
  gambar secara efisien.
draft: false
keywords:
- how to get ocr
- extract raw text
- turn off spell correction
- recognize handwritten text
- how to load image
language: id
og_description: Cara mendapatkan OCR di Java dan mengekstrak teks mentah dari gambar.
  Panduan ini menunjukkan cara mematikan koreksi ejaan, mengenali teks tulisan tangan,
  dan cara memuat gambar dengan benar.
og_title: Cara Mendapatkan OCR di Java – Ekstrak Teks Mentah Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  headline: How to Get OCR in Java – Complete Guide to Extract Raw Text
  type: TechArticle
- description: How to get OCR in Java and extract raw text from images. Learn to turn
    off spell correction, recognize handwritten text, and how to load image efficiently.
  name: How to Get OCR in Java – Complete Guide to Extract Raw Text
  steps:
  - name: Maven Dependency
    text: If you’re using Maven, paste this into your `pom.xml`. It pulls the latest
      Aspose.OCR library (as of May 2026).
  - name: Gradle Alternative
    text: '```gradle implementation ''com.aspose:aspose-ocr:23.11'' ```'
  - name: Expected Output
    text: 'Assuming `handwritten.png` contains the phrase *“Hello World”* written
      in cursive, you’ll see something like:'
  type: HowTo
tags:
- OCR
- Java
- Aspose.OCR
title: Cara Mendapatkan OCR di Java – Panduan Lengkap untuk Mengekstrak Teks Mentah
url: /id/java/advanced-ocr-techniques/how-to-get-ocr-in-java-complete-guide-to-extract-raw-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mendapatkan OCR di Java – Panduan Lengkap untuk Mengekstrak Teks Mentah

Pernah bertanya-tanya **cara mendapatkan OCR** hasil tanpa pembersihan otomatis dari pustaka? Mungkin Anda sedang menangani catatan tulisan tangan dan membutuhkan karakter persis yang dilihat mesin, bukan versi “cantik”. Dalam tutorial ini kami akan menunjukkan contoh langsung yang memperlihatkan **cara mendapatkan OCR** output, cara **mengekstrak teks mentah**, dan mengapa Anda mungkin ingin **mematikan koreksi ejaan** saat mengenali teks tulisan tangan. Pada akhir tutorial Anda juga akan tahu **cara memuat gambar** ke dalam mesin Aspose OCR tanpa masalah.

Kami akan menggunakan Aspose.OCR untuk Java, tetapi konsepnya dapat diterapkan pada SDK OCR apa pun yang menyediakan saklar koreksi ejaan. Tanpa teori berat—hanya solusi praktis, salin‑tempel yang dapat Anda jalankan hari ini.

---

## Apa yang Akan Anda Pelajari

- Cara menyiapkan Aspose.OCR dalam proyek Java  
- Langkah‑langkah tepat **cara mendapatkan OCR** output mentah  
- Mengapa dan **cara mematikan koreksi ejaan** untuk teks murni  
- Cara terbaik **cara memuat gambar** untuk pengenalan optimal  
- Cara **mengenali teks tulisan tangan** dan memverifikasi hasilnya  

Prasyaratnya minimal: Java 8+ terpasang, IDE yang kompatibel dengan Maven (IntelliJ, Eclipse, atau VS Code), dan contoh gambar yang berisi karakter tulisan tangan. Jika Anda belum memiliki salah satunya, cukup unduh JDK dari Oracle dan gambar dari ponsel Anda—tidak masalah.

![Diagram yang menggambarkan alur kerja OCR, menunjukkan cara mendapatkan teks mentah OCR dari sebuah gambar](/images/ocr-workflow.png){: .center alt="cara mendapatkan teks mentah OCR workflow"}

---

## Langkah 1: Tambahkan Aspose.OCR ke Proyek Anda

### Dependensi Maven

Jika Anda menggunakan Maven, tempelkan ini ke dalam `pom.xml` Anda. Ini akan mengambil pustaka Aspose.OCR terbaru (per Mei 2026).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.11</version>
</dependency>
```

> **Pro tip:** Selalu periksa repositori Maven resmi Aspose untuk versi yang lebih baru. Rilis `23.11` menambahkan dukungan lebih baik untuk skrip kursif, yang berguna ketika Anda **mengenali teks tulisan tangan**.

### Alternatif Gradle

```gradle
implementation 'com.aspose:aspose-ocr:23.11'
```

Setelah dependensi terresolusi, Anda siap menulis kode yang benar‑benar **mendapatkan OCR** hasil.

---

## Langkah 2: Buat Instance Mesin OCR

Mesin adalah inti dari proses. Membuatnya sangat sederhana, tetapi keajaiban sesungguhnya dimulai ketika Anda mengkonfigurasinya.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

Mengapa kita memerlukan objek `OcrEngine` khusus? Ia menyimpan semua opsi runtime, termasuk saklar koreksi ejaan yang akan kita ubah selanjutnya. Menjaga mesin terisolasi juga memungkinkan Anda menjalankan beberapa pengenalan secara paralel tanpa kontaminasi silang.

---

## Langkah 3: Matikan Koreksi Ejaan (Jika Anda Membutuhkan Output Mentah)

Sebagian besar pustaka OCR berusaha membantu dengan memperbaiki kata yang salah eja secara otomatis. Itu bagus untuk teks cetak tetapi bencana untuk ekstraksi data mentah. Berikut cara **mematikan koreksi ejaan**:

```java
        // Step 3: Turn off the built‑in spell‑corrector to get raw text
        engine.getEngineOptions().setSpellCorrectorEnabled(false);
```

Ketika flag bernilai `false`, mesin mengembalikan tepat apa yang dilihatnya pada bitmap, mempertahankan pemisah baris, tanda baca, dan bahkan glyph yang terlepas sesekali. Ini penting ketika Anda kemudian memasukkan output ke dalam pipeline pembelajaran mesin yang mengharapkan kebisingan asli.

---

## Langkah 4: Muat Gambar – Cara yang Tepat

Anda mungkin berpikir `engine.getImage().loadFromFile("path")` sudah cukup, tetapi ada beberapa nuansa:

1. **Path absolut vs. relatif** – Gunakan `Paths.get(...)` untuk independensi platform.  
2. **Format yang didukung** – Aspose.OCR menangani PNG, JPEG, BMP, TIFF, dan GIF.  
3. **Resolusi penting** – DPI yang lebih tinggi menghasilkan pengenalan yang lebih baik, terutama untuk tulisan kursif.

Berikut cuplikan kode yang kuat yang memperlihatkan **cara memuat gambar** dengan aman:

```java
        // Step 4: Load the image that contains handwritten text
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        // Validate the file exists
        java.nio.file.Path path = java.nio.file.Paths.get(imagePath);
        if (!java.nio.file.Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }

        // Load the image into the OCR engine
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());
```

Jika Anda menangani aliran (misalnya, mengunggah dari formulir web), ganti `loadFromFile` dengan `loadFromStream`. Inti pentingnya: selalu verifikasi file sebelum memberikannya ke mesin, karena file yang hilang akan memunculkan `NullPointerException` yang samar dan sulit di‑debug.

---

## Langkah 5: Lakukan Pengenalan

Sekarang saatnya menguji—**cara mendapatkan OCR** hasil. Metode `recognize()` menjalankan pipeline internal, menerapkan model bahasa, segmentasi, dan (jika diaktifkan) koreksi ejaan. Karena kami menonaktifkannya, Anda akan menerima karakter yang belum diubah.

```java
        // Step 5: Perform OCR recognition
        OcrResult result = engine.recognize();
```

Objek `OcrResult` menyimpan lebih dari sekadar teks; Anda juga dapat mengambil skor kepercayaan, kotak pembatas, dan bahkan probabilitas per‑karakter. Untuk tutorial ini kami fokus pada teks polos.

---

## Langkah 6: Keluarkan Hasil OCR Mentah

Akhirnya, cetak hasil ke konsol. Ini cara paling sederhana untuk **mengekstrak teks mentah** untuk debugging atau pemrosesan lanjutan.

```java
        // Step 6: Output the raw OCR result
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

### Output yang Diharapkan

Dengan asumsi `handwritten.png` berisi frasa *“Hello World”* yang ditulis kursif, Anda akan melihat sesuatu seperti:

```
Raw OCR output:
H e l l o   W o r l d
```

Perhatikan spasi ekstra—itu disengaja karena mesin mempertahankan spasi persis yang terdeteksi. Jika Anda kemudian perlu menghilangkan spasi berlebih, lakukan pada langkah pasca‑pemrosesan Anda sendiri.

---

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **String kosong** | DPI gambar terlalu rendah atau gambar sepenuhnya putih. | Pastikan gambar sumber setidaknya 300 DPI; gunakan `engine.getImage().setResolution(300, 300)`. |
| **Karakter sampah** | Format file salah atau byte rusak. | Verifikasi file dengan penampil gambar; ekspor ulang sebagai PNG. |
| **Koreksi ejaan masih aktif** | Tidak sengaja diaktifkan kembali di tempat lain dalam kode. | Simpan pemanggilan `setSpellCorrectorEnabled(false)` tepat setelah pembuatan engine. |
| **Teks tulisan tangan tidak dikenali** | Bahasa default engine diatur ke teks cetak Inggris. | Panggil `engine.getEngineOptions().setLanguage(Language.English);` dan opsional `engine.getEngineOptions().setUseDictionary(false);`. |

---

## Memperluas Contoh: Mengenali Teks Tulisan Tangan

Jika kasus penggunaan Anda khusus menargetkan **mengenali teks tulisan tangan**, Anda dapat menyesuaikan beberapa opsi untuk akurasi lebih baik:

```java
        // Enable handwritten mode (available in 23.11+)
        engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);
```

Ini memberi tahu jaringan saraf internal untuk lebih memprioritaskan pola kursif daripada glyph cetak. Pada praktiknya, Anda akan melihat lonjakan signifikan pada skor kepercayaan untuk tanda tangan, catatan, atau sketsa cepat.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut kelas Java lengkap yang mencakup semua langkah yang telah dibahas. Ganti saja `YOUR_DIRECTORY/handwritten.png` dengan jalur ke gambar Anda sendiri dan jalankan.

```java
import com.aspose.ocr.*;

import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Turn off spell correction to get raw output
        engine.getEngineOptions().setSpellCorrectorEnabled(false);

        // Optional: set handwritten mode if needed
        // engine.getEngineOptions().setRecognitionMode(RecognitionMode.Handwritten);

        // 3️⃣ Load the image (how to load image safely)
        String imagePath = "YOUR_DIRECTORY/handwritten.png";
        Path path = Paths.get(imagePath);
        if (!Files.exists(path)) {
            throw new IllegalArgumentException("Image file not found: " + imagePath);
        }
        engine.getImage().loadFromFile(path.toAbsolutePath().toString());

        // 4️⃣ Perform OCR (how to get OCR raw text)
        OcrResult result = engine.recognize();

        // 5️⃣ Print raw result (extract raw text)
        System.out.println("Raw OCR output:");
        System.out.println(result.getText());
    }
}
```

Jalankan dengan:

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectDemo
```

Anda seharusnya melihat karakter mentah dicetak persis seperti yang dibaca mesin.

---

## Kesimpulan

Kami telah membahas **cara mendapatkan OCR** hasil mentah di Java, menunjukkan cara **mematikan koreksi ejaan**, memperlihatkan praktik terbaik **cara memuat gambar**, dan menjelaskan nuansa **mengenali teks tulisan tangan**. Dengan mengikuti langkah‑langkah ini Anda dapat **mengekstrak teks mentah** secara andal, baik Anda membangun pipeline digitalisasi dokumen, alat analisis forensik, atau aplikasi pencatatan sederhana.

Selanjutnya, Anda mungkin ingin menjelajahi:

- **Pemrosesan lanjutan**: memotong spasi, menormalisasi Unicode, atau mengirim output ke model bahasa.  
- **Pemrosesan batch**: mengulang direktori gambar dan menyimpan hasil ke basis data.  
- **Opsi lanjutan**: menyesuaikan `EngineOptions` untuk dukungan multi‑bahasa atau kamus khusus.

Cobalah itu, dan jangan ragu meninggalkan pertanyaan di kolom komentar. Selamat coding, semoga OCR Anda selalu akurat!

## Tutorial Terkait

- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Ekstrak Teks dari Gambar Java dengan Aspose.OCR Mode Deteksi Area](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [mengenali gambar teks dengan Aspose OCR – Tutorial Java OCR Lengkap](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}