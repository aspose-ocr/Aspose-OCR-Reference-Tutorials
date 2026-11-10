---
category: general
date: 2026-02-09
description: Jalankan OCR pada gambar menggunakan Aspose OCR di Java – pelajari cara
  mengekstrak teks dari PNG dan mengaktifkan deteksi bahasa otomatis OCR dalam beberapa
  langkah saja.
draft: false
keywords:
- run OCR on image
- extract text from PNG
- auto detect language OCR
- Aspose OCR Java
- Hindi OCR example
language: id
og_description: Jalankan OCR pada gambar secara instan. Panduan ini menunjukkan cara
  mengekstrak teks dari file PNG dan mengaktifkan deteksi bahasa otomatis OCR menggunakan
  Aspose OCR untuk Java.
og_title: Jalankan OCR pada Gambar dengan Java – Tutorial Lengkap Aspose OCR
tags:
- OCR
- Java
- Aspose
title: Jalankan OCR pada Gambar dengan Java – Panduan Lengkap Aspose OCR
url: /id/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Gambar dengan Java – Panduan Lengkap Aspose OCR

Pernahkah Anda perlu **menjalankan OCR pada gambar** tetapi tidak yakin harus mulai dari mana? Mungkin Anda memiliki beberapa screenshot PNG yang berisi teks Hindi, dan Anda bertanya-tanya apakah Java dapat mengambil kata‑kata tersebut tanpa pengaturan machine‑learning yang besar. Kabar baiknya: Anda bisa, dan itu ternyata sangat sederhana dengan Aspose OCR.

Dalam tutorial ini kami akan membahas contoh dunia nyata yang **mengekstrak teks dari PNG** file, menunjukkan cara mengaktifkan **auto detect language OCR**, dan memberikan program Java yang siap dijalankan. Pada akhir tutorial, Anda akan memiliki potongan kode yang mencetak karakter Hindi ke konsol, dan Anda akan memahami mengapa setiap baris penting.

## Apa yang Anda Butuhkan

- **Java Development Kit (JDK) 8** atau yang lebih baru – kode akan dikompilasi dengan versi terbaru apa pun.  
- **Aspose.OCR for Java** library – unduh JAR terbaru dari situs Aspose atau Maven Central.  
- Sebuah gambar contoh (`hindi_sample.png`) yang berisi skrip Devanagari – Anda dapat membuatnya dengan alat screenshot apa pun.  
- Sebuah IDE atau editor teks sederhana – Saya menggunakan IntelliJ IDEA, tetapi `javac` biasa juga berfungsi.

Tidak ada layanan eksternal, tidak ada kunci API cloud, hanya JAR lokal dan sebuah gambar. Sederhana, kan?

## Langkah 1: Tambahkan Aspose OCR ke Proyek Anda

Pertama, pastikan JAR Aspose OCR berada di classpath Anda. Jika Anda menggunakan Maven, tambahkan dependensi berikut:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

Jika Anda lebih suka cara manual, unduh `aspose-ocr-23.10.jar` dan letakkan di folder `libs/` Anda, lalu kompilasi dengan:

```bash
javac -cp "libs/*" LanguageExample.java
```

> **Pro tip:** Simpan nomor versi JAR dalam komentar di bagian atas file sumber Anda – ini membantu Anda di masa depan mengingat API mana yang Anda targetkan.

## Langkah 2: Buat Instance OCR Engine

Sekarang kita membuat objek inti yang melakukan semua pekerjaan berat. Anggap `OcrEngine` sebagai otak di balik operasi.

```java
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

Mengapa menginstansiasinya di sini? Engine menyimpan pengaturan konfigurasi (seperti bahasa) dan sumber daya yang dapat digunakan kembali, sehingga membuatnya sekali per aplikasi mengurangi beban.

## Langkah 3: Konfigurasikan Pengaturan Bahasa (dan Aktifkan Auto‑Detect)

Jika Anda mengetahui bahasa sebelumnya—misalnya Hindi—Anda dapat memberi tahu engine untuk fokus pada Devanagari. Ini meningkatkan akurasi dan mempercepat pemrosesan.

```java
// Step 3a: Force Hindi (Devanagari) recognition
ocrEngine.getConfiguration().setLanguage(Language.HINDI);

// Step 3b (optional): Let the engine guess the language if you're unsure
ocrEngine.getConfiguration().setAutoDetectLanguage(true);
```

Baris `setAutoDetectLanguage(true)` adalah saklar **auto detect language OCR**. Ketika Anda memberi gambar dengan bahasa campuran, engine akan mencoba mengidentifikasi setiap skrip secara otomatis. Ini berguna untuk pekerjaan batch di mana Anda tidak dapat menandai setiap file secara manual.

## Langkah 4: Jalankan OCR pada Gambar PNG

Di sinilah kita benar‑benar **menjalankan OCR pada gambar** data. Metode `recognize` menerima jalur file, membaca bitmap, dan mengembalikan `RecognitionResult`.

```java
// Step 4: Perform OCR on the PNG file
RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");
```

Ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya. Jika file tidak ditemukan, Aspose akan melemparkan pengecualian yang jelas – tidak perlu menebak mengapa gagal nanti.

## Langkah 5: Ambil dan Tampilkan Teks yang Diekstrak

Akhirnya, ambil string yang dikenali dari objek result dan cetak. Untuk Hindi, Anda akan melihat karakter Unicode di konsol, asalkan terminal Anda mendukung UTF‑8.

```java
// Step 5: Output the recognized Hindi text
System.out.println("Hindi text:");
System.out.println(result.getText());
```

**Output yang diharapkan** (asumsi gambar contoh menampilkan “नमस्ते दुनिया”):

```
Hindi text:
नमस्ते दुनिया
```

Jika Anda mengaktifkan auto‑detect dan gambar juga berisi bahasa Inggris, output akan mencakup kedua skrip, tercampur dengan baik.

## Contoh Lengkap yang Dapat Dijalankan

Berikut adalah program lengkap yang dapat dijalankan. Salin‑tempel ke dalam `LanguageExample.java`, sesuaikan jalur gambar, dan Anda siap.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Specify the language to be recognized (Hindi – Devanagari script)
        ocrEngine.getConfiguration().setLanguage(Language.HINDI);

        // Step 3: (Optional) Enable automatic fallback to language detection
        ocrEngine.getConfiguration().setAutoDetectLanguage(true);

        // Step 4: Run OCR on the input image
        RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");

        // Step 5: Print the extracted Hindi text
        System.out.println("Hindi text:");
        System.out.println(result.getText());
    }
}
```

> **Catatan:** Jika Anda menggunakan IDE, pastikan jalur build proyek menyertakan JAR Aspose OCR. Di IntelliJ, buka *File → Project Structure → Libraries* dan tambahkan JAR di sana.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika PNG saya beresolusi rendah?

Akurasi OCR menurun tajam di bawah 150 dpi. Perbesar gambar dengan alat seperti ImageMagick (`convert input.png -resize 200% output.png`) sebelum memberikannya ke engine. Flag `auto detect language OCR` tetap berfungsi, tetapi Anda akan melihat lebih sedikit kesalahan pengenalan.

### Bisakah saya memproses banyak gambar dalam loop?

Tentu saja. Bungkus panggilan `recognize` dalam loop `for`, dan gunakan kembali instance `OcrEngine` yang sama. Menggunakan kembali engine menghindari pemuatan ulang model bahasa setiap iterasi, yang menghemat memori dan waktu CPU.

```java
String[] files = {"img1.png", "img2.png", "img3.png"};
for (String file : files) {
    RecognitionResult r = ocrEngine.recognize(file);
    System.out.println("Text from " + file + ":");
    System.out.println(r.getText());
}
```

### Bagaimana cara menangani konsol non‑Unicode?

Jika terminal Anda menampilkan simbol kacau, atur encoding file ke UTF‑8 saat meluncurkan Java:

```bash
java -Dfile.encoding=UTF-8 -cp "libs/*" LanguageExample
```

### Apakah ada cara untuk mendapatkan skor kepercayaan?

Ya. `RecognitionResult` berisi `getConfidence()` yang mengembalikan nilai float antara 0 dan 1 untuk setiap baris yang dikenali. Anda dapat mengiterasi `result.getLines()` untuk mengekstrak nilai tersebut—berguna untuk menyaring hasil dengan kepercayaan rendah.

## Tips Pro untuk Penggunaan Produksi

- **Cache language models**: Jika Anda memproses ribuan gambar, pertahankan engine tetap hidup untuk seluruh batch.  
- **Parallel processing**: Bungkus setiap gambar dalam `Callable` dan kirim ke thread pool. Ingat bahwa engine tidak thread‑safe; buat satu per thread.  
- **Logging**: Gunakan logger yang tepat (SLF4J) alih-alih `System.out.println` untuk pekerjaan besar.  
- **Memory management**: Panggil `ocrEngine.dispose()` setelah selesai untuk membebaskan sumber daya native.

## Gambaran Visual

![Diagram contoh menjalankan OCR pada gambar](ocr_flow.png "Diagram contoh menjalankan OCR pada gambar")

Diagram di atas menggambarkan alur: **menjalankan OCR pada gambar → konfigurasi bahasa → auto detect language OCR (opsional) → mengekstrak teks dari PNG**.

## Kesimpulan

Kami baru saja menunjukkan cara **menjalankan OCR pada gambar** file menggunakan Aspose OCR untuk Java, cara **mengekstrak teks dari PNG** dengan pengaturan bahasa khusus, dan cara mengaktifkan **auto detect language OCR** untuk skenario fleksibel multibahasa. Contoh kode lengkap siap disalin, dikompilasi, dan dijalankan—tanpa langkah tersembunyi, tanpa layanan eksternal.

Siap untuk tantangan berikutnya? Coba ganti `Language.HINDI` dengan `Language.AUTO` dan beri dokumen dengan skrip campuran, atau bereksperimen dengan input PDF (Aspose OCR juga mendukung PDF). Anda juga dapat mengintegrasikan potongan kode ini ke dalam endpoint REST Spring Boot untuk mengekspos OCR sebagai layanan web.

Selamat coding, dan semoga gambar Anda selalu dapat dibaca!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}