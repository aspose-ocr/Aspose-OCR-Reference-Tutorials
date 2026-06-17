---
category: general
date: 2026-05-06
description: Cara menggunakan OCR untuk mengekstrak teks dari gambar di Java. Pelajari
  konversi gambar ke teks dengan OCR, perbaiki kesalahan OCR, dan muat gambar untuk
  OCR dengan Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: id
og_description: Cara menggunakan OCR di Java untuk mengekstrak teks dari gambar, memperbaiki
  kesalahan OCR, dan memuat gambar untuk OCR menggunakan Aspose OCR.
og_title: Cara Menggunakan OCR di Java – Panduan Lengkap
tags:
- OCR
- Java
- Aspose
title: Cara Menggunakan OCR di Java – Mengekstrak Teks dari Gambar dengan Koreksi
  Ejaan
url: /id/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di Java – Ekstrak Teks dari Gambar dengan Koreksi Ejaan

Pernah bertanya‑tanya **bagaimana cara menggunakan OCR** untuk mengubah foto struk yang buram menjadi teks bersih yang dapat dicari? Anda tidak sendirian. Dalam banyak proyek—aplikasi pelacakan pengeluaran, pipeline digitalisasi faktur, atau bahkan skrip pencatatan cepat—mendapatkan teks yang dapat diandalkan dari sebuah gambar adalah rintangan pertama.  

Tutorial ini menunjukkan secara tepat cara menggunakan OCR di Java, mencakup semua hal mulai dari memuat gambar untuk OCR hingga memperbaiki kesalahan OCR sehingga hasilnya terbaca seperti ditulis manusia. Pada akhir tutorial, Anda akan dapat **mengekstrak teks dari gambar**, melakukan konversi **OCR image to text**, dan memperbaiki kesalahan pengenalan umum secara otomatis.

## Apa yang Akan Anda Bangun

Kami akan membuat program konsol Java kecil yang:

1. Memuat file PNG (atau format lain yang didukung) ke dalam mesin Aspose OCR.  
2. Mengaktifkan fitur koreksi ejaan bawaan untuk **memperbaiki kesalahan OCR**.  
3. Menjalankan proses pengenalan dan mencetak teks yang telah dibersihkan.  

Tanpa layanan eksternal, tanpa kerangka kerja berat—hanya satu JAR dan beberapa baris kode.

### Prasyarat

- Java Development Kit (JDK) 8 atau yang lebih baru.  
- Maven (atau alat build lain) untuk mengambil pustaka Aspose OCR.  
- Sebuah file gambar (misalnya `receipt.png`) yang ingin Anda analisis.  

Jika Anda belum memiliki JAR Aspose OCR, tambahkan dependensi ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Tips pro:** Versi evaluasi gratis cukup untuk pengujian, tetapi lisensi akan menghilangkan watermark evaluasi.

## Langkah 1 – Inisialisasi OCR Engine (Kata Kunci Utama dalam Aksi)

Hal pertama yang harus Anda lakukan adalah membuat instance `OcrEngine`. Anggap saja ini sebagai otak yang akan membaca piksel dan mengubahnya menjadi karakter.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Mengapa ini penting:* Inisialisasi engine menyiapkan sumber daya internal (model bahasa, kamus, dll.). Melewatkan langkah ini akan menyebabkan `NullPointerException` nanti saat Anda mencoba memuat gambar.

## Langkah 2 – Muat Gambar untuk OCR

Sekarang kita benar‑benar **memuat gambar untuk OCR**. Aspose menyediakan helper `ImageStream.fromFile` yang praktis, tetapi Anda juga dapat memberi `byte[]` jika lebih suka.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Jebakan umum:* Path file harus absolut atau relatif terhadap direktori kerja. Jika gambar tidak dapat ditemukan, engine akan melempar `IOException`. Periksa kembali path, terutama saat menjalankan dari IDE dibandingkan dengan JAR yang sudah dipaketkan.

## Langkah 3 – Aktifkan Spell Correction untuk **Memperbaiki Kesalahan OCR**

OCR bawaan dapat berisik—bayangkan “l0ve” alih‑alih “love” atau “0” untuk “O”. Mengaktifkan spell correction memberi tahu engine untuk menjalankan proses pasca‑pemrosesan yang memperbaiki kesalahan tipikal.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Mengapa Anda menginginkannya:* Tanpa koreksi ejaan, Anda mungkin harus membersihkan output secara manual, yang menghilangkan tujuan otomatisasi. Kamus bawaan bekerja baik untuk bahasa Inggris dan beberapa bahasa lain.

## Langkah 4 – Lakukan Pengenalan (**OCR Image to Text**)

Dengan gambar yang sudah dimuat dan spell correction diaktifkan, kita akhirnya dapat meminta engine mengenali teks.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Kasus tepi:* Jika gambar berkontras rendah atau sangat miring, hasilnya masih mungkin berisi sampah. Pertimbangkan pra‑pemrosesan (misalnya binarisasi, deskew) sebelum memberikannya ke engine.

## Langkah 5 – Keluarkan Teks yang Telah Dibersihkan

Langkah terakhir cukup mencetak hasilnya. Dalam aplikasi nyata Anda mungkin menulisnya ke basis data atau file, tetapi untuk demo ini `System.out` sudah cukup.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Output yang Diharapkan

Misalkan `receipt.png` berisi daftar item yang jelas, Anda mungkin melihat sesuatu seperti:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Perhatikan bagaimana “Qty” dan “Price” dieja dengan benar meskipun pemindaian asli memiliki “Qy” yang menyimpang.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke file bernama `SpellCorrectDemo.java`. Pastikan JAR Aspose OCR berada di classpath Anda.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Jalankan dengan:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Sekarang Anda seharusnya melihat teks yang telah dibersihkan tercetak di konsol.

## Bonus: Menyetel Pengaturan untuk Akurasi Lebih Baik

Meskipun konfigurasi default bekerja untuk kebanyakan dokumen cetak, Anda mungkin perlu menyesuaikan beberapa parameter untuk skenario khusus:

| Pengaturan | Fungsinya | Kapan Diubah |
|------------|-----------|--------------|
| `setLanguage(OcrLanguage.English)` | Memaksa kamus bahasa Inggris (mengurangi false positive) | Jika gambar hanya berisi teks bahasa Inggris. |
| `setResolution(300)` | Menentukan DPI gambar sumber | Untuk pemindaian beresolusi tinggi. |
| `setEnableAutoSkewCorrection(true)` | Memutar otomatis halaman yang sedikit miring | Ketika gambar diambil dengan ponsel. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja dengan PDF?**  
J: Ya. Konversi setiap halaman PDF menjadi gambar (misalnya dengan Aspose PDF) dan berikan gambar tersebut ke OCR engine.

**T: Bagaimana jika gambar saya berformat BMP?**  
J: `ImageStream.fromFile` mendukung PNG, JPEG, BMP, TIFF, dan GIF secara bawaan. Cukup ubah ekstensi file.

**T: Bisakah saya menonaktifkan spell correction?**  
J: Tentu—set `setEnableSpellCorrection(false)` jika Anda memerlukan output OCR mentah untuk pemrosesan lanjutan.

## Kesimpulan

Anda kini tahu **cara menggunakan OCR** di Java untuk **mengekstrak teks dari gambar**, secara otomatis **memperbaiki kesalahan OCR**, dan dengan tepat **memuat gambar untuk OCR** menggunakan Aspose OCR. Alur lima langkah—inisialisasi, muat, aktifkan spell correction, kenali, dan keluarkan—mencakup mayoritas tugas OCR sehari‑hari.  

Selanjutnya, pertimbangkan menghubungkan logika ini dengan penulisan kembali ke basis data, endpoint REST, atau proses batch untuk menangani puluhan struk sekaligus. Bereksperimenlah dengan tabel pengaturan tambahan di atas untuk memaksimalkan akurasi hingga karakter terakhir.

Selamat coding, semoga hasil OCR Anda selalu lebih bersih daripada struk yang ternoda kopi! 

![diagram cara menggunakan ocr menunjukkan alur gambar → mesin OCR → teks yang dikoreksi flow]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}