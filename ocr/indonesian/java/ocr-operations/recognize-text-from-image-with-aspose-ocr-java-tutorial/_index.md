---
category: general
date: 2026-02-17
description: Pelajari cara mengenali teks dari gambar dan memuat gambar untuk OCR
  menggunakan pustaka Aspose OCR Java. Panduan langkah demi langkah dengan korektor
  ejaan.
draft: false
keywords:
- recognize text from image
- load image for OCR
- Aspose OCR Java
- spell corrector OCR
- OCR engine setup
language: id
og_description: Mengenali teks dari gambar menggunakan Aspose OCR Java. Tutorial ini
  menunjukkan cara memuat gambar untuk OCR, mengaktifkan koreksi ejaan, dan menghasilkan
  teks bersih.
og_title: Mengenali teks dari gambar – Panduan Lengkap Aspose OCR Java
tags:
- Java
- OCR
- Aspose
title: Mengenali teks dari gambar dengan Aspose OCR – Tutorial Java
url: /id/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/
---

:** ... translate.

Make sure to keep markdown formatting.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar dengan Aspose OCR – Tutorial Java

Pernah perlu **mengenali teks dari gambar** tetapi tidak yakin pustaka mana yang harus dipilih? Anda tidak sendirian. Dalam banyak proyek dunia nyata—misalnya memindai faktur, mendigitalkan catatan tulisan tangan, atau mengekstrak keterangan dari tangkapan layar—mendapatkan hasil OCR yang akurat sangat penting.  

Dalam panduan ini kami akan menunjukkan cara memuat gambar untuk OCR, mengaktifkan korektor ejaan bawaan Aspose OCR, dan akhirnya mencetak teks yang telah dibersihkan. Pada akhir tutorial Anda akan memiliki program Java siap‑jalankan yang **mengenali teks dari gambar** hanya dengan beberapa baris kode.

## Apa yang Dibahas dalam Tutorial Ini

- Cara menerapkan lisensi Aspose OCR Anda (agar demo berjalan tanpa watermark)  
- Membuat instance `OcrEngine` dan memilih bahasa Inggris sebagai bahasa pengenalan  
- **Memuat gambar untuk OCR** menggunakan `OcrInput` dan menunjuk ke file PNG yang berisi kata‑kata salah eja  
- Mengaktifkan korektor ejaan, opsional menunjuk ke kamus khusus  
- Menjalankan proses pengenalan dan mencetak hasil yang telah dikoreksi  

Tanpa layanan eksternal, tanpa file konfigurasi tersembunyi—hanya Java biasa dan JAR Aspose OCR.

> **Pro tip:** Jika Anda baru mengenal Aspose, dapatkan lisensi percobaan gratis selama 30 hari dari situs web Aspose dan letakkan file `.lic` ke dalam folder yang dapat direferensikan dari kode Anda.

## Prasyarat

- Java 8 atau yang lebih baru (kode ini juga dapat dikompilasi dengan JDK 11)  
- Aspose.OCR untuk Java JAR di classpath Anda  
- File `Aspose.OCR.lic` yang valid (atau Anda dapat menjalankan dalam mode evaluasi, tetapi demo akan menambahkan watermark)  
- File gambar (`misspelled.png`) yang berisi teks dengan kesalahan ejaan yang disengaja—sempurna untuk melihat korektor ejaan beraksi  

Sudah siap? Baik—mari kita mulai.

## Langkah 1: Terapkan Lisensi Aspose OCR Anda

Sebelum mesin melakukan pekerjaan berat, ia harus tahu bahwa Anda memiliki lisensi. Jika tidak, Anda akan melihat banner “Trial version” pada output.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – replace the path with where you stored your .lic file
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

*Mengapa ini penting:* Lisensi menonaktifkan watermark percobaan dan membuka seluruh kamus korektor ejaan. Melewatkan langkah ini tetap dapat berjalan, tetapi output Anda akan dipenuhi teks “Aspose OCR Demo”.

## Langkah 2: Buat dan Konfigurasikan OCR Engine

Sekarang kami memulai mesin dan memberi tahu bahasa yang akan digunakan. Bahasa Inggris adalah yang paling umum, tetapi Aspose mendukung puluhan bahasa.

```java
        // Step 2: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Choose English for recognition – you could pick French, German, etc.
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
```

*Mengapa kami mengatur bahasa:* Model bahasa menentukan set karakter dan memengaruhi saran korektor ejaan. Menggunakan bahasa yang salah dapat secara dramatis menurunkan akurasi.

## Langkah 3: Aktifkan Koreksi Ejaan dan (Opsional) Tunjuk ke Kamus Khusus

Aspose OCR dilengkapi dengan kamus bahasa Inggris bawaan, tetapi Anda dapat menyediakan kamus sendiri jika memiliki istilah khusus domain (misalnya jargon medis atau kode produk).

```java
        // Step 3: Turn on the spell corrector
        engine.getSpellCorrector().setEnable(true); // activate spell‑checking

        // Optional: use a custom dictionary folder
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english");
```

*Apa yang dilakukan korektor:* Ketika mesin OCR menemukan kata yang tidak ada dalam kamus, ia akan mencoba menggantinya dengan kecocokan terdekat. Inilah mengapa demo dapat mengubah “recieve” menjadi “receive” secara otomatis.

## Langkah 4: Muat Gambar untuk OCR

Berikut bagian yang secara langsung menjawab **memuat gambar untuk OCR**. Kami membuat objek `OcrInput` dan menambahkan file PNG kami.

```java
        // Step 4: Prepare the image input
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // path to the image you want to process
```

*Mengapa kami menggunakan `OcrInput`:* Ia mengabstraksi logika pembacaan file dan memungkinkan Anda menambahkan banyak halaman nanti jika perlu memproses PDF multi‑halaman atau sekumpulan gambar.

## Langkah 5: Jalankan Pengenalan dan Dapatkan Teks yang Telah Dikoreksi

Sekarang mesin melakukan pekerjaan berat—mengenali karakter, menerapkan model bahasa, dan akhirnya memperbaiki ejaan.

```java
        // Step 5: Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Step 6: Output the corrected text to the console
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

*Output yang diharapkan:* Asumsikan `misspelled.png` berisi frasa “Ths is a smple test”, konsol akan mencetak:

```
Corrected text:
This is a simple test
```

Perhatikan bagaimana kata‑kata yang salah eja (`Ths`, `smple`) telah otomatis diperbaiki.

## Contoh Lengkap yang Siap‑Jalankan

Berikut seluruh program dalam satu blok. Salin‑tempel, sesuaikan jalur, dan tekan **Run**.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (replace with your license file)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Select the language for recognition (e.g., English)
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);

        // Enable the built‑in spell corrector and optionally set a custom dictionary
        engine.getSpellCorrector().setEnable(true);                     // activate spell‑checking
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english"); // optional

        // Prepare the input image containing the text to be recognized
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // load image for OCR

        // Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

**Tip:** Jika Anda ingin memproses JPEG atau BMP alih‑alih PNG, cukup ubah ekstensi file—Aspose OCR mendukung semua format raster umum.

## Pertanyaan Umum & Kasus Tepi

- **Bagaimana jika gambar saya beresolusi rendah?**  
  Tingkatkan DPI sebelum memberi ke Aspose dengan memperbesar menggunakan pustaka seperti `java.awt.Image`. DPI yang lebih tinggi memberi mesin lebih banyak piksel untuk diproses, yang biasanya meningkatkan akurasi.

- **Bisakah saya mengenali beberapa bahasa dalam satu gambar?**  
  Ya. Panggil `engine.getLanguage().setLanguage(OcrLanguage.MULTI_LANGUAGE);` dan opsional berikan daftar bahasa melalui `engine.getLanguage().addLanguage(OcrLanguage.SPANISH);`.

- **Kamus khusus saya tidak digunakan—kenapa?**  
  Pastikan folder berisi file teks biasa dengan satu kata per baris dan bahwa jalurnya absolut atau relatif dengan benar terhadap direktori kerja Anda.

- **Bagaimana cara mengekstrak skor kepercayaan?**  
  `result.getConfidence()` mengembalikan nilai float antara 0 dan 1 untuk seluruh halaman. Untuk kepercayaan per karakter, jelajahi `result.getWordList()`.

## Kesimpulan

Anda kini tahu cara **mengenali teks dari gambar** menggunakan Aspose OCR untuk Java, cara **memuat gambar untuk OCR**, dan cara mengaktifkan korektor ejaan untuk membersihkan typo umum. Contoh lengkap di atas siap dimasukkan ke dalam proyek Maven atau Gradle apa pun, dan dengan beberapa penyesuaian Anda dapat memperluasnya untuk memproses batch folder, menghubungkannya ke layanan web, atau mengintegrasikannya dengan sistem manajemen dokumen.

Siap untuk langkah selanjutnya? Coba proses PDF multi‑halaman, bereksperimen dengan kamus khusus untuk terminologi industri, atau sambungkan output ke API terjemahan. Kemungkinannya tak terbatas, dan pola inti—lisensi → mesin → bahasa → korektor ejaan → input → mengenali → output—tetap sama.

Selamat coding, semoga hasil OCR Anda selalu tepat sasaran!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}