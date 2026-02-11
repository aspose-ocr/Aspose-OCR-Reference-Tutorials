---
category: general
date: 2026-02-09
description: Pelajari cara mengenali teks dari gambar menggunakan Aspose OCR di Java.
  Tutorial langkah demi langkah ini juga mencakup pemeriksaan ejaan, kamus khusus,
  dan konfigurasi mesin OCR.
draft: false
keywords:
- recognize text from image
- Aspose OCR Java
- OCR spell checking
- custom OCR dictionary
- Java image processing
language: id
og_description: Kenali teks dari gambar dalam Java menggunakan Aspose OCR. Ikuti panduan
  ini untuk mengaktifkan pemeriksaan ejaan, mengatur bahasa, dan mendapatkan output
  yang telah dikoreksi secara instan.
og_title: Mengenali Teks dari Gambar dengan Aspose OCR – Tutorial Java Lengkap
tags:
- OCR
- Java
- Aspose
title: Mengenali Teks dari Gambar dengan Aspose OCR – Panduan Java Lengkap
url: /id/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali Teks dari Gambar – Tutorial Java Lengkap

Pernah membutuhkan untuk **recognize text from image** tetapi tidak yakin API mana yang dapat dipercaya? Anda tidak sendirian. Dalam banyak proyek—pemindaian faktur, mendigitalkan catatan tulisan tangan, atau membangun arsip yang dapat dicari—kemampuan untuk mengambil teks yang bersih dan dapat dibaca dari sebuah gambar adalah pengubah permainan.  

Kabar baiknya? Dengan Aspose OCR untuk Java Anda dapat melakukannya dalam beberapa baris kode, dan Anda bahkan akan mendapatkan pemeriksaan ejaan bawaan untuk membersihkan output OCR. Dalam tutorial ini kami akan membahas seluruh proses, mulai dari membuat mesin OCR hingga mencetak hasil yang telah diperbaiki. Pada akhir tutorial Anda akan memiliki kelas Java siap‑jalankan yang **recognizes text from image** secara andal.

---

## Apa yang Anda Butuhkan

- **Java 8+** (kode ini bekerja dengan JDK terbaru apa pun)
- **Aspose OCR for Java** library – Anda dapat mengambil JAR terbaru dari repositori Maven Aspose atau mengunduhnya langsung dari situs web Aspose.
- Sebuah file gambar yang berisi teks yang diketik atau dicetak (misalnya `typed_scanned_doc.png`).
- Jumlah RAM yang cukup; OCR tidak memerlukan banyak sumber daya, tetapi heap 1 GB sudah lebih dari cukup untuk kebanyakan pemindaian.

> *Pro tip:* Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Setelah prasyarat selesai, mari kita masuk ke kode.

---

## Langkah 1: Inisialisasi Mesin OCR dan Ambil Konfigurasinya

Hal pertama yang Anda lakukan adalah membuat instance `OcrEngine`. Objek ini adalah inti dari library; ia menyimpan semua pengaturan yang akan Anda ubah nanti.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();
```

Mengapa ini penting: Objek konfigurasi memberi Anda akses langsung ke pemilihan bahasa, flag pemeriksaan ejaan, dan jalur kamus. Tanpanya Anda akan terjebak dengan nilai default, yang mungkin tidak cocok dengan materi sumber Anda.

---

## Langkah 2: Pilih Bahasa dan Aktifkan Pemeriksaan Ejaan

Selanjutnya, beri tahu mesin bahasa apa yang Anda harapkan dalam gambar. Di sini kami memilih Bahasa Inggris, tetapi Aspose mendukung puluhan locale.

```java
        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);
```

Mengaktifkan pemeriksaan ejaan bersifat opsional, namun secara signifikan meningkatkan keterbacaan output—terutama untuk dokumen yang dipindai di mana mesin OCR mungkin salah menafsirkan “0” sebagai “O”.  

---

## Langkah 3: (Opsional) Muat Kamus Pemeriksaan Ejaan Kustom

Jika Anda bekerja dengan jargon khusus industri—misalnya istilah medis, singkatan hukum, atau kode produk khusus—Aspose memungkinkan Anda memasukkan kamus Anda sendiri.

```java
        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // use a locale‑specific dictionary
```

Anda juga dapat mengarahkan `setSpellCheckDictionary` ke file `.dic` dengan jalur lengkap jika memiliki daftar khusus. Mesin akan menggabungkan kata‑kata kustom Anda dengan kamus bawaan, memastikan kosakata spesifik domain tetap utuh.

---

## Langkah 4: Jalankan OCR pada File Gambar Anda

Sekarang pekerjaan sebenarnya dimulai. Berikan jalur ke gambar Anda, dan biarkan mesin melakukan keajaibannya.

```java
        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");
```

Di balik layar, Aspose menerapkan serangkaian langkah pra‑pemrosesan—deskewing, binarisasi, dan segmentasi karakter—sebelum mengirim data piksel ke pengenalan jaringan sarafnya. Hasilnya dibungkus dalam objek `RecognitionResult` yang berisi teks mentah dan teks yang telah diperbaiki.

---

## Langkah 5: Tampilkan Teks yang Telah Diperbaiki

Akhirnya, cetak string yang telah dibersihkan ke konsol. Anda akan melihat output OCR **with spell‑checking applied**, yang biasanya siap disimpan langsung ke basis data atau dimasukkan ke indeks pencarian.

```java
        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

### Output yang Diharapkan

Dengan asumsi `typed_scanned_doc.png` berisi kalimat *“The quick brown fox jumps over the lazy dog.”*, konsol akan menampilkan:

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

Jika pemindaian asli memiliki noda yang mengubah “quick” menjadi “qu1ck”, pemeriksa ejaan akan otomatis memperbaikinya kembali menjadi “quick”.

---

## Menangani Kasus Edge Umum

### 1. Gambar Resolusi Rendah

Akurasi OCR turun tajam di bawah 150 dpi. Jika gambar sumber Anda beresolusi rendah, pertimbangkan untuk memperbesarnya terlebih dahulu (misalnya dengan OpenCV) atau minta pemindaian dengan kualitas lebih tinggi.  

### 2. Dokumen Multi‑Bahasa

Aspose OCR dapat beralih bahasa secara dinamis, tetapi Anda harus mengatur enum `Language` yang sesuai sebelum setiap pemanggilan `recognize`. Untuk halaman dengan bahasa campuran, Anda mungkin perlu menjalankan gambar melalui mesin dua kali—sekali per bahasa—dan kemudian menggabungkan hasilnya.

### 3. PDF Besar atau TIFF Multi‑Halaman

Jika Anda perlu **recognize text from image** yang tertanam dalam PDF, ekstrak setiap halaman sebagai gambar (menggunakan Aspose PDF atau library lain) dan beri ke mesin OCR satu per satu. Mesin bersifat stateless, sehingga Anda dapat menggunakan kembali instance `OcrEngine` yang sama untuk semua halaman.

### 4. Menyesuaikan Sensitivitas Pemeriksaan Ejaan

Ambang batas pemeriksaan ejaan default bekerja untuk kebanyakan teks Bahasa Inggris. Untuk dokumen yang sangat teknis Anda dapat menurunkan sensitivitas dengan menyesuaikan `SpellCheckOptions` internal—meskipun hal itu memerlukan penjelajahan ke API lanjutan Aspose, yang berada di luar lingkup panduan pemula ini.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut adalah kelas Java lengkap, siap untuk dikompilasi dan dijalankan. Ganti `YOUR_DIRECTORY/typed_scanned_doc.png` dengan jalur sebenarnya ke gambar Anda.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();

        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);

        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // or a full path to your .dic file

        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");

        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

Kompilasi dengan:

```bash
javac -cp "path/to/aspose-ocr.jar" SpellCheckExample.java
java -cp ".;path/to/aspose-ocr.jar" SpellCheckExample
```

Anda akan melihat teks yang telah diperbaiki tercetak di konsol, mengonfirmasi bahwa Anda berhasil **recognize text from image** dan menerapkan pemeriksaan ejaan.

---

## Pertanyaan yang Sering Diajukan

**Q: Apakah Aspose OCR mendukung tulisan tangan?**  
A: Library ini dioptimalkan untuk teks cetak. Pengenalan tulisan tangan tersedia dalam modul terpisah (`aspose-ocr-handwriting`), yang dapat Anda integrasikan dengan cara serupa.

**Q: Bisakah saya memproses gambar dari URL alih‑alih file lokal?**  
A: Ya. Unduh gambar ke buffer sementara (misalnya menggunakan `java.net.URL`) dan berikan array byte ke `ocrEngine.recognize(InputStream)`.

**Q: Bagaimana jika saya hanya perlu mengekstrak wilayah tertentu dari gambar?**  
A: Gunakan `ocrEngine.setRegion(Rectangle)` sebelum memanggil `recognize`. Ini membatasi OCR pada persegi panjang yang ditentukan, menghemat waktu dan mengurangi false positive.

---

## Kesimpulan

Kami baru saja menelusuri contoh lengkap end‑to‑end tentang cara **recognize text from image** menggunakan Aspose OCR untuk Java. Dengan mengonfigurasi mesin OCR, mengaktifkan pemeriksaan ejaan, dan secara opsional memuat kamus kustom, Anda dapat mengubah pemindaian berisik menjadi teks bersih yang dapat dicari dengan kode yang minimal.

Dari sini Anda dapat mengeksplorasi:

- **Batch processing** – iterasi melalui folder gambar dan simpan setiap hasil ke basis data.  
- **Integrasi dengan Aspose PDF** – ekstrak gambar dari PDF dan beri ke mesin OCR.  
- **Dukungan bahasa lanjutan** – ubah `ocrConfig.setLanguage` menjadi `Language.FRENCH` atau `Language.SPANISH` untuk proyek multibahasa.  

Cobalah, sesuaikan pengaturan, dan lihat bagaimana kualitas meningkat untuk kasus penggunaan spesifik Anda. Selamat coding, semoga pemindaian Anda selalu tajam!  

![Diagram showing OCR workflow to recognize text from image](/images/ocr-workflow.png "recognize text from image workflow")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}