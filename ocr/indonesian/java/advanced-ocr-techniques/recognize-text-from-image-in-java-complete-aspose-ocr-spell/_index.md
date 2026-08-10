---
category: general
date: 2026-06-19
description: Mengenali teks dari gambar dengan Aspose OCR di Java. Pelajari cara mengaktifkan
  pemeriksaan ejaan, menambahkan kamus, dan melakukan OCR dengan pemeriksaan ejaan
  dalam satu tutorial.
draft: false
keywords:
- recognize text from image
- how to enable spellcheck
- how to add dictionary
- ocr with spell check
language: id
og_description: Mengenali teks dari gambar menggunakan Aspense OCR di Java. Panduan
  ini menunjukkan cara mengaktifkan pemeriksaan ejaan, menambahkan kamus, dan menjalankan
  OCR dengan pemeriksaan ejaan.
og_title: Mengenali Teks dari Gambar – Tutorial Pemeriksaan Ejaan OCR Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  headline: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  type: TechArticle
- description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  name: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  steps:
  - name: How to Enable SpellCheck
    text: 'The spell checker lives inside the engine, but it’s disabled by default.
      Flip the switch with a single line:'
  - name: Expected Output
    text: 'Assuming `receipt.png` contains the line “Totel: $12.99” and your custom
      dictionary includes “Total”, the console will display:'
  - name: What if I need multiple languages?
    text: You can call `ocrEngine.setLanguage(Language.English, Language.French)`
      to enable multilingual recognition. Spell‑checking will follow each language’s
      rules, but you still need to enable it with `setEnable(true)`.
  - name: How does the engine handle unknown words?
    text: If a word isn’t in the internal dictionary *and* not in your custom dictionary,
      the spell checker attempts a best‑guess correction based on Levenshtein distance.
      For truly unknown terms, add them to `my-terms.txt`.
  - name: Does the spell checker work on numbers?
    text: By default, numeric strings are left untouched. If you have alphanumeric
      codes (e.g., “AB12C”), add them to your custom dictionary; otherwise the engine
      may try to “fix” them to real words.
  - name: Performance considerations
    text: Enabling spell checking adds a modest overhead—roughly 10‑15 % extra CPU
      per page. For batch processing, consider disabling it on the first pass, then
      re‑run only on pages that failed quality checks.
  type: HowTo
tags:
- OCR
- Java
- SpellCheck
title: Mengenali Teks dari Gambar di Java – Panduan Lengkap Pemeriksaan Ejaan OCR
  Aspose
url: /id/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-aspose-ocr-spell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengenali Teks dari Gambar di Java – Panduan Lengkap Aspose OCR Spell‑Check

Pernahkah Anda perlu **mengenali teks dari gambar** tetapi khawatir hasilnya penuh dengan typo? Anda tidak sendirian. Dalam banyak proyek pemindaian struk atau digitalisasi dokumen, teks OCR mentah terlihat seperti diketik oleh kucing mengantuk. Kabar baiknya? Dengan Aspose OCR Anda dapat mengubah dump berisik itu menjadi teks bersih yang telah diperiksa ejaannya—langsung di dalam Java.

Dalam tutorial ini kami akan membahas contoh siap‑jalankan yang menunjukkan **cara mengaktifkan spellcheck**, **cara menambahkan entri kamus** untuk istilah khusus domain, dan akhirnya cara melakukan **ocr dengan spell check**. Pada akhir tutorial Anda akan memiliki program mandiri yang membaca file gambar, memperbaiki ejaan secara langsung, dan mencetak hasil yang telah dipoles.

## Apa yang Akan Anda Pelajari

- Cara menerapkan lisensi Aspose OCR sehingga API berjalan dengan kecepatan penuh.  
- Langkah‑langkah tepat untuk **mengaktifkan spellcheck** pada mesin OCR.  
- Cara yang tepat untuk **menambahkan kamus khusus** untuk kata‑kata seperti kode produk atau nama merek.  
- Cara memanggil `recognizeImage` dan mengambil teks bersih yang telah dikoreksi.  

Tanpa alat eksternal, tanpa pustaka spell‑checking buatan sendiri—hanya Java murni dan Aspose OCR.

## Prasyarat

- Java 8+ (kode dapat dikompilasi dengan JDK terbaru apa pun).  
- File lisensi Aspose OCR (`Aspose.OCR.lic`). Jika Anda hanya menguji, evaluasi gratis dapat digunakan tetapi akan menambahkan watermark.  
- Maven atau Gradle untuk mengambil dependensi `aspose-ocr`, atau Anda dapat menambahkan JAR secara manual.  
- Sebuah gambar contoh (mis., PNG struk) dan file teks yang berisi istilah khusus.  

> **Pro tip:** Simpan kamus khusus Anda dalam format UTF‑8 dengan satu istilah per baris—Aspose OCR membacanya langsung dari sistem file.

---

## Langkah 1: Siapkan Proyek dan Tambahkan Dependensi Aspose OCR

Jika Anda menggunakan Maven, tambahkan potongan kode berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.8</version> <!-- use the latest version -->
</dependency>
```

Untuk Gradle, idenya sama:

```groovy
implementation 'com.aspose:aspose-ocr:23.8'
```

Setelah dependensi terpasang, buat kelas Java baru bernama `SpellCheckDemo`. Di sinilah keajaiban terjadi.

## Langkah 2: Terapkan Lisensi Aspose OCR

Sebelum melakukan pekerjaan OCR apa pun, Anda harus memberi tahu Aspose bahwa ia diizinkan berjalan tanpa batas. Melewatkan langkah ini akan memicu pengecualian runtime.

```java
// Apply the Aspose OCR license – this removes evaluation watermarks
License license = new License();
license.setLicense("Aspose.OCR.lic");   // path to your .lic file
```

> **Mengapa ini penting:** Lisensi membuka seluruh mesin OCR, termasuk modul spell‑checking bawaan. Tanpa lisensi, mesin tetap berfungsi tetapi akan menolak menggunakan beberapa fitur premium.

## Langkah 3: Buat dan Konfigurasikan Mesin OCR

Sekarang kami menginstansiasi `OcrEngine` inti dan mengatur bahasa ke Inggris. Ini menjadi dasar untuk pengenalan dan spell‑checking.

```java
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.setLanguage(Language.English);   // choose the language that matches your image
```

### Cara Mengaktifkan SpellCheck

Spell checker berada di dalam mesin, tetapi secara default dinonaktifkan. Aktifkan dengan satu baris kode:

```java
ocrEngine.getSpellChecker().setEnable(true);   // enables spell‑checking
```

Baris tersebut memenuhi persyaratan **cara mengaktifkan spellcheck**. Setelah diaktifkan, mesin akan secara otomatis membandingkan setiap kata yang dikenali dengan kamus internalnya dan menyarankan koreksi.

## Langkah 4: Muat Kamus Khusus (Cara Menambahkan Kamus)

Jika dokumen Anda berisi jargon—misalnya SKU produk, istilah medis, atau nama merek—Anda ingin mengajarkan spell checker tentangnya. Aspose OCR memungkinkan Anda menunjuk ke file teks biasa, satu istilah per baris.

```java
// Load a custom word list for spell‑checking
Path customDict = java.nio.file.Paths.get("YOUR_DIRECTORY/my-terms.txt");
ocrEngine.getSpellChecker().addUserDictionary(customDict);
```

> **Bagaimana jika file tidak ditemukan?** API akan melempar `FileNotFoundException`. Bungkus pemanggilan dalam `try/catch` jika Anda memerlukan penurunan yang elegan.

Sekarang mesin mengetahui “AcmeWidget” atau “RX‑9000” dan tidak akan menandainya sebagai salah eja.

## Langkah 5: Mengenali Teks dari Gambar

Dengan mesin yang siap, Anda akhirnya dapat **mengenali teks dari gambar**. Metode `recognizeImage` mengembalikan objek `OcrResult` yang berisi teks mentah dan teks yang telah dikoreksi.

```java
// Recognize text from the image file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png");
```

Karena kami mengaktifkan spell checking sebelumnya, pemanggilan `getText()` sudah mengembalikan versi yang telah dikoreksi.

## Langkah 6: Keluarkan Teks yang Telah Dikoreksi

Yang tersisa hanyalah mencetak (atau menyimpan) string yang telah dibersihkan.

```java
// Output the corrected, spell‑checked text
System.out.println(ocrResult.getText());
```

Saat Anda menjalankan program, Anda akan melihat struk yang diformat dengan rapi dan ejaan yang tepat, bahkan jika gambar asli berisi karakter yang kabur.

---

## Contoh Lengkap yang Berfungsi

Berikut adalah program Java lengkap yang siap dijalankan. Salin‑tempel ke IDE Anda, sesuaikan jalur file, dan tekan **Run**.

```java
import com.aspose.ocr.*;

import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCheckDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");   // <-- replace with your license path

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(Language.English);

        // Step 3: Load a custom word list for spell‑checking
        Path dictPath = Paths.get("YOUR_DIRECTORY/my-terms.txt"); // <-- your dictionary file
        ocrEngine.getSpellChecker().addUserDictionary(dictPath);
        ocrEngine.getSpellChecker().setEnable(true); // <-- how to enable spellcheck

        // Step 4: Recognize text from the image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png"); // <-- your image

        // Step 5: Output the corrected text
        System.out.println(ocrResult.getText());
    }
}
```

### Output yang Diharapkan

Dengan asumsi `receipt.png` berisi baris “Totel: $12.99” dan kamus khusus Anda mencakup “Total”, konsol akan menampilkan:

```
Total: $12.99
```

Typo “Totel” telah otomatis diperbaiki berkat **ocr dengan spell check**.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya membutuhkan banyak bahasa?

Anda dapat memanggil `ocrEngine.setLanguage(Language.English, Language.French)` untuk mengaktifkan pengenalan multibahasa. Spell‑checking akan mengikuti aturan masing‑masing bahasa, tetapi Anda tetap harus mengaktifkannya dengan `setEnable(true)`.

### Bagaimana mesin menangani kata yang tidak dikenal?

Jika sebuah kata tidak ada di kamus internal *dan* tidak ada di kamus khusus Anda, spell checker akan mencoba koreksi perkiraan terbaik berdasarkan jarak Levenshtein. Untuk istilah yang benar‑benar tidak dikenal, tambahkan ke `my-terms.txt`.

### Apakah spell checker bekerja pada angka?

Secara default, string numerik dibiarkan apa adanya. Jika Anda memiliki kode alfanumerik (mis., “AB12C”), tambahkan ke kamus khusus Anda; jika tidak, mesin mungkin mencoba “memperbaiki” menjadi kata nyata.

### Pertimbangan Kinerja

Mengaktifkan spell checking menambah overhead ringan—sekitar 10‑15 % CPU tambahan per halaman. Untuk pemrosesan batch, pertimbangkan menonaktifkannya pada proses pertama, lalu jalankan kembali hanya pada halaman yang gagal pemeriksaan kualitas.

---

## Ringkasan

Kami telah membahas semua yang Anda perlukan untuk **mengenali teks dari gambar** menggunakan Aspose OCR di Java sambil menjaga output tetap bersih. Langkah‑langkahnya adalah:

1. Terapkan lisensi.  
2. Buat `OcrEngine` dan atur bahasa.  
3. **Cara menambahkan kamus** – muat daftar kata khusus.  
4. **Cara mengaktifkan spellcheck** – aktifkan spell‑checker.  
5. Jalankan `recognizeImage` (pemanggilan inti **ocr dengan spell check**).  
6. Cetak teks yang telah dikoreksi.  

Itulah seluruh alur—dari piksel mentah hingga string yang dipoles dan telah diperiksa ejaannya.

---

## Apa Selanjutnya?

- **Pemrosesan batch:** Loop melalui folder gambar dan tulis setiap hasil ke file `.txt` terpisah.  
- **Output PDF:** Gunakan Aspose PDF untuk menyematkan teks yang telah dikoreksi kembali ke PDF yang dapat dicari.  
- **Kamus lanjutan:** Muat beberapa kamus pengguna untuk domain yang berbeda (mis., keuangan vs. medis).  
- **Skor kepercayaan:** Periksa `ocrResult.getConfidence()` untuk menyaring hasil dengan ketidakpastian tinggi.  

Silakan bereksperimen—ganti bahasa, ubah kamus, atau gabungkan dengan pustaka pra‑pemrosesan gambar untuk akurasi yang lebih baik.

Jika Anda mengalami kendala, tinggalkan komentar di bawah. Selamat coding, semoga OCR Anda selalu tercek ejaannya!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [mengenali teks gambar dengan Aspose OCR – Tutorial OCR Java Lengkap](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Cara mengekstrak teks dari gambar melalui URL menggunakan Aspose.OCR untuk Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}