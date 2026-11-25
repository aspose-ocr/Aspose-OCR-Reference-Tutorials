---
category: general
date: 2026-06-19
description: Lakukan OCR pada ROI di Java menggunakan Aspose OCR. Pelajari cara mengenali
  teks di wilayah dengan kode langkah demi langkah dan praktik terbaik.
draft: false
keywords:
- perform OCR on ROI
- recognize text in region
- Aspose OCR Java
- OCR region detection
- Java image processing
language: id
og_description: Lakukan OCR pada ROI di Java dengan Aspose OCR. Panduan ini menunjukkan
  cara mengenali teks di wilayah, menangani banyak bahasa, dan menghindari jebakan
  umum.
og_title: Lakukan OCR pada ROI di Java – Tutorial Lengkap Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on ROI in Java using Aspose OCR. Learn how to recognize
    text in region with step‑by‑step code and best practices.
  headline: Perform OCR on ROI in Java – Full Aspose OCR Guide
  type: TechArticle
- description: Perform OCR on ROI in Java using Aspose OCR. Learn how to recognize
    text in region with step‑by‑step code and best practices.
  name: Perform OCR on ROI in Java – Full Aspose OCR Guide
  steps:
  - name: 1. License Path Errors
    text: If `setLicense` throws a `FileNotFoundException`, double‑check the absolute
      path or place the `.lic` file in the project’s resources folder and load it
      with `getResourceAsStream`.
  - name: 2. Overlapping or Out‑of‑Bounds ROIs
    text: Aspose does not automatically clip ROIs that extend beyond the image dimensions.
      Overlapping rectangles can cause duplicated text. Use `engine.getImageSize()`
      to verify bounds before creating rectangles.
  - name: 3. Unsupported Languages
    text: Attempting to set a language not bundled with the library will raise `UnsupportedOperationException`.
      Stick to the languages listed in Aspose’s documentation, or download the additional
      language packs.
  - name: 4. Low‑Resolution Images
    text: OCR accuracy drops dramatically below 100 dpi. If you have a low‑resolution
      scan, consider up‑scaling with a library like **Imgscalr** before feeding it
      to Aspose.
  type: HowTo
tags:
- OCR
- Java
- Aspose
- Image Recognition
title: Lakukan OCR pada ROI di Java – Panduan Lengkap Aspose OCR
url: /id/java/advanced-ocr-techniques/perform-ocr-on-roi-in-java-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada ROI di Java – Tutorial Lengkap Aspose OCR

Pernah bertanya-tanya bagaimana **melakukan OCR pada ROI** di Java? Anda tidak sendirian—para pengembang terus bertanya, *“Bagaimana cara mengekstrak hanya bagian tabel dari faktur tanpa memindai seluruh gambar?”* Dalam panduan ini kami akan menunjukkan secara detail cara **melakukan OCR pada ROI** menggunakan Aspose OCR, dan kami juga akan memperlihatkan cara **mengenali teks dalam wilayah** ketika bahasa yang berbeda muncul berdampingan.

Intinya: menargetkan persegi panjang tertentu (atau ROI) menghemat waktu pemrosesan, mengurangi noise, dan sering menghasilkan hasil yang lebih bersih. Baik Anda menangani kwitansi multibahasa, formulir, atau kontrak yang dipindai, menguasai OCR berbasis ROI adalah pengubah permainan. Mari kita mulai.

## Apa yang Anda Butuhkan

Sebelum memulai, pastikan Anda memiliki:

- **Java 8+** (kode ini bekerja pada JDK terbaru apa pun)
- **Aspose.OCR for Java** library (unduh dari situs Aspose atau tambahkan melalui Maven)
- File lisensi **Aspose OCR** yang valid (`Aspose.OCR.lic`) – demo dapat berjalan tanpa lisensi tetapi akan menambahkan watermark.
- Gambar yang berisi wilayah-wilayah terpisah yang ingin Anda proses (misalnya, faktur dengan header dan tabel berbahasa Prancis).

Itu saja—tanpa kerangka kerja tambahan, tanpa dependensi berat. Jika Anda nyaman dengan IDE dasar seperti IntelliJ IDEA atau Eclipse, Anda siap melanjutkan.

## Lakukan OCR pada ROI – Menyiapkan Mesin

Langkah pertama adalah menyiapkan mesin OCR dan menentukan bahasa default yang akan digunakan. Di sinilah alur kerja **melakukan OCR pada ROI** benar‑benar dimulai.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.geometry.*;

public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

> **Tips profesional:** Jika Anda lupa mengatur lisensi, Aspose tetap akan berjalan tetapi akan menyisipkan watermark “Evaluation” pada output. Ini tidak berbahaya untuk pengujian tetapi tidak cocok untuk produksi.

## Tentukan Wilayah yang Ingin Anda Kenali

Sekarang kita buat persegi panjang yang mewakili bagian gambar yang penting. Anggap setiap `Rectangle` sebagai “kotak potong” yang memberi tahu mesin *di mana* harus mencari.

```java
        // Step 2: Create an OCR engine and set the default language
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(Language.English);

        // Step 3: Define the regions (ROIs) you want to recognize
        // Header region (top part of the image)
        Rectangle header = new Rectangle(0, 0, 1200, 200);
        // Table body region (below the header)
        Rectangle table = new Rectangle(0, 210, 1200, 800);
```

Perhatikan bagaimana kami secara implisit menggunakan istilah **melakukan OCR pada ROI**—setiap `Rectangle` adalah ROI. Anda dapat menyesuaikan koordinat agar cocok dengan tata letak dokumen Anda. Persegi panjang `header` menangkap banner atas, sementara persegi panjang `table` mengambil bagian tubuh di mana kami akan **mengenali teks dalam wilayah** nanti.

## Tambahkan Wilayah dan Atur Bahasa per‑Wilayah

Aspose OCR memungkinkan Anda menetapkan bahasa per wilayah, yang sangat cocok untuk dokumen multibahasa. Di sini kami menggunakan bahasa Inggris untuk header dan beralih ke bahasa Prancis untuk tabel.

```java
        // Step 4: Add the regions to the engine
        engine.addRegion(header);                     // uses default language (English)
        engine.addRegion(table, Language.French);    // optional per‑region language
```

Jika Anda hanya membutuhkan satu bahasa, Anda dapat menghilangkan argumen kedua. Mesin akan otomatis kembali ke bahasa default yang Anda setel sebelumnya.

## Lakukan OCR pada ROI dan Dapatkan Teks Gabungan

Akhirnya, kami menjalankan proses OCR pada seluruh gambar, tetapi hanya ROI yang telah didefinisikan yang akan diproses. Hasilnya menggabungkan teks dalam urutan wilayah yang ditambahkan, sehingga pasca‑pemrosesan menjadi sederhana.

```java
        // Step 5: Perform OCR on the image and retrieve the combined text
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/invoice.png");
        System.out.println(result.getText()); // text from all defined regions in order
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
Invoice #12345
Date: 2026‑06‑01
...
Produit   Quantité   Prix
Café      2          5,00 €
...
```

Blok pertama berasal dari header berbahasa Inggris, blok kedua dari tabel berbahasa Prancis—contoh klasik **mengenali teks dalam wilayah** dengan bahasa campuran.

## Menangani Kendala Umum

Bahkan alur **melakukan OCR pada ROI** yang sederhana sekalipun dapat menemui beberapa jebakan tersembunyi. Berikut adalah masalah paling sering muncul dan cara menghindarinya.

### 1. Kesalahan Jalur Lisensi

Jika `setLicense` melempar `FileNotFoundException`, periksa kembali jalur absolut atau letakkan file `.lic` di folder resources proyek dan muat dengan `getResourceAsStream`.

```java
License license = new License();
license.setLicense(RoiDemo.class.getResourceAsStream("/Aspose.OCR.lic"));
```

### 2. ROI yang Tumpang Tindih atau Keluar Batas

Aspose tidak secara otomatis memotong ROI yang melampaui dimensi gambar. Persegi panjang yang tumpang tindih dapat menyebabkan teks duplikat. Gunakan `engine.getImageSize()` untuk memverifikasi batas sebelum membuat persegi panjang.

```java
Size imgSize = engine.getImageSize("YOUR_DIRECTORY/invoice.png");
if (header.getRight() > imgSize.getWidth()) {
    // Adjust width to stay inside the image
    header.setWidth(imgSize.getWidth() - header.getX());
}
```

### 3. Bahasa yang Tidak Didukung

Mencoba menetapkan bahasa yang tidak termasuk dalam paket library akan memicu `UnsupportedOperationException`. Gunakan bahasa yang tercantum dalam dokumentasi Aspose, atau unduh paket bahasa tambahan.

### 4. Gambar Beresolusi Rendah

Akurasi OCR turun drastis di bawah 100 dpi. Jika Anda memiliki pemindaian beresolusi rendah, pertimbangkan untuk memperbesar dengan library seperti **Imgscalr** sebelum memberikannya ke Aspose.

```java
BufferedImage src = ImageIO.read(new File("invoice.png"));
BufferedImage highRes = Scalr.resize(src, Scalr.Method.QUALITY, 300);
ImageIO.write(highRes, "png", new File("invoice_high.png"));
```

Kemudian arahkan `recognizeImage` ke `invoice_high.png`.

## Memperluas Contoh: Banyak ROI dan Deteksi Dinamis

Demo ini menggunakan persegi panjang statis, tetapi dalam skenario dunia nyata Anda mungkin ingin mendeteksi tabel secara otomatis. Gabungkan Aspose OCR dengan library **pemrosesan gambar** sederhana (misalnya OpenCV) untuk menemukan kontur, lalu masukkan batas tersebut ke `engine.addRegion`. Ini mengubah skrip **melakukan OCR pada ROI** statis menjadi pipeline dinamis yang bekerja pada tata letak faktur apa pun.

```java
// Pseudo‑code: Detect contours → create Rectangle objects → addRegion()
List<Rect> detected = OpenCVHelper.findTables("invoice.png");
for (Rect r : detected) {
    engine.addRegion(new Rectangle(r.x, r.y, r.width, r.height), Language.French);
}
```

Sekarang Anda dapat **mengenali teks dalam wilayah** tanpa menuliskan nilai piksel secara manual—praktis untuk pemrosesan batch.

## Contoh Lengkap yang Siap Dijalankan (Copy‑Paste)

Berikut adalah program lengkap yang siap dijalankan. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya di mesin Anda.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.geometry.*;

public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Apply license (optional for evaluation)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Initialize engine with default language
        OcrEngine engine = new OcrEngine();
        engine.setLanguage(Language.English);

        // Define ROIs
        Rectangle header = new Rectangle(0, 0, 1200, 200);   // top banner
        Rectangle table  = new Rectangle(0, 210, 1200, 800); // body table

        // Add regions – per‑region language optional
        engine.addRegion(header);                     // English (default)
        engine.addRegion(table, Language.French);    // French for table

        // Run OCR on the image – only the defined ROIs are processed
        OcrResult result = engine.recognizeImage("YOUR_DIRECTORY/invoice.png");

        // Output combined text
        System.out.println("--- OCR Result ---");
        System.out.println(result.getText());
    }
}
```

Jalankan `javac RoiDemo.java && java RoiDemo`. Jika semuanya sudah disiapkan dengan benar, Anda akan melihat teks gabungan dari kedua wilayah tercetak di konsol.

## Kesimpulan

Kami baru saja membahas cara **melakukan OCR pada ROI** di Java menggunakan Aspose OCR, dan Anda kini tahu cara **mengenali teks dalam wilayah** untuk skenario bahasa tunggal maupun multibahasa. Dengan memotong gambar menjadi persegi panjang logis, Anda:

1. Mengurangi waktu pemrosesan,
2. Mengurangi false positive,
3. Mendapatkan kontrol granular atas pemilihan bahasa.

Selanjutnya Anda dapat menjelajahi deteksi ROI dinamis, mengintegrasikan hasil ke basis data, atau menghasilkan PDF yang dapat dicari. Langit adalah batasnya—hanya ingat untuk memvalidasi koordinat ROI, menjaga jalur lisensi tetap rapi, dan memilih paket bahasa yang tepat.

Punya tata letak rumit yang membuat Anda bingung? Tinggalkan komentar atau kirim pull request dengan perbaikan Anda. Selamat coding, semoga OCR Anda selalu akurat!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}