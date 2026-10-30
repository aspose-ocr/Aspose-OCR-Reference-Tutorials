---
category: general
date: 2026-10-30
description: Pelajari cara mengekstrak teks dari gambar dengan cepat menggunakan dukungan
  Aspose OCR GPU di Java. Panduan ini menunjukkan cara mengatur GPU device ID dan
  mencapai OCR berkinerja tinggi.
draft: false
keywords:
- extract text from image
- how to extract text
- aspose ocr gpu
- recognize text image java
- gpu acceleration OCR
lastmod: 2026-10-30
og_description: Pelajari cara mengekstrak teks dari gambar dengan cepat menggunakan
  dukungan Aspose OCR GPU di Java. Panduan ini menunjukkan cara mengatur GPU device
  ID untuk kinerja optimal.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR GPU in Java'
og_title: Cara mengekstrak teks dari gambar dengan Aspose OCR GPU di Java
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to extract text from image quickly with Aspose OCR GPU support
    in Java. This guide shows how to set GPU device ID and achieve high‑performance
    OCR.
  headline: How to extract text from image with Aspose OCR GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—just install a valid Aspose OCR license. The free trial is for evaluation
      only.
    question: Can I use this in a commercial application?
  - answer: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed,
      the library runs on headless Linux environments.
    question: Does the GPU version work on Linux servers?
  - answer: Aspose OCR can process images up to **5000 × 5000 px** without loading
      the whole file into memory.
    question: What is the maximum image size supported?
  - answer: Replace the old JAR with the new one and update your Maven/Gradle dependency
      version number.
    question: How do I upgrade to the latest Aspose OCR version?
  - answer: Yes—`OcrResult` provides layout information, including word‑level bounding
      boxes, when you enable the `setIncludeLayout(true)` option.
    question: Is there a way to get bounding‑box coordinates for each word?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Cara mengekstrak teks dari gambar dengan Aspose OCR GPU di Java
url: /id/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekstrak teks dari gambar dengan Aspose OCR GPU di Java

Jika Anda pernah mencoba **mengekstrak teks dari gambar** dalam aplikasi Java dan menemukan CPU kewalahan dengan pemindaian resolusi tinggi, Anda tidak sendirian. Banyak pengembang mengalami bottleneck kinerja saat memproses dokumen besar. Aspose OCR untuk Java menghilangkan hambatan tersebut dengan memungkinkan Anda menjalankan OCR pada GPU, secara dramatis mengurangi waktu pemrosesan. Dalam tutorial ini Anda akan melihat contoh lengkap yang siap dijalankan yang menunjukkan cara mengatur lisensi, mengaktifkan percepatan GPU, dan **set gpu device id** ketika ada beberapa kartu grafis.

## Jawaban Cepat
- **Apa cara tercepat untuk mengekstrak teks dari gambar di Java?** Gunakan Aspose OCR dengan percepatan GPU dan atur GPU device ID yang sesuai.  
- **Versi Java mana yang diperlukan?** Java 17 atau yang lebih baru disarankan untuk kinerja terbaik.  
- **Apakah saya memerlukan lisensi untuk dukungan GPU?** Ya—fitur GPU hanya dapat diaktifkan dengan lisensi Aspose OCR yang valid.  
- **Bisakah saya menjalankannya di server tanpa tampilan (headless)?** Tentu saja; hanya driver GPU dan toolkit CUDA yang diperlukan.  
- **Berapa banyak bahasa yang didukung?** Lebih dari 30 bahasa, termasuk English, Chinese, Arabic, dan Hindi.

## Apa itu mengekstrak teks dari gambar?
Mengekstrak teks dari gambar berarti mengubah representasi visual karakter yang disimpan dalam format bitmap seperti PNG, JPG, atau TIFF menjadi teks Unicode yang dapat diedit dan dicari. Proses ini, yang dikenal sebagai Optical Character Recognition (OCR), memungkinkan tugas-tugas selanjutnya seperti pengindeksan, terjemahan, dan ekstraksi data.

## Mengapa menggunakan Aspose OCR GPU?
Aspose OCR memanfaatkan percepatan GPU untuk menangani gambar besar dengan resolusi tinggi jauh lebih efisien dibandingkan pemrosesan hanya dengan CPU. Ia mendukung lebih dari 30 format input dan dapat memproses gambar hingga 5000 × 5000 px sambil menjaga penggunaan memori tetap rendah, memberikan pengenalan hingga lima kali lebih cepat pada GPU NVIDIA modern.

## Apa yang Anda perlukan
- **Java 17** atau yang lebih baru (kompatibel dengan Java 8+, tetapi rilis LTS memberikan kinerja JIT yang lebih baik).  
- **Aspose OCR for Java** library (unduh JAR dari situs web Aspose).  
- File lisensi **Aspose OCR** yang valid (`Aspose.OCR.lic`). Versi percobaan gratis berfungsi, tetapi fitur GPU memerlukan versi berlisensi.  
- File gambar (`sample-image.png`) yang berisi teks yang jelas dan dapat dibaca mesin.  
- GPU NVIDIA yang kompatibel dengan CUDA (atau setara) dengan driver yang sesuai terpasang.

Jika ada yang terdengar tidak familiar, jangan khawatir—setiap poin akan dijelaskan seiring berjalan.

## Langkah 1: tambahkan Aspose OCR ke proyek Anda
Pertama, sertakan JAR Aspose OCR pada classpath Anda. Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Untuk Gradle, gunakan:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Jika Anda lebih suka cara manual, letakkan JAR ke dalam folder `libs/` dan tambahkan ke path modul IDE.

> **Pro tip:** Jaga nomor versi tetap sesuai dengan catatan rilis; versi yang lebih baru sering menyertakan peningkatan kinerja untuk pemrosesan GPU.

## Langkah 2: muat lisensi Aspose OCR (diperlukan untuk penggunaan GPU)
Tanpa lisensi, pemanggilan `setEnableGpu(true)` akan diam-diam kembali ke mode CPU. Muat lisensi tepat di awal `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Ganti `YOUR_DIRECTORY` dengan path absolut atau relatif tempat Anda menyimpan file `.lic`. Path yang salah akan memicu `FileNotFoundException`, jadi periksa kembali ejaannya.

## Langkah 3: buat mesin OCR dan aktifkan percepatan GPU
Kelas `OcrEngine` adalah komponen inti yang melakukan operasi OCR pada gambar.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Mengapa memperhatikan device ID? Dalam lingkungan multi‑GPU Anda dapat memperuntukkan satu kartu untuk preprocessing dan kartu lain untuk OCR. Menetapkan ID memastikan beban kerja berat dijalankan pada perangkat keras yang dimaksud.

## Langkah 4: siapkan gambar input
Kelas `OcrInput` mewakili kumpulan gambar yang ingin Anda proses.

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Jika Anda perlu memproses aliran (misalnya, file yang diunggah), gunakan `ocrInput.add(InputStream)` sebagai gantinya.

## Langkah 5: jalankan proses pengenalan dan ambil hasil
Kelas `OcrResult` mengenkapsulasi teks polos, skor kepercayaan, dan informasi tata letak opsional yang dikembalikan oleh mesin.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

Konsol akan menampilkan sesuatu seperti:

```
Recognized text:
Hello, world!
This is a sample image.
```

Jika gambar buram atau bahasa tidak didukung, hasilnya mungkin kosong. Dalam kasus tersebut, periksa nilai `ocrResult.getConfidence()` (0‑100) untuk memutuskan apakah harus mencoba lagi dengan preprocessing.

## Contoh lengkap yang dapat dijalankan
Menggabungkan semua bagian memberikan Anda satu kelas Java yang dapat Anda salin‑tempel ke IDE:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Expected output:** Konsol mencetak teks persis yang muncul di `sample-image.png`. Ketika GPU aktif, waktu pemrosesan biasanya turun dari beberapa detik (CPU) menjadi kurang dari satu detik untuk pemindaian 300 dpi tipikal.

## Pertanyaan umum & kasus tepi

### Apakah ini bekerja di server tanpa tampilan?
Ya. Driver GPU harus terpasang, tetapi tidak diperlukan tampilan. Pastikan toolkit `CUDA` (atau setara untuk GPU Anda) tersedia di `PATH` sistem. Pengaturan ini memungkinkan OCR berjalan di lingkungan berbasis cloud atau terkontainer tanpa antarmuka grafis.

### Bagaimana jika saya memiliki lebih dari satu GPU dan ingin menggunakan GPU 1?
Ubah device ID seperti yang ditunjukkan:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

Menetapkan ID ke `1` mengarahkan mesin OCR untuk menggunakan GPU kedua dalam sistem, yang dapat berguna ketika GPU pertama dicadangkan untuk beban kerja lain.

### Bagaimana cara mengekstrak teks dari gambar dalam bahasa lain?
Atur bahasa sebelum memanggil `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose OCR mendukung **lebih dari 30 bahasa**, termasuk skrip right‑to‑left seperti Arabic dan Hebrew. Memilih bahasa yang tepat secara dramatis meningkatkan akurasi.

### Bagaimana jika gambar berisi beberapa halaman (mis., PDF yang dikonversi menjadi gambar)?
Buat entri `OcrInput` terpisah untuk setiap halaman, atau lakukan loop pada file:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Mesin menggabungkan hasil secara berurutan, mempertahankan urutan halaman dalam output akhir.

### Bagaimana menangani hasil dengan kepercayaan rendah?
Periksa skor kepercayaan:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Langkah preprocessing umum meliputi binarisasi, pengurangan noise, atau mengubah ukuran menjadi 300 dpi. Menjalankan kembali OCR setelah preprocessing tersebut sering meningkatkan tingkat kepercayaan.

## Tips kinerja
- **Batch processing:** Menambahkan banyak gambar ke satu `OcrInput` mengurangi overhead inisialisasi konteks GPU berulang.  
- **Warm‑up:** Jalankan pengenalan dummy sekali setelah memulai JVM; panggilan pertama menimbulkan latensi inisialisasi driver.  
- **Memory management:** Buang objek `OcrInput` besar (`ocrInput.clear()`) setelah selesai untuk membebaskan memori GPU.  

## Kesimpulan
Anda sekarang tahu cara **mengekstrak teks dari gambar** secara efisien dengan mesin GPU Aspose OCR di Java, cara **set gpu device id** saat bekerja dengan beberapa kartu grafis, dan cara menangani skenario multibahasa. Kode lengkap yang dapat dijalankan di atas seharusnya langsung berfungsi—cukup ganti lisensi dan path gambar Anda.

Siap untuk langkah selanjutnya? Coba proses seluruh folder PDF yang dipindai, bereksperimen dengan opsi `setLanguage` yang berbeda, atau gabungkan output OCR dengan model machine‑learning untuk post‑processing. Peningkatan kinerja dari percepatan GPU membuat proyek berskala besar menjadi memungkinkan.

Selamat coding, dan silakan tinggalkan komentar jika Anda menemukan masalah!

## Pertanyaan yang sering diajukan

**Q: Bisakah saya menggunakan ini dalam aplikasi komersial?**  
A: Ya—cukup pasang lisensi Aspose OCR yang valid. Versi percobaan gratis hanya untuk evaluasi.

**Q: Apakah versi GPU bekerja di server Linux?**  
A: Tentu saja; selama driver NVIDIA dan toolkit CUDA terpasang, perpustakaan dapat berjalan di lingkungan Linux tanpa tampilan.

**Q: Berapa ukuran gambar maksimum yang didukung?**  
A: Aspose OCR dapat memproses gambar hingga **5000 × 5000 px** tanpa memuat seluruh file ke memori.

**Q: Bagaimana cara memperbarui ke versi Aspose OCR terbaru?**  
A: Ganti JAR lama dengan yang baru dan perbarui nomor versi dependensi Maven/Gradle Anda.

**Q: Apakah ada cara untuk mendapatkan koordinat bounding‑box untuk setiap kata?**  
A: Ya—`OcrResult` menyediakan informasi tata letak, termasuk bounding box tingkat kata, ketika Anda mengaktifkan opsi `setIncludeLayout(true)`.

**Last Updated:** 2026-10-30  
**Tested With:** Aspose OCR for Java 24.11  
**Author:** Aspose

## Tutorial Terkait

- [Mengenali Teks Dari Gambar Java Ocr Dengan Akselerasi GPU](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [Cara Mengaktifkan GPU Untuk OCR di Java Ekstrak Teks Dari Gambar](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [Ekstrak Teks Dari Gambar Dengan Aspose Ocr Java Panduan Cepat](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}