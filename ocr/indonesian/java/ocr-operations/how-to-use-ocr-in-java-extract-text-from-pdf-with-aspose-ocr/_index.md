---
category: general
date: 2026-02-17
description: Cara menggunakan OCR di Java untuk mengekstrak teks dari PDF, mengonversi
  PDF menjadi gambar, dan melakukan OCR pada file PDF yang dipindai menggunakan Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: id
og_description: Cara menggunakan OCR di Java untuk mengekstrak teks dari file PDF.
  Pelajari cara mengonversi PDF menjadi gambar dan mengenali PDF yang dipindai dengan
  Aspose.OCR.
og_title: Cara Menggunakan OCR di Java – Panduan Lengkap
tags:
- OCR
- Java
- Aspose
title: Cara Menggunakan OCR di Java – Ekstrak Teks dari PDF dengan Aspose.OCR
url: /id/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di Java – Ekstrak Teks dari PDF dengan Aspose.OCR

Pernah bertanya‑tanya **cara menggunakan OCR** untuk mengubah PDF yang dipindai menjadi teks yang dapat dicari? Anda tidak sendirian. Kebanyakan pengembang menemui kebuntuan ketika PDF datang sebagai sekumpulan gambar, dan pengekstrak teks biasa hanya mengembalikan kosong. Kabar baik? Dengan beberapa baris Java dan Aspose.OCR Anda dapat **mengekstrak teks dari PDF**, **mengonversi PDF ke gambar**, dan **mengenali PDF yang dipindai** dalam satu alur kerja yang mudah.

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui—dari melisensikan pustaka hingga mencetak hasil akhir. Pada akhir tutorial Anda akan memiliki program siap‑jalankan yang mengambil teks biasa dari laporan, faktur, atau ebook yang dipindai. Tanpa layanan eksternal, tanpa keajaiban—hanya kode Java murni yang Anda kendalikan.

## Apa yang Anda Butuhkan

- **Java Development Kit (JDK) 8+** – versi terbaru apa saja dapat dipakai.  
- **Aspose.OCR for Java** JAR (unduh dari situs Aspose).  
- **File lisensi Aspose.OCR yang valid** (`Aspose.OCR.lic`). Versi percobaan gratis dapat dipakai, tetapi lisensi membuka akurasi penuh.  
- **Contoh PDF yang dipindai** (misalnya `scanned-report.pdf`).  
- IDE atau editor teks sederhana plus terminal.

Itu saja. Tanpa Maven, tanpa Gradle, tanpa dependensi tambahan—hanya JAR Aspose.OCR di classpath Anda.

![how to use OCR example](image-placeholder.png "how to use OCR example")

## Langkah 1 – Muat Lisensi Aspose.OCR Anda (Mengapa Ini Penting)

Sebelum mesin dapat berjalan pada kecepatan penuh, Anda harus memberi tahu di mana lisensi berada. Melewatkan langkah ini memaksa pustaka masuk ke mode evaluasi, yang menambahkan watermark pada output dan mungkin membatasi akurasi.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Mengapa ini berhasil:** Kelas `License` membaca file `.lic` dan mendaftarkannya secara global. Setelah diatur, setiap `OcrEngine` yang Anda buat akan otomatis menggunakan fitur berlisensi.

## Langkah 2 – Buat OCR Engine (Mesin di Balik Keajaiban)

Instansi `OcrEngine` adalah pekerja keras yang memindai gambar dan menghasilkan teks. Anggaplah ini sebagai otak yang menafsirkan pola piksel.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Tips pro:** Anda dapat menyesuaikan bahasa, ambang kepercayaan, atau bahkan mengaktifkan akselerasi GPU melalui properti mesin. Untuk kebanyakan PDF berbahasa Inggris, nilai bawaan sudah cukup.

## Langkah 3 – Siapkan Input: Tambahkan PDF Anda (Mengonversi PDF ke Gambar di Balik Layar)

Aspose.OCR memperlakukan setiap halaman PDF sebagai gambar. Ketika Anda memanggil `addPdf`, pustaka secara diam‑diam meraster setiap halaman, yang persis diperlukan untuk **mengonversi PDF ke gambar** sebelum pengenalan.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**Apa yang terjadi:**  
- PDF dibuka.  
- Setiap halaman dirender pada 300 dpi (default) untuk mempertahankan detail karakter.  
- Objek bitmap yang dirender disimpan dalam koleksi `OcrInput`.

Jika Anda membutuhkan gambar mentah (untuk debugging atau pra‑pemrosesan khusus), panggil `ocrInput.getPages()` setelah langkah ini.

## Langkah 4 – Jalankan Proses OCR (Melakukan OCR pada PDF)

Sekarang pekerjaan berat dimulai. Metode `recognize` mengulangi setiap gambar, menjalankan algoritma pengenalan, dan menggabungkan hasil ke dalam `OcrResult`.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Mengapa ini penting:** `OcrResult` tidak hanya berisi teks biasa tetapi juga skor kepercayaan, kotak pembatas, dan referensi gambar asli. Untuk kebanyakan kasus penggunaan Anda cukup memanggil `getText()`.

## Langkah 5 – Ambil dan Tampilkan Teks yang Diekstrak

Akhirnya, ambil string teks biasa dari hasil dan cetak. Anda juga dapat menuliskannya ke file, memasukkannya ke indeks pencarian, atau mengalirkannya ke pipeline NLP selanjutnya.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### Output yang Diharapkan

Jika `scanned-report.pdf` berisi paragraf sederhana, Anda akan melihat sesuatu seperti:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

Pemformatan persis mencerminkan tata letak asli, mempertahankan jeda baris bila memungkinkan.

## Menangani Kasus Pinggiran Umum

### 1. PDF Multi‑Bahasa

Jika dokumen Anda berisi teks Prancis atau Spanyol, atur bahasa sebelum memanggil `recognize`:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Anda dapat menyediakan array bahasa agar mesin dapat mendeteksi secara otomatis.

### 2. Scan Resolusi Rendah

Saat berhadapan dengan scan 150 dpi, tingkatkan DPI rendering internal:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

DPI yang lebih tinggi meningkatkan kejelasan karakter tetapi memakan lebih banyak memori.

### 3. PDF Besar (Manajemen Memori)

Untuk PDF dengan puluhan halaman, proses dalam batch:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

Pendekatan ini mencegah heap JVM membengkak.

## Contoh Lengkap yang Siap‑Jalankan

Berikut adalah program lengkap—termasuk impor dan penanganan lisensi—sehingga Anda dapat menyalin‑tempel dan menjalankannya langsung.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

Jalankan dengan:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

Anda akan melihat teks yang diekstrak tercetak di konsol.

## Ringkasan – Apa yang Telah Kita Bahas

- **Cara menggunakan OCR** di Java dengan Aspose.OCR.  
- Alur kerja untuk **mengekstrak teks dari file PDF**.  
- Secara internal, pustaka **mengonversi PDF ke gambar** sebelum mengenali karakter.  
- Tips untuk **melakukan OCR pada PDF** dengan banyak bahasa, scan resolusi rendah, dan dokumen besar.  
- Contoh kode lengkap yang dapat dijalankan dan dapat dimasukkan ke proyek Java apa pun.

## Langkah Selanjutnya & Topik Terkait

Setelah Anda dapat **mengenali PDF yang dipindai**, pertimbangkan ide‑ide lanjutan berikut:

- **Pembuatan PDF yang Dapat Dicari** – menimpa teks OCR kembali ke PDF asli untuk membuat dokumen yang dapat dicari.  
- **Layanan Pemrosesan Batch** – bungkus kode dalam microservice Spring Boot yang menerima PDF melalui REST.  
- **Integrasi dengan Elasticsearch** – indeks teks yang diekstrak untuk pencarian full‑text cepat di repositori dokumen Anda.  
- **Pra‑Pemrosesan Gambar** – gunakan OpenCV untuk mengoreksi kemiringan atau menghilangkan noise pada halaman sebelum OCR demi akurasi yang lebih tinggi.

Setiap topik ini membangun di atas konsep inti yang telah kita bahas, jadi silakan bereksperimen dan biarkan mesin OCR melakukan pekerjaan berat.

---

*Selamat coding! Jika Anda mengalami kendala—seperti kesalahan lisensi atau hasil null yang tidak terduga—tinggalkan komentar di bawah. Saya selalu siap untuk sesi debugging.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}