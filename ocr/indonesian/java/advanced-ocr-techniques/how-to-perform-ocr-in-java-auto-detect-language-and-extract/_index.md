---
category: general
date: 2026-04-26
description: Pelajari cara melakukan OCR dan mengekstrak teks dari gambar menggunakan
  Aspose OCR. Panduan ini menunjukkan cara memuat gambar untuk OCR, mengaktifkan deteksi
  bahasa otomatis, dan mendeteksi bahasa secara otomatis pada OCR.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image for OCR
- enable automatic language detection
- auto detect language OCR
language: id
og_description: Cara melakukan OCR di Java dengan Aspose OCR. Pelajari cara memuat
  gambar untuk OCR, mengaktifkan deteksi bahasa otomatis, dan mengekstrak teks dari
  gambar.
og_title: Cara Melakukan OCR di Java – Deteksi Bahasa Otomatis
tags:
- OCR
- Java
- Aspose
title: Cara Melakukan OCR di Java – Deteksi Otomatis Bahasa dan Ekstrak Teks
url: /id/java/advanced-ocr-techniques/how-to-perform-ocr-in-java-auto-detect-language-and-extract/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan OCR di Java – Deteksi Bahasa Otomatis dan Ekstrak Teks

Pernahkah Anda perlu **melakukan OCR** pada foto yang mencampur bahasa Inggris, Spanyol, dan mungkin beberapa karakter Jepang? Anda tidak sendirian—para pengembang sering menemui kendala ini ketika aplikasi mereka harus membaca teks dari dokumen yang dipindai, kwitansi, atau tanda multibahasa.  

Kabar baiknya? Dengan beberapa baris Java dan Aspose OCR Anda dapat **memuat gambar untuk OCR**, mengaktifkan **enable automatic language detection**, dan langsung **mengekstrak teks dari gambar** tanpa menebak bahasa terlebih dahulu. Pada tutorial ini kami akan menelusuri contoh lengkap yang dapat dijalankan, menjelaskan mengapa setiap langkah penting, dan menunjukkan cara memverifikasi hasil **auto detect language OCR**.

> **Apa yang akan Anda dapatkan**  
> * Program Java yang berfungsi membaca PNG berbahasa campuran.  
> * Pengetahuan tentang pengaturan OCR kunci yang membuat deteksi bahasa menjadi mudah.  
> * Tips menangani file yang hilang, bahasa yang tidak didukung, dan penyesuaian performa.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

| Prasyarat | Mengapa penting |
|-------------|----------------|
| Java 17 (atau lebih baru) | Aspose OCR menargetkan JVM modern; versi lama mungkin tidak memiliki fitur API. |
| Aspose OCR for Java library (versi terbaru) | Menyediakan `OcrEngine` dan kemampuan deteksi bahasa otomatis. |
| File gambar (`mixed_lang.png`) yang berisi teks dalam setidaknya dua bahasa | Menunjukkan fitur **auto detect language OCR**. |
| IDE Java atau setup command‑line sederhana | Untuk mengompilasi dan menjalankan contoh kode. |

Jika Anda belum mengunduh JAR Aspose OCR, dapatkan dari repositori Maven resmi:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest -->
</dependency>
```

---

## Langkah 1: Buat Instance OCR Engine – Cara Melakukan OCR

Hal pertama yang Anda lakukan ketika ingin **melakukan OCR** adalah menginstansiasi engine. Anggap `OcrEngine` sebagai otak yang akan menganalisis bitmap dan mengubah piksel menjadi karakter.

```java
// Step 1: Initialize the OCR engine
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Create a fresh OcrEngine object – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();
```

> **Tip profesional:** Menggunakan kembali `OcrEngine` yang sama untuk banyak gambar dapat meningkatkan performa karena engine menyimpan model bahasa secara internal.

---

## Langkah 2: Aktifkan Deteksi Bahasa Otomatis – Enable Automatic Language Detection

Secara default Aspose OCR mengasumsikan bahasa Inggris. Untuk gambar multibahasa Anda harus memberitahunya untuk “menebak” bahasa per blok teks. Itulah fungsi flag **enable automatic language detection**.

```java
        // Step 2: Turn on auto‑language detection for each region
        ocrEngine.getRecognitionSettings()
                 .setLanguage(OcrLanguage.AUTO_DETECT);
```

Mengapa ini penting: Engine kini memeriksa setiap segmen gambar, memilih bahasa yang paling mungkin, dan menerapkan set karakter yang tepat. Tanpa ini, Anda akan mendapatkan output yang berantakan untuk bagian non‑Inggris.

---

## Langkah 3: Muat Gambar untuk OCR – Load Image for OCR

Sekarang kita benar‑benar **memuat gambar untuk OCR**. Path dapat berupa absolut atau relatif; pastikan file tersebut ada, jika tidak Anda akan mendapatkan `FileNotFoundException`.

```java
        // Step 3: Point the engine at the image that contains mixed‑language text
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");
```

> **Kasus tepi:** Jika gambar Anda berada di folder resources proyek Maven, gunakan `getClass().getResource("/mixed_lang.png")` untuk menghindari path yang di‑hard‑code.

---

## Langkah 4: Jalankan Pengakuan dan Ekstrak Teks dari Gambar – Extract Text from Image

Dengan engine yang telah dikonfigurasi dan gambar yang sudah dimuat, saatnya **melakukan OCR**. Pemanggilan `recognize()` melakukan pekerjaan berat, sementara `getText()` mengembalikan sebuah `String` sederhana.

```java
        // Step 4: Execute OCR and fetch the recognized text
        String recognizedText = ocrEngine.recognize().getText();
```

Pada titik ini library sudah melakukan **auto detect language OCR** untuk setiap blok, sehingga variabel `recognizedText` berisi transkripsi bersih yang menyadari bahasa.

---

## Langkah 5: Tampilkan Hasil – Verify Auto‑Detect Language OCR Output

Akhirnya, kita mencetak hasil ke konsol. Pada aplikasi nyata Anda mungkin menuliskannya ke file, basis data, atau mengirimkannya ke layanan terjemahan.

```java
        // Step 5: Show the output – you’ll see language tags if you enable them
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

### Output yang Diharapkan

Dengan asumsi `mixed_lang.png` berisi “Hello” (Inggris) dan “¡Hola!” (Spanyol), Anda akan melihat sesuatu seperti:

```
Auto‑detected language output:
Hello
¡Hola!
```

Jika Anda mengaktifkan `setShowLanguage(true)` pada pengaturan, engine akan menambahkan kode bahasa di depan tiap baris, misalnya `[en] Hello` dan `[es] ¡Hola!`.

---

## Pertanyaan Umum & Jebakan

### Bagaimana jika path gambar salah?

Engine akan melempar `FileNotFoundException`. Bungkus pemanggilan dalam blok try‑catch dan berikan pesan yang ramah kepada pengguna:

```java
try {
    ocrEngine.setImage("path/to/image.png");
} catch (FileNotFoundException e) {
    System.err.println("Image not found – check the file path!");
    return;
}
```

### Bisakah saya membatasi bahasa untuk mempercepat deteksi?

Ya. Daripada menggunakan `AUTO_DETECT`, Anda dapat menyediakan daftar bahasa:

```java
ocrEngine.getRecognitionSettings()
         .setLanguage(new OcrLanguage[]{OcrLanguage.ENGLISH, OcrLanguage.SPANISH});
```

Ini mengurangi ruang pencarian dan dapat meningkatkan performa pada batch besar.

### Bagaimana **auto detect language OCR** menangani teks tulisan tangan?

Aspose OCR fokus pada teks cetak. Skrip tulisan tangan biasanya memerlukan engine berbeda (misalnya Aspose OCR for Handwriting). Memaksa deteksi pada tulisan tangan akan menghasilkan hasil yang buruk.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut seluruh program, siap untuk dikompilasi dan dijalankan. Ganti `YOUR_DIRECTORY` dengan folder yang berisi `mixed_lang.png`.

```java
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection for each text block
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.AUTO_DETECT);

        // Step 3: Load the image that contains mixed‑language text
        // Make sure the file exists; otherwise an exception is thrown
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");

        // Step 4: Run the recognition process and obtain the extracted text
        String recognizedText = ocrEngine.recognize().getText();

        // Step 5: Display the auto‑detected language output
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

Jalankan dengan:

```bash
javac -cp "aspose-ocr-23.10.jar" AutoDetectDemo.java
java -cp ".:aspose-ocr-23.10.jar" AutoDetectDemo
```

Anda akan melihat output konsol yang dijelaskan sebelumnya.

---

## Memperluas Solusi

Setelah Anda mengetahui **cara melakukan OCR**, pertimbangkan langkah selanjutnya berikut:

* **Pemrosesan batch** – Loop melalui folder gambar, gunakan kembali instance `OcrEngine` yang sama untuk kecepatan.
* **Menyimpan hasil** – Tulis teks yang diekstrak ke file `.txt` atau simpan di basis data.
* **Pasca‑pemrosesan** – Gunakan regular expression untuk membersihkan baris baru atau menghapus karakter yang tidak diinginkan.
* **Integrasi** – Kirim output ke API terjemahan (Google Translate, Azure Translator) untuk aplikasi multibahasa.

Setiap ekstensi ini tetap bergantung pada konsep inti yang telah kami bahas: memuat gambar, mengaktifkan deteksi bahasa, dan mengekstrak teks.

---

## Kesimpulan

Kami telah menelusuri contoh lengkap end‑to‑end yang menunjukkan **cara melakukan OCR** di Java sambil secara otomatis mendeteksi bahasa. Dengan mengikuti lima langkah—membuat engine, mengaktifkan deteksi bahasa otomatis, memuat gambar, menjalankan pengenalan, dan menampilkan hasil—Anda dapat secara andal **mengekstrak teks dari gambar** yang berisi beberapa skrip.  

Ingat, kunci **auto detect language OCR** yang mulus adalah membiarkan engine memutuskan per blok; memaksa satu bahasa saja sering menghasilkan output yang berantakan. Eksperimen dengan kualitas gambar yang berbeda, daftar bahasa, dan penyesuaian performa untuk menyempurnakan pengalaman sesuai kebutuhan Anda.

Punya skenario yang belum tercakup di sini? Tinggalkan komentar, dan mari kita selesaikan bersama. Selamat coding!  

![how to perform OCR example](/images/ocr-demo.png "Screenshot showing how to perform OCR with Aspose OCR in Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}