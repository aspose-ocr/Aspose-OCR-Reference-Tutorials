---
category: general
date: 2026-01-12
description: Learn how to recognize text from images and extract text from png files
  using Aspose OCR in Java. Parallel processing makes it fast.
draft: false
keywords:
- recognize text from images
- extract text from png
language: id
og_description: Temukan cara termudah untuk mengenali teks dari gambar di Java dan
  mengekstrak teks dari file PNG menggunakan Aspose OCR dengan pemrosesan paralel.
og_title: Mengenali teks dari gambar dengan Java – Panduan OCR Paralel
tags:
- OCR
- Java
- Aspose
title: Mengenali teks dari gambar dengan Java – Tutorial OCR Paralel
url: /id/java/advanced-ocr-techniques/recognize-text-from-images-with-java-parallel-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar dengan Java – Tutorial OCR Paralel

Pernah membutuhkan untuk **mengenali teks dari gambar** tetapi merasa terhambat pada “bagaimana‑saya‑melakukannya?”? Anda bukan satu-satunya. Baik Anda sedang mendigitalkan faktur, mengambil data dari tangkapan layar, atau membangun arsip yang dapat dicari, kemampuan untuk *mengenali teks dari gambar* adalah pengubah permainan.  

Dalam panduan ini kami akan membahas contoh Java lengkap yang siap dijalankan yang tidak hanya **mengenali teks dari gambar** tetapi juga menunjukkan cara **mengekstrak teks dari png** menggunakan mesin paralel bawaan Aspose OCR. Tanpa skrip eksternal, tanpa bagian yang hilang—hanya kode yang sederhana dan penjelasan yang jelas.

## Apa yang Akan Anda Pelajari

- Menyiapkan Aspose OCR dalam proyek Java  
- Mengaktifkan pemrosesan paralel untuk mempercepat pekerjaan batch  
- Memuat kumpulan file PNG dan **mengekstrak teks dari png** secara efisien  
- Menangani jebakan umum (file besar, hasil kosong, batas thread)  
- Melihat kode sumber lengkap yang dapat dijalankan di akhir artikel  

Setelah selesai, Anda akan memiliki solusi salin‑tempel yang dapat Anda sesuaikan dengan alur kerja ekstraksi teks berbasis gambar apa pun.

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|----------------|
| Java 8 or newer | Aspose OCR’s Java API targets Java 8+ |
| Maven atau Gradle (untuk manajemen dependensi) | Mempermudah menambahkan pustaka Aspose OCR |
| Beberapa gambar PNG yang ingin Anda proses | Tutorial menggunakan `doc1.png`‑`doc4.png` sebagai contoh |
| Pengetahuan dasar tentang sintaks Java | Kode ini sederhana, tetapi Anda perlu mengompilasi dan menjalankannya |

Jika Anda belum memiliki salah satu dari ini, dapatkan JDK terbaru dari Oracle atau AdoptOpenJDK dan siapkan proyek Maven sederhana—tidak perlu yang rumit.

![recognize text from images diagram](image.png){alt="diagram mengenali teks dari gambar"}

## Langkah 1 – Tambahkan Aspose OCR ke Proyek Anda

Pertama, beri tahu Maven (atau Gradle) untuk mengambil pustaka Aspose OCR. Di file `pom.xml`, tambahkan:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Jika Anda lebih suka Gradle, setaraannya adalah:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Periksa [Aspose OCR Maven repository](https://repo.aspose.com/repo) untuk versi terbaru. Menjaga pustaka tetap terbaru memastikan Anda mendapatkan perbaikan OCR terbaru dan perbaikan bug.

## Langkah 2 – Aktifkan Pemrosesan Paralel (rahasia utama)

Aspose OCR dapat menyebarkan beban kerja ke beberapa inti CPU. Itulah cara kami menjaga operasi **mengenali teks dari gambar** tetap cepat, bahkan ketika Anda memiliki puluhan file PNG.

```java
// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Configure parallel options – up to 4 cores in this demo
ParallelOptions parallelOptions = new ParallelOptions();
parallelOptions.setMaxDegreeOfParallelism(4); // Adjust based on your machine
ocrEngine.setParallelOptions(parallelOptions);
```

Mengapa menetapkan batas? Mengalokasikan terlalu banyak thread dapat menghambat proses lain, terutama pada server bersama. Empat inti adalah default yang aman untuk kebanyakan desktop; tingkatkan jika Anda tahu perangkat keras Anda dapat menangani lebih banyak.

## Langkah 3 – Siapkan Daftar File PNG

Tutorial ini berfokus pada **mengekstrak teks dari png** file, tetapi kode yang sama bekerja untuk JPEG, BMP, dll. Letakkan gambar Anda dalam folder dan referensikan seperti ini:

```java
String[] imageFiles = {
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
};
```

> **Note:** Ganti `YOUR_DIRECTORY` dengan jalur absolut atau relatif tempat file PNG berada. Jika Anda perlu memproses folder dinamis, Anda dapat menggunakan `Files.list(Paths.get("YOUR_DIRECTORY"))` untuk membangun array secara otomatis.

## Langkah 4 – Jalankan OCR pada Setiap Gambar (mesin melakukan pekerjaan berat)

Meskipun kami mengaktifkan paralelisme, kami tetap melakukan loop pada array file. Aspose OCR secara internal mendistribusikan pekerjaan pengenalan ke thread yang kami konfigurasi.

```java
for (String imagePath : imageFiles) {
    // Load the image into the engine
    ocrEngine.setImage(imagePath);
    
    // Perform recognition
    OcrResult result = ocrEngine.recognize();
    
    // Guard against empty results
    String text = result.getText();
    if (text == null || text.isEmpty()) {
        System.out.println("[" + imagePath + "] => No text found.");
        continue;
    }
    
    // Print a short preview (first 50 characters)
    System.out.println("[" + imagePath + "] => " +
        text.substring(0, Math.min(50, text.length())) + "...");
}
```

### Mengapa loop dan bukan parallel stream?

Aspose OCR sudah membagi pemrosesan gambar secara internal berdasarkan `ParallelOptions`. Membungkus pemanggilan dalam parallel stream eksternal akan menggandakan pekerjaan dan bahkan dapat menurunkan kinerja. Percayakan pustaka untuk mengelola thread.

## Langkah 5 – Kasus Edge & Tips Praktis

| Situasi | Apa yang harus dilakukan |
|-----------|------------|
| **Huge PNG ( > 10 MB )** | Tingkatkan heap JVM (`-Xmx2g`) atau ubah ukuran gambar sebelum memasukkannya ke mesin. |
| **Mixed image formats** | Gunakan `ocrEngine.setImage(new File(imagePath))` – mesin secara otomatis mendeteksi format. |
| **Need the full text, not just a preview** | Simpan `result.getText()` dalam `StringBuilder` atau tulis ke file untuk analisis selanjutnya. |
| **Running on a CI server without a GUI** | Tidak ada langkah tambahan—Aspose OCR sepenuhnya headless. |
| **License expiration** | Daftarkan lisensi sementara dengan `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` untuk menghindari watermark evaluasi. |

## Contoh Lengkap yang Berfungsi

Berikut adalah kelas Java lengkap yang dapat Anda salin, tempel, dan jalankan. Ini mencakup semua bagian yang kami bahas, plus beberapa komentar untuk kejelasan.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.parallel.*;

public class ParallelOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing (up to 4 CPU cores)
        ParallelOptions parallelOptions = new ParallelOptions();
        parallelOptions.setMaxDegreeOfParallelism(4); // Adjust as needed
        ocrEngine.setParallelOptions(parallelOptions);

        // Step 3: Define the PNG files to be processed
        String[] imageFiles = {
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.png",
            "YOUR_DIRECTORY/doc3.png",
            "YOUR_DIRECTORY/doc4.png"
        };

        // Step 4: Recognize text from each image (engine handles parallelism internally)
        for (String imagePath : imageFiles) {
            // Load the image
            ocrEngine.setImage(imagePath);

            // Perform OCR
            OcrResult result = ocrEngine.recognize();

            // Extract the recognized text
            String text = result.getText();

            // Guard against empty results
            if (text == null || text.isEmpty()) {
                System.out.println("[" + imagePath + "] => No text found.");
                continue;
            }

            // Step 5: Output a short preview (first 50 characters)
            System.out.println("[" + imagePath + "] => " +
                text.substring(0, Math.min(50, text.length())) + "...");
        }
    }
}
```

### Output yang Diharapkan

Jika `doc1.png` berisi frasa “Invoice #12345 – Total $250.00”, Anda akan melihat sesuatu seperti:

```
[YOUR_DIRECTORY/doc1.png] => Invoice #12345 – Total $250.00...
[YOUR_DIRECTORY/doc2.png] => No text found.
[YOUR_DIRECTORY/doc3.png] => Customer Name: John Doe...
[YOUR_DIRECTORY/doc4.png] => ...
```

Pratinjau dipotong pada 50 karakter, tetapi string lengkap berada di dalam `result.getText()` untuk pemrosesan lanjutan apa pun yang Anda butuhkan.

## Kesimpulan

Anda kini memiliki pola yang solid dan siap produksi untuk **mengenali teks dari gambar** menggunakan Aspose OCR dalam Java, dan Anda telah melihat secara tepat cara **mengekstrak teks dari png** file dengan percepatan paralel. Langkah utama—penyiapan mesin, konfigurasi paralel, persiapan daftar gambar, dan penanganan hasil—semua telah dibahas, plus beberapa tips praktis untuk menghindari masalah umum.

Apa selanjutnya? Coba ganti daftar PNG dengan pemindaian direktori dinamis, alirkan output OCR ke indeks pencarian seperti Elasticsearch, atau bereksperimen dengan pengaturan OCR spesifik bahasa (`ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH)`). Langit adalah batasnya setelah Anda menguasai alur kerja inti.

Jika Anda menemukan kejanggalan atau memiliki ide untuk memperluas tutorial ini, tinggalkan komentar di bawah. Selamat coding, dan nikmati mengubah gambar yang membandel menjadi teks yang dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}