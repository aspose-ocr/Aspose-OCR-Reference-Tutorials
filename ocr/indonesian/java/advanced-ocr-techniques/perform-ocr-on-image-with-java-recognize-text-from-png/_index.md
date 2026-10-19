---
category: general
date: 2026-03-28
description: Lakukan OCR pada gambar menggunakan Aspose OCR di Java. Pelajari cara
  mengenali teks dari PNG dan meningkatkan akurasi OCR dengan koreksi ejaan bawaan.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- read image text
- improve OCR accuracy
- Aspose OCR Java
- spell correction OCR
language: id
og_description: Lakukan OCR pada gambar dengan Aspose OCR untuk Java. Panduan ini
  menunjukkan cara mengenali teks dari PNG dan meningkatkan akurasi OCR dalam hitungan
  menit.
og_title: Lakukan OCR pada Gambar dengan Java – Panduan Lengkap
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Lakukan OCR pada Gambar dengan Java – Kenali Teks dari PNG
url: /id/java/advanced-ocr-techniques/perform-ocr-on-image-with-java-recognize-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lakukan OCR pada Gambar dengan Java – Mengenali Teks dari PNG

Pernah membutuhkan untuk **perform OCR on image** file tetapi terus mendapatkan hasil yang berantakan? Anda tidak sendirian—pemindaian yang berisik, PNG dengan kontras rendah, dan font yang aneh dapat mengubah dokumen bersih menjadi kumpulan karakter yang kacau.  

Dalam panduan ini kami akan memandu Anda melalui contoh Java lengkap yang siap‑jalankan yang **recognize text from PNG** menggunakan Aspose OCR, dan kami juga akan menunjukkan cara **improve OCR accuracy** dengan fitur koreksi ejaan library. Pada akhir panduan, Anda akan dapat **read image text** secara andal, bahkan ketika sumbernya tidak sempurna.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan Aspose OCR untuk Java dalam proyek Maven.  
- Langkah-langkah tepat untuk **perform OCR on image** data, mulai dari memuat file hingga mengekstrak teks bersih.  
- Mengapa mengaktifkan koreksi ejaan dapat secara dramatis meningkatkan kualitas output.  
- Jebakan umum (file hilang, format tidak didukung) dan cara menanganinya dengan elegan.  
- Contoh kode lengkap yang siap‑copy‑paste yang dapat Anda jalankan hari ini.

### Prasyarat

- Java 8 atau lebih baru terpasang di mesin Anda.  
- Maven untuk manajemen dependensi (setiap IDE yang mendukung Maven dapat digunakan).  
- Gambar PNG yang berisi teks yang dapat dibaca—sebaiknya yang agak berisik sehingga Anda dapat melihat manfaat koreksi ejaan.

> **Pro tip:** Jika Anda tidak memiliki PNG yang siap pakai, ambil tangkapan layar dokumen apa saja atau foto tanda. Semakin “berisik” tampilannya, semakin Anda akan menghargai peningkatan akurasi.

---

## Langkah 1: Tambahkan Dependensi Aspose OCR

Pertama-tama—tambahkan library Aspose OCR ke `pom.xml` Anda. Baris tunggal ini mengambil versi terbaru (per Maret 2026) dan menyelesaikan semua dependensi transitive.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

> **Why this matters:** Tanpa library Anda tidak dapat membuat `OcrEngine`, dan seluruh alur kerja **perform OCR on image** akan gagal pada saat runtime.

---

## Langkah 2: Inisialisasi Mesin OCR

Membuat mesin ini sederhana, tetapi ada alasan halus untuk memisahkan inisialisasi dari pemanggilan pengenalan: ini memberi Anda tempat untuk menyesuaikan pengaturan seperti bahasa, DPI, atau, yang paling penting bagi kami, koreksi ejaan.

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {

    public static void main(String[] args) {
        try {
            // Step 2: Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Pro tip: you can set the language here if you need something other than English
            // ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

Perhatikan komentar—menetapkan bahasa dapat menjadi penyelamat ketika PNG Anda berisi karakter non‑English.

---

## Langkah 3: Aktifkan Koreksi Ejaan untuk **Improve OCR Accuracy**

Aspose OCR dilengkapi dengan modul koreksi ejaan bawaan yang berfungsi seperti kamus ringan. Mengaktifkannya hanya satu baris kode, namun dampaknya pada output akhir bisa sangat besar, terutama untuk gambar berisik.

```java
            // Step 3: Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);
```

> **What if you don’t need it?** Anda cukup mengatur flag menjadi `false`. Menonaktifkannya mungkin berguna untuk teks khusus domain di mana kamus akan menandai istilah sah sebagai kesalahan.

---

## Langkah 4: Muat dan Kenali PNG

Sekarang kita benar‑benar **read image text** dari file. Metode `recognizeImage` menerima string path, tetapi Anda juga dapat memberikannya `java.io.InputStream` jika Anda mengambil gambar dari basis data atau web.

```java
            // Step 4: Perform OCR on the input image
            String imagePath = "YOUR_DIRECTORY/noisy-image.png"; // replace with your actual path
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Jika file tidak ditemukan, Aspose melemparkan pengecualian yang deskriptif—tidak perlu Anda memeriksa `File.exists()` secara manual. Namun, membungkus pemanggilan dalam `try/catch` (seperti yang kami lakukan) memberi Anda pesan error yang bersih untuk pengguna akhir.

---

## Langkah 5: Keluarkan Teks yang Diperbaiki

Akhirnya, cetak hasil ke konsol. Dalam aplikasi dunia nyata Anda mungkin akan menulis ini ke basis data atau layanan hilir, tetapi konsol sangat cocok untuk demo cepat.

```java
            // Step 5: Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

**Expected output** (asumsikan PNG berisi frasa “Aspose OCR library” dengan sedikit noise):

```
Corrected text:
Aspose OCR library
```

Jika Anda menonaktifkan koreksi ejaan, Anda mungkin melihat sesuatu seperti “Asp0se OCR libr@ry” sebagai gantinya—itulah mengapa **improve OCR accuracy** penting.

---

## Langkah 6: Verifikasi Hasil – Apakah Itu Benar‑benar **Read Image Text**?

Memang menggoda untuk mempercayai output konsol begitu saja, tetapi pemeriksaan cepat dapat menyelamatkan Anda berjam‑jam kemudian. Berikut beberapa cara untuk memverifikasi teks yang diekstrak:

1. **Length check** – Bandingkan `ocrResult.getText().length()` dengan jumlah karakter yang diharapkan.  
2. **Keyword search** – Gunakan `String.contains("Aspose")` untuk memastikan istilah kunci muncul.  
3. **Unit test** – Jika Anda mengintegrasikan ini ke dalam sistem yang lebih besar, tulis tes JUnit yang memastikan output cocok dengan nilai yang diketahui baik.

```java
// Example sanity check
if (ocrResult.getText().contains("Aspose")) {
    System.out.println("✅ Text successfully read from image.");
} else {
    System.out.println("⚠️ Unexpected OCR result – consider tweaking settings.");
}
```

---

## Kasus Edge Umum & Cara Menanganinya

| Situasi | Mengapa Terjadi | Solusi Cepat |
|-----------|----------------|-----------|
| **File not found** | Path salah atau izin kurang | Verifikasi `imagePath` dan gunakan `Files.isReadable(Paths.get(imagePath))` sebelum memanggil `recognizeImage`. |
| **Unsupported format** | Aspose OCR mendukung PNG, JPEG, BMP, TIFF, dll. | Konversi gambar ke PNG terlebih dahulu (mis., dengan ImageIO) atau gunakan `ocrEngine.recognizeImage(InputStream)`. |
| **Very low DPI** | Mesin OCR membutuhkan setidaknya ~300 DPI untuk akurasi yang layak | Perbesar gambar menggunakan `BufferedImage` dan `Graphics2D` sebelum memberi ke mesin. |
| **Domain‑specific jargon** | Koreksi ejaan dapat mengganti istilah valid dengan kata kamus | Nonaktifkan koreksi ejaan (`setEnableSpellCorrection(false)`) atau sediakan kamus khusus melalui `ocrEngine.getRecognitionSettings().setCustomDictionary(...)`. |

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut seluruh file sumber, siap untuk dikompilasi dan dijalankan. Ganti `YOUR_DIRECTORY/noisy-image.png` dengan path aktual ke gambar uji Anda.

```java
import com.aspose.ocr.*;

public class SpellCorrectExample {
    public static void main(String[] args) {
        try {
            // Initialize the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Enable spell correction to improve OCR accuracy on noisy text
            ocrEngine.getRecognitionSettings().setEnableSpellCorrection(true);

            // Path to the PNG you want to process
            String imagePath = "YOUR_DIRECTORY/noisy-image.png";

            // Perform OCR on the input image
            OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

            // Output the corrected text
            System.out.println("Corrected text:\\n" + ocrResult.getText());

            // Simple verification that we actually read image text
            if (ocrResult.getText().toLowerCase().contains("aspose")) {
                System.out.println("✅ OCR succeeded – key term found.");
            } else {
                System.out.println("⚠️ OCR may need tweaking – key term missing.");
            }
        } catch (Exception e) {
            System.err.println("Error during OCR processing: " + e.getMessage());
        }
    }
}
```

Jalankan dengan:

```bash
mvn compile exec:java -Dexec.mainClass=SpellCorrectExample
```

Anda akan melihat **corrected text** tercetak, mengonfirmasi bahwa Anda telah berhasil **performed OCR on image** data.

---

## Ringkasan Visual

![Contoh perform OCR pada gambar](/images/ocr-example.png){alt="perform OCR on image – before and after spell correction"}

Screenshot menggambarkan PNG berisik di sebelah kiri dan output bersih yang telah dikoreksi ejaannya di sebelah kanan.

---

## Kesimpulan

Kami baru saja menelusuri solusi lengkap, end‑to‑end untuk cara **perform OCR on image** file menggunakan Aspose OCR untuk Java. Dengan mengaktifkan flag koreksi ejaan bawaan, Anda dapat **improve

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}