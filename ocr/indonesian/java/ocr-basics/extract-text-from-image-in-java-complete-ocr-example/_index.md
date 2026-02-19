---
category: general
date: 2026-02-19
description: Ekstrak teks dari gambar menggunakan Java OCR. Pelajari contoh Java OCR
  yang memuat gambar untuk OCR dan mengekstrak teks dari file faktur dalam beberapa
  langkah saja.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: id
og_description: Ekstrak teks dari gambar menggunakan Java OCR. Panduan ini menunjukkan
  cara memuat gambar untuk OCR dan mengambil teks dari faktur dengan contoh Java OCR
  sederhana.
og_title: Ekstrak Teks dari Gambar di Java – Contoh OCR Lengkap
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Ekstrak Teks dari Gambar di Java – Contoh OCR Lengkap
url: /id/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar di Java – Contoh OCR Lengkap

Pernah perlu **mengekstrak teks dari gambar** tapi tidak yakin pustaka mana yang harus dipilih? Anda tidak sendirian—banyak pengembang menghadapi hal ini saat mengotomatisasi pemrosesan faktur atau membangun arsip yang dapat dicari. Kabar baiknya? Dengan beberapa baris Java Anda dapat memuat gambar untuk OCR, menentukan wilayah minat, dan mengambil teks yang tepat.  

Dalam tutorial ini kami akan membahas **java ocr example** yang menunjukkan cara **memuat gambar untuk OCR**, mengatur ROI, dan **mengekstrak teks dari faktur** menggunakan Aspose.OCR. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan dan dapat dimasukkan ke proyek Java mana pun.

## Apa yang Akan Anda Pelajari

- Cara membuat instance `OcrEngine` dan mengapa itu penting.
- Cara yang benar untuk **memuat gambar untuk OCR** dengan `ImageStream` milik Aspose.
- Menetapkan **region of interest (ROI)** sehingga Anda hanya memproses bagian gambar yang berisi jumlah faktur.
- Mengekstrak teks yang dikenali dan mencetaknya ke konsol.
- Jebakan umum (misalnya, koordinat persegi panjang yang salah) dan cara memperbaikinya dengan cepat.

**Prasyarat**

- Java 8 atau lebih baru terpasang.
- Maven atau Gradle untuk mengambil pustaka Aspose.OCR (`com.aspose:aspose-ocr`).
- Contoh gambar faktur (`invoice.png`) ditempatkan di direktori yang diketahui.

Sudah siap? Baik—mari kita mulai.

![Extract text from image using Java OCR](/images/extract-text-from-image-java.png "extract text from image example")

## Ekstrak Teks dari Gambar – Contoh OCR Java Langkah‑per‑Langkah

Berikut adalah kode sumber lengkapnya. Silakan salin‑tempel ke dalam `RoiOcrExample.java` dan jalankan langsung.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Mengapa Setiap Langkah Penting

1. **Membuat mesin OCR** – tanpa mesin tidak ada konteks untuk pemrosesan gambar. Objek ini juga memungkinkan Anda menyesuaikan paket bahasa nanti jika membutuhkan dukungan multibahasa.  
2. **Memuat gambar** – `ImageStream.fromFile` mengabstraksi format file, memastikan mesin membaca byte dengan benar. Jika Anda melewatkannya, akan muncul `NullPointerException`.  
3. **Menetapkan ROI** – memproses seluruh halaman dapat membuang-buang sumber daya. Dengan mempersempit persegi panjang ke area total faktur, Anda mempercepat pengenalan dan mengurangi noise.  
4. **Memanggil `recognize()`** – inilah tempat keajaiban terjadi. Metode ini menjalankan algoritma OCR pada ROI dan menghasilkan objek hasil.  
5. **Mencetak output** – dalam proyek nyata Anda mungkin menyimpan teks ke basis data, tetapi `System.out.println` sudah cukup untuk demo cepat.

## Memuat Gambar untuk OCR

Jika Anda bertanya-tanya apakah path harus absolut atau relatif, jawabannya keduanya dapat bekerja—pastikan proses Java dapat membaca file tersebut. Di Windows, backslash harus di‑escape (`C:\\images\\invoice.png`) atau Anda dapat menggunakan slash maju (`C:/images/invoice.png`).  

**Tips pro:** Jika Anda memproses banyak faktur dalam sebuah loop, gunakan kembali instance `OcrEngine` yang sama; ia menyimpan cache sumber daya internal dan meningkatkan throughput.

## Menentukan Region of Interest (ROI)

Memilih persegi panjang yang tepat bisa memerlukan percobaan. Cara praktis untuk menemukan koordinat adalah membuka gambar di editor grafis apa pun (seperti GIMP atau Paint.NET) dan mengarahkan kursor ke area yang diinginkan—Anda akan melihat nilai X/Y di bilah status.  

Kasus tepi: beberapa faktur memiliki tata letak yang bervariasi. Dalam situasi ini Anda dapat melakukan pra‑pemindaian cepat pada seluruh gambar, menemukan kata kunci seperti “Total:” dengan regex, lalu menyesuaikan ROI secara dinamis.

## Lakukan OCR dan Dapatkan Teks

Pemanggilan `recognize()` bersifat sinkron—thread Anda akan terblokir sampai mesin selesai. Untuk batch besar Anda mungkin ingin membuat thread pool dan memproses gambar secara paralel. Ingat bahwa setiap thread memerlukan instance `OcrEngine` masing‑masing; mereka tidak thread‑safe.

## Jalankan dan Verifikasi Output

Kompilasi dan jalankan:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

Anda akan melihat sesuatu seperti:

```
ROI text: $1,254.00
```

Jika output terlihat berantakan, periksa kembali koordinat ROI dan pastikan kualitas gambar tinggi (300 dpi atau lebih memberikan hasil terbaik).  

### Jebakan Umum & Cara Memperbaikinya

| Gejala | Penyebab Kemungkinan | Perbaikan |
|---------|----------------------|-----------|
| String kosong | ROI berada di luar batas gambar | Verifikasi nilai persegi panjang terhadap dimensi gambar |
| Kata salah eja | Resolusi rendah | Gunakan sumber beresolusi lebih tinggi atau terapkan pra‑pemrosesan gambar (mis., binarisasi) |
| `java.lang.NoClassDefFoundError` | JAR Aspose tidak ada di classpath | Tambahkan `aspose-ocr.jar` ke `-cp` atau gunakan manajemen dependensi Maven/Gradle |

## Kesimpulan

Sekarang Anda tahu cara **mengekstrak teks dari gambar** di Java menggunakan **java ocr example** yang ringkas. Dengan memuat gambar secara tepat, mendefinisikan ROI yang terfokus, dan memanggil `recognize()`, Anda dapat secara andal **mengekstrak teks dari faktur** dan mengalirkan data tersebut ke sistem hilir.

Apa selanjutnya? Coba ganti ROI untuk bidang lain (tanggal, nama vendor), bereksperimen dengan paket bahasa untuk faktur multibahasa, atau integrasikan langkah OCR ke dalam microservice Spring Boot. Pola yang sama berlaku untuk kwitansi, paspor, atau dokumen apa pun yang memerlukan ekstraksi teks yang akurat.

Jika Anda memiliki pertanyaan tentang skalabilitas solusi ini atau menangani pemindaian yang berisik, tinggalkan komentar di bawah—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}