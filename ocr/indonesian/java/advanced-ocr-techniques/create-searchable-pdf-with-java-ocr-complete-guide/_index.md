---
category: general
date: 2026-05-25
description: Buat PDF yang dapat dicari dalam Java menggunakan Aspose OCR. Pelajari
  cara mengonversi PDF menjadi PDF yang dapat dicari, memuat PDF untuk OCR, dan mempercepat
  dengan GPU.
draft: false
keywords:
- create searchable pdf
- convert pdf to searchable pdf
- load pdf for ocr
- ocr pdf with gpu
language: id
og_description: Buat PDF yang dapat dicari di Java menggunakan Aspose OCR. Tutorial
  ini menunjukkan cara mengonversi PDF menjadi PDF yang dapat dicari, memuat PDF untuk
  OCR, dan menggunakan percepatan GPU.
og_title: Buat PDF yang Dapat Dicari dengan Java OCR – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  headline: Create Searchable PDF with Java OCR – Complete Guide
  type: TechArticle
- description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  name: Create Searchable PDF with Java OCR – Complete Guide
  steps:
  - name: Runs OCR on each page image.
    text: Runs OCR on each page image.
  - name: Generates an invisible text layer that matches the visual content.
    text: Generates an invisible text layer that matches the visual content.
  - name: Embeds that layer into a new PDF, preserving the original appearance.
    text: Embeds that layer into a new PDF, preserving the original appearance.
  type: HowTo
tags:
- OCR
- Java
- PDF
- Aspose
title: Buat PDF yang Dapat Dicari dengan Java OCR – Panduan Lengkap
url: /id/java/advanced-ocr-techniques/create-searchable-pdf-with-java-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dengan Java OCR – Panduan Lengkap

Pernah membutuhkan untuk **create searchable PDF** file dari dokumen yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Banyak pengembang mengalami hal yang sama ketika mencoba mengubah PDF yang hanya berisi gambar menjadi aset yang dapat dicari teks, terutama ketika kinerja menjadi penting.

Dalam tutorial ini kami akan membahas solusi praktis yang **creates searchable PDF** file menggunakan Aspose OCR untuk Java. Kami juga akan menunjukkan cara **convert PDF to searchable PDF**, **load PDF for OCR**, dan bahkan **OCR PDF with GPU** acceleration—semua dalam satu skrip yang mudah dibaca. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan dan pemahaman yang jelas mengapa setiap langkah penting.

> **Apa yang akan Anda dapatkan**  
> * Proyek Java lengkap yang membaca PDF berbahasa campuran  
> * OCR dengan GPU yang mempercepat pemrosesan pada perangkat keras modern  
> * Output PDF yang dapat dicari yang dapat Anda masukkan ke dalam sistem manajemen dokumen apa pun  

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* Java 17 (atau lebih baru) terpasang – versi lama mungkin tidak memiliki API yang diperlukan.  
* Maven atau Gradle untuk manajemen dependensi – kami akan menggunakan Maven dalam contoh.  
* Lisensi Aspose OCR untuk Java (versi percobaan gratis dapat digunakan untuk pengujian).  
* File PDF yang berisi halaman yang dipindai (demo menggunakan `mixed_lang.pdf`).  

Jika ada yang tidak familiar, jangan panik – langkah-langkah di bawah ini mencakup perintah tepat untuk memulai.

![Buat PDF yang dapat dicari menggunakan Aspose OCR Java](https://example.com/images/create-searchable-pdf.png "Buat PDF yang dapat dicari menggunakan Aspose OCR Java")

## Langkah 1: Siapkan Proyek dan **Create Searchable PDF** – Inisialisasi Proyek

Pertama, buat proyek Maven. Buka terminal dan jalankan:

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=SearchablePdfDemo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

Masuk ke dalam folder:

```bash
cd SearchablePdfDemo
```

Tambahkan dependensi Aspose OCR ke `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- check Maven Central for the latest -->
    </dependency>
</dependencies>
```

> **Mengapa ini penting:** Proses **create searchable pdf** bergantung pada kelas `OcrEngine`, yang berada di dalam pustaka Aspose OCR. Tanpa versi yang tepat Anda akan mendapatkan kesalahan kompilasi atau fitur yang hilang.

Sekarang buat kelas Java utama `QuickDemo.java` di bawah `src/main/java/com/example/ocr/`.

## Langkah 2: Aktifkan Akselerasi GPU – **OCR PDF with GPU**

Akselerasi GPU dapat mengurangi menit pada pekerjaan OCR multi‑halaman. Aspose OCR memungkinkan Anda mengaktifkannya dengan satu baris kode:

```java
// Enable GPU processing
engine.getEngineOptions().setUseGpu(true);
```

Jika mesin Anda memiliki GPU NVIDIA atau AMD yang kompatibel dan driver yang tepat terpasang, mesin OCR akan memindahkan beban kerja berat ke kartu grafis. Jika tidak, panggilan tersebut akan kembali ke pemrosesan CPU secara aman—tidak ada crash, hanya proses yang lebih lambat.

> **Tips pro:** Di Linux, Anda mungkin perlu mengatur `LD_LIBRARY_PATH` untuk menunjuk ke pustaka CUDA sebelum meluncurkan JVM.

## Langkah 3: **Load PDF for OCR** dan Konfigurasikan Dukungan Bahasa

Sekarang kita benar‑benarnya **load pdf for ocr**. Aspose OCR memperlakukan halaman PDF sebagai gambar secara internal, jadi Anda cukup mengarahkan mesin ke file:

```java
// Load the source PDF document (image‑only PDF)
engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");
```

Selanjutnya, beri tahu mesin bahasa apa yang Anda harapkan. Dalam demo kami kami fokus pada Thai, tetapi Anda dapat mengirimkan array bahasa jika dokumen mencampur skrip:

```java
engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
```

Jika Anda memiliki kamus khusus (misalnya, istilah domain‑spesifik), sambungkan ke dalamnya:

```java
engine.getEngineOptions().getSpellCorrectorOptions()
      .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");
```

> **Mengapa mengatur bahasa?** Akurasi OCR bergantung pada model bahasa. Menyediakan `OcrLanguage` yang tepat mengurangi kesalahan pengenalan secara dramatis, terutama untuk skrip non‑Latin.

## Langkah 4: **Convert PDF to Searchable PDF** dalam Satu Panggilan

Aspose OCR unggul karena dapat **convert PDF to searchable PDF** dengan satu pemanggilan metode—tidak perlu menyatukan gambar dan lapisan teks secara manual.

```java
// Export a searchable PDF in a single operation
engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");
```

Di balik layar, mesin:

1. Menjalankan OCR pada setiap gambar halaman.  
2. Menghasilkan lapisan teks tak terlihat yang cocok dengan konten visual.  
3. Menyematkan lapisan tersebut ke dalam PDF baru, mempertahankan tampilan asli.

Hasilnya adalah file yang tampak identik dengan input tetapi dapat diindeks oleh penampil PDF apa pun.

## Langkah 5: Ambil Teks yang Diakui dan Verifikasi Output

Meskipun kami sudah menyimpan PDF yang dapat dicari, Anda mungkin juga menginginkan teks mentah untuk pencatatan atau pemrosesan lebih lanjut:

```java
// Output the recognized text to the console
System.out.println(engine.recognize().getText());
```

Saat Anda menjalankan program, Anda akan melihat teks Thai yang diekstrak dicetak di konsol, diikuti oleh `mixed_lang_searchable.pdf` yang baru dibuat di direktori Anda.

### Output Konsol yang Diharapkan (dipotong)

```
สวัสดีครับ นี่คือเอกสารตัวอย่าง...
...
```

Buka PDF yang dihasilkan di Adobe Reader atau penampil apa pun, tekan **Ctrl + F**, dan Anda akan dapat mencari kata-kata yang baru saja Anda lihat di konsol. Itu bukti bahwa kami berhasil **create searchable pdf** file.

## Langkah 6: Kesalahan Umum dan **Pro Tips** untuk OCR Berkinerja Tinggi

| Issue | Symptom | Fix |
|-------|----------|-----|
| **GPU tidak terdeteksi** | Tidak ada peningkatan kecepatan, mesin kembali ke CPU | Pastikan driver CUDA terpasang dan `java.library.path` mencakup pustaka GPU. |
| **Font hilang** | Lapisan teks menampilkan karakter yang rusak | Instal font bahasa yang sesuai pada OS host atau sematkan melalui `engine.getEngineOptions().setEmbedFonts(true)`. |
| **PDF besar (> 500 halaman)** | Kesalahan kehabisan memori | Tingkatkan heap JVM (`-Xmx4g`) dan atur `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors())` untuk menyebarkan pekerjaan ke seluruh core. |
| **Kamus khusus tidak diterapkan** | Pengoreksi ejaan tampaknya diabaikan | Verifikasi bahwa path bersifat absolut dan file menggunakan encoding UTF-8. |

> **Ingat:** Baris `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());` sangat penting ketika Anda ingin **ocr pdf with gpu** *dan* memanfaatkan CPU multi‑core sepenuhnya. Baris ini memberi tahu mesin untuk membuat pekerja per core, menjaga GPU tetap sibuk sementara CPU menangani pra‑ dan pasca‑pemrosesan.

## Contoh Lengkap yang Berfungsi

Berikut adalah program Java lengkap yang siap dijalankan yang menggabungkan setiap langkah yang kami bahas. Ganti path placeholder dengan direktori Anda sendiri.

```java
import com.aspose.ocr.*;

public class QuickDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Enable GPU acceleration and use all available CPU cores
        engine.getEngineOptions().setUseGpu(true);
        engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 3: Configure language support and a custom spell‑corrector dictionary
        engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
        engine.getEngineOptions().getSpellCorrectorOptions()
              .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");

        // Step 4: Load the source PDF document (this is where we **load pdf for ocr**)
        engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");

        // Step 5: Export a searchable PDF in a single operation (**convert pdf to searchable pdf**)
        engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");

        // Step 6: Output the recognized text to the console
        System.out.println(engine.recognize().getText());
    }
}
```

Kompilasi dan jalankan:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.QuickDemo"
```

Jika semuanya terhubung dengan benar, Anda akan melihat teks yang diekstrak dicetak dan PDF yang dapat dicari baru di samping file asli.

## Kesimpulan

Kami baru saja mendemonstrasikan cara **create searchable pdf** file di Java menggunakan Aspose OCR, mencakup semua mulai dari penyiapan proyek hingga pemrosesan dengan akselerasi GPU. Dengan **loading pdf for OCR**, mengonfigurasi dukungan bahasa, dan memanggil metode satu‑baris **convert pdf to searchable pdf**, Anda mendapatkan dokumen yang sepenuhnya terindeks siap untuk mesin pencari atau sistem pengambilan internal.

Apa selanjutnya? Coba ganti `OcrLanguage.THAI` dengan `OcrLanguage.ENGLISH` atau gabungkan beberapa bahasa untuk PDF multibahasa. Bereksperimenlah dengan pengaturan `engine.getEngineOptions().setResolution(300)` untuk melihat bagaimana DPI memengaruhi akurasi, atau sematkan font khusus untuk rendering yang lebih baik pada penampil lama.

Ada pertanyaan tentang penyetelan kinerja, lisensi, atau mengintegrasikan alur kerja ini ke dalam layanan Spring Boot? Tinggalkan komentar di bawah atau periksa dokumentasi Aspose OCR Java untuk penjelasan lebih mendalam. Selamat coding, dan nikmati mengubah pemindaian statis menjadi harta karun yang dapat dicari!

## Tutorial Terkait

- [Mengenali Teks PDF – Operasi OCR dengan Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/)
- [OCR Mengenali Dokumen PDF dalam Aspose.OCR untuk Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Cara OCR PDF di .NET dengan Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}