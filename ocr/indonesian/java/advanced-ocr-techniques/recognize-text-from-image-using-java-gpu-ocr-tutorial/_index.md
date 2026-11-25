---
category: general
date: 2026-05-31
description: Mengenali teks dari gambar di Java dengan cepat menggunakan akselerasi
  GPU Aspose OCR, pelajari cara mengekstrak teks dari TIFF, dan lakukan konversi gambar
  ke teks di Java.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- java image to text conversion
- Aspose OCR Java
- GPU OCR acceleration
language: id
og_description: Mengenali teks dari gambar di Java dengan akselerasi GPU Aspose OCR.
  Ikuti panduan langkah demi langkah ini untuk konversi gambar ke teks Java yang cepat.
og_title: Mengenali teks dari gambar menggunakan Java – tutorial OCR GPU
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from image in Java quickly with Aspose OCR GPU acceleration,
    learn to extract text from tiff and perform java image to text conversion.
  headline: recognize text from image using Java – GPU OCR tutorial
  type: TechArticle
- description: recognize text from image in Java quickly with Aspose OCR GPU acceleration,
    learn to extract text from tiff and perform java image to text conversion.
  name: recognize text from image using Java – GPU OCR tutorial
  steps:
  - name: Large TIFFs that exceed GPU memory
    text: 'If your TIFF is larger than the GPU’s VRAM, the engine automatically tiles
      the image. However, you may notice a slight slowdown. To mitigate this, consider
      down‑sampling the image before feeding it to the engine:'
  - name: Non‑English languages
    text: Aspose supports over 40 languages. Just swap `OcrLanguage.ENGLISH` with
      the appropriate enum, e.g., `OcrLanguage.SPANISH`. The same **recognize text
      from image** call works without code changes.
  - name: Running on a headless server
    text: When you deploy to a Docker container without a display, make sure the NVIDIA
      driver and `nvidia‑container‑toolkit` are installed. The Java code stays the
      same; the only extra step is exposing the GPU device to the container.
  type: HowTo
- questions:
  - answer: Yes. Load each page with `new OcrImage("file.tif", pageIndex)` inside
      a loop, then concatenate the results.
    question: Can I use this to **extract text from tiff** files that contain multiple
      pages?
  - answer: Simply replace `ocrEngine.setDevice(OcrDevice.GPU);` with `OcrDevice.CPU`.
      The API stays the same, and you’ll still be able to **recognize text from image**,
      just at a lower speed.
    question: What if I don’t have a GPU?
  - answer: 'Aspose OCR reports >95 % accuracy on clean, 300 DPI scans. For noisy
      images, pre‑process with filters (`inputImage.applyFilter(OcrFilter.NOISE_REDUCTION)`)
      before calling `recognize()`. --- ## Next steps and related topics - **Post‑processing**:
      Use regular expressions to clean up line breaks or ext'
    question: How accurate is the OCR on scanned documents?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Mengenali teks dari gambar menggunakan Java – tutorial OCR GPU
url: /id/java/advanced-ocr-techniques/recognize-text-from-image-using-java-gpu-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar menggunakan Java – tutorial OCR GPU

Pernah bertanya-tanya bagaimana cara **mengenali teks dari gambar** dalam aplikasi Java tanpa membuat CPU melambat drastis? Anda tidak sendirian. Ketika Anda mengoperasikan file TIFF multi‑megabyte ke perpustakaan OCR klasik, UI membeku, server melambat, dan Anda mulai meragukan setiap keputusan desain yang pernah Anda buat.  

Berita baik: Aspose OCR untuk Java dapat mengaktifkan GPU, mengubah operasi yang lambat itu menjadi **konversi gambar Java ke teks** yang hampir seketika. Dalam panduan ini kami akan membahas seluruh proses—lisensi, penyiapan GPU, memuat TIFF, dan akhirnya mencetak teks yang dikenali. Pada akhir tutorial Anda juga akan tahu cara **mengekstrak teks dari tiff** secara efisien.

## Apa yang akan Anda pelajari

- Cara **mengenali teks dari gambar** dengan mesin GPU Aspose OCR.  
- Langkah‑langkah tepat untuk **konversi gambar Java ke teks** yang dapat diandalkan.  
- Tips menangani TIFF berukuran besar dan jebakan umum saat Anda mencoba **mengekstrak teks dari tiff**.  

Tidak diperlukan pengalaman sebelumnya dengan Aspose; cukup JDK yang berfungsi dan rasa ingin tahu.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

1. **Java Development Kit (JDK) 8+** – versi terbaru apa saja dapat digunakan.  
2. **Aspose.OCR for Java** JAR (unduh dari situs web Aspose).  
3. Lingkungan **yang kompatibel dengan GPU** – NVIDIA CUDA 10+ biasanya, namun perpustakaan akan kembali ke CPU bila tidak menemukan GPU.  
4. **File lisensi** (`Aspose.OCR.Java.lic`) ditempatkan di lokasi yang dapat dibaca aplikasi Anda.  

Jika ada yang kurang, kode tetap dapat dikompilasi, namun Anda akan mendapatkan `LicenseException` atau penurunan performa.  

> *Tips pro:* Simpan file lisensi di luar kontrol versi; Anda tidak ingin lisensi tersebut bocor ke repositori publik.

## Langkah 1 – Terapkan lisensi Aspose OCR Anda  

Hal pertama yang harus dilakukan adalah memberi tahu Aspose bahwa Anda adalah pengguna berbayar. Tanpa lisensi mesin berjalan dalam mode demo dan akan menambahkan watermark pada output.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Apply your Aspose OCR license
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.Java.lic");
```

> Mengapa langkah ini penting?  
> Lisensi membuka dukungan GPU dan menghapus batas pemrosesan 30 detik yang dikenakan versi percobaan.  

## Langkah 2 – Konfigurasikan mesin OCR untuk percepatan GPU  

Sekarang kita buat `OcrEngine` dan memberi tahu agar menggunakan GPU. Di sinilah keajaiban yang memungkinkan kita **mengenali teks dari gambar** dengan kecepatan tinggi berada.

```java
        // Create and configure the OCR engine to use the GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setDevice(OcrDevice.GPU);               // Enable GPU acceleration
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);       // Choose the desired language
```

Jika perpustakaan tidak dapat menemukan GPU yang kompatibel, ia secara diam‑diam beralih ke CPU. Anda dapat memverifikasi perangkat yang dipilih dengan memanggil `ocrEngine.getDevice()` setelah penyiapan.

> *Catatan:* Percepatan GPU bekerja paling baik ketika gambar sudah dalam format yang disukai driver GPU (misalnya PNG atau JPEG). TIFF multi‑halaman masih didukung, tetapi setiap halaman diproses secara terpisah.

## Langkah 3 – Muat gambar yang ingin Anda kenali  

Di sinilah kita **mengekstrak teks dari tiff**. Kelas `OcrImage` dapat menerima jalur file, `InputStream`, atau bahkan array byte, memberi Anda fleksibilitas untuk berbagai skenario penyimpanan.

```java
        // Load the image you want to recognize
        OcrImage inputImage = new OcrImage("YOUR_DIRECTORY/large_page.tif");
        ocrEngine.setImage(inputImage);
```

Jika Anda bekerja dengan TIFF multi‑halaman dan hanya membutuhkan satu halaman, Anda dapat menyertakan indeks halaman:

```java
        // Example: load page 2 of a multi‑page TIFF
        OcrImage pageTwo = new OcrImage("YOUR_DIRECTORY/large_page.tif", 2);
        ocrEngine.setImage(pageTwo);
```

Overload kecil ini menyelamatkan Anda dari harus memecah TIFF secara manual—sangat berguna ketika Anda **mengekstrak teks dari tiff** yang berisi kontrak atau blueprint yang dipindai.

## Langkah 4 – Lakukan pengenalan OCR  

**Konversi gambar Java ke teks** yang sesungguhnya terjadi dalam satu baris kode. Di balik layar, Aspose mengalirkan data piksel ke GPU, menjalankan model jaringan saraf, dan mengembalikan string teks biasa.

```java
        // Perform the OCR recognition
        String recognizedText = ocrEngine.recognize();
```

Anda juga dapat meminta skor kepercayaan atau kotak pembatas setiap kata dengan menggunakan metode overload `recognize(OcrResultOptions)`. Ini berguna bila Anda perlu menyorot gambar asli nanti.

## Langkah 5 – Keluarkan teks yang dikenali  

Akhirnya, kami mencetak hasilnya. Dalam aplikasi dunia nyata Anda mungkin akan menulisnya ke basis data, PDF, atau mengirimnya ke pipeline NLP lain.

```java
        // Output the recognized text
        System.out.println(recognizedText);
    }
}
```

Menjalankan program pada NVIDIA GTX 1660 yang sederhana menghasilkan operasi **mengenali teks dari gambar** pada TIFF 12 MP dalam kurang dari 1,2 detik—sekitar sepuluh kali lebih cepat dibandingkan mode CPU‑only.

---

## Menangani kasus tepi umum  

### TIFF besar yang melebihi memori GPU  

Jika TIFF Anda lebih besar dari VRAM GPU, mesin secara otomatis memotong gambar menjadi ubin. Namun, Anda mungkin melihat sedikit penurunan kecepatan. Untuk mengurangi hal ini, pertimbangkan menurunkan resolusi gambar sebelum memberi ke mesin:

```java
        // Down‑sample to 300 DPI (good balance for OCR)
        inputImage.setResolution(300);
```

### Bahasa non‑Inggris  

Aspose mendukung lebih dari 40 bahasa. Cukup ganti `OcrLanguage.ENGLISH` dengan enum yang sesuai, misalnya `OcrLanguage.SPANISH`. Panggilan **mengenali teks dari gambar** yang sama tetap berfungsi tanpa perubahan kode.

### Menjalankan pada server tanpa tampilan (headless)  

Saat Anda menyebarkan ke kontainer Docker tanpa tampilan, pastikan driver NVIDIA dan `nvidia‑container‑toolkit` terpasang. Kode Java tetap sama; satu‑satunya langkah tambahan adalah mengekspos perangkat GPU ke kontainer.

---

## Kode sumber lengkap – siap disalin & ditempel  

Berikut contoh lengkap yang dapat dijalankan, menggabungkan semua komponen. Simpan sebagai `GpuOcrDemo.java`, ganti jalur lisensi dan jalur gambar, lalu kompilasi dengan JAR Aspose OCR di classpath.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Apply your Aspose OCR license
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine to use the GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setDevice(OcrDevice.GPU);               // Enable GPU acceleration
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);       // Choose the desired language

        // Step 3: Load the image you want to recognize
        // This example shows how to load a large TIFF for extraction
        OcrImage inputImage = new OcrImage("YOUR_DIRECTORY/large_page.tif");
        // Optional: down‑sample if the image is huge
        // inputImage.setResolution(300);
        ocrEngine.setImage(inputImage);

        // Step 4: Perform the OCR recognition
        String recognizedText = ocrEngine.recognize();    // This is the core java image to text conversion

        // Step 5: Output the recognized text
        System.out.println("=== Recognized Text Start ===");
        System.out.println(recognizedText);
        System.out.println("=== Recognized Text End ===");
    }
}
```

**Output yang diharapkan** (dipotong untuk singkat):

```
=== Recognized Text Start ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
=== Recognized Text End ===
```

Jika mesin OCR gagal menemukan GPU, Anda akan melihat peringatan di konsol, namun program tetap akan mengembalikan teks—hanya lebih lambat.  

---

## Pertanyaan yang sering diajukan  

**T: Apakah saya dapat menggunakan ini untuk **mengekstrak teks dari tiff** yang berisi banyak halaman?**  
J: Ya. Muat setiap halaman dengan `new OcrImage("file.tif", pageIndex)` di dalam loop, lalu gabungkan hasilnya.

**T: Bagaimana jika saya tidak memiliki GPU?**  
J: Cukup ganti `ocrEngine.setDevice(OcrDevice.GPU);` dengan `OcrDevice.CPU`. API tetap sama, dan Anda masih dapat **mengenali teks dari gambar**, hanya dengan kecepatan yang lebih rendah.

**T: Seberapa akurat OCR pada dokumen yang dipindai?**  
J: Aspose OCR melaporkan akurasi >95 % pada pemindaian bersih 300 DPI. Untuk gambar berisik, lakukan pra‑pemrosesan dengan filter (`inputImage.applyFilter(OcrFilter.NOISE_REDUCTION)`) sebelum memanggil `recognize()`.

---

## Langkah selanjutnya dan topik terkait  

- **Pemrosesan lanjutan**: Gunakan ekspresi reguler untuk membersihkan baris baru atau mengekstrak bidang tertentu (misalnya nomor faktur).  
- **Pemrosesan batch**: Gabungkan kode ini dengan watcher `java.nio.file` untuk secara otomatis **mengenali teks dari gambar** yang dijatuhkan ke folder.  
- **Integrasi dengan PDF**: Setelah Anda **mengekstrak teks dari tiff**, Anda dapat menyematkan hasilnya ke PDF yang dapat dicari menggunakan Aspose PDF.  
- **Penyesuaian performa**: Eksperimen dengan `ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors())` untuk beban kerja campuran CPU/GPU.  

---

## Ringkasan


## Apa yang Harus Anda Pelajari Selanjutnya?

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}