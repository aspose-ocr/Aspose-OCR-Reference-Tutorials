---
category: general
date: 2026-03-18
description: Cara meluruskan gambar dengan cepat menggunakan Aspose OCR Java. Pelajari
  cara pra‑proses gambar untuk OCR, membersihkan gambar yang dipindai, dan meningkatkan
  akurasi OCR dalam beberapa langkah saja.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: id
og_description: Cara mengoreksi kemiringan gambar dengan Aspose OCR Java, memproses
  gambar untuk OCR, membersihkan gambar hasil pemindaian, dan meningkatkan akurasi
  OCR.
og_title: Cara Mengoreksi Kemiringan Gambar untuk OCR – Panduan Java
tags:
- OCR
- Java
- Image Processing
title: Cara Mengoreksi Kemiringan Gambar untuk OCR – Panduan Pra‑Pemrosesan Java
url: /id/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Meluruskan Gambar untuk OCR – Panduan Pra‑Pemrosesan Java

Pernah bertanya‑tanya **cara meluruskan gambar** yang keluar dari pemindai dengan sudut yang aneh? Anda bukan satu‑satunya—banyak pengembang mengalami masalah ini ketika mencoba mengekstrak teks dari dokumen yang penuh gambar. Kabar baiknya? Dengan beberapa baris kode Java dan Aspose OCR Anda dapat meluruskan, mengurangi noise, dan mengambil teks bersih tanpa susah payah.

Dalam tutorial ini kami akan membahas seluruh alur kerja: memuat pemindaian yang berisik dan terputar, menerapkan filter meluruskan, menghilangkan gangguan visual, dan akhirnya **mengekstrak teks dari gambar**. Pada akhir tutorial Anda akan tahu cara **memproses gambar untuk OCR**, **membersihkan gambar yang dipindai**, dan **meningkatkan akurasi OCR** untuk proyek apa pun yang membutuhkan ekstraksi teks yang andal.

## Apa yang Anda Butuhkan

- Java 17 (atau JDK terbaru) – kode menggunakan fitur bahasa standar.
- Perpustakaan Aspose OCR untuk Java (versi percobaan gratis sudah cukup untuk percobaan).
- Contoh gambar yang berisik dan terputar (misalnya `noisy-rotated.png`).
- IDE favorit Anda (IntelliJ IDEA, Eclipse, VS Code…) – apa saja yang dapat mengompilasi Java.

Tidak diperlukan kerangka kerja tambahan, tidak ada keajaiban Maven/Gradle; satu‑satunya pernyataan impor hanyalah yang ditampilkan di bawah ini.

---

## Cara Meluruskan Gambar dengan Aspose OCR

Hal pertama yang harus diatasi adalah kemiringan gambar. Jika baris teks tidak horizontal, mesin OCR akan salah membaca karakter. `DeskewFilter` melakukan pekerjaan berat tersebut.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **Mengapa ini penting:** `DeskewFilter` menganalisis geometri gambar, memperkirakan sudut rotasi, dan memutar bitmap kembali ke horizon yang rata. Tanpa langkah ini kebanyakan mesin OCR memperlakukan huruf miring sebagai glyph yang sepenuhnya berbeda, menurunkan upaya **meningkatkan akurasi OCR** Anda ke dalam lubang kelinci.
> 
> **Tip profesional:** Jika Anda menangani dokumen yang mungkin terbalik, aktifkan flag `setAutoRotate` pada `DeskewFilter` (tersedia pada rilis Aspose yang lebih baru). Ia secara otomatis membalik 180° bila diperlukan.

![Diagram yang menunjukkan sebelum dan sesudah rotasi – cara meluruskan gambar](https://example.com/deskew-diagram.png "contoh cara meluruskan gambar")

*Teks alt gambar: contoh cara meluruskan gambar*

---

## Memproses Gambar untuk OCR – Pengurangan Noise dan Pembersihan

Setelah gambar lurus, tantangan berikutnya adalah noise visual—bintik‑bintik, artefak kompresi, atau pola latar belakang samar yang membingungkan mesin OCR. `DenoiseFilter` menerapkan algoritma penyamaran halus yang mempertahankan tepi (huruf) sambil menghilangkan butir‑butir.

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### Kapan Menyesuaikan Pengaturan Denoising

- **Pemindaian sangat gelap:** Tingkatkan kekuatan filter (`denoiseFilter.setStrength(2)`) untuk menghapus bayangan latar belakang.
- **Font cetak halus:** Turunkan kekuatan agar tidak mengaburkan serif kecil.
- **Dokumen berwarna:** Konversi ke skala abu‑abu terlebih dahulu (`scannedImage = scannedImage.toGrayscale();`)—mesin OCR bekerja paling baik pada gambar satu kanal.

Penyesuaian ini merupakan bagian dari praktik terbaik **membersihkan gambar yang dipindai**; bitmap yang lebih bersih secara langsung meningkatkan skor kepercayaan dari mesin OCR.

---

## Mengekstrak Teks dari Gambar – Menjalankan Mesin OCR

Sekarang gambar sudah lurus dan bersih, saatnya **mengekstrak teks dari gambar**. Kelas `OcrEngine` menangani semuanya di balik layar: segmentasi, klasifikasi karakter, dan pemodelan bahasa.

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### Output yang Diharapkan

Jika file sumber Anda berisi baris “**Invoice # 12345**”, konsol seharusnya mencetak sesuatu seperti:

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

Jika output terlihat berantakan, periksa kembali langkah‑langkah sebelumnya—khususnya proses meluruskan. Bahkan kemiringan 1‑derajat saja dapat merusak angka dan simbol.

---

## Kesalahan Umum & Tips untuk **Meningkatkan Akurasi OCR**

| Masalah | Mengapa mengurangi akurasi | Solusi cepat |
|---------|---------------------------|--------------|
| **Rotasi residual** | OCR mengharapkan baseline horizontal. | Verifikasi dengan `deskewFilter.getAngle()` dan catat nilainya. |
| **Over‑denoising** | Memburamkan goresan tipis, mengubah “i” menjadi “l”. | Gunakan `setStrength(0.5)` untuk font yang halus. |
| **Format gambar salah** | Kompresi JPEG menambah artefak. | Pilih PNG atau TIFF untuk penyimpanan lossless. |
| **Bahasa salah** | Mesin default ke Bahasa Inggris; alfabet lain memerlukan pengaturan eksplisit. | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **DPI rendah (≤150)** | Tidak cukup data piksel untuk segmentasi yang dapat diandalkan. | Resample ke 300 DPI sebelum pemrosesan (`scannedImage = scannedImage.resample(300);`). |

### Bonus: Pemrosesan Batch

Jika Anda memiliki folder berisi banyak pemindaian, bungkus demo dalam loop:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

Pola ini memungkinkan Anda **memproses gambar untuk OCR** secara skala, menjaga basis kode tetap rapi dan kinerja dapat diprediksi.

---

## Ringkasan & Langkah Selanjutnya

Kami telah membahas **cara meluruskan gambar**, **memproses gambar untuk OCR**, dan akhirnya **mengekstrak teks dari gambar** menggunakan Aspose OCR Java. Dengan meluruskan pemindaian, membersihkan noise, dan memberi bitmap yang bersih kepada mesin, Anda akan **meningkatkan akurasi OCR** secara signifikan di semua proyek.

Apa selanjutnya? Pertimbangkan ekstensi berikut:

- **Deteksi bahasa** – ubah `ocrEngine.setLanguage` berdasarkan skrip yang terdeteksi.
- **Output PDF** – alirkan teks yang dikenali ke generator PDF untuk dokumen yang dapat dicari.
- **Pemrosesan pasca‑machine‑learning** – jalankan pemeriksaan ejaan atau kamus khusus pada hasil OCR.

Cobalah ide‑ide tersebut, eksperimen dengan kekuatan filter yang berbeda, dan Anda akan segera memiliki pipeline yang kuat untuk proyek digitalisasi dokumen apa pun.

---

*Selamat coding! Jika Anda menemui kendala, tinggalkan komentar di bawah—saya akan membantu Anda menyesuaikan parameter meluruskan dan mengurangi noise.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}