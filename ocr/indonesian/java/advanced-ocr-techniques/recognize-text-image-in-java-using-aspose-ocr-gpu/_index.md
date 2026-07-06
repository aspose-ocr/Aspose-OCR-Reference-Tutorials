---
category: general
date: 2026-06-16
description: Mengenali gambar teks dengan cepat menggunakan Aspose OCR di Java. Pelajari
  cara mengatur perangkat GPU, mengekstrak teks JPG, dan membaca gambar teks menggunakan
  percepatan GPU.
draft: false
keywords:
- recognize text image
- set gpu device
- extract text jpg
- how to recognize text
- read text picture
language: id
og_description: Mengenali gambar teks dengan Aspose OCR di Java. Panduan ini menunjukkan
  cara mengatur perangkat GPU, mengekstrak teks JPG, dan membaca gambar teks secara
  efisien.
og_title: Mengenali teks pada gambar di Java menggunakan Aspose OCR + GPU
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text image quickly with Aspose OCR in Java. Learn how to
    set gpu device, extract text jpg, and read text picture using GPU acceleration.
  headline: recognize text image in Java using Aspose OCR + GPU
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- GPU
title: Mengenali gambar teks di Java menggunakan Aspose OCR + GPU
url: /id/java/advanced-ocr-techniques/recognize-text-image-in-java-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali gambar teks dalam Java menggunakan Aspose OCR + GPU

Pernah bertanya-tanya bagaimana cara mengenali gambar teks dalam aplikasi Java tanpa membuat CPU Anda melambat? Anda tidak sendirian—para pengembang terus mengejar pipeline OCR yang lebih cepat dan lebih andal. Dalam tutorial ini kami akan membahas solusi lengkap yang dipercepat oleh GPU yang memungkinkan Anda mengekstrak teks dari gambar JPG dalam sekejap.

Kami akan mulai dengan menyiapkan Aspose OCR, kemudian mengaktifkan percepatan GPU, dan akhirnya menunjukkan cara membaca file gambar teks, mencetak hasilnya, serta menangani gangguan sesekali. Pada akhir tutorial Anda akan tahu **cara mengenali teks** pada gambar apa pun, baik itu faktur yang dipindai maupun screenshot kasual.

## Apa yang Anda Butuhkan

- **Java 17** (atau JDK terbaru) – kode ini berjalan pada semua runtime modern.  
- **Aspose.OCR for Java** – tersedia melalui Maven Central.  
- **GPU** dengan dukungan CUDA (opsional tetapi sangat disarankan untuk kecepatan).  
- Sebuah gambar JPEG contoh (misalnya `sample.jpg`) yang ingin Anda proses.  

Tidak ada pustaka pihak ketiga lain yang diperlukan; semua hal lain sudah termasuk dalam Aspose OCR.

## Langkah 1: Tambahkan Aspose OCR ke Proyek Anda

Jika Anda menggunakan Maven, letakkan dependensi berikut ke dalam `pom.xml` Anda. Pengguna Gradle dapat menyalin baris `implementation` yang setara.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **Pro tip:** Versi evaluasi gratis menambahkan watermark kecil. Untuk produksi, dapatkan lisensi dari portal Aspose dan panggil `License license = new License(); license.setLicense("Aspose.OCR.lic");` sebelum melakukan pekerjaan OCR apa pun.

## Langkah 2: Muat Gambar yang Ingin Diproses

Hal pertama yang Anda lakukan ketika ingin **mengenali gambar teks** adalah memberi gambar ke mesin OCR. Aspose menyediakan pembungkus `ImageStream` yang dapat membaca dari path file, `InputStream`, atau bahkan byte array.

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Load the image – replace the path with your own picture
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Perhatikan bagaimana kami menjaga kode tetap minimal; pemanggilan `setImage` menerima format raster apa pun yang didukung Aspose, termasuk JPEG, PNG, dan BMP.

## Langkah 3: Aktifkan Percepatan GPU (set gpu device)

Sekarang bagian yang membuat panduan ini menonjol: kami akan **set gpu device** agar mesin OCR berjalan di kartu grafis alih-alih CPU. Ini dapat mengurangi beberapa detik dari waktu pemrosesan, terutama untuk gambar beresolusi tinggi.

```java
        // Enable GPU acceleration – this is where the magic happens
        engine.getRecognitionSettings().setUseGpu(true);

        // Optional: pick a specific GPU if you have more than one
        // engine.getRecognitionSettings().setGpuDeviceId(0);
```

Jika Anda memiliki beberapa GPU, hapus komentar pada baris `setGpuDeviceId` dan ganti `0` dengan indeks perangkat yang Anda inginkan. Aspose secara otomatis akan kembali ke CPU jika tidak ada GPU yang kompatibel, jadi Anda tidak perlu khawatir tentang crash.

## Langkah 4: Lakukan OCR – cara mengenali teks

Dengan gambar yang sudah dimuat dan GPU diaktifkan, kita akhirnya dapat **cara mengenali teks** pada gambar. Metode `recognize()` menjalankan seluruh pipeline—pra‑pemrosesan, segmentasi, klasifikasi karakter, dan pasca‑pemrosesan.

```java
        // Execute the OCR process
        OcrResult result = engine.recognize();
```

Objek `OcrResult` yang dikembalikan berisi string mentah, skor kepercayaan, dan bahkan bounding box jika Anda memerlukan informasi tata letak nanti.

## Langkah 5: Keluarkan Teks yang Dikenali – extract text jpg / read text picture

Mari **extract text jpg** dan **read text picture** dengan cukup mencetak hasilnya ke konsol. Dalam aplikasi dunia nyata Anda mungkin akan menulisnya ke basis data atau file.

```java
        // Show the recognized text in the console
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
Recognized text:
Invoice #12345
Date: 2026-06-15
Total: $1,250.00
```

Jika gambar mengandung noise, Anda dapat menyesuaikan pengaturan pra‑pemrosesan Aspose (kontras, binarisasi, dll.)—tetapi default sudah cukup untuk kebanyakan file JPG yang bersih.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut adalah kelas lengkap yang siap dijalankan:

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the image to be processed
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 2: Enable GPU acceleration for faster recognition
        engine.getRecognitionSettings().setUseGpu(true);
        // Optional: specify a GPU device index if multiple GPUs are present
        // engine.getRecognitionSettings().setGpuDeviceId(0);

        // Step 3: Perform OCR on the loaded image
        OcrResult result = engine.recognize();

        // Step 4: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

> **Expected output:** Konsol mencetak teks persis yang muncul di `sample.jpg`. Jika gambar tersebut adalah foto struk, Anda akan melihat setiap baris sebagai string terpisah, mempertahankan jeda baris.

## Kasus Pinggir & Kesalahan Umum

| Situasi | Hal yang Perlu Diperhatikan | Solusi yang Disarankan |
|-----------|-------------------|---------------|
| **Multiple GPUs** | GPU default mungkin bukan yang paling kuat. | Gunakan `setGpuDeviceId` untuk menargetkan kartu berperforma tinggi. |
| **Out‑of‑memory pada gambar besar** | JPG beresolusi sangat tinggi dapat menghabiskan memori GPU. | Turunkan skala gambar terlebih dahulu (`engine.getPreprocessingSettings().setResizeFactor(0.5)`). |
| **Kepercayaan rendah** | Beberapa karakter dapat salah dibaca jika gambar blur. | Aktifkan `engine.getRecognitionSettings().setUseLanguageModel(true)` untuk koreksi berbasis konteks. |
| **Format gambar tidak didukung** | Aspose OCR mendukung banyak format, tetapi tidak data sensor RAW. | Konversi file ke JPEG atau PNG sebelum memberi ke mesin. |

Menangani skenario ini memastikan alur kerja **mengenali gambar teks** Anda tetap kuat di berbagai lingkungan.

## Pro Tips untuk OCR yang Lebih Cepat dan Bersih

- **Pemrosesan batch:** Gunakan satu instance `OcrEngine` untuk banyak gambar; konteks GPU tetap hidup, menghemat overhead inisialisasi.  
- **Keamanan thread:** Setiap thread harus memiliki objek `OcrEngine` masing‑masing; kelas ini tidak thread‑safe.  
- **Lisensi lebih awal:** Muat lisensi Aspose saat aplikasi mulai untuk menghindari watermark evaluasi.  
- **Logging:** Aktifkan `engine.getLogSettings().setEnableLogging(true)` jika Anda perlu men-debug mengapa gambar tertentu gagal.

## Kesimpulan

Kami baru saja menunjukkan cara **mengenali gambar teks** dalam Java menggunakan Aspose OCR dengan percepatan GPU. Dengan mengikuti langkah‑langkah—menambahkan pustaka, memuat JPEG, **set gpu device**, menjalankan mesin OCR, dan akhirnya **extract text jpg** atau **read text picture**—Anda dapat mengubah

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}