---
date: 2026-06-24
description: Pelajari cara melakukan OCR teks gambar dengan pemilihan bahasa menggunakan
  Aspose.OCR untuk Java. Panduan langkah demi langkah ini mencakup ekstraksi teks
  java, koreksi skew OCR, dan lainnya.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Cara Melakukan Koreksi Skew OCR dan Pemilihan Bahasa dengan Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Cara Melakukan Koreksi Skew OCR dan Pemilihan Bahasa dengan Aspose.OCR
url: /id/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Melakukan Koreksi Skew OCR dan Pemilihan Bahasa dengan Aspose.OCR

## Pendahuluan

Mengekstrak teks dari file gambar adalah kebutuhan umum baik Anda sedang mendigitalkan dokumen yang dipindai, memproses kwitansi, atau membangun arsip yang dapat dicari. Dalam tutorial ini kami akan memandu Anda melalui contoh lengkap, langkah‑demi‑langkah yang menunjukkan **how to OCR image text** dengan pengaturan bahasa tertentu, sehingga Anda dapat mengintegrasikan OCR yang handal ke dalam aplikasi Java Anda hari ini. Anda juga akan melihat cara menangani **OCR skew correction** dan pengenalan berbasis wilayah untuk akurasi optimal, yang bersama‑sama dapat **improve OCR accuracy** hingga 30 % pada pemindaian yang miring.

## Jawaban Cepat
- **Apa perpustakaan yang menangani OCR di Java?** Aspose.OCR for Java  
- **Pengaturan mana yang memilih bahasa?** `settings.setLanguage(Language.Eng)` (or any supported language)  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi evaluasi gratis dapat digunakan untuk pengujian; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya membatasi OCR ke wilayah gambar?** Ya, gunakan `RecognitionSettings.setRecognitionAreas()` dengan persegi panjang.  
- **Berapa biasanya waktu eksekusi?** Beberapa detik per halaman pada laptop standar, tergantung ukuran gambar dan kompleksitas bahasa.  

`Language` adalah enumerasi yang mencantumkan bahasa OCR yang didukung oleh Aspose.OCR, seperti English, French, Spanish, dll.

## Apa itu OCR Skew Correction?

OCR skew correction adalah proses mendeteksi dan meluruskan baris teks yang miring sebelum pengenalan karakter. Dengan menyelaraskan garis dasar teks, mesin OCR dapat menerapkan model bahasa secara lebih efektif, mengurangi kesalahan pengenalan yang disebabkan oleh pemindaian yang miring. Langkah ini meningkatkan kualitas visual gambar masukan, memungkinkan algoritma pengenalan fokus pada bentuk karakter yang sebenarnya daripada distorsi akibat rotasi.

## Mengapa OCR Skew Correction Meningkatkan Akurasi

Ketika teks miring, bentuk karakter menjadi terdistorsi, yang dapat meningkatkan tingkat kesalahan hingga 20 %. Menerapkan **ocr skew correction** menghilangkan distorsi tersebut, memungkinkan mesin fokus pada glif yang sebenarnya. Dalam pengujian benchmark Aspose.OCR mencapai peningkatan akurasi pengenalan sebesar 15‑30 % pada dokumen dengan rotasi 10‑15° setelah menerapkan koreksi skew.

## Mengapa Menggunakan Aspose.OCR dengan Pemilihan Bahasa?

Memilih bahasa sumber teks secara tepat memungkinkan mesin OCR menggunakan kamus dan model karakter khusus bahasa, yang secara dramatis meningkatkan presisi pengenalan dan mengurangi waktu pemrosesan. Selain itu, Aspose.OCR menawarkan kontrol yang disesuaikan atas koreksi skew, pemilihan wilayah, dan format output, menjadikannya pilihan serbaguna untuk pipeline pemrosesan dokumen multibahasa.

- **Dukungan multibahasa** – Pilih bahasa yang tepat(s) yang ada dalam gambar Anda untuk meningkatkan akurasi.  
- **Kontrol yang disesuaikan** – Sesuaikan skew, definisikan wilayah pengenalan, dan atur perilaku auto‑skew.  
- **Pure Java API** – Tanpa ketergantungan native, mudah diintegrasikan ke proyek Java apa pun.  
- **Data hasil yang kaya** – Dapatkan teks polos, JSON, persegi pembatas, dan peringatan dalam satu panggilan.  
- **Kemampuan terkuantifikasi** – Aspose.OCR mendukung **50+** format input dan output serta dapat memproses batch gambar **500‑page** tanpa memuat seluruh dokumen ke memori.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- **Java Development Kit (JDK)** terpasang (JDK 8 atau lebih baru).  
- **Aspose.OCR for Java** library – unduh dari situs resmi [di sini](https://reference.aspose.com/ocr/java/).  
- File gambar yang berisi teks yang ingin Anda ekstrak, misalnya `p3.png`.  

## Impor Paket

Impor berikut memberi Anda akses ke kelas OCR inti dan utilitas Java standar.  
`import com.aspose.ocr.*;` – membawa mesin OCR utama.  
`import com.aspose.ocr.config.*;` – berisi objek konfigurasi seperti `RecognitionSettings`.  
`import java.awt.Rectangle;` – digunakan untuk mendefinisikan wilayah pengenalan.  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Cara Menerapkan OCR Skew Correction di Java?

Muat gambar, nonaktifkan deteksi skew otomatis, dan berikan sudut yang diukur atau biarkan mesin menghitungnya menggunakan `settings.setAutoSkew(false)`. Mesin OCR akan pertama‑tama meluruskan gambar berdasarkan sudut yang diberikan atau terdeteksi, kemudian melanjutkan dengan pengenalan karakter. Pendekatan dua langkah ini memastikan setiap kemiringan dihilangkan sebelum model bahasa diterapkan, menghasilkan output teks yang lebih bersih dan lebih sedikit kesalahan pengenalan.

## Panduan Langkah‑ demi‑Langkah

### Langkah 1: Siapkan Direktori Dokumen Anda

Buat objek `File` yang menunjuk ke folder yang berisi gambar sumber Anda. Ini membuat penanganan jalur menjadi portabel di berbagai sistem operasi.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Ganti `"Your Document Directory"` dengan jalur absolut tempat `p3.png` berada.

### Langkah 2: Tentukan Jalur Gambar

Instansiasi objek `File` untuk gambar spesifik yang ingin Anda proses. Menggunakan objek `File` memberi Anda akses mudah ke metadata file jika diperlukan nanti.

```java
// The image path
String file = dataDir + "p3.png";
```

Pastikan variabel `file` menunjuk ke gambar yang tepat yang ingin Anda proses.

### Langkah 3: Buat Instance API Aspose.OCR

Kelas `AsposeOCR` adalah titik masuk untuk semua operasi OCR. Ia mengenkapsulasi mesin, mengelola sumber daya, dan menyediakan metode `recognizePage`.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Objek `AsposeOCR` memberi Anda akses ke semua operasi OCR.

### Langkah 4: Atur Opsi Pengenalan (Pemilihan Bahasa)

`RecognitionSettings` adalah kontainer konfigurasi Aspose.OCR yang memungkinkan Anda menyesuaikan proses OCR.

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Di sini kami:

1. Menonaktifkan auto‑skew karena kami menyediakan nilai skew manual.  
2. Mendefinisikan wilayah persegi panjang (`RecognitionAreas`) untuk membatasi OCR pada bagian gambar yang memang berisi teks.  
3. Menetapkan **language** ke English (`Language.Eng`). Ubah ini menjadi `Language.Fra`, `Language.Spa`, dll., tergantung pada gambar sumber Anda.

### Langkah 5: Lakukan OCR dan Dapatkan Hasil

Memanggil `recognizePage` menjalankan mesin OCR menggunakan gambar dan pengaturan yang Anda definisikan. Hasilnya disimpan dalam objek `RecognitionResult`, yang mengagregasi semua data berguna.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Pemanggilan `RecognizePage` menjalankan mesin OCR menggunakan gambar dan pengaturan yang Anda definisikan. Hasilnya disimpan dalam objek `RecognitionResult`.

### Langkah 6: Cetak dan Manfaatkan Hasil

Output konsol menampilkan:

- Teks lengkap yang diekstrak (`recognitionText`).  
- Teks untuk setiap persegi panjang yang didefinisikan (`recognitionAreasText`).  
- Koordinat persegi pembatas.  
- Representasi JSON untuk pemrosesan lanjutan yang mudah.  
- Sudut skew yang terdeteksi dan peringatan apa pun.

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Output konsol menampilkan teks lengkap yang diekstrak, teks spesifik wilayah, kotak pembatas, JSON, sudut skew, dan peringatan. Anda kini dapat memasukkan `result.recognitionText` ke dalam logika bisnis Anda—menyimpannya, mengindeksnya, atau mengirimkannya ke layanan lain.

## Masalah Umum dan Solusinya

| Masalah | Penyebab | Solusi |
|---------|----------|--------|
| **Garbage characters** | Bahasa yang dipilih salah | Tetapkan enum `Language` yang benar (mis., `Language.Fra` untuk bahasa Prancis). |
| **No text returned** | Wilayah pengenalan tidak mencakup teks | Sesuaikan koordinat `Rectangle` atau hapus `RecognitionAreas` untuk memproses seluruh gambar. |
| **Slow performance** | Gambar sangat besar atau resolusi tinggi | Turunkan resolusi gambar sebelum OCR atau tingkatkan alokasi memori JVM. |
| **Warnings about unsupported format** | Format gambar tidak dikenali | Konversi gambar ke PNG, JPEG, atau TIFF sebelum diproses. |

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya mengenali beberapa bahasa dalam satu panggilan OCR?**  
A: Ya. Gunakan `settings.setLanguage(Language.Eng | Language.Fra)` untuk mengaktifkan pengenalan multibahasa.

**Q: Format gambar apa saja yang didukung Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF, dan beberapa lainnya. Cukup berikan jalur file yang benar.

**Q: Apakah ada batas ukuran untuk gambar?**  
A: Tidak ada batas keras, tetapi memproses gambar lebih besar dari 10 MB dapat meningkatkan penggunaan memori dan waktu eksekusi. Pertimbangkan untuk mengubah ukuran file besar.

**Q: Bagaimana cara mendapatkan lisensi produksi?**  
A: Beli lisensi dari situs web Aspose dan terapkan melalui kelas `License` seperti yang ditunjukkan dalam dokumentasi Aspose.

**Q: Bisakah saya mengekstrak teks langsung dari halaman PDF?**  
A: Tidak secara langsung dengan Aspose.OCR. Konversi halaman PDF ke gambar terlebih dahulu (mis., menggunakan Aspose.PDF) lalu jalankan OCR.

## Kesimpulan

Anda kini telah melihat cara **extract text from image** menggunakan Aspose.OCR untuk Java sambil memilih bahasa yang tepat dan menerapkan **OCR skew correction** untuk meningkatkan keandalan. Pendekatan ini memberikan OCR yang akurat dan berperforma tinggi yang dapat disematkan ke dalam alur kerja berbasis Java apa pun—dari sistem manajemen dokumen hingga pipeline penangkapan data. Bereksperimenlah dengan enum `Language` yang berbeda, sesuaikan `RecognitionAreas`, dan integrasikan output JSON ke dalam analitik lanjutan Anda untuk solusi yang benar‑benar end‑to‑end.

---

**Terakhir Diperbarui:** 2026-06-24  
**Diuji Dengan:** Aspose.OCR 24.11 for Java  
**Penulis:** Aspose

## Tutorial Terkait

- [Cara menghitung sudut skew java menggunakan Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Mengenali Dokumen PDF dalam Aspose.OCR untuk Java](/ocr/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}