---
category: general
date: 2026-03-28
description: Jalankan OCR pada gambar di Java menggunakan Aspose OCR untuk mengubah
  gambar menjadi teks, mengekstrak teks Thai dari PNG dengan cepat dan andal.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: id
og_description: Jalankan OCR pada gambar menggunakan Java dan Aspose OCR. Pelajari
  cara mengonversi gambar menjadi teks, mengekstrak teks Thai dari PNG, dan menangani
  jebakan umum.
og_title: Jalankan OCR pada Gambar dengan Java – Ekstrak Teks Thai dengan Cepat
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Jalankan OCR pada Gambar dengan Java – Ekstrak Teks Thai dari PNG
url: /id/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Gambar dengan Java – Tutorial Lengkap

Pernah bertanya-tanya bagaimana **menjalankan OCR pada gambar** langsung dari kode Java? Mungkin Anda memiliki koleksi struk Thailand, dokumen yang dipindai, atau tangkapan layar dan Anda membutuhkan teksnya tanpa harus mengetiknya secara manual. Itu adalah masalah umum, terutama ketika sumbernya berupa PNG dan bahasanya bukan Latin.  

Dalam panduan ini kami akan menunjukkan secara tepat cara **menjalankan OCR pada gambar** menggunakan pustaka Aspose OCR, mengonversi gambar menjadi teks biasa, dan mengekstrak karakter Thai dengan andal. Pada akhir tutorial Anda akan dapat **mengonversi gambar menjadi teks**, **mengekstrak teks dari PNG**, dan bahkan **mengenali teks Thai** hanya dengan beberapa baris kode.

## Apa yang Dibahas dalam Tutorial Ini

* Menyiapkan dependensi Aspose OCR dalam proyek Maven/Gradle.  
* Menginisialisasi `OcrEngine` dan mengkonfigurasinya untuk bahasa Thai.  
* Menjalankan OCR pada file PNG dan menangani kemungkinan error.  
* Mencetak hasil ke konsol dan memverifikasi output.  

Tidak diperlukan pengalaman sebelumnya dengan Aspose—hanya IDE Java dasar dan file gambar yang ingin Anda proses.

## Prasyarat

* Java 8 atau yang lebih baru terpasang (pustaka ini juga bekerja dengan Java 11+).  
* Alat build – Maven atau Gradle (kami akan menunjukkan contoh Maven).  
* Lisensi Aspose OCR (versi percobaan gratis cukup untuk pengujian, tetapi lisensi menghilangkan batas evaluasi).  
* Sebuah PNG yang berisi teks Thai, misalnya `input.png` yang diletakkan di folder resources proyek Anda.

---

## Langkah 1: Tambahkan Aspose OCR ke Proyek Anda

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Pro tip:** Jaga agar versi pustaka tetap selaras dengan catatan rilis resmi Aspose; versi yang lebih baru menambahkan paket bahasa dan peningkatan performa.

Setelah dependensi terpasang, IDE Anda seharusnya otomatis mengimpor kelas‑kelas yang diperlukan.

## Langkah 2: Inisialisasi OCR Engine

Engine adalah inti dari proses – anggaplah sebagai “otak” yang menganalisis pola piksel. Kami juga akan memberi tahu bahwa kami hanya peduli pada karakter Thai.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Mengapa harus mengatur bahasa secara eksplisit? Karena menentukan `"th"` mempersempit set karakter, yang mempercepat pengenalan dan mengurangi kesalahan baca pada glyph yang mirip.

## Langkah 3: Jalankan OCR pada File PNG

Sekarang kami memberi engine gambar yang ingin kami dekode. Metode `recognizeImage` mengembalikan objek `OcrResult` yang berisi string yang diekstrak serta skor kepercayaan.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Jika file tidak dapat ditemukan, Aspose akan melempar `FileNotFoundException`. Sebaiknya bungkus pemanggilan dalam blok `try‑catch` untuk kode produksi, tetapi untuk tutorial ini kami tetap sederhana.

## Langkah 4: Tampilkan Teks yang Dikenali

Akhirnya, kami mencetak hasilnya. Metode `getText()` mengembalikan `String` Java biasa yang dapat Anda simpan, kirim melalui jaringan, atau tulis ke file.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Jika output terlihat berantakan, periksa kembali bahwa PNG sumber beresolusi tinggi (minimal 300 dpi) dan bahwa kode bahasa `"th"` cocok dengan bahasa target Anda.

### Daftar Lengkap

Berikut adalah file Java lengkap yang siap dijalankan. Salin‑tempel ke IDE Anda, ganti jalur gambar jika diperlukan, dan tekan **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![contoh menjalankan OCR pada gambar](image.png "contoh menjalankan OCR pada gambar – kode Java mengekstrak teks Thai dari PNG")

## Langkah 5: Variasi Umum & Kasus Edge

### Mengonversi Gambar menjadi Teks dalam Format Lain

Jika Anda perlu **mengonversi gambar menjadi teks** untuk JPEG atau BMP, cukup ubah ekstensi file pada `imagePath`. Aspose OCR mendukung PNG, JPEG, BMP, TIFF, dan bahkan halaman PDF.

### Mengekstrak Teks dari PNG dengan Banyak Bahasa

Anda dapat meminta engine mendeteksi beberapa bahasa sekaligus:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

Hasilnya akan berisi campuran karakter Thai dan Inggris, yang berguna untuk struk dwibahasa.

### Menangani Gambar Berkualitas Rendah

Untuk pemindaian yang buram, pertimbangkan mengaktifkan preprocessing:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Ini memicu algoritma pengurangan noise dan peningkatan kontras bawaan, meningkatkan langkah **mengekstrak teks dari PNG**.

### Aktivasi Lisensi

Tanpa lisensi, Aspose menyisipkan baris watermark pada output setelah 100 halaman. Aktifkan lisensi Anda lebih awal:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

Letakkan file `.lic` di samping JAR Anda atau referensikan melalui jalur absolut.

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja di Linux?**  
J: Tentu saja. Aspose OCR murni Java, jadi semua OS yang kompatibel dengan JVM dapat menjalankannya.

**T: Bagaimana jika PNG berisi tulisan tangan Thai?**  
J: Pengenalan tulisan tangan terbatas; Anda mungkin memerlukan model jaringan saraf khusus. Aspose OCR unggul pada teks cetak.

**T: Bisakah saya memproses banyak gambar dalam satu folder?**  
J: Bungkus pemanggilan `recognizeImage` dalam loop atas `Files.list(Paths.get("folder"))`. Ingat untuk menggunakan instance `OcrEngine` yang sama demi performa.

## Kesimpulan

Kami telah menelusuri contoh lengkap, end‑to‑end, tentang cara **menjalankan OCR pada gambar** di Java, khususnya untuk **mengekstrak teks Thai** dari PNG. Dengan menginisialisasi `OcrEngine`, mengatur bahasa, memanggil `recognizeImage`, dan mencetak hasilnya, Anda kini memiliki cara andal untuk **mengonversi gambar menjadi teks** tanpa layanan pihak ketiga.

Dari sini Anda dapat:

* **mengekstrak teks dari PNG** secara massal untuk proyek data‑mining.  
* Menggabungkan output OCR dengan API terjemahan untuk mendapatkan padanan bahasa Inggris.  
* Menjelajahi bahasa lain yang didukung Aspose, seperti Mandarin atau Arab, dengan mengganti kode bahasa.

Cobalah dengan gambar Anda sendiri—sesuaikan pengaturan preprocessing, bereksperimen dengan format file berbeda, dan lihat seberapa kuat solusi ini dalam alur kerja dunia nyata Anda.

Selamat coding, semoga pipeline OCR Anda selalu akurat!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}