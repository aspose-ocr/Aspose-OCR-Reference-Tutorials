---
category: general
date: 2026-05-31
description: Muat gambar untuk OCR menggunakan perpustakaan Aspose OCR Java – panduan
  langkah demi langkah dengan koreksi ejaan, pengaturan bahasa, dan tiga saran teratas.
draft: false
keywords:
- load image for OCR
- Aspose OCR Java
- spell correction OCR
- OCR engine Java
- set OCR language
- max suggestions OCR
language: id
og_description: Muat gambar untuk OCR di Java dengan Aspose OCR. Pelajari cara mengaktifkan
  koreksi ejaan, mengatur bahasa, dan membatasi saran hingga tiga teratas.
og_title: Muat Gambar untuk OCR dengan Aspose OCR Java – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Load image for OCR using Aspose OCR Java library – step‑by‑step guide
    with spell correction, language settings, and top‑3 suggestions.
  headline: Load Image for OCR with Aspose OCR Java – Complete Guide
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Muat Gambar untuk OCR dengan Aspose OCR Java – Panduan Lengkap
url: /id/java/ocr-operations/load-image-for-ocr-with-aspose-ocr-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memuat Gambar untuk OCR dengan Aspose OCR Java – Panduan Lengkap

Perlu **memuat gambar untuk OCR** dalam aplikasi Java? Anda bukan satu‑satunya yang kebingungan tentang hal itu. Untungnya, Aspose OCR untuk Java membuat seluruh proses hampir tanpa rasa sakit, terutama ketika Anda menambahkan koreksi ejaan.

Dalam tutorial ini kami akan membahas setiap baris yang Anda perlukan untuk menempatkan gambar teks yang salah eja ke mesin OCR, mengaktifkan **spell correction**, membatasi saran ke tiga teratas, dan akhirnya mencetak hasil yang telah diperbaiki. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan dan dapat dimasukkan ke proyek apa pun.

## Apa yang Akan Anda Pelajari

- Cara menerapkan lisensi **Aspose OCR Java** Anda sehingga perpustakaan berfungsi tanpa watermark.  
- Cara tepat untuk **memuat gambar untuk OCR** menggunakan `OcrImage`.  
- Mengatur bahasa OCR (ya, Anda dapat beralih dari bahasa Inggris ke Prancis dalam sekejap).  
- Mengaktifkan **spell correction OCR** dan mengonfigurasi batas `max suggestions`.  
- Menjalankan mesin dan mengambil teks bersih yang telah dikoreksi.  

Tidak diperlukan pengalaman sebelumnya dengan Aspose, hanya IDE yang kompatibel dengan Java dan file gambar kecil. Mari kita mulai.

![Diagram yang menunjukkan alur memuat gambar untuk OCR, menerapkan koreksi ejaan, dan mengambil teks](load-image-ocr.png "diagram memuat gambar untuk OCR")

## Langkah 1 – Memuat Gambar untuk OCR

Hal pertama yang harus Anda lakukan adalah mengarahkan mesin ke gambar yang berisi teks yang ingin Anda baca. Di Aspose ini hanya satu baris:

```java
// Step 1: Load the image that contains misspelled text
engine.setImage(new OcrImage("YOUR_DIRECTORY/misspelled.png"));
```

`OcrImage` menerima jalur file, aliran, atau bahkan `BufferedImage`. Jika gambar Anda berada di classpath, Anda dapat menggunakan `getResourceAsStream` sebagai gantinya—sangat cocok untuk unit test.  

> **Pro tip:** Simpan file gambar Anda di bawah 2 MB; file yang lebih besar secara dramatis meningkatkan penggunaan memori dan dapat memperlambat mesin OCR.

## Langkah 2 – Inisialisasi Lisensi Aspose OCR

Sebelum mesin melakukan apa pun yang berguna, Anda memerlukan lisensi yang valid; jika tidak, Anda akan mendapatkan output ber‑watermark dan peringatan di konsol.

```java
// Step 2: Apply your Aspose OCR license
License license = new License();
license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

Jika Anda belum memiliki lisensi, Anda dapat meminta lisensi sementara gratis dari portal Aspose. Cukup letakkan file `.lic` di tempat aplikasi Anda dapat membacanya, dan Anda siap melanjutkan.

## Langkah 3 – Mengonfigurasi Mesin OCR dan Bahasa

Mesin OCR tanpa pengaturan bahasa seperti GPS tanpa peta—hilang arah. Untuk bahasa Inggris kita lakukan:

```java
// Step 3: Create an OCR engine and set the language to English
OcrEngine engine = new OcrEngine();
engine.setLanguage(OcrLanguage.ENGLISH);
```

Berpindah bahasa semudah mengganti `OcrLanguage.ENGLISH` dengan `OcrLanguage.FRENCH`, `OcrLanguage.SPANISH`, dll. Perpustakaan ini dilengkapi dengan puluhan paket bahasa bawaan.

## Langkah 4 – Mengaktifkan Spell Correction dan Menetapkan Max Suggestions

Sekarang datanglah keajaiban yang membuat demo kami berbeda dari OCR biasa: **spell correction OCR**. Secara default fitur ini mati, tetapi mengaktifkannya dan membatasi saran menjadi tiga memberikan output yang rapi dan mudah dibaca.

```java
// Step 4: Enable spell correction and limit suggestions to the top 3
engine.getSpellCorrector().setEnabled(true);
engine.getSpellCorrector().setMaxSuggestions(3);
```

Parameter `max suggestions` mengontrol berapa banyak kata alternatif yang akan diusulkan mesin untuk setiap token yang salah eja. Menjaganya rendah mengurangi kebisingan, terutama ketika gambar sumber buram.

## Langkah 5 – Menjalankan OCR dan Mengambil Teks yang Diperbaiki

Dengan semua pengaturan terhubung, pengenalan sebenarnya cukup dengan satu pemanggilan metode. Mesin mengembalikan `String` yang sudah berisi teks yang telah diperbaiki.

```java
// Step 5: Perform OCR and obtain the corrected text
String correctedText = engine.recognize();
```

Di balik layar, Aspose menjalankan classifier berbasis jaringan saraf, kemudian mengalirkan hasil mentah melalui korektor ejaan. Seluruh pipeline selesai dalam beberapa milidetik untuk gambar berukuran tipikal 300 × 200 px.

## Langkah 6 – Mengeluarkan Hasil yang Diperbaiki

Akhirnya, cukup cetak string—atau kirim ke tempat lain, seperti basis data atau respons REST.

```java
// Step 6: Output the corrected result
System.out.println(correctedText);
```

### Output yang Diharapkan

Jika `misspelled.png` berisi frasa “Ths is a smple test”, konsol akan menampilkan:

```
This is a simple test
```

Perhatikan bagaimana kata yang salah eja “Ths” dan “smple” secara otomatis diperbaiki, dan hanya tiga saran terbaik yang dipertimbangkan.

## Kesalahan Umum dan Tips

| Masalah | Mengapa Terjadi | Cara Memperbaiki |
|------|----------------|------------|
| **Output kosong** | Lisensi tidak dimuat atau jalur gambar salah. | Verifikasi jalur file `.lic` dan pastikan `misspelled.png` ada. |
| **Karakter sampah** | DPI gambar terlalu rendah (di bawah 70). | Gunakan sumber dengan resolusi lebih tinggi atau tingkatkan ukuran dengan `ImageMagick`. |
| **Terlalu banyak saran** | `setMaxSuggestions` dibiarkan pada nilai default (0 = tak terbatas). | Panggil secara eksplisit `setMaxSuggestions(3)` seperti yang ditunjukkan. |
| **Bahasa salah** | `setLanguage` tidak dipanggil atau enum salah. | Periksa kembali nilai enum `OcrLanguage` sesuai dengan teks Anda. |

### Tips Pro: Pemrosesan Batch

Jika Anda perlu OCR puluhan file, bungkus langkah 1‑5 dalam sebuah loop dan gunakan kembali instance `OcrEngine` yang sama. Menggunakan kembali mesin menghemat memori karena jaringan saraf internal hanya dimuat sekali.

```java
OcrEngine engine = new OcrEngine();
engine.setLanguage(OcrLanguage.ENGLISH);
engine.getSpellCorrector().setEnabled(true);
engine.getSpellCorrector().setMaxSuggestions(3);

for (String path : imagePaths) {
    engine.setImage(new OcrImage(path));
    System.out.println(engine.recognize());
}
```

## Ringkasan

Kami telah membahas semua yang Anda perlukan untuk **memuat gambar untuk OCR** dengan Aspose OCR Java, mulai dari lisensi dan pemilihan bahasa hingga mengaktifkan **spell correction OCR** dan membatasi output ke tiga alternatif teratas. Program lengkap yang dapat dijalankan hanya terdiri dari beberapa baris, namun memiliki kekuatan besar.

Apa selanjutnya? Coba ganti `OcrLanguage.ENGLISH` dengan bahasa lain, bereksperimen dengan format gambar berbeda (`.tif`, `.bmp`), atau hubungkan hasilnya ke generator PDF. Kemungkinannya tak terbatas, dan pola yang sama—lisensi → mesin → gambar → pengaturan → mengenali—berlaku untuk setiap skenario.

Selamat coding, dan semoga hasil OCR Anda selalu jernih!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Ekstrak Teks dari Gambar Java dengan Mode Deteksi Area Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Konversi Gambar ke Teks di Java menggunakan Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}