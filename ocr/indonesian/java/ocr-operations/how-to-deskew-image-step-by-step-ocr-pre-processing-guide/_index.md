---
category: general
date: 2026-02-19
description: Pelajari cara mengoreksi kemiringan gambar dan menghilangkan noise untuk
  OCR. Tutorial ini menunjukkan cara mengenali gambar teks, memperbaiki rotasi gambar,
  dan melakukan pra‑pemrosesan gambar OCR dengan Aspose OCR.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: id
og_description: Cara mengoreksi kemiringan gambar dan membersihkan noise sehingga
  Anda dapat mengenali teks gambar dengan cepat. Ikuti panduan ini untuk memperbaiki
  rotasi gambar dan memproses pra‑OCR gambar dengan Aspose.
og_title: Cara Meluruskan Gambar – Tutorial Lengkap Pra‑Pemrosesan OCR
tags:
- OCR
- Java
- Image Processing
title: Cara Mengoreksi Kemiringan Gambar — Panduan Pra‑Pemrosesan OCR Langkah demi
  Langkah
url: /id/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengoreksi Kemiringan Gambar — Tutorial Lengkap Pra‑Pemrosesan OCR

Pernah bertanya‑tanya **bagaimana cara mengoreksi kemiringan gambar** sebelum memberi makan ke mesin OCR? Mungkin Anda telah memindai sekumpulan kwitansi, dan halamannya tampak miring sedikit, atau hasil scan dipenuhi titik‑titik acak. Itu adalah masalah umum—gambar yang miring dan berisik membuat pengenalan teks terhambat.  

Kabar baik? Anda dapat meluruskan (mengoreksi rotasi gambar) dan menghilangkan noise (cara menghapus noise) hanya dengan beberapa baris Java menggunakan Aspose.OCR. Dalam panduan ini kami akan menelusuri seluruh alur: mulai dari memuat PNG yang berisik‑mirir, menerapkan deskew + median denoise, hingga **recognize text image** dan mencetak hasilnya. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dipakai ulang di proyek Java mana pun.

## Apa yang Anda Butuhkan

- **Java 17** atau lebih baru (kode dapat dikompilasi dengan versi lebih lama, tetapi 17 adalah pilihan ideal).  
- **Aspose.OCR untuk Java** – Anda dapat mengambil JAR terbaru dari Maven Central (`com.aspose:aspose-ocr`).  
- Sebuah file gambar yang sekaligus miring dan berisik (misalnya `noisy-rotated.png`).  
- IDE sederhana (IntelliJ, Eclipse, atau bahkan VS Code).  

Tidak diperlukan alat build yang rumit; cukup menjalankan `javac` + `java` sudah cukup.

---

## Langkah 1 – Buat Instance OCR Engine  

Hal pertama yang Anda lakukan adalah memulai sebuah `OcrEngine`. Anggap saja ini sebagai otak yang nanti akan membaca karakter untuk Anda.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Tip profesional:** Simpan engine sebagai singleton jika Anda memproses banyak gambar; ini akan menggunakan kembali buffer internal dan mempercepat proses.

## Langkah 2 – Aktifkan Deskew dan Median Denoise (Cara Menghapus Noise)

Sekarang kita memberi tahu engine untuk **mengoreksi rotasi gambar** dan **cara menghapus noise**. Kedua filter bersifat opsional, tetapi bila digabungkan secara signifikan meningkatkan akurasi.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

Mengapa median denoise? Karena ia mempertahankan tepi (garis yang mendefinisikan karakter) sambil menghilangkan piksel terisolasi—tepat apa yang dibutuhkan untuk OCR yang bersih.

## Langkah 3 – Muat Gambar yang Ingin Diproses  

Di sini kita menunjuk engine ke file yang perlu dibersihkan. `ImageStream.fromFile` membaca PNG ke dalam memori.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

Jika gambar Anda berada di server remote, cukup berikan sebuah `InputStream` saja—Aspose akan menanganinya dengan baik.

## Langkah 4 – Jalankan OCR dan Tangkap Teks yang Diakui  

Dengan pra‑pemrosesan diaktifkan, engine kini membaca gambar yang telah dikoreksi. Pemanggilan `recognize()` mengembalikan sebuah `RecognitionResult` yang berisi string hasil ekstraksi.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

Anda akan melihat teks yang bersih dan dapat dibaca di konsol, meskipun gambar asli miring dan berbutir.

## Langkah 5 – Verifikasi Hasil (Apa yang Diharapkan)

Ketika semuanya berjalan lancar, konsol akan mencetak sesuatu seperti:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

Jika output masih berisi karakter yang kacau, periksa kembali:

- Resolusi gambar (≥ 300 dpi ideal).  
- Apakah jalur file sudah benar.  
- Apakah filter tambahan (misalnya `setContrastStretch`) dapat membantu.

---

## Opsional: Konfirmasi Visual dengan Contoh Gambar  

Berikut adalah pratinjau kecil dari kwitansi yang miring dan berisik. Perhatikan kemiringannya—kode kami akan meluruskannya untuk Anda.

![how to deskew image example](deskew-demo.png "how to deskew image")

*Alt text: how to deskew image – before and after processing.*

---

## Pertanyaan yang Sering Diajukan

### Apakah ini bekerja dengan PDF atau hanya PNG/JPEG?  
Aspose.OCR dapat membaca PDF secara langsung; cukup ganti `ImageStream.fromFile` dengan `ImageStream.fromPdf`. Flag pra‑pemrosesan yang sama tetap berlaku, sehingga Anda tetap mendapatkan **how to deskew image** dan **how to remove noise**.

### Bagaimana jika saya perlu mempertahankan orientasi asli untuk langkah selanjutnya?  
Anda dapat mengkloning gambar sebelum pra‑pemrosesan:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### Bisakah saya mengubah sudut deskew secara manual?  
Ya—`setDeskewAngle(double degrees)` memungkinkan Anda menimpa algoritma deteksi otomatis. Berguna ketika deteksi otomatis gagal pada rotasi ekstrem.

### Bagaimana median denoise berbeda dari Gaussian blur?  
Filter median menggantikan setiap piksel dengan nilai median dari tetangganya, yang mempertahankan tepi. Gaussian blur menghaluskan semuanya, berpotensi mengaburkan goresan karakter—sehingga median lebih aman untuk OCR.

---

## Penutup  

Dalam tutorial ini kami membahas **how to deskew image**, mendemonstrasikan **how to remove noise**, dan menunjukkan cara **recognize text image** menggunakan pra‑pemrosesan bawaan Aspose OCR. Dengan mengaktifkan `setDeskew(true)` dan `setMedianDenoise(true)`, Anda secara otomatis **mengoreksi rotasi gambar** dan membersihkan bintik‑bintik, mengubah scan berantakan menjadi string teks yang bersih.  

Silakan bereksperimen: coba strategi denoise lain, proses PDF, atau rangkaian beberapa gambar dalam loop. Pola yang sama—engine → preprocess → recognize—berlaku untuk setiap skenario, menjadikannya fondasi yang solid untuk pipeline OCR apa pun.

**Langkah selanjutnya** yang dapat Anda jelajahi:

- **Pemrosesan batch** – iterasi melalui folder gambar dan tulis setiap hasil ke file `.txt`.  
- **Paket bahasa** – muat kamus bahasa tertentu untuk meningkatkan akurasi teks non‑Inggris.  
- **Filter lanjutan** – seperti `setContrastStretch` atau `setBinarization` untuk scan berkontras rendah.  

Punya pertanyaan lebih lanjut? Tinggalkan komentar, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}