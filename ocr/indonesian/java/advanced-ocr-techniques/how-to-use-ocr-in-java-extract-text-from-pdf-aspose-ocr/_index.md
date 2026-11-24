---
category: general
date: 2026-10-24
description: Pelajari cara menjalankan contoh Aspose OCR Java yang mengekstrak teks
  dari file PDF, termasuk pemrosesan OCR paralel, penanganan PDF yang dilindungi kata
  sandi, dan mengonversi PDF yang dipindai menjadi teks yang dapat dicari.
draft: false
keywords:
- aspose ocr java example
- parallel ocr processing
- extract text pdf java
- ocr password protected pdf
- convert scanned pdf searchable
lastmod: 2026-10-24
og_description: Jalankan contoh Aspose OCR Java untuk mengekstrak teks dari PDF dengan
  cepat. Panduan ini mencakup pemrosesan OCR paralel, PDF yang dilindungi kata sandi,
  dan mengonversi PDF yang dipindai menjadi dokumen yang dapat dicari.
og_image_alt: Screenshot of a Java console showing extracted text after parallel OCR
  processing with Aspose OCR
og_title: Contoh Aspose OCR Java – mengekstrak teks dari PDF dengan cepat
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  headline: 'Aspose OCR Java example: extract text from PDF quickly'
  type: TechArticle
- description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  name: 'Aspose OCR Java example: extract text from PDF quickly'
  steps:
  - name: set up your project
    text: 'Add the Aspose OCR dependency to your `pom.xml`: If you prefer Gradle,
      replace the snippet with the equivalent `implementation` line. After the dependency
      resolves, you can import the required classes in your Java source file.'
  - name: create and configure the OCR engine
    text: '`OcrEngine` is the core class that performs optical character recognition.
      The `OcrEngine` class is Aspose OCR''s primary object that encapsulates all
      OCR settings and execution logic. Enable parallel processing and optionally
      limit the thread pool: **Why this matters:** - `setParallelProcessing(true'
  - name: load the PDF you want to process
    text: '`OcrInput` represents the collection of files (PDFs, images, or mixed media)
      that the engine will analyze. The `OcrInput` class aggregates one or more input
      sources, allowing you to feed PDFs, TIFFs, or JPEGs to the OCR engine in a single
      batch. Add your PDF (or a set of PDFs) to the input collectio'
  - name: run OCR across all pages in parallel
    text: '`OcrResult` holds the combined text output and per‑page confidence information
      after recognition completes. The `OcrResult` object contains the concatenated
      plain‑text result and a list of `PageResult` objects that expose confidence
      scores for each processed page. Execute the recognition: **Under th'
  - name: retrieve and display the combined text
    text: '`OcrResult.getText()` returns the full searchable string. The `getText()`
      method of `OcrResult` returns a single `String` that contains the OCR‑extracted
      text from every page, with line breaks preserved as they appeared in the source
      PDF. **Expected output:** The console prints one continuous string'
  - name: handle special scenarios
    text: '#### How does the engine deal with password‑protected PDFs? Supply the
      password when adding the file to `OcrInput`: The `add` method overload that
      accepts a password decrypts the document on the fly, allowing seamless OCR without
      manual decryption.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR free trial works for development and testing; a commercial
      license is required for production deployments.
    question: Can I use this example with a free trial license?
  - answer: Absolutely – pass the password to `OcrInput.add(filePath, password)` and
      the engine will decrypt the document automatically.
    question: Does the example support OCR on password‑protected PDFs?
  - answer: Over 70 languages, including right‑to‑left scripts such as Arabic and
      Hebrew.
    question: How many languages does Aspose OCR recognise?
  - answer: The engine can handle multi‑hundred‑page PDFs; you can set a memory limit
      to keep RAM usage predictable.
    question: What is the maximum PDF size I can process?
  - answer: Yes, by configuring `setMaxThreadCount` you control the maximum number
      of concurrent threads, preventing resource exhaustion.
    question: Is parallel OCR safe on shared servers?
  type: FAQPage
tags:
- ocr
- java
- aspose
- pdf
title: 'Contoh Aspose OCR Java: mengekstrak teks dari PDF dengan cepat'
url: /id/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Contoh Aspose OCR Java: mengekstrak teks dari PDF dengan cepat

Dalam tutorial ini Anda akan menemukan **cara menggunakan contoh Aspose OCR Java** untuk mengubah PDF yang dipindai menjadi teks yang dapat dicari dan dapat dibaca mesin. Baik Anda memiliki satu file multi‑halaman atau sekumpulan PDF yang dilindungi password, langkah‑langkah di bawah ini menunjukkan cara mengonfigurasi mesin OCR, mengaktifkan pemrosesan paralel, dan mengambil output gabungan hanya dalam beberapa baris kode Java.

Anda juga akan belajar kapan menyesuaikan jumlah thread untuk kinerja optimal, cara menangani PDF terenkripsi, dan mengapa pendekatan ini ideal untuk mengonversi dokumen PDF yang dipindai menjadi arsip yang dapat dicari.

![cara menggunakan OCR dengan Aspose OCR Java](/images/ocr-parallel.png "Ilustrasi pemrosesan OCR paralel di Java – cara menggunakan OCR")
[cara menggunakan OCR dengan Aspose OCR Java](/images/ocr-parallel.png "Ilustrasi pemrosesan OCR paralel di Java – cara menggunakan OCR")

## Jawaban Cepat
- **Apa yang dilakukan contoh Aspose OCR Java?** Ia memuat PDF, menjalankan OCR pada setiap halaman secara paralel, dan mengembalikan teks yang dapat dicari lengkap sebagai satu string.  
- **Apakah dapat memproses PDF yang dilindungi password?** Ya – Anda dapat menyediakan password dokumen saat menambahkan file ke `OcrInput`.  
- **Apakah pemrosesan OCR paralel layak?** Pada mesin 4‑core, ini mengurangi waktu pemrosesan sebesar 30‑70 % untuk PDF dengan lebih dari lima halaman.  
- **Bahasa apa yang didukung?** Lebih dari 70 bahasa, termasuk Inggris, Prancis, Jerman, Mandarin, dan Arab.  
- **Apakah saya memerlukan lisensi untuk produksi?** Lisensi komersial Aspose OCR diperlukan untuk penggunaan non‑trial; versi percobaan gratis dapat digunakan untuk evaluasi.

## Apa itu contoh Aspose OCR Java?
**Contoh Aspose OCR Java** adalah program singkat yang dapat dijalankan yang menunjukkan cara menginstansiasi `OcrEngine`, mengonfigurasi eksekusi paralel, dan mengekstrak teks dari file PDF menggunakan pustaka Aspose OCR untuk Java. Contoh ini juga memperlihatkan cara menangani skenario umum seperti dokumen yang dilindungi password, penyesuaian batas memori, dan pemilihan bahasa, memberikan fondasi yang kuat untuk membangun pipeline pemrosesan dokumen yang lebih besar.

## Mengapa menggunakan pemrosesan OCR paralel?
Aspose OCR dapat membagi PDF multi‑halaman menjadi halaman terpisah dan memproses setiap halaman pada threadnya masing‑masing. Pada server 8‑core, dokumen 120‑halaman biasanya diproses dalam kurang dari 30 detik, dibandingkan lebih dari satu menit ketika dijalankan secara berurutan. Peningkatan kecepatan ini sangat berharga ketika Anda perlu **mengonversi arsip PDF yang dipindai menjadi dapat dicari** secara massal.

## Prasyarat
- Java 8 atau lebih baru terpasang.  
- Alat build Maven atau Gradle (contoh ini menggunakan Maven).  
- Lisensi Aspose OCR untuk Java (versi percobaan gratis dapat digunakan untuk pengujian).  

## Cara menjalankan contoh Aspose OCR Java langkah demi langkah

### Langkah 1: siapkan proyek Anda

Tambahkan dependensi Aspose OCR ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.11</version>
</dependency>
```

Jika Anda lebih suka Gradle, ganti potongan kode tersebut dengan baris `implementation` yang setara.  
Setelah dependensi terpasang, Anda dapat mengimpor kelas yang diperlukan dalam file sumber Java Anda.

### Langkah 2: buat dan konfigurasikan mesin OCR

`OcrEngine` adalah kelas inti yang melakukan pengenalan karakter optik.

Kelas `OcrEngine` adalah objek utama Aspose OCR yang mengenkapsulasi semua pengaturan OCR dan logika eksekusi.  
Aktifkan pemrosesan paralel dan secara opsional batasi kumpulan thread:

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**Mengapa ini penting:**  
- `setParallelProcessing(true)` mendistribusikan halaman ke beberapa inti CPU, memotong waktu eksekusi secara dramatis pada perangkat keras multi‑core.  
- `setMaxThreadCount` melindungi sumber daya server dengan mencegah mesin menguasai semua inti, yang penting dalam lingkungan shared‑hosting atau CI.

### Langkah 3: muat PDF yang ingin diproses

`OcrInput` mewakili kumpulan file (PDF, gambar, atau media campuran) yang akan dianalisis oleh mesin.

Kelas `OcrInput` menggabungkan satu atau lebih sumber input, memungkinkan Anda memasukkan PDF, TIFF, atau JPEG ke mesin OCR dalam satu batch.  
Tambahkan PDF Anda (atau sekumpulan PDF) ke koleksi input:

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**Tip:** Gunakan path absolut atau path relatif terhadap direktori kerja untuk menghindari `FileNotFoundException`. Metode `add` dapat dipanggil berulang kali untuk mengantri beberapa dokumen untuk pemrosesan batch.

### Langkah 4: jalankan OCR pada semua halaman secara paralel

`OcrResult` menyimpan output teks gabungan dan informasi kepercayaan per‑halaman setelah pengenalan selesai.

Objek `OcrResult` berisi hasil teks polos yang digabungkan dan daftar objek `PageResult` yang menampilkan skor kepercayaan untuk setiap halaman yang diproses.  
Jalankan pengenalan:

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Di balik layar:** Setiap halaman diberikan ke thread pekerja terpisah (hingga `maxThreadCount` yang Anda tentukan). Library menyinkronkan hasil sehingga `OcrResult` akhir mempertahankan urutan halaman asli.

### Langkah 5: ambil dan tampilkan teks gabungan

`OcrResult.getText()` mengembalikan string yang dapat dicari lengkap.

Metode `getText()` dari `OcrResult` mengembalikan satu `String` yang berisi teks hasil OCR dari setiap halaman, dengan jeda baris dipertahankan sebagaimana muncul di PDF sumber.  

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**Output yang diharapkan:** Konsol mencetak satu string kontinu yang berisi teks yang dapat dibaca dari semua halaman, siap untuk diindeks, disimpan, atau diproses lebih lanjut.

### Langkah 6: tangani skenario khusus

#### Bagaimana mesin menangani PDF yang dilindungi password?

Berikan password saat menambahkan file ke `OcrInput`:

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

Overload metode `add` yang menerima password mendekripsi dokumen secara langsung, memungkinkan OCR tanpa dekripsi manual.

#### Bagaimana saya dapat membatasi penggunaan memori untuk file sangat besar?

Panggil `ocrEngine.setMemoryLimit(256);` untuk membatasi konsumsi RAM pada 256 MB. Mesin akan secara otomatis memindahkan data berlebih ke file sementara, mencegah crash out‑of‑memory bahkan pada PDF ratusan halaman.

## Pertanyaan umum & kasus tepi

### Apakah saya benar‑benar membutuhkan pemrosesan paralel?

Jika PDF Anda berisi **lebih dari beberapa halaman** dan Anda memiliki setidaknya empat inti CPU, mengaktifkan pemrosesan paralel biasanya mengurangi total waktu eksekusi sebesar **30‑70 %**. Untuk pemindaian satu halaman, overhead threading mungkin melebihi manfaatnya, sehingga Anda dapat menonaktifkannya dengan `ocrEngine.setParallelProcessing(false)`.

### Apa yang terjadi ketika sebuah halaman gagal OCR?

Aspose OCR melempar `OcrException` hanya untuk kesalahan fatal seperti file yang rusak. Halaman yang tidak dapat dikenali hanya mengembalikan string kosong, yang kemudian digabungkan mesin secara diam‑diam. Anda dapat memeriksa `ocrResult.getPageResults()` untuk mendapatkan skor kepercayaan per‑halaman dan menangani halaman dengan kepercayaan rendah secara manual.

### Bagaimana cara mengubah bahasa pengenalan?

Mesin secara default menggunakan bahasa Inggris, tetapi Anda dapat mengganti bahasa dengan:

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing and optionally limit threads
        ocrEngine.setParallelProcessing(true);
        ocrEngine.setMaxThreadCount(4); // Adjust based on your hardware

        // Step 3: Load the multi‑page PDF to be processed
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");
        // Uncomment and set password if needed:
        // ocrInput.add("protected.pdf", "mySecretPassword");

        // Step 4: Recognize text from all pages in parallel
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the combined OCR result
        System.out.println("Combined text from all pages:");
        System.out.println(ocrResult.getText());
    }
}
```

Ganti `Language.FRENCH` dengan enum bahasa yang didukung apa pun. Ini penting ketika Anda perlu **mengekstrak teks PDF Java** dari dokumen multibahasa.

## Tips pro untuk OCR siap produksi

- **Pemrosesan batch:** Bungkus alur dalam loop yang membaca nama file dari direktori, mengubah demo menjadi layanan yang dapat diskalakan.  
- **Logging:** Atur `ocrEngine.setLogLevel(LogLevel.ERROR)` di produksi untuk menekan output yang berlebihan.  
- **Pembersihan hasil:** Proses lanjutan `ocrResult.getText()` dengan ekspresi reguler untuk menghapus spasi berlebih atau artefak.  
- **Penyesuaian thread‑pool:** Gunakan `ocrEngine.setMaxThreadCount(Runtime.getRuntime().availableProcessors())` pada server dengan banyak inti untuk throughput maksimum.  
- **Benchmark kinerja:** Pada Intel Xeon 8‑core, PDF 200‑halaman (300 MB) diproses dalam ~22 detik dengan OCR paralel diaktifkan.

## Kesimpulan

Anda kini memiliki **contoh Aspose OCR Java** lengkap yang mengekstrak teks yang dapat dicari dari PDF yang dipindai apa pun, mendukung file yang dilindungi password, dan memanfaatkan pemrosesan paralel untuk kecepatan. Dengan mengintegrasikan kode ini ke dalam aplikasi Anda, Anda dapat membangun pipeline digitalisasi dokumen yang kuat, memasukkan output OCR ke indeks pencarian, atau menggabungkannya dengan layanan terjemahan untuk arsip multibahasa.

Siap untuk langkah berikutnya? Coba alirkan teks yang diekstrak ke Elasticsearch untuk pencarian full‑text, atau rangkaikan output dengan API terjemahan bahasa untuk membuat repositori multibahasa yang dapat dicari. Selamat coding!

---

**Terakhir Diperbarui:** 2026-10-24  
**Diuji Dengan:** Aspose OCR for Java 24.11  
**Penulis:** Aspose  

## Pertanyaan yang Sering Diajukan

**Q: Dapatkah saya menggunakan contoh ini dengan lisensi percobaan gratis?**  
A: Ya, percobaan gratis Aspose OCR dapat digunakan untuk pengembangan dan pengujian; lisensi komersial diperlukan untuk penerapan produksi.

**Q: Apakah contoh ini mendukung OCR pada PDF yang dilindungi password?**  
A: Tentu – berikan password ke `OcrInput.add(filePath, password)` dan mesin akan mendekripsi dokumen secara otomatis.

**Q: Berapa banyak bahasa yang dikenali Aspose OCR?**  
A: Lebih dari 70 bahasa, termasuk skrip kanan‑ke‑kiri seperti Arab dan Ibrani.

**Q: Apa ukuran PDF maksimum yang dapat saya proses?**  
A: Mesin dapat menangani PDF ratusan halaman; Anda dapat menetapkan batas memori untuk menjaga penggunaan RAM tetap dapat diprediksi.

**Q: Apakah OCR paralel aman pada server bersama?**  
A: Ya, dengan mengonfigurasi `setMaxThreadCount` Anda mengontrol jumlah maksimum thread bersamaan, mencegah kehabisan sumber daya.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

```bash
javac -cp "path/to/aspose-ocr.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
```

## Tutorial Terkait

- [Cara Menggunakan OCR di Java dengan Pemrosesan Paralel Menggunakan Aspose](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/)
- [Buat PDF Dapat Dicari dengan Panduan Aspose OCR Java](/ocr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/)
- [Cara Menggunakan OCR di Java untuk Mengekstrak Teks Dari PDF Aspose OCR](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}