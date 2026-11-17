---
category: general
date: 2026-03-28
description: Priproses gambar untuk OCR dan kenali teks dari gambar dengan Aspose
  OCR. Pelajari cara mengekstrak teks dari foto, meningkatkan akurasi OCR langkah
  demi langkah.
draft: false
keywords:
- preprocess image for OCR
- recognize text from image
- extract text from photo
- improve OCR accuracy preprocessing
- Aspose OCR Java
- image preprocessing pipeline
language: id
og_description: Pra-proses gambar untuk OCR dan ekstrak teks dari foto dengan Aspose
  OCR Java. Ikuti tutorial ini untuk meningkatkan akurasi OCR melalui pra‑pemrosesan
  dalam beberapa langkah saja.
og_title: Pra-proses Gambar untuk OCR – Panduan Java Lengkap
tags:
- OCR
- Java
- Image Processing
title: Pra-pemrosesan Gambar untuk OCR – Tingkatkan Akurasi Ekstraksi Teks di Java
url: /id/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-text-extraction-accuracy-in-j/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pra‑pemrosesan Gambar untuk OCR – Panduan Java Lengkap

Pernah mencoba **preprocess image for OCR** dan masih mendapatkan output yang berantakan? Anda tidak sendirian. Dalam banyak proyek dunia nyata, pemindaian mentah atau foto smartphone mengandung kemiringan, noise, atau kontras rendah yang mengacaukan bahkan mesin pengenalan paling pintar. Kabar baik? Pipeline pra‑pemrosesan singkat—de‑skew, denoise, binarize—dapat secara dramatis **meningkatkan akurasi OCR pra‑pemrosesan**.

Dalam tutorial ini kami akan memandu Anda melalui contoh langsung yang menunjukkan secara tepat cara **recognize text from image** menggunakan Aspose OCR untuk Java. Pada akhir tutorial Anda akan dapat **extract text from photo** dengan jauh lebih sedikit kesalahan, dan Anda akan memahami mengapa setiap langkah pra‑pemrosesan penting.

> **Apa yang akan Anda dapatkan**  
> * Program Java yang dapat dijalankan sepenuhnya, memuat foto miring, menerapkan tiga filter klasik, dan mencetak teks bersih.  
> * Wawasan tentang “mengapa” di balik de‑skew, denoise, dan binarize.  
> * Tips menangani kasus tepi—file besar, format gambar berbeda, dan urutan filter khusus.

## Prerequisites

- Java 8 atau lebih baru terpasang (kode dapat dikompilasi dengan JDK 11 juga).  
- Maven atau Gradle untuk mengunduh pustaka Aspose OCR.  
- Contoh gambar (misalnya `angled-photo.jpg`) yang sedikit diputar dan mengandung sedikit noise visual.  
- Familiaritas dasar dengan metode `main` Java—tidak diperlukan keahlian OCR mendalam.

Jika Anda belum memiliki salah satu hal di atas, cukup unduh JDK terbaru dari Oracle atau OpenJDK dan tambahkan dependensi Maven berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the newest version -->
</dependency>
```

Sekarang, mari kita selami kode.

## Step 1 – Create the OCR Engine Instance

Hal pertama yang Anda perlukan adalah objek `OcrEngine`. Anggap saja ini sebagai otak yang nanti akan membaca gambar yang telah diproses.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Mengapa ini penting:** Mesin menyatukan pengaturan pengenalan, paket bahasa, dan—yang paling penting bagi kami—opsi pra‑pemrosesan. Tanpa mesin ini, Anda harus menautkan pustaka pemrosesan gambar secara manual, yang menghilangkan tujuan pipeline yang bersih.

## Step 2 – Build a Preprocessing Pipeline (de‑skew → denoise → binarize)

Aspose OCR menyertakan kelas `PreprocessingOptions` bawaan yang memungkinkan Anda menumpuk filter dalam urutan yang tepat. Di sini kami menambahkan tiga filter:

1. **DE_SKEW** – meluruskan teks yang diputar.  
2. **DENOISE** – menghaluskan piksel berbutir yang dapat disalahartikan sebagai karakter.  
3. **BINARIZE** – mengubah gambar menjadi hitam‑putih murni, memudahkan kerja mesin OCR.

```java
        // Step 2: Assemble the preprocessing pipeline
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);   // correct rotation
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);  // remove grain
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE); // high‑contrast B&W

        // Attach the pipeline to the OCR engine
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);
```

> **Pro tip:** Urutan filter sangat krusial. Jika Anda melakukan binarize *sebelum* denoise, noise dapat menjadi bintik hitam berbentuk tajam yang membingungkan pengenalan. De‑skew terlebih dahulu memastikan garis dasar teks horizontal, yang meningkatkan hasil denoise dan binarize.

## Step 3 – Feed the Image to the Engine

Sekarang kami mengarahkan mesin ke file yang ingin dibaca. Path dapat berupa absolut atau relatif terhadap root proyek Anda.

```java
        // Step 3: Run OCR on the target image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

> **Bagaimana jika gambar sangat besar?** Aspose OCR secara otomatis memperkecil gambar yang lebih besar dari 2000 px pada sisi terpanjang, tetapi Anda dapat menimpanya lewat `ocrEngine.getRecognitionSettings().setMaxImageDimension(1500)` jika memori menjadi masalah.

## Step 4 – Output the Recognized Text

Akhirnya, kami mencetak string yang diekstrak ke konsol. Dalam aplikasi nyata Anda mungkin menuliskannya ke basis data, file, atau mengirimnya ke pipeline NLP berikutnya.

```java
        // Step 4: Print the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Expected Output

Jika `angled-photo.jpg` berisi kalimat *“The quick brown fox jumps over the lazy dog.”* Anda akan melihat sesuatu seperti:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Perhatikan bagaimana outputnya bersih—tidak ada simbol asing, tidak ada baris terputus. Itulah kekuatan **preprocess image for OCR**.

## Step 5 – Verify and Tweak (Optional)

Meskipun pipeline sudah solid, Anda mungkin menemukan kasus tepi:

| Situasi | Saran penyesuaian |
|-----------|-----------------|
| **Very low contrast** (misalnya dokumen hasil scan yang pudar) | Sisipkan filter `ContrastAdjustment` tambahan sebelum binarisasi. |
| **Colorful background** (misalnya kwitansi dengan stempel berwarna) | Tambahkan filter `BackgroundRemoval` atau konversi ke grayscale terlebih dahulu. |
| **Multi‑page PDFs** | Loop melalui setiap gambar halaman dan gunakan kembali `preprocessingOptions` yang sama. |

Anda dapat bereksperimen dengan memanggil `preprocessingOptions.addFilter(PreprocessFilter.CONTRAST)` atau filter lain yang tercantum dalam dokumentasi API Aspose OCR.

## Full, Runnable Example

Berikut adalah program lengkap, siap disalin‑tempel ke file bernama `PreprocessExample.java`. Pastikan dependensi Maven sudah terpasang sebelum Anda mengompilasi.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing: de‑skew → denoise → binarize
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE);
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);

        // 3️⃣ Perform OCR on the chosen image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // 4️⃣ Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Compile and run:

```bash
mvn compile exec:java -Dexec.mainClass=PreprocessExample
```

Anda akan melihat teks bersih tercetak di konsol, mengonfirmasi bahwa Anda telah berhasil **preprocess image for OCR** dan **recognize text from image**.

## Common Questions & Answers

**Q1: Apakah ini bekerja dengan file PNG atau TIFF?**  
Ya—Aspose OCR mendukung JPEG, PNG, BMP, TIFF, dan beberapa format lainnya. Pipeline pra‑pemrosesan yang sama diterapkan; pustaka secara otomatis mendeteksi format.

**Q2: Bagaimana jika saya perlu mengekstrak teks dari foto yang diambil dengan ponsel?**  
Foto ponsel sering mengalami pencahayaan tidak merata. Menambahkan filter `LIGHTING_CORRECTION` sebelum binarisasi dapat membantu. Perubahan kode hanya satu baris:

```java
preprocessingOptions.addFilter(PreprocessFilter.LIGHTING_CORRECTION);
```

**Q3: Bisakah saya mengubah bahasa OCR?**  
Tentu saja. Setelah membuat mesin, atur bahasa:

```java
ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.SPANISH);
```

**Q4: Bagaimana ini meningkatkan akurasi OCR pra‑pemrosesan?**  
Setiap filter mengurangi jenis noise visual tertentu. De‑skew menyelaraskan baris teks, denoise menghilangkan bintik acak, dan binarize menciptakan gambar berkontras tinggi. Bersama‑sama mereka memberi algoritma pengenalan sinyal yang lebih bersih, yang diterjemahkan menjadi akurasi karakter yang lebih tinggi—seringkali peningkatan 15‑30 % pada input yang berisik.

## Next Steps & Related Topics

- **Batch processing:** Bungkus logika inti dalam loop untuk menangani seluruh folder foto.  
- **Custom filter order:** Bereksperimen dengan `BINARIZE` sebelum `DENOISE` untuk dokumen yang sudah berkontras tinggi.  
- **Performance tuning:** Gunakan `ocrEngine.getRecognitionSettings().setThreadCount(4)` untuk paralelisasi pada mesin multi‑core.  
- **Alternative libraries:** Bandingkan Aspose OCR dengan Tesseract‑Java untuk skenario open‑source.  
- **Post‑processing:** Terapkan pemeriksaan ejaan atau pembersihan regex pada output mentah untuk hasil yang lebih bersih.

Dengan menguasai alur kerja **preprocess image for OCR**, Anda akan menemukan bahwa mengekstrak teks dari sumber foto menjadi tugas yang dapat diprediksi dan dapat diulang, bukan eksperimen hit‑or‑miss.

---

*Siap meningkatkan pipeline OCR Anda? Ambil kode, sesuaikan filter, dan saksikan akurasi meningkat. Jika mengalami kendala, tinggalkan komentar di bawah—selamat coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}