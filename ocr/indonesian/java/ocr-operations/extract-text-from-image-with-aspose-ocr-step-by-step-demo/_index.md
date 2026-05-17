---
category: general
date: 2026-02-14
description: Ekstrak teks dari gambar menggunakan Aspose OCR. Pelajari cara memuat
  gambar untuk OCR, membaca teks dari persegi panjang, dan ikuti tutorial Aspose OCR
  ini dalam hitungan menit.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: id
og_description: Ekstrak teks dari gambar secara instan. Panduan ini menunjukkan cara
  memuat gambar untuk OCR, membaca teks dari persegi panjang, dan menyelesaikan tutorial
  Aspose OCR.
og_title: Ekstrak Teks dari Gambar dengan Aspose OCR – Panduan Cepat
tags:
- Aspose
- OCR
- Java
title: Ekstrak Teks dari Gambar dengan Aspose OCR – Demo Langkah demi Langkah
url: /id/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak Teks dari Gambar dengan Aspose OCR – Demo Langkah‑per‑Langkah

Pernah membutuhkan untuk **mengekstrak teks dari gambar** tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang mengalami kebuntuan saat pertama kali menangani pemindaian struk atau verifikasi ID. Kabar baiknya? Dengan Aspose OCR Anda dapat memuat sebuah gambar, menentukan wilayah tepat tempat teks berada, dan mengambil karakter‑karakter tersebut dalam beberapa baris kode.

Dalam **aspose ocr tutorial** ini kami akan membahas semua yang Anda perlukan: memuat gambar untuk OCR, mengatur sebuah persegi panjang yang memberi tahu mesin di mana harus mencari, dan akhirnya membaca teks yang diekstrak. Pada akhir tutorial Anda akan memiliki program Java yang dapat dijalankan dan mencetak teks ROI ke konsol—tidak ada misteri, hanya solusi yang jelas dan berfungsi.

## Apa yang Anda Butuhkan

| Prasyarat | Mengapa penting |
|--------------|----------------|
| **Java JDK 8+** | Aspose OCR disediakan sebagai pustaka Java; JDK modern apa pun dapat digunakan. |
| **Aspose.OCR for Java** (download from the Aspose website or add via Maven) | Menyediakan kelas `OcrEngine`, `ImageStream`, dan kelas terkait lainnya. |
| **An image file** (e.g., `receipt.jpg`) that contains printable text | File gambar (misalnya `receipt.jpg`) yang berisi teks yang dapat dicetak. |
| **IDE or editor** (IntelliJ, Eclipse, VS Code…) | Membantu Anda mengompilasi dan menjalankan contoh dengan cepat. |

Jika Anda menggunakan Maven, tambahkan dependensi ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Tip pro:** Nomor versi di atas berlaku hingga Februari 2026. Memperbarui ke rilis terbaru memastikan Anda mendapatkan perbaikan bug dan peningkatan performa.

## Langkah 1 – Inisialisasi Mesin OCR

Hal pertama yang harus dilakukan: Anda memerlukan sebuah instance `OcrEngine`. Anggaplah itu sebagai otak yang akan menganalisis piksel.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

Mengapa membuatnya dengan cara ini? Aspose memisahkan mesin (yang menyimpan konfigurasi) dari data gambar, memberi Anda fleksibilitas untuk menggunakan kembali mesin yang sama untuk beberapa gambar jika diinginkan.

## Langkah 2 – Muat Gambar untuk OCR

Sekarang kita benar‑benarnya **memuat gambar untuk OCR**. Helper `ImageStream.fromFile` membaca file ke dalam stream yang dapat dipahami oleh Aspose.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Jika file tidak ditemukan, mesin akan melemparkan pengecualian, jadi Anda mungkin ingin membungkusnya dalam blok try‑catch pada kode produksi. Untuk demo ini kami membiarkan pengecualian mengalir—menjaga contoh tetap rapi.

## Langkah 3 – Tentukan Persegi Panjang (Baca Teks dari Persegi Panjang)

Di sinilah bagian **baca teks dari persegi panjang** bersinar. Anda memberi tahu mesin secara tepat di mana harus mencari, yang mempercepat proses dan mengurangi hasil positif palsu.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Mengapa persegi panjang?**  
> Kebanyakan dokumen memiliki tata letak yang dapat diprediksi—misalnya struk di mana jumlah selalu muncul di bagian bawah. Dengan memfokuskan pada bagian itu, mesin OCR mengabaikan grafik yang tidak relevan dan meningkatkan akurasi.

**Kasus tepi:** Jika persegi panjang melebihi batas gambar, Aspose secara diam‑diam memotongnya, tetapi Anda akan kehilangan data. Pemeriksaan cepat dapat mencegah hal itu:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Langkah 4 – Proses Gambar

Setelah semuanya diatur, kami meminta mesin melakukan keajaibannya.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

Pemanggilan `process()` mengembalikan objek `OcrResult` yang berisi teks yang diekstrak, skor kepercayaan, dan bahkan kotak pembatas untuk setiap kata jika Anda membutuhkannya nanti.

## Langkah 5 – Keluarkan Teks yang Diekstrak

Akhirnya, cetak hasilnya. Dalam aplikasi nyata Anda mungkin menyimpannya di basis data atau mengirimnya ke layanan lain, tetapi untuk tutorial ini output ke konsol sudah cukup.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Output yang diharapkan** (asumsi persegi panjang menangkap total jumlah pada struk):

```
ROI text:
$12.34
```

Jika ROI kosong atau gambar buram, Anda akan melihat string kosong atau karakter yang kacau. Sesuaikan persegi panjang, tingkatkan kualitas gambar, atau aktifkan opsi pra‑pemrosesan Aspose (misalnya, `setAutoSkewCorrection(true)`).

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke dalam file bernama `RoiDemo.java`, sesuaikan jalur gambar, dan jalankan `javac RoiDemo.java && java RoiDemo`.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Verifikasi hasil:** Setelah dijalankan, bandingkan output konsol dengan teks sebenarnya di dalam persegi panjang. Jika cocok, Anda telah berhasil **mengekstrak teks dari gambar** menggunakan Aspose OCR.

## Pertanyaan Umum & Tips

### What if I need to process multiple ROIs in the same image?
Buat `Rectangle` baru untuk setiap area, panggil `setRegionOfInterest` lagi, dan jalankan kembali `process()`. Mesin menggunakan kembali data gambar yang sama, sehingga kinerja tetap cepat.

### How does Aspose handle different languages or fonts?
Anda dapat mengganti model bahasa melalui `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)`. Untuk skrip non‑Latin, muat paket bahasa yang sesuai (tersedia di halaman unduhan Aspose).

### Does the library support PDF input?
Ya—Aspose OCR dapat menerima aliran PDF secara langsung. Cukup ganti `ImageStream.fromFile` dengan `ImageStream.fromPdfFile("doc.pdf")` dan opsional tentukan nomor halaman.

### Can I improve accuracy on low‑quality scans?
Aktifkan pra‑pemrosesan:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

## Kesimpulan

Kami baru saja melewati **aspose ocr tutorial** lengkap yang menunjukkan cara **mengekstrak teks dari gambar**, **memuat gambar untuk OCR**, dan **membaca teks dari persegi panjang** menggunakan Java. Langkah‑langkah kunci adalah menginisialisasi mesin, memberi gambar, menentukan wilayah minat, memproses, dan akhirnya mencetak hasilnya.

Dari sini Anda mungkin ingin mengeksplor:

* **Pemrosesan batch** – iterasi folder berisi struk dan simpan setiap total ke basis data.  
* **Deteksi ROI dinamis** – gunakan pustaka pemrosesan gambar (OpenCV) untuk menemukan blok teks secara otomatis.  
* **Pasca‑pemrosesan** – terapkan regex atau pencocokan fuzzy untuk membersihkan keanehan OCR.

Cobalah ide‑ide tersebut, sesuaikan persegi panjang agar cocok dengan dokumen Anda, dan Anda akan memiliki alur ekstraksi teks yang kuat dalam waktu singkat. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}