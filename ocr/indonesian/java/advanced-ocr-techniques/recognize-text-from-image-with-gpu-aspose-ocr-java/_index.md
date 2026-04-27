---
category: general
date: 2026-04-26
description: Pelajari cara mengenali teks dari gambar menggunakan Aspose OCR dengan
  percepatan GPU di Java. Termasuk mengatur batas memori GPU dan memuat gambar untuk
  langkah-langkah OCR.
draft: false
keywords:
- recognize text from image
- set gpu memory limit
- load image for ocr
- Aspose OCR Java
- GPU acceleration OCR
language: id
og_description: Temukan cara mengenali teks dari gambar dengan cepat menggunakan Aspose
  OCR yang dipercepat GPU di Java. Panduan langkah demi langkah dengan mengatur batas
  memori GPU dan memuat gambar untuk OCR.
og_title: Mengenali teks dari gambar dengan GPU Aspose OCR (Java)
tags:
- OCR
- Java
- GPU
- Aspose
title: Mengenali teks dari gambar dengan GPU Aspose OCR (Java)
url: /id/java/advanced-ocr-techniques/recognize-text-from-image-with-gpu-aspose-ocr-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar dengan GPU Aspose OCR (Java)

Pernahkah Anda perlu **mengenali teks dari gambar** dengan cepat pada backend Java? Dengan akselerasi GPU Aspose OCR, Anda dapat menghemat beberapa detik pada setiap pemindaian—tidak lagi menunggu CPU memproses megabyte piksel. Dalam tutorial ini kami akan menjelaskan cara mengaktifkan GPU, secara opsional **atur batas memori GPU**, dan akhirnya **muat gambar untuk OCR** sehingga Anda mendapatkan string teks bersih hanya dalam beberapa baris kode.

Kami akan membahas semua yang Anda perlukan untuk menjalankan demo pada kartu yang mendukung CUDA, menjelaskan mengapa setiap pengaturan penting, dan menunjukkan contoh lengkap yang siap dijalankan. Pada akhir tutorial Anda akan dapat menyisipkan OCR yang dipercepat GPU ke layanan Java apa pun, baik itu pipeline ingest dokumen atau backend seluler real‑time.

## Apa yang Anda butuhkan

- **Java 17** atau lebih baru (JAR Aspose OCR menargetkan JVM modern)  
- **GPU yang kompatibel dengan CUDA** dengan setidaknya 2 GB VRAM (demo membatasi penggunaan hingga 1024 MB)  
- Perpustakaan **Aspose.OCR for Java** (unduh dari situs Aspose atau tarik dari Maven)  
- File gambar yang ingin Anda proses – sebaiknya hasil pemindaian atau foto beresolusi tinggi  

Tidak ada layanan eksternal, tidak ada kunci cloud, hanya instalasi lokal. Jika Anda belum memiliki GPU, Anda masih dapat menjalankan kode; pemanggilan `setUseGpu(true)` akan otomatis beralih ke CPU.

## Langkah 1: Tambahkan Aspose OCR ke proyek Anda dan mengenali teks dari gambar

Pertama, pastikan JAR Aspose OCR berada di classpath Anda. Jika Anda menggunakan Maven, tambahkan:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Setelah perpustakaan tersedia, buat instance `OcrEngine`. Objek ini merupakan titik masuk untuk operasi **mengenali teks dari gambar**.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

Mengapa kita menginstansiasi `OcrEngine` terlebih dahulu? Ia menyimpan semua pengaturan pengenalan (flag GPU, paket bahasa, dll.) dan mengisolasi tiap pemindaian, sehingga Anda dapat dengan aman menggunakan kembali engine yang sama untuk banyak gambar tanpa kebocoran memori.

## Langkah 2: Aktifkan akselerasi GPU dan secara opsional **atur batas memori GPU**

Akselerasi GPU adalah rahasia yang membuat OCR skala besar menjadi memungkinkan. Aspose memungkinkan Anda mengaktifkannya dengan satu panggilan:

```java
// Step 2: Turn on GPU acceleration (requires a CUDA‑enabled GPU)
ocrEngine.getRecognitionSettings().setUseGpu(true);
```

Jika GPU Anda dibagi dengan beban kerja lain, Anda mungkin ingin membatasi berapa banyak VRAM yang dapat diambil engine. Di sinilah **atur batas memori GPU** berperan:

```java
// Optional: Limit the amount of GPU memory the engine may use (in MB)
ocrEngine.getRecognitionSettings().setGpuMemoryLimit(1024);
```

Menetapkan batas memori mencegah crash out‑of‑memory saat memproses banyak gambar beresolusi tinggi secara paralel. Nilainya dalam megabyte, jadi `1024` berarti “gunakan paling banyak 1 GB VRAM”.

> **Pro tip:** Pada kartu 4 GB, batas 2 GB biasanya merupakan titik aman; Anda dapat bereksperimen dengan nilai lebih tinggi jika melihat GPU menganggur.

## Langkah 3: **Muat gambar untuk OCR** – arahkan engine ke file Anda

Sekarang engine sudah siap, kita harus memberi tahu gambar mana yang akan dipindai. Aspose menerima jalur file, `java.io.File`, atau bahkan `java.awt.image.BufferedImage`. Untuk kesederhanaan kita akan menggunakan jalur:

```java
// Step 3: Load the high‑resolution image to be processed
ocrEngine.setImage("YOUR_DIRECTORY/high_res_photo.jpg");
```

Ganti `YOUR_DIRECTORY/high_res_photo.jpg` dengan lokasi sebenarnya dari gambar uji Anda. Jika gambar berada di folder resources, Anda dapat menggunakan `getClass().getResource("/images/sample.png").getPath()` sebagai gantinya.

Mengapa pemuatan penting? Engine melakukan langkah pra‑pemrosesan (deskew, binarisasi) yang sangat bergantung pada GPU. Menyediakan file bersih dan beresolusi tinggi memungkinkan GPU bekerja secara efisien dan meningkatkan akurasi **mengenali teks dari gambar**.

## Langkah 4: Jalankan pengenalan dan ambil string yang diekstrak

Dengan GPU aktif dan gambar sudah dimuat, panggilan akhir sangat sederhana:

```java
// Step 4: Run the recognition and retrieve the extracted text
String extractedText = ocrEngine.recognize().getText();
```

Metode `recognize()` akan menunggu hingga GPU selesai, kemudian `getText()` mengembalikan `String` biasa. Di balik layar, Aspose menggunakan model deep‑learning yang berjalan pada inti CUDA, sehingga latensi biasanya hanya sebagian kecil dari OCR berbasis CPU.

## Langkah 5: Tampilkan hasil

Mari cetak output OCR ke konsol agar Anda dapat memverifikasi bahwa proses berhasil:

```java
// Step 5: Output the GPU‑accelerated OCR result
System.out.println("GPU‑accelerated result:\n" + extractedText);
```

Jika semuanya terhubung dengan benar, Anda akan melihat teks yang ditranskripsi muncul seketika. Pada RTX 2060 yang sederhana, gambar 3000 × 2000 px diproses dalam kurang dari satu detik.

![mengenali teks dari gambar menggunakan GPU Aspose OCR](/images/gpu-ocr-demo.png "Demo OCR dipercepat GPU")

*Teks alt gambar:* **recognize text from image** – tangkapan layar output konsol setelah OCR GPU.

## Output yang diharapkan

Menjalankan program lengkap terhadap contoh struk menghasilkan sesuatu seperti:

```
GPU‑accelerated result:
Item      Qty   Price
Apple      2    $1.20
Banana     5    $0.75
Total          $3.75
```

Teks aktual Anda akan berbeda tergantung pada gambar sumber, tetapi format di atas menunjukkan bahwa engine berhasil mengekstrak jeda baris dan angka dengan benar.

## Kesulitan umum & tips praktis

| Masalah | Mengapa terjadi | Cara memperbaikinya |
|-------|----------------|---------------|
| **GPU tidak terdeteksi** | Driver CUDA hilang atau versi JAR tidak kompatibel | Instal driver NVIDIA terbaru, pastikan `nvidia-smi` berfungsi, dan gunakan Aspose OCR 23.12 atau lebih baru |
| **Error out‑of‑memory** | Gambar terlalu besar untuk VRAM yang dibatasi | Tingkatkan `setGpuMemoryLimit` atau turunkan resolusi gambar sebelum memuat |
| **Karakter sampah** | Gambar blur atau kontras rendah | Pra‑proses dengan `ocrEngine.getPreprocessingSettings().setBinarization(true)` |
| **Performa lambat pada run pertama** | Overhead inisialisasi konteks GPU | Panaskan engine dengan memproses gambar dummy kecil sebelum beban kerja sebenarnya |

Ingat, **atur batas memori gpu** bersifat opsional tetapi

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}