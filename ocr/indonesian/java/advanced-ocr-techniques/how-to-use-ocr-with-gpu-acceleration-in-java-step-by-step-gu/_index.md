---
category: general
date: 2026-02-09
description: Cara menggunakan OCR dengan cepat menggunakan Aspose OCR, mengenali teks
  dari gambar, dan mengekstrak teks dari PNG sambil mengatur mode serta batas memori
  GPU.
draft: false
keywords:
- how to use ocr
- recognize text from image
- extract text from png
- how to set mode
- set gpu memory limit
language: id
og_description: Cara menggunakan OCR secara efisien – pelajari cara mengenali teks
  dari gambar, mengekstrak teks dari PNG, mengatur mode, dan mengontrol batas memori
  GPU di Java.
og_title: Cara Menggunakan OCR dengan Akselerasi GPU di Java
tags:
- OCR
- Java
- GPU
- Aspose
title: Cara Menggunakan OCR dengan Akselerasi GPU di Java – Panduan Langkah demi Langkah
url: /id/java/advanced-ocr-techniques/how-to-use-ocr-with-gpu-acceleration-in-java-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR dengan Akselerasi GPU di Java – Tutorial Pemrograman Lengkap

Pernah bertanya-tanya **cara menggunakan OCR** untuk mengambil teks dari gambar tanpa menulis jutaan baris kode? Anda tidak sendirian. Dalam banyak proyek—pemindaian faktur, pemrosesan struk, atau sekadar mendigitalkan dokumen lama—para pengembang membutuhkan cara yang andal untuk **mengenali teks dari gambar** file, terutama PNG yang sering berisi grafik bersih dengan resolusi tinggi.  

Berita baik? Aspose OCR membuat ini menjadi sangat mudah, dan dengan beberapa penyesuaian konfigurasi Anda bahkan dapat memindahkan beban kerja berat ke GPU Anda. Dalam tutorial ini kami akan membahas seluruh proses: mulai dari memuat PNG, hingga **menetapkan mode** untuk pemrosesan GPU, hingga **menetapkan batas memori GPU**, dan akhirnya mencetak teks yang diekstrak. Pada akhir tutorial Anda akan memiliki program Java yang dapat dijalankan dan melakukan persis apa yang Anda butuhkan.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mengimpor Aspose OCR untuk Java.
- Cara **mengenali teks dari gambar** file menggunakan perpustakaan.
- Cara **mengekstrak teks dari PNG** secara efisien.
- Cara **menetapkan mode** ke GPU dan mengontrol jejak memori dengan **set GPU memory limit**.
- Jebakan umum dan tips untuk penggunaan di dunia nyata.

### Prasyarat

- Java 8 atau lebih baru (kode juga dapat dikompilasi dengan JDK 11).
- GPU NVIDIA dengan driver yang kompatibel dengan CUDA jika Anda menginginkan akselerasi GPU.
- Aspose OCR for Java JAR (unduh dari situs Aspose atau tambahkan melalui Maven/Gradle).
- Contoh gambar PNG (misalnya `sample1.png`) yang ditempatkan di folder yang dapat Anda referensikan.

---

## Cara Menggunakan OCR – Aktifkan Mode GPU

Hal pertama yang perlu Anda lakukan adalah memberi tahu Aspose OCR bahwa Anda ingin menjalankannya di GPU alih-alih CPU. Di sinilah kata kunci **how to set mode** berperan.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Grab the configuration object
OcrEngineConfiguration config = ocrEngine.getConfiguration();

// Step 3: Switch processing mode to GPU
config.setProcessingMode(ProcessingMode.GPU);   // requires a CUDA‑compatible driver

// (Optional) Step 4: Limit GPU memory usage to 1024 MB
config.setGpuMemoryLimit(1024);                 // set gpu memory limit (MB)
```

**Mengapa ini penting:**  
Pemrosesan GPU dapat jauh lebih cepat untuk batch besar atau gambar beresolusi tinggi, tetapi juga mengonsumsi memori video. Dengan memanggil `setGpuMemoryLimit`, Anda mencegah aplikasi Anda menguasai seluruh GPU, yang penting ketika perangkat yang sama menjalankan beban kerja lain (misalnya, UI atau model pembelajaran mesin).

---

## Mengenali Teks dari Gambar Menggunakan Aspose OCR

Setelah mesin dikonfigurasi, kita perlu menunjukkannya ke file yang ingin dibaca. Ini adalah inti dari **recognize text from image**.

```java
// Step 5: Define the image to be processed
ImageRecognitionResult imageInfo = new ImageRecognitionResult();
imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

// Step 6: Run the OCR operation
RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);
```

**Apa yang terjadi di balik layar?**  
Aspose OCR memuat PNG, melakukan pra‑pemrosesan (binarisasi, perbaikan kemiringan, dll.), kemudian menjalankan jaringan saraf OCR pada GPU. Objek hasil berisi teks mentah serta skor kepercayaan untuk setiap baris.

---

## Mengekstrak Teks dari PNG dengan Batas Memori GPU

Setelah pengenalan, mengekstrak string biasa sangat sederhana, namun banyak pengembang lupa memverifikasi outputnya. Berikut cara Anda dapat dengan aman **extract text from PNG** dan menampilkannya.

```java
// Step 7: Output the recognized text
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Output yang diharapkan (contoh):**

```
Recognized text:
Invoice #12345
Date: 2026-02-09
Total: $1,250.00
Thank you for your business!
```

Jika gambar mengandung noise atau font yang tidak biasa, Anda mungkin melihat karakter yang kacau. Dalam kasus tersebut, pertimbangkan untuk menyesuaikan opsi pra‑pemrosesan (misalnya, `config.setLanguage(Language.ENGLISH)` atau `config.setAutoSkewCorrection(true)`).

---

## Contoh Lengkap yang Dapat Dijalankan

Berikut adalah program Java lengkap yang menggabungkan semuanya. Salin‑tempel ke dalam file bernama `GpuExample.java`, sesuaikan path gambar, dan jalankan dengan `javac`/`java` atau dari IDE Anda.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.configuration.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the image to be processed
        ImageRecognitionResult imageInfo = new ImageRecognitionResult();
        imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

        // Step 2: Create the OCR engine and enable GPU processing
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration config = ocrEngine.getConfiguration();

        // Step 3: Set processing mode to GPU (requires CUDA driver)
        config.setProcessingMode(ProcessingMode.GPU);

        // Step 4 (optional): Limit GPU memory usage to 1024 MB
        config.setGpuMemoryLimit(1024);

        // Step 5: Perform recognition
        RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);

        // Step 6: Print the extracted text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Menjalankan program**

```bash
javac -cp "path/to/aspose-ocr.jar" GpuExample.java
java -cp ".:path/to/aspose-ocr.jar" GpuExample
```

Pastikan JAR berada di classpath Anda; jika tidak, Anda akan mendapatkan `ClassNotFoundException`.

---

## Tips Pro & Jebakan Umum

- **Versi driver GPU:** Flag `ProcessingMode.GPU` akan melemparkan pengecualian jika driver CUDA tidak ada atau tidak kompatibel. Periksa kembali dengan `nvidia-smi`.
- **Penganggaran memori:** Jika Anda memproses banyak gambar secara bersamaan, tingkatkan nilai `setGpuMemoryLimit` atau jalankan pekerjaan secara berurutan untuk menghindari kesalahan out‑of‑memory.
- **Format gambar:** Meskipun PNG bekerja dengan baik, JPEG dengan kompresi tinggi dapat menyebabkan kesalahan pengenalan. Pertimbangkan untuk mengonversi ke PNG lossless sebelum OCR.
- **Dukungan bahasa:** Secara default Aspose OCR mengasumsikan bahasa Inggris. Untuk bahasa lain, panggil `config.setLanguage(Language.SPANISH)` (atau enum yang sesuai) sebelum `recognize`.
- **Pengujian kinerja:** Jalankan benchmark cepat (`System.nanoTime()`) dengan dan tanpa GPU untuk memverifikasi bahwa percepatan kecepatan memang sebanding dengan kompleksitas tambahan.

---

## Pertanyaan yang Sering Diajukan

**Apakah ini bekerja di macOS atau Linux?**  
Ya—Aspose OCR bersifat lintas‑platform. Pastikan Anda memiliki GPU yang kompatibel dengan CUDA dan driver yang tepat terinstal untuk OS Anda.

**Bagaimana jika saya tidak memiliki GPU?**  
Anda cukup menghilangkan baris `setProcessingMode(ProcessingMode.GPU)`; mesin akan otomatis beralih ke mode CPU.

**Bisakah saya memproses PDF secara langsung?**  
Aspose OCR fokus pada gambar raster. Untuk PDF, ekstrak setiap halaman menjadi gambar terlebih dahulu (misalnya, menggunakan Aspose PDF) lalu masukkan PNG ke alur OCR.

---

## Kesimpulan

Singkatnya, **cara menggunakan OCR** dengan Aspose di Java dapat diringkas menjadi tiga langkah jelas: mengonfigurasi mesin (termasuk **how to set mode** dan **set GPU memory limit**), menunjukkannya ke PNG Anda, dan membaca string hasilnya. Potongan kode di atas adalah solusi lengkap yang berfungsi penuh dan dapat langsung dimasukkan ke proyek Java mana pun.

Sekarang Anda telah menguasai **recognize text from image** dan **extract text from PNG**, Anda dapat memperluas alur kerja: memproses folder secara batch, menyimpan hasil ke basis data, atau bahkan memasukkan teks ke pipeline NLP berikutnya. Tidak ada batasan—tetapi ingatlah untuk selalu memantau memori GPU dan kompatibilitas driver.

Ada pertanyaan lebih lanjut tentang OCR, akselerasi GPU, atau fitur Aspose? Silakan tinggalkan komentar atau jelajahi dokumentasi resmi Aspose OCR untuk opsi penyesuaian yang lebih mendalam. Selamat coding! 🚀

![diagram cara menggunakan ocr](https://example.com/images/ocr-gpu-diagram.png "diagram cara menggunakan ocr")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}