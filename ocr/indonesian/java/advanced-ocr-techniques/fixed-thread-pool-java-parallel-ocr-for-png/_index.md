---
category: general
date: 2026-02-17
description: Pelajari cara menggunakan fixed thread pool di Java untuk mengekstrak
  teks dari gambar PNG dengan pemrosesan OCR paralel dan menutup layanan executor
  dengan benar.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: id
og_description: Temukan bagaimana fixed thread pool Java dapat mengekstrak teks dari
  gambar PNG secara paralel, mengonversi teks halaman yang dipindai, dan mematikan
  layanan executor dengan aman.
og_title: fixed thread pool java – OCR paralel untuk PNG
tags:
- java
- ocr
- multithreading
- aspose
title: fixed thread pool Java – OCR paralel untuk PNG
url: /id/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

block unchanged.

Now produce final content.

Let's write translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fixed thread pool java – OCR paralel untuk PNG

Pernah bertanya-tanya bagaimana cara mempercepat OCR pada sekumpulan file PNG menggunakan **fixed thread pool java**? Dalam tutorial ini kami akan membahas **extract text from PNG** gambar secara paralel, **convert scanned pages text** menjadi string yang dapat diedit, dan dengan aman **shut down executor service** setelah pekerjaan selesai.

Jika Anda pernah menatap sebuah loop single‑threaded yang berjalan berjam‑jam, Anda pasti tahu rasa frustrasi menunggu setiap halaman selesai sebelum yang berikutnya bahkan mulai. Kabar baik? Dengan beberapa baris Java dan Aspose OCR Anda dapat memanfaatkan semua core CPU, mengubah halaman yang dipindai menjadi teks yang dapat dicari, dan menjaga aplikasi tetap responsif.  

Di bawah ini Anda akan menemukan contoh lengkap yang siap dijalankan, beserta penjelasan mengapa setiap bagian penting, jebakan umum, dan tips yang dapat diterapkan pada pustaka OCR apa pun.

---

## Apa yang Anda Perlukan

- **Java 17** (atau JDK terbaru) – kode ini menggunakan sintaks `var` secara terbatas, tetapi tetap dapat berjalan pada versi lebih lama.  
- **Aspose.OCR for Java** library – dapat diunduh dari Maven Central atau coba versi trial dari Aspose.  
- Sekumpulan file **PNG** yang ingin Anda proses – misalnya struk yang dipindai, halaman buku, atau screenshot.  
- Familiaritas dasar dengan concurrency di Java – tidak wajib, tetapi membantu.

Itu saja. Tanpa layanan eksternal, tanpa Docker, hanya Java biasa dan sedikit sihir multithreading.

---

## Langkah 1: Tambahkan Dependensi Aspose OCR & Lisensi (Opsional)

Pertama, pastikan JAR Aspose OCR berada di classpath Anda. Jika menggunakan Maven, tambahkan:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Jika Anda tidak memiliki lisensi, pustaka akan berjalan dalam mode evaluasi; kode tetap berfungsi sama. Untuk memuat lisensi (disarankan untuk produksi), letakkan `Aspose.OCR.lic` di folder resources Anda dan gunakan:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro tip:** Simpan file lisensi di luar kontrol versi untuk menghindari paparan tidak sengaja.

---

## Langkah 2: Buat Instance `OcrEngine` yang Thread‑Safe

`OcrEngine` milik Aspose OCR bersifat thread‑safe selama Anda menggunakan instance yang sama di seluruh tugas. Membuatnya sekali saja menghemat memori dan menghindari overhead inisialisasi ulang engine untuk setiap gambar.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Mengapa reuse? Anggap engine sebagai pekerja berat yang memuat model bahasa ke memori. Membuat engine baru per gambar ibarat mempekerjakan spesialis baru untuk setiap pekerjaan kecil – mahal dan tidak perlu.

---

## Langkah 3: Siapkan Fixed Thread Pool Java

Sekarang saatnya bintang utama: **fixed thread pool java**. Kita akan menyesuaikannya dengan jumlah prosesor logis sehingga setiap core mendapatkan pekerjaan tanpa oversubscribing.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Menggunakan pool *fixed* (bukan cached) memberi Anda penggunaan sumber daya yang dapat diprediksi dan mencegah lonjakan “out‑of‑memory” ketika ratusan gambar datang sekaligus.

---

## Langkah 4: Daftar File PNG yang Ingin Diproses (Extract Text from PNG)

Kumpulkan path ke gambar yang ingin Anda OCR. Pada proyek nyata Anda mungkin memindai sebuah direktori atau membaca dari database; di sini kita akan hard‑code beberapa contoh.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Catatan:** Ekstensi file **png** penting karena Aspose OCR secara otomatis mendeteksi format, namun Anda juga dapat memberi JPEG atau TIFF.

---

## Langkah 5: Submit Tugas OCR – Pemrosesan OCR Paralel

Setiap gambar menjadi callable yang mengembalikan teks yang dikenali. Karena `OcrEngine` dibagi, kita hanya perlu mengirimkan path file ke dalam tugas.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Mengapa membungkusnya dalam `Future`? Ini memungkinkan kita meluncurkan semua pekerjaan sekaligus, lalu kemudian mengumpulkan hasil sesuai urutan pengiriman – sempurna untuk mempertahankan urutan halaman saat **convert scanned pages text** kembali ke dokumen.

---

## Langkah 6: Ambil Hasil dan Tampilkan (Convert Scanned Pages Text)

Sekarang kita menunggu setiap `Future` selesai dan mencetak output. Pemanggilan `get()` hanya memblokir sampai tugas spesifik selesai, bukan seluruh pool.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Output konsol tipikal terlihat seperti:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Jika Anda lebih suka menulis hasil ke file, ganti `System.out.println` dengan pemanggilan `Files.writeString`.

---

## Langkah 7: Matikan Executor Service dengan Bersih

Setelah semua tugas selesai, sangat penting untuk **shut down executor service**; bila tidak, JVM Anda mungkin tetap menjaga thread non‑daemon hidup, mencegah keluar yang elegan.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

Pola `awaitTermination` memberi pool kesempatan menyelesaikan pekerjaan yang sedang berjalan sebelum dipaksa berhenti. Mengabaikan langkah ini adalah sumber umum memory leak pada aplikasi yang berjalan lama.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel ke `ParallelBatchDemo.java` dan jalankan:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}