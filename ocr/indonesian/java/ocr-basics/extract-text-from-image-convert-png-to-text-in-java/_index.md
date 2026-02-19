---
category: general
date: 2026-02-19
description: Ekstrak teks dari gambar menggunakan Aspose OCR Java – pelajari cara
  mengonversi PNG ke teks, memuat gambar untuk OCR, dan ikuti tutorial OCR Java.
draft: false
keywords:
- extract text from image
- convert png to text
- load image for ocr
- java ocr tutorial
- Aspose OCR Java
- OCR language support
language: id
og_description: Ekstrak teks dari gambar dengan Aspose OCR Java. Ikuti tutorial OCR
  Java langkah demi langkah ini untuk mengonversi PNG menjadi teks dan memuat gambar
  untuk OCR.
og_title: Ekstrak Teks dari Gambar – Panduan OCR Java
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Ekstrak teks dari gambar – konversi PNG ke teks dalam Java
url: /id/java/ocr-basics/extract-text-from-image-convert-png-to-text-in-java/
---

: they are {{CODE_BLOCK_X}}. Keep them.

Check any other markdown like blockquote > etc. Keep translation inside.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ekstrak teks dari gambar – Tutorial Java OCR

Pernahkah Anda perlu **ekstrak teks dari gambar** tetapi tidak yakin perpustakaan mana yang memungkinkan Anda melakukannya tanpa ribet? Anda tidak sendirian—para pengembang terus bertanya, “Bagaimana cara mengubah PNG menjadi teks di Java?” Kabar baiknya, Aspose OCR membuat seluruh proses terasa seperti berjalan di taman. Dalam panduan ini kami akan membahas **tutorial java ocr** lengkap, menunjukkan cara **muat gambar untuk OCR**, dan menghasilkan teks bersih yang dapat dicari.

Kami akan membahas semuanya mulai dari menyiapkan engine hingga menangani konten multibahasa, sehingga pada akhir Anda dapat **ekstrak teks dari gambar** berkas dengan ukuran, format, atau bahasa apa pun. Tanpa layanan eksternal, tanpa kunci API—hanya satu JAR dan beberapa baris kode.

## Apa yang Anda Butuhkan

- JDK 8 atau yang lebih baru terpasang (kode ini juga berfungsi pada JDK 11+).  
- Maven atau Gradle untuk mengambil pustaka Aspose OCR, atau Anda dapat mengunduh JAR secara manual dari situs web Aspose.  
- Gambar PNG yang berisi teks yang dapat dibaca (untuk contoh kami akan menggunakan `khmer-sign.png`).  
- IDE atau editor teks yang Anda nyaman gunakan—IntelliJ IDEA, Eclipse, VS Code, apa saja dapat.

Itu saja. Tanpa kerangka kerja berat, tanpa kredensial cloud. Siap? Mari kita mulai mengekstrak teks dari berkas gambar.

## Langkah 1: Tambahkan Aspose OCR ke Proyek Anda

Pertama-tama—Anda memerlukan engine OCR di classpath Anda. Jika Anda menggunakan Maven, tambahkan dependensi ini ke `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

Atau dengan Gradle:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

Jika Anda lebih suka cara manual, unduh JAR dari halaman unduhan Aspose dan letakkan di folder `libs` proyek Anda, kemudian tambahkan ke build path.

> **Pro tip:** Selalu pilih versi stabil terbaru; rilis lama mungkin tidak menyertakan paket bahasa atau perbaikan bug.

## Langkah 2: Buat Instance Engine OCR

Sekarang pustaka tersedia, kita dapat membuat `OcrEngine`. Anggap engine sebagai otak yang akan membaca piksel dan mengubahnya menjadi karakter.

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        // ... further steps will follow
    }
}
```

Mengapa kita membuat engine baru setiap kali? Engine menyimpan buffer internal dan data bahasa; memulai dengan bersih menjamin hasil yang deterministik, terutama ketika Anda beralih bahasa nanti.

## Langkah 3: Aktifkan Bahasa yang Diinginkan (Opsional tetapi Disarankan)

Aspose OCR dilengkapi dengan puluhan paket bahasa. Jika Anda mengetahui bahasa gambar sumber Anda, aktifkan secara eksplisit; ini mempercepat pengenalan dan meningkatkan akurasi. Dalam contoh kami akan mengaktifkan Khmer (`khm`), tetapi Anda dapat menggantinya dengan `ENG` untuk Bahasa Inggris, `CHN` untuk Bahasa Mandarin, dll.

```java
// Enable Khmer language support (ISO 639‑2 code "khm")
ocrEngine.getLanguages().add(OcrLanguage.KHM);
```

> **Mengapa ini penting:** Saat Anda **muat gambar untuk OCR**, engine hanya akan mencari kamus bahasa yang diaktifkan. Membiarkan semua bahasa aktif dapat memperlambat proses dan meningkatkan false positive.

## Langkah 4: Muat Gambar untuk OCR – Mengonversi PNG ke Teks

Di sinilah langkah **muat gambar untuk OCR** terjadi. Aspose menyediakan helper `ImageStream.fromFile` yang memudahkan I/O tingkat rendah.

```java
// Load the PNG that contains the text you want to extract
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));
```

Jika gambar Anda dalam format lain (JPEG, BMP, TIFF), metode yang sama tetap berfungsi—Aspose secara otomatis mendeteksi formatnya. Pastikan jalur file benar; jika tidak Anda akan mendapatkan `FileNotFoundException`.

## Langkah 5: Jalankan Proses OCR dan Konversi PNG ke Teks

Dengan engine siap dan gambar dimuat, pengenalan sebenarnya cukup satu pemanggilan metode. Objek hasil memberikan string mentah serta skor kepercayaan.

```java
// Run OCR and fetch the recognized text
String recognizedText = ocrEngine.recognize().getText();
```

Itu saja—Anda baru saja **mengonversi PNG ke teks**. String yang dikembalikan mungkin berisi pemisah baris dan spasi persis seperti yang dilihat engine. Anda dapat memprosesnya lebih lanjut dengan `trim()`, `replaceAll("\\s+", " ")`, atau pembersihan lain yang diperlukan.

## Langkah 6: Tampilkan Hasil (atau Simpan)

Untuk pemeriksaan cepat, cetak hasil ke konsol. Dalam aplikasi nyata Anda mungkin menulisnya ke file, basis data, atau mengirimnya ke layanan lain.

```java
System.out.println("Recognized text:");
System.out.println(recognizedText);
```

**Output yang diharapkan** (untuk tanda Khmer yang disediakan) mungkin terlihat seperti:

```
សួស្តី
Welcome
```

Jika outputnya berantakan, periksa kembali bahwa Anda telah mengaktifkan bahasa yang tepat pada Langkah 3 dan gambar tidak terlalu buram. Meningkatkan resolusi gambar (mis., menggunakan pemindaian 300 dpi) sering membantu.

## Contoh Kerja Lengkap

Menggabungkan semua bagian, berikut program mandiri yang dapat Anda salin‑tempel ke `ExtractTextExample.java` dan jalankan:

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable the language you need (Khmer in this case)
        ocrEngine.getLanguages().add(OcrLanguage.KHM);

        // 3️⃣ Load the PNG image you want to extract text from
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));

        // 4️⃣ Run OCR – this step actually converts PNG to text
        String recognizedText = ocrEngine.recognize().getText();

        // 5️⃣ Show the result
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

Jalankan program dengan:

```bash
mvn compile exec:java -Dexec.mainClass=ExtractTextExample
```

atau, jika Anda menggunakan Gradle:

```bash
./gradlew run --args='ExtractTextExample'
```

Anda akan melihat teks yang diekstrak dicetak ke konsol, mengonfirmasi bahwa Anda berhasil **mengekstrak teks dari gambar** menggunakan Aspose OCR.

## Kesalahan Umum & Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Perbaikan |
|---------|----------------------|-----------|
| String kosong dikembalikan | Tidak ada bahasa yang diaktifkan atau kode bahasa salah | Tambahkan `OcrLanguage` yang sesuai (mis., `ENG` untuk Bahasa Inggris). |
| Karakter berantakan | Resolusi gambar terlalu rendah atau latar belakang berisik | Gunakan sumber dengan resolusi lebih tinggi, atau pra‑proses dengan filter penajaman. |
| `OutOfMemoryError` | Gambar sangat besar dimuat dalam ukuran penuh | Kurangi ukuran gambar sebelum memberi ke engine (`ImageStream.fromFile(...).scale(0.5)`). |
| `FileNotFoundException` | Jalur tidak tepat | Verifikasi jalur absolut atau relatif; gunakan `Paths.get(...).toAbsolutePath()`. |

> **Ingat:** OCR adalah proses probabilistik. Bahkan dengan pengaturan sempurna Anda mungkin perlu memperbaiki beberapa karakter secara manual, terutama untuk skrip kursif.

## Memperluas Tutorial – Langkah Selanjutnya

- **Pemrosesan batch:** Loop melalui direktori berkas PNG, memanggil logika yang sama untuk setiap gambar.  
- **Output PDF:** Gunakan Aspose PDF untuk menyematkan teks yang diekstrak kembali ke PDF yang dapat dicari.  
- **Deteksi bahasa:** Panggil `ocrEngine.detectLanguage()` sebelum mengatur bahasa agar engine menebak secara otomatis.  
- **Integrasi cloud:** Jika Anda perlu skala, bungkus kode dalam endpoint REST dan biarkan micro‑services memanggilnya.

Semua topik ini secara alami dibangun di atas **tutorial java ocr** yang baru saja kami selesaikan, dan menunjukkan betapa serbagunanya API Aspose OCR sebenarnya.

## Kesimpulan

Kami telah membahas tutorial **java ocr** lengkap yang memungkinkan Anda **mengekstrak teks dari gambar** berkas, **mengonversi PNG ke teks**, dan **memuat gambar untuk OCR** dengan benar menggunakan Aspose OCR. Langkah‑langkahnya sederhana: tambahkan pustaka, buat engine, aktifkan bahasa yang tepat, muat PNG, jalankan `recognize()`, dan tangani output. Dengan fondasi ini Anda dapat mengotomatisasi entri data, membangun arsip yang dapat dicari, atau memberi daya pada aplikasi apa pun yang membutuhkan teks yang dapat dibaca mesin dari gambar.

Cobalah dengan gambar Anda sendiri—mungkin tangkapan layar struk atau kontrak yang dipindai. Sesuaikan pengaturan bahasa, bereksperimen dengan resolusi, dan Anda akan segera melihat betapa fleksibelnya solusi ini. Jika Anda mengalami masalah, tinjau kembali tabel kesalahan atau periksa dokumentasi resmi Aspose; dokumen tersebut lengkap dan selalu diperbarui.

Selamat coding, semoga proyek Anda berikutnya penuh dengan teks bersih yang dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}