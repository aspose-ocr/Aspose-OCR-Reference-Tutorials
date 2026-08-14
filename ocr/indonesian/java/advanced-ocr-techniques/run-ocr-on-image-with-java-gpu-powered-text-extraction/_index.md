---
category: general
date: 2026-03-07
description: Jalankan OCR pada gambar menggunakan Java. Pelajari cara mengenali teks
  dari PNG, mengekstrak teks dari struk, dan memuat gambar untuk OCR dengan contoh
  lengkap OCR Java.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: id
og_description: Jalankan OCR pada gambar dengan Java. Panduan ini menunjukkan cara
  mengenali teks dari PNG, mengekstrak teks dari struk, dan memuat gambar untuk OCR
  menggunakan contoh lengkap OCR Java.
og_title: Jalankan OCR pada Gambar dengan Java – Ekstraksi Teks Berbasis GPU
tags:
- OCR
- Java
- GPU
- Image Processing
title: Jalankan OCR pada Gambar dengan Java – Ekstraksi Teks Berbasis GPU
url: /id/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan OCR pada Gambar dengan Java – Ekstraksi Teks Berbasis GPU

Pernahkah Anda perlu **run OCR on image** file tetapi tidak yakin harus mulai dari mana di Java? Anda tidak sendirian—banyak pengembang mengalami hal yang sama ketika pertama kali mencoba mengekstrak teks dari kwitansi yang dipindai atau screenshot PNG.  

Dalam tutorial ini kami akan memandu Anda melalui **complete Java OCR example** yang tidak hanya **recognizes text from PNG** file tetapi juga menunjukkan cara **extract text from receipt** gambar, sambil memanfaatkan percepatan GPU untuk kecepatan. Pada akhir tutorial Anda akan memiliki program siap‑jalankan yang memuat gambar untuk OCR, memprosesnya, dan mencetak hasil teks polos.

## Apa yang Akan Anda Pelajari

- Cara **load image for OCR** menggunakan `ImageInputStream` sederhana.  
- Mengaktifkan dukungan GPU sehingga mesin berjalan lebih cepat pada perangkat keras modern.  
- Langkah‑langkah tepat untuk **recognize text from PNG** dan mengambil string berguna dari kwitansi.  
- Kesulitan umum (misalnya ID perangkat GPU yang salah) dan tips praktik terbaik.  
- Potongan kode lengkap yang dapat Anda salin‑tempel ke IDE Anda.

**Prasyarat**

- Java 17 atau lebih baru (kode menggunakan kata kunci `var` untuk singkat, tetapi Anda dapat menggantinya dengan tipe eksplisit jika menggunakan Java 8).  
- Sebuah pustaka OCR yang menyediakan kelas `OcrEngine`, `ImageInputStream`, dan `OcrResult` (misalnya SDK *FastOCR* fiktif; ganti dengan yang sebenarnya Anda gunakan).  
- Mesin yang mendukung GPU jika Anda menginginkan peningkatan performa (opsional tetapi disarankan).

---

## Langkah 1: Jalankan OCR pada Gambar – Aktifkan Akselerasi GPU

Hal pertama yang harus dilakukan adalah membuat engine OCR dan memberitahukan agar menggunakan GPU. Langkah ini penting karena tanpa dukungan GPU engine akan kembali ke CPU, yang dapat terasa jauh lebih lambat untuk kwitansi beresolusi tinggi.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Mengapa ini penting:**  
Akselerasi GPU mengalihkan perhitungan matriks berat yang dilakukan mesin OCR. Jika Anda memiliki beberapa GPU, Anda dapat memilih yang memiliki memori terbanyak dengan mengubah nilai `setGpuDeviceId`. Lupa mengaktifkan GPU adalah penyebab umum keluhan “mengapa OCR saya begitu lambat?”.

> **Pro tip:** Jika mesin Anda tidak memiliki GPU yang kompatibel, pemanggilan `setUseGpu(true)` hanya akan diabaikan—tidak ada crash, hanya pemrosesan yang lebih lambat.

---

## Langkah 2: Muat Gambar untuk OCR

Setelah engine siap, kita perlu memberinya gambar. Contoh di bawah menunjukkan cara memuat kwitansi PNG yang disimpan di disk. Anda dapat mengganti path dengan format gambar apa pun yang didukung oleh pustaka OCR Anda.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Kasus tepi:**  
Jika file tidak ada atau path salah, `ImageInputStream` akan melempar `IOException`. Bungkus pemanggilan dalam blok try‑catch dan catat pesan yang membantu:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Langkah 3: Recognize Text from PNG

Dengan gambar dimuat, engine OCR kini dapat melakukan magisnya. Langkah ini sebenarnya **recognizes text from PNG** (atau format lain yang didukung) dan mengembalikan objek `OcrResult`.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**Apa yang terjadi di balik layar?**  
Engine melakukan pra‑pemrosesan (deskew, binarisasi), menjalankan jaringan saraf untuk mendeteksi karakter, dan kemudian menyusunnya menjadi baris‑baris teks. Karena kami telah mengaktifkan GPU sebelumnya, perhitungan jaringan saraf tersebut terjadi di kartu grafis, mengurangi beberapa detik dari total waktu proses.

---

## Langkah 4: Extract Text from Receipt

Setelah pengenalan, biasanya Anda hanya menginginkan teks mentah. Kelas `OcrResult` biasanya menyediakan metode `getText()` yang mengembalikan satu `String`. Anda kemudian dapat melakukan pasca‑pemrosesan (misalnya regex untuk mengambil total, tanggal, dll.).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Output kwitansi tipikal:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Sekarang Anda dapat memberi string ini ke parser Anda sendiri untuk mengekstrak jumlah total, item baris, atau informasi pajak.

---

## Langkah 5: Contoh Java OCR Lengkap – Siap Jalankan

Menggabungkan semuanya, berikut **complete Java OCR example** yang dapat Anda letakkan ke dalam file `Main.java`. Pastikan pustaka OCR ada di classpath Anda.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Output konsol yang diharapkan** (asumsi kwitansi contoh di atas):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Jika output terlihat berantakan, periksa kembali bahwa gambar jelas (DPI tinggi) dan paket bahasa OCR cocok dengan bahasa kwitansi Anda.

---

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

| Question | Answer |
|----------|--------|
| *What if my GPU isn’t detected?* | Engine akan otomatis beralih ke CPU. Verifikasi driver dan pastikan `setGpuDeviceId` sesuai dengan perangkat yang ada (`nvidia-smi` di Linux dapat membantu). |
| *Can I process JPEG or TIFF files?* | Ya—cukup ubah ekstensi file di `ImageInputStream`. Pustaka OCR biasanya mendeteksi format secara otomatis. |
| *Is there a way to batch‑process many receipts?* | Bungkus kode pengenalan dalam loop dan gunakan kembali instance `OcrEngine` yang sama; menginisialisasi ulang per gambar membuang memori GPU. |
| *How do I improve accuracy on low‑contrast receipts?* | Lakukan pra‑pemrosesan gambar (tingkatkan kontras, konversi ke grayscale) sebelum memberi ke engine OCR. Beberapa pustaka menyediakan API `preprocess`. |

---

## Kesimpulan

Anda kini tahu **how to run OCR on image** file di Java, mulai dari memuat gambar hingga mengekstrak teks bersih dari kwitansi. Panduan ini mencakup **recognize text from PNG**, **extract text from receipt**, dan menampilkan **java OCR example** yang dapat Anda adaptasi ke proyek apa pun.  

Langkah selanjutnya? Coba matikan flag GPU untuk melihat perbedaan performa, bereksperimen dengan resolusi gambar yang berbeda, atau integrasikan parser berbasis regex untuk otomatis mengambil total. Jika Anda tertarik pada topik lanjutan, selidiki **OCR post‑processing**, **language model correction**, atau **batch processing pipelines**.

Selamat coding, semoga kwitansi Anda selalu dapat dibaca!  

![run OCR on image example](/images/run-ocr-on-image.png "run OCR on image – Java example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}