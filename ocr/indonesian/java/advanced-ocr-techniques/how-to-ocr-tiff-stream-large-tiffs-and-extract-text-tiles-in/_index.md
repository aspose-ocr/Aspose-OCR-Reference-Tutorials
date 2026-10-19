---
category: general
date: 2026-04-29
description: Pelajari cara melakukan OCR pada file TIFF menggunakan mode streaming
  Aspose OCR. Panduan ini menunjukkan cara mengekstrak ubin teks dari gambar TIFF
  berubin secara efisien.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: id
og_description: cara melakukan OCR pada TIFF menggunakan streaming Aspose OCR. Kode
  langkah demi langkah untuk mengekstrak ubin teks dari gambar TIFF berukuran besar.
og_title: cara OCR TIFF – Panduan Streaming Lengkap
tags:
- OCR
- Java
- Aspose
- TIFF
title: Cara OCR TIFF – Streaming TIFF Besar dan Mengekstrak Tile Teks di Java
url: /id/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara ocr tiff – Streaming TIFF Besar dan Mengekstrak Tile Teks di Java

Pernah bertanya‑tanya **how to ocr tiff** file yang terlalu besar untuk dimuat ke memori sekaligus? Anda bukan satu‑satunya. Banyak pengembang mengalami kendala ketika gambar TIFF mereka terbagi menjadi puluhan tile, dan pemanggilan `ocrEngine.recognize()` biasa justru gagal.  

Kabar baik? Mode streaming Aspose OCR memungkinkan Anda memberi setiap tile sebagai aliran terpisah, sehingga Anda dapat **extract text tiles** tanpa membebani heap. Dalam tutorial ini kami akan menelusuri contoh Java lengkap yang siap dijalankan, menjelaskan mengapa setiap baris penting, dan menunjukkan jebakan yang perlu Anda hindari.

> **What you’ll get:** program yang dapat dijalankan yang menyatukan TIFF ber‑tile secara langsung, mencetak teks gabungan, dan menunjukkan cara menyesuaikan kode untuk bahasa atau format gambar lain.

---

## Prerequisites

- **Java 17** atau lebih baru (kode menggunakan try‑with‑resources, jadi JDK 8+ dapat bekerja, namun JDK 17 adalah LTS saat ini).
- **Aspose.OCR for Java** library (v23.10 atau lebih baru). Tambahkan melalui Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Sebuah folder yang berisi tile TIFF individual (misalnya `tile_0.tif`, `tile_1.tif`, …).  
- Opsional: IDE seperti IntelliJ IDEA atau VS Code – namun editor teks sederhana juga cukup.

---

## Step 1 – Prepare the Tile Paths (Why It Matters)

Sebelum mesin OCR dapat melakukan apa pun, ia harus tahu di mana setiap potongan gambar berada. Menuliskan jalur secara hard‑code memang cukup untuk demo, tetapi dalam produksi Anda mungkin akan memindai direktori atau membaca file manifest.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Pro tip:** simpan tile dalam urutan leksikal (0, 1, 2…) karena mesin akan menggabungkan teks yang dikenali dalam urutan yang sama dengan aliran yang Anda berikan.

---

## Step 2 – Enable Streaming Mode on the OCR Engine (Primary Keyword)

Sekarang kita buat instance `OcrEngine` dan mengaktifkan streaming. Inilah inti dari **how to ocr tiff** tanpa memuat seluruh gambar ke RAM.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Why streaming?**  
Ketika `setEnableStreaming(true)` dipanggil, mesin memperlakukan setiap `ImageStream` yang masuk sebagai kelanjutan dari yang sebelumnya. Ia membangun kanvas virtual internal, menyatukan tile secara virtual, dan menjalankan OCR sekali di akhir. Ini menghindari “OutOfMemoryError” yang akan terjadi jika Anda mencoba memuat TIFF multi‑gigabyte sekaligus.

---

## Step 3 – Append Each Tile as an Input Stream (Secondary Keyword)

Berikut loop yang memberi setiap tile ke mesin. Blok `try‑with‑resources` menjamin handle file ditutup dengan cepat, yang sangat penting saat Anda berurusan dengan puluhan file.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Perhatikan bahwa frasa **extract text tiles** secara alami tertanam: setiap iterasi *extracts* teks dari sebuah tile dan menambahkannya ke kumpulan hasil yang terus bertambah.

---

## Step 4 – Run Recognition and Output the Combined Text (Primary Keyword)

Setelah semua tile masuk antrian, satu panggilan melakukan OCR pada gambar virtual. Hasilnya berisi teks lengkap, seolah‑olah Anda memiliki satu TIFF raksasa.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Expected output** (asumsi tile berisi frasa “Hello World” yang terbagi):

```
=== OCR Output ===
Hello World
```

Jika tile Anda berisi lebih banyak baris, mereka akan muncul dalam urutan yang sama dengan yang Anda berikan. Anda juga dapat menulis `ocrResult.getText()` ke file untuk pemrosesan lanjutan.

---

## Step 5 – Full, Runnable Example (All Steps in One Place)

Berikut program lengkap yang dapat Anda salin‑tempel ke `StreamingExample.java`. Program ini mencakup semua impor, komentar, dan penanganan error.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Simpan, kompilasi, dan jalankan:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Anda akan melihat teks OCR yang telah digabungkan tercetak di konsol.

---

## Advanced Tips & Common Pitfalls (Why This Works)

| Masalah | Mengapa Terjadi | Cara Memperbaiki / Mengoptimalkan |
|---------|----------------|-----------------------------------|
| **Out‑of‑memory errors** | Memuat TIFF berukuran penuh ke dalam `BufferedImage` menghabiskan seluruh heap. | Gunakan mode streaming (`setEnableStreaming(true)`) – mesin tidak pernah mematerialisasi seluruh gambar. |
| **Tile order mismatch** | File diurutkan secara alfabetik vs. urutan numerik (misalnya `tile_10.tif` sebelum `tile_2.tif`). | Tambahkan nol di depan angka (`tile_00.tif`, `tile_01.tif`) atau urutkan secara programatik menggunakan `Comparator`. |
| **Wrong language** | OCR default ke bahasa Inggris; teks non‑Inggris menjadi rusak. | Panggil `ocrEngine.getLanguageSettings().setLanguage("fr")` (atau kode ISO yang didukung). |
| **Partial failures** | Satu tile rusak menghentikan seluruh proses. | Tangkap `IOException` per tile, log, dan tentukan apakah melanjutkan atau menghentikan. |
| **Performance bottleneck** | I/O disk mendominasi saat membaca banyak file kecil. | Gabungkan tile ke dalam ZIP dan streaming dari memori, atau gunakan SSD cepat. |

---

## When to Use Streaming vs. Single‑Image OCR

- **Streaming** ideal untuk:
  - TIFF multi‑halaman atau pemindaian gigapiksel.
  - Situasi dengan memori terbatas (misalnya kontainer Docker, perangkat seluler).
  - Pipeline yang sudah menerima potongan gambar (misalnya aliran kamera).

- **Single‑image OCR** cocok untuk:
  - File PNG/JPEG kecil (< 5 MB).
  - Pemindaian satu kali di mana kesederhanaan lebih penting daripada performa.

---

## Conclusion

Anda kini memiliki pemahaman yang kuat tentang **how to ocr tiff** menggunakan kemampuan streaming Aspose OCR, dan tahu cara **extract text tiles** secara efisien. Solusi lengkap—menginisialisasi mesin, mengaktifkan streaming, menambahkan setiap tile, dan akhirnya melakukan pengenalan pada kanvas virtual—menutupi “apa”, “mengapa”, dan “bagaimana” yang Anda perlukan untuk kode siap produksi.

Langkah selanjutnya? Coba ganti `"en"` dengan bahasa lain, atau bereksperimen dengan format gambar berbeda (`.png`, `.jpg`). Anda juga dapat mengalirkan hasil OCR langsung ke indeks pencarian atau generator PDF. Polanya tetap sama: streaming, menyatukan, mengenali.

Punya pertanyaan tentang skala ratusan tile, atau butuh bantuan dengan penanganan error? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}