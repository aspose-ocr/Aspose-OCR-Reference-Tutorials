---
category: general
date: 2026-05-03
description: Buat pool thread tetap di Java untuk mengekstrak teks dari gambar dengan
  cepat. Pelajari cara menjalankan OCR, mengonversi gambar menjadi teks, dan meningkatkan
  kinerja dengan pemrosesan OCR paralel.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: id
og_description: Buat pool thread tetap di Java untuk mengekstrak teks dari gambar
  dengan cepat. Pelajari cara menjalankan OCR, mengonversi gambar menjadi teks, dan
  meningkatkan kinerja dengan pemrosesan OCR paralel.
og_title: Buat Fixed Thread Pool untuk OCR Paralel di Java
tags:
- Java
- OCR
- Multithreading
title: Buat Fixed Thread Pool untuk OCR Paralel di Java
url: /id/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Fixed Thread Pool untuk Parallel OCR di Java

Pernah perlu **create fixed thread pool** untuk mempercepat pekerjaan OCR, tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Dalam banyak proyek yang banyak gambar, bottleneck adalah pemanggilan OCR satu‑thread, dan solusinya ternyata sangat sederhana: buat pool thread pekerja dan biarkan mereka memproses file secara paralel.  

Dalam tutorial ini Anda akan belajar cara **extract text from images** menggunakan Aspose OCR, cara **run OCR** secara efisien, dan cara **convert image to text** tanpa membebani CPU Anda. Pada akhir tutorial Anda akan memiliki program Java siap‑jalankan yang mendemonstrasikan **parallel OCR processing** pada beberapa gambar contoh.

## Apa yang Akan Anda Bangun

Kami akan menyusun sebuah aplikasi console kecil yang:

* Membaca daftar path gambar (PNG, JPG, TIFF, BMP).
* **Creates a fixed thread pool** berukuran sesuai jumlah core CPU.
* Mengirimkan tugas OCR untuk setiap gambar.
* Mengumpulkan teks yang dikenali dan mencetaknya ke console.
* Menutup executor dengan bersih.

Tanpa alat build eksternal, tanpa kerangka kerja mewah—hanya Java murni dan library Aspose OCR. Jika Anda memiliki Java 8+ dan IDE yang layak, Anda siap.

## Prasyarat

* **Java Development Kit (JDK) 8 atau lebih baru** – kode menggunakan lambda, jadi versi lebih lama tidak akan terkompilasi.
* **Aspose OCR for Java** – unduh JAR dari situs Aspose atau tarik via Maven (`com.aspose:aspose-ocr`).
* Sebuah folder dengan beberapa gambar uji (kode mengarah ke `YOUR_DIRECTORY`).  
* Familiaritas dasar dengan concurrency Java (kami akan menjelaskan sisanya).

> *Pro tip:* Jika Anda menggunakan Maven, tambahkan dependensi ke `pom.xml` Anda dan biarkan IDE menangani classpath.  

---

## Langkah 1: Tambahkan Import yang Diperlukan

Pertama, bawa kelas yang kita butuhkan ke dalam ruang lingkup. Ini bukan sekadar boilerplate; setiap import memberi tahu JVM di mana menemukan engine OCR, utilitas penanganan gambar, dan alat concurrency yang memungkinkan kita **create fixed thread pool**.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – API OCR inti.  
* `java.util.*` – koleksi untuk menyimpan path gambar dan hasil.  
* `java.util.concurrent.*` – paket concurrency yang berisi `ExecutorService` dan `Future`.

## Langkah 2: Tentukan Gambar yang Akan Diproses

Selanjutnya, kami membuat daftar file yang ingin **extract text from images**. Menggunakan `Arrays.asList` membuat kode ringkas dan memungkinkan kita mengganti direktori Anda sendiri tanpa mengubah logika lainnya.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Silakan tambahkan lebih banyak entri; thread pool akan secara otomatis menyesuaikan berdasarkan jumlah core CPU yang Anda miliki.

## Langkah 3: **Create Fixed Thread Pool** Sesuai Core CPU

Berikut inti tutorial. Kami menanyakan ke runtime berapa banyak core yang tersedia dan meminta pabrik `Executors` memberikan pool dengan ukuran tepat itu. Mengapa fixed? Karena jumlah thread yang dapat diprediksi mencegah “ledakan thread” yang dapat menguras sumber daya OS.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` mengembalikan jumlah core logis (termasuk hyper‑threads).  
* `newFixedThreadPool(coreCount)` menjamin kami tidak pernah melampaui kapasitas CPU, yang merupakan cara paling aman untuk **run OCR** secara paralel.

## Langkah 4: Kirim Tugas OCR untuk Setiap Gambar

Sekarang kami mengubah setiap path file menjadi callable yang **runs OCR**, mengenali teks, dan mengembalikan hasilnya. Perhatikan kami membuat instance `OcrEngine` baru di dalam lambda—ini menghindari berbagi state engine yang tidak thread‑safe.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Setiap pemanggilan `submit` menyerahkan lambda ke pool, yang menjadwalkannya pada thread yang idle.  
* Objek `Future<String>` memungkinkan kami mengambil teks yang dikenali nanti, mempertahankan urutan jika diperlukan.

## Langkah 5: Ambil dan Tampilkan Teks yang Dikenali

Setelah semua tugas berada dalam antrian, kami cukup iterasi daftar `Future`, memanggil `get()` untuk menunggu hingga setiap pekerjaan OCR selesai. Di sinilah langkah **convert image to text** menjadi terlihat: pemanggilan `engine.getText()` mengembalikan string mentah.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Output console tipikal terlihat seperti:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Jika sebuah file gagal (mungkin korup), Anda akan melihat baris yang dimulai dengan `Failed:` diikuti path—berguna untuk debugging cepat.

## Langkah 6: Bersihkan Executor Service

Jangan pernah lupa menutup pool; bila tidak, JVM dapat tetap berjalan, mengira masih ada pekerjaan. Shutdown yang anggun memungkinkan semua tugas yang berjalan selesai sebelum proses berakhir.

```java
executor.shutdown();
```

Anda juga dapat memanggil `awaitTermination` jika perlu menegakkan batas waktu, tetapi untuk kebanyakan utilitas command‑line, `shutdown()` saja sudah cukup.

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke file bernama `ParallelOcrTutorial.java`, sesuaikan path gambar, dan jalankan `javac` + `java` seperti biasa.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Hasil yang diharapkan:** konten teks setiap gambar dicetak ke console, dalam urutan yang sama dengan daftar `imagePaths`. Jika ada gambar yang tidak dapat diproses, Anda akan melihat pemberitahuan kegagalan alih-alih baris kosong.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya memiliki lebih banyak gambar daripada thread?

Fixed thread pool akan otomatis menempatkan tugas berlebih ke dalam antrian. Begitu sebuah thread menyelesaikan pekerjaan OCR saat ini, ia mengambil tugas berikutnya. Perilaku antrian ini adalah inti dari **parallel OCR processing**—Anda mendapatkan throughput maksimal tanpa membebani CPU.

### Bisakah saya mengubah bahasa?

Tentu saja. Ganti `engine.getLanguage().setEnglish(true);` dengan flag bahasa yang sesuai, misalnya `setFrench(true)` atau aktifkan beberapa bahasa dengan memanggil beberapa setter sebelum `recognize()`.

### Bagaimana cara menangani gambar yang sangat besar?

File besar dapat mengonsumsi banyak memori per thread. Jika Anda melihat `OutOfMemoryError`, pertimbangkan untuk memperkecil ukuran gambar sebelum memberi ke engine, atau tingkatkan ukuran heap dengan `-Xmx`. Pendekatan lain adalah menggunakan **cached thread pool** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}