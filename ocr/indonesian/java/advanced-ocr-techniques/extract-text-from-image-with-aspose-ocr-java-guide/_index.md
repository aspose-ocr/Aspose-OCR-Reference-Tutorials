---
category: general
date: 2026-02-14
description: Ekstrak teks dari gambar menggunakan Aspose OCR di Java. Pelajari cara
  mengekstrak teks dari bidang formulir dengan wilayah minat untuk hasil yang presisi.
draft: false
keywords:
- extract text from image
- extract text from form
language: id
og_description: Ekstrak teks dari gambar menggunakan Aspose OCR di Java. Tutorial
  ini menunjukkan cara mengekstrak teks dari bidang formulir melalui wilayah minat.
og_title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Java
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Java
url: /id/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Java

Pernah membutuhkan untuk **mengekstrak teks dari gambar** tetapi berakhir dengan memparsing seluruh gambar, membuang siklus CPU, dan mendapatkan hasil yang berisik? Anda bukan satu-satunya. Dalam banyak aplikasi dunia nyata—seperti pemindai faktur, pembaca paspor, atau formulir entri data—Anda hanya peduli pada beberapa bidang saja, bukan seluruh kanvas.  

Kabar baiknya, Aspose OCR memungkinkan Anda **mengekstrak teks dari gambar** *dan* dari area formulir tertentu dengan mendefinisikan poligon. Dalam tutorial ini Anda akan melihat secara tepat cara **mengekstrak teks dari formulir** menggunakan Java, mengapa pendekatan ini penting, dan apa yang perlu disesuaikan ketika sesuatu tidak berjalan sesuai rencana.

Di bawah ini kami akan membahas semuanya mulai dari menyiapkan pustaka hingga menangani kasus tepi yang rumit, sehingga pada akhirnya Anda akan memiliki potongan kode siap‑jalankan yang mengambil hanya data yang Anda butuhkan.

## Apa yang Anda Butuhkan

- Java 17 (atau JDK terbaru) – versi yang lebih baru memiliki dukungan Unicode yang lebih baik.  
- Aspose.OCR untuk Java 23.10 (atau versi terbaru pada saat Anda membaca).  
- Sebuah gambar contoh bernama `form.png` yang berisi bidang yang jelas terdefinisi.  
- Sebuah IDE atau editor teks sederhana—IntelliJ IDEA, VS Code, atau bahkan Notepad sudah cukup.

Tidak diperlukan sihir Maven/Gradle untuk demo inti; cukup tambahkan JAR Aspose OCR ke classpath Anda.

---

## Langkah 1 – Inisialisasi Mesin OCR dan Muat Gambar Anda

Hal pertama yang dibutuhkan mesin adalah bitmap untuk diproses. Kami akan menunjukkannya ke `form.png`, yang berada di folder yang sama dengan file sumber.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Mengapa ini penting:*  
Membuat `OcrEngine` baru memberikan Anda kanvas bersih, memastikan tidak ada pengaturan yang tersisa memengaruhi proses Anda. Memuat gambar lebih awal juga memvalidasi bahwa file tersebut ada, sehingga Anda mendapatkan pengecualian yang membantu sebelum membuang waktu pada langkah selanjutnya.

> **Pro tip:** Jika gambar Anda sangat besar (lebih dari 5 MB), pertimbangkan untuk mengubah ukurannya terlebih dahulu. Aspose OCR bekerja lebih cepat pada gambar dengan ukuran kurang dari 2000 px pada salah satu dimensi.

---

## Langkah 2 – Definisikan Poligon untuk Bidang yang Ingin Anda Baca

Sebuah *Region of Interest* (ROI) hanyalah poligon yang memberi tahu mesin di mana harus mencari. Di bawah ini kami membuat dua persegi panjang—satu untuk “First Name” dan satu lagi untuk “Date of Birth”. Sesuaikan koordinatnya agar cocok dengan formulir Anda.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Mengapa poligon bukan persegi panjang?*  
Poligon memberi Anda fleksibilitas untuk menangani kotak yang miring atau tidak berbentuk persegi panjang—hal yang umum saat memindai formulir cetak yang tidak sepenuhnya rata.

---

## Langkah 3 – Beri tahu Aspose OCR untuk Fokus Hanya pada Region Tersebut

Sekarang kami mengikat poligon ke mesin. Metode `setRegionsOfInterest` menerima sebuah daftar, sehingga Anda dapat menambahkan sebanyak mungkin bidang yang Anda inginkan.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Apa yang terjadi di balik layar?*  
Aspose OCR memotong setiap poligon menjadi bitmap terpisah, menjalankan algoritma pengenalan, dan kemudian menyatukan hasilnya. Ini secara dramatis mengurangi false positive dari grafik di sekitarnya.

---

## Langkah 4 – Jalankan Proses OCR

Dengan semua konfigurasi selesai, kami menjalankan OCR. Pemanggilan `process()` mengembalikan objek `OcrResult` yang berisi teks yang diekstrak dan skor kepercayaan.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Jika Anda memerlukan kepercayaan per‑bidang, Anda dapat memeriksa `ocrResult.getRegions()`—setiap region memiliki skor masing‑masing. Untuk kebanyakan formulir sederhana, teks keseluruhan sudah cukup.

---

## Langkah 5 – Tampilkan (atau Simpan) Teks yang Diekstrak

Akhirnya, kami mencetak hasil ke konsol. Dalam aplikasi nyata Anda mungkin menulis ke basis data, file JSON, atau mengirim melalui API.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Output yang diharapkan (contoh):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

Dua baris tersebut sesuai dengan dua poligon yang kami definisikan. Jika Anda melihat spasi berlebih, pangkas dengan `String.trim()`.

---

## Cara Mengekstrak Teks dari Formulir Ketika Anda Memiliki Banyak Bidang

Ketika sebuah formulir berisi puluhan input, mengetik koordinat secara manual menjadi melelahkan. Berikut pola cepat yang dapat Anda gunakan:

1. **Buat sebuah CSV** di mana setiap baris berisi `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`.  
2. **Muat CSV** pada saat runtime, iterasi setiap baris, buat `Polygon`, dan tambahkan ke daftar ROI.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Mengapa repot?*  
Mengotomatisasi pembuatan ROI memungkinkan Anda menggunakan kembali kode Java yang sama pada berbagai tata letak formulir, menjaga proyek Anda tetap DRY (Don’t Repeat Yourself).

---

## Kasus Tepi & Tips yang Mungkin Belum Anda Pikirkan

- **Pemindaian terrotasi:** Jika seluruh gambar terrotasi, panggil `ocrEngine.getEngineOptions().setRotateAngle(degrees)`.  
- **Kontras rendah:** Atur `ocrEngine.getEngineOptions().setContrast(1.5f)` untuk meningkatkan keterbacaan.  
- **Skrip non‑Latin:** Ganti bahasa dengan `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (atau bahasa lain yang didukung).  
- **Kegagalan OCR parsial:** Selalu periksa `ocrResult.getConfidence()`; jika di bawah 80 %, pertimbangkan untuk meminta pengguna melakukan verifikasi manual.  

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Di bawah ini adalah program lengkap, siap untuk dikompilasi dan dijalankan. Ganti `YOUR_DIRECTORY` dengan folder yang berisi `form.png`.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Kompilasi dengan:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

Anda akan melihat dua baris teks yang merupakan hasil dari ROI yang didefinisikan.

---

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja dengan PDF?**  
A: Tidak secara langsung. Konversikan setiap halaman PDF menjadi gambar terlebih dahulu (misalnya, menggunakan Aspose PDF) lalu berikan gambar tersebut ke mesin OCR.

**Q: Bagaimana jika formulir saya memiliki kotak centang?**  
A: OCR tidak dapat membaca status boolean, tetapi Anda dapat memperlakukan area kotak centang sebagai ROI dan memeriksa kepadatan piksel untuk menebak apakah tercentang.

**Q: Bisakah saya mengekstrak teks dari formulir multi‑halaman sekaligus?**  
A: Lakukan iterasi pada setiap gambar halaman, gunakan kembali daftar ROI yang sama, dan gabungkan hasilnya.

---

## Kesimpulan

Kami telah membahas solusi lengkap end‑to‑end untuk **mengekstrak teks dari gambar** menggunakan Aspose OCR, dan menunjukkan bagaimana teknik yang sama memungkinkan Anda **mengekstrak teks dari formulir** dengan akurasi tepat. Dengan mendefinisikan poligon, membatasi fokus mesin, dan menangani jebakan umum, Anda mendapatkan data yang cepat dan bersih tanpa beban memproses seluruh gambar.

Siap untuk langkah selanjutnya? Cobalah menghubungkan output OCR ini ke payload JSON, atau berikan ke model machine‑learning untuk validasi. Langit adalah batasnya, dan sekarang Anda

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}