---
category: general
date: 2026-06-19
description: Mengenali teks dari gambar menggunakan Aspose OCR di Java dan belajar
  mengonversi gambar ke docx, mengekstrak teks dari PNG, serta mengonversi gambar
  yang dipindai ke spreadsheet.
draft: false
keywords:
- recognize text from image
- convert image to docx
- extract text from png
- convert scanned image to spreadsheet
language: id
og_description: Mengenali teks dari gambar di Java menggunakan Aspose OCR. Ikuti tutorial
  langkah demi langkah ini untuk mengonversi gambar ke docx, mengekstrak teks dari
  png, dan mengonversi gambar yang dipindai ke spreadsheet.
og_title: Mengenali teks dari gambar dengan Aspose OCR – Panduan Java
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: recognize text from image using Aspose OCR in Java and learn to convert
    image to docx, extract text from png, and convert scanned image to spreadsheet.
  headline: recognize text from image with Aspose OCR – Java guide
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Mengenali Teks dari Gambar dengan Aspose OCR – Panduan Java
url: /id/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali teks dari gambar dengan Aspose OCR – Panduan Java

Pernah membutuhkan untuk **mengenali teks dari gambar** tetapi tidak yakin perpustakaan mana yang dapat menangani PDF berbahasa Jerman, PNG, dan bahkan menghasilkan spreadsheet? Anda tidak sendirian. Dalam tutorial ini kami akan membahas contoh lengkap Java yang tidak hanya mengekstrak karakter tetapi juga **mengonversi gambar ke docx**, **mengekstrak teks dari png**, dan bahkan **mengonversi gambar yang dipindai ke spreadsheet**—semua dengan beberapa baris kode.

Kami akan menggunakan Aspose.OCR, sebuah perpustakaan komersial yang dilengkapi dengan API yang sederhana. Jangan khawatir jika Anda tidak memiliki lisensi; demo ini berfungsi dalam mode evaluasi, meskipun beberapa fitur (seperti output resolusi tinggi) terbatas. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan yang mengambil screenshot PNG dari sebuah laporan dan secara otomatis menghasilkan file DOCX, XLSX, dan EPUB.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

* **Java Development Kit (JDK) 17** atau yang lebih baru terpasang.
* **Aspose.OCR for Java** JAR (unduh dari situs web Aspose atau tarik melalui Maven).
* File **Aspose.OCR.lic** opsional jika Anda menginginkan fungsionalitas penuh tanpa watermark evaluasi.
* Sebuah gambar contoh—misalnya `report.png`—diletakkan di folder yang dapat Anda referensikan dari kode.

Jika Anda menggunakan Maven, tambahkan dependensi ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

Setelah persiapan selesai, mari kita mulai.

## Langkah 1: mengenali teks dari gambar – terapkan lisensi (opsional)

Pertama-tama, kita perlu memberi tahu Aspose bahwa kita memiliki lisensi. Melewatkan langkah ini tidak akan merusak demo, tetapi Anda akan melihat banner “Evaluation” kecil di file output.

```java
import com.aspose.ocr.*;

public class ExportDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (optional for full functionality)
        License license = new License();
        try {
            license.setLicense("Aspose.OCR.lic");
            System.out.println("License loaded successfully.");
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }
```

> **Pro tip:** Simpan file `.lic` di samping JAR yang telah dikompilasi atau arahkan ke jalur absolut; jika tidak, pemanggilan `setLicense` akan menghasilkan error.

## Langkah 2: mengenali teks dari gambar – buat dan konfigurasikan mesin OCR

Sekarang kita memulai mesin OCR dan memberi tahu bahasa yang diharapkan. Pada contoh ini kita menangani bahasa Jerman, tetapi Aspose mendukung puluhan bahasa secara langsung.

```java
        // Create an OCR engine and set the recognition language to German
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(Language.German); // change to Language.English for English text
```

Mengapa mengatur bahasa? Mesin menggunakan kamus khusus bahasa untuk meningkatkan akurasi, terutama untuk karakter seperti “ß” atau “ü”. Jika Anda melewatkannya, Anda masih akan mendapatkan hasil, tetapi akan lebih berisik.

## Langkah 3: mengenali teks dari gambar – beri PNG dan dapatkan hasil mentah

Berikut inti demo: kami memberikan mesin jalur ke file PNG dan membiarkannya melakukan pekerjaan berat.

```java
        // Recognize text from the input image
        String inputImagePath = "YOUR_DIRECTORY/report.png"; // <-- replace with your actual path
        OcrResult ocrResult = ocrEngine.recognizeImage(inputImagePath);
        System.out.println("OCR completed. Extracted " + ocrResult.getText().length() + " characters.");
```

Objek `OcrResult` berisi string Unicode mentah, plus informasi tata letak yang dapat Anda gunakan nanti jika perlu mempertahankan format. Jika gambar adalah tabel yang dipindai, mesin tetap akan mengembalikan teks biasa—sempurna untuk langkah berikutnya di mana kami **mengonversi gambar yang dipindai ke spreadsheet**.

## Langkah 4: mengonversi gambar ke docx – menyimpan hasil sebagai dokumen Word

Aspose memudahkan mengekspor output OCR ke file DOCX. Ini berguna ketika Anda membutuhkan dokumen Word yang dapat diedit untuk proses selanjutnya.

```java
        // Save the recognized text in DOCX format
        String outputDocxPath = "YOUR_DIRECTORY/report.docx";
        ocrResult.save(outputDocxPath, OutputFormat.Docx);
        System.out.println("Saved DOCX to " + outputDocxPath);
```

Di balik layar, perpustakaan membuat dokumen Word sederhana dengan satu paragraf yang berisi teks yang diekstrak. Jika Anda membutuhkan gaya yang lebih kaya (judul, tabel), Anda dapat memproses DOCX lebih lanjut dengan Apache POI atau Aspose.Words nanti.

## Langkah 5: mengonversi gambar yang dipindai ke spreadsheet – mengekspor ke XLSX

Terkadang faktur yang dipindai atau tabel keuangan lebih mudah dikerjakan di Excel. `OcrResult` yang sama dapat disimpan sebagai file XLSX, dan Aspose akan berusaha mempertahankan struktur tabel saat mendeteksinya.

```java
        // Save the same result in additional formats (XLSX, EPUB)
        String outputXlsxPath = "YOUR_DIRECTORY/report.xlsx";
        ocrResult.save(outputXlsxPath, OutputFormat.Xlsx);
        System.out.println("Saved XLSX to " + outputXlsxPath);
```

Jika PNG asli berisi grid bersih, spreadsheet yang dihasilkan akan memiliki sel terpisah untuk setiap kolom. Jika tidak, Anda akan mendapatkan satu kolom dengan pemisah baris—tetap lebih baik daripada menyalin‑tempel secara manual.

## Langkah 6: mengekstrak teks dari png – juga mengekspor ke EPUB (opsional)

Untuk melengkapi, mari tunjukkan cara menghasilkan e‑book EPUB. Ini menunjukkan fleksibilitas metode `save` Aspose dan memberi Anda cara lain untuk **mengekstrak teks dari png** untuk publikasi.

```java
        // Optional: export to EPUB for e‑reading devices
        String outputEpubPath = "YOUR_DIRECTORY/report.epub";
        ocrResult.save(outputEpubPath, OutputFormat.Epub);
        System.out.println("Saved EPUB to " + outputEpubPath);
    }
}
```

Itulah seluruh program. Kompilasi dengan (`javac ExportDemo.java`) dan jalankan (`java ExportDemo`). Jika semuanya sudah diatur dengan benar, Anda akan melihat empat file muncul di `YOUR_DIRECTORY`: `report.docx`, `report.xlsx`, `report.epub`, dan konsol akan menampilkan jumlah karakter yang diekstrak.

## Kesalahan umum dan cara menghindarinya

| Masalah | Mengapa terjadi | Solusi |
|-------|----------------|-----|
| **Lisensi tidak ditemukan** | Jalur ke `Aspose.OCR.lic` salah atau tidak ada. | Letakkan file di samping JAR atau gunakan jalur absolut dalam `setLicense`. |
| **Karakter sampah** | Bahasa yang diatur salah (misalnya Inggris untuk teks Jerman). | Panggil `ocrEngine.setLanguage(Language.German)` atau enum bahasa yang tepat. |
| **File output kosong** | Typo pada jalur gambar input atau format tidak didukung. | Verifikasi jalur, pastikan file ada, dan bahwa itu merupakan format raster yang didukung (PNG, JPEG, BMP). |
| **Ukuran file besar** | Menggunakan gambar resolusi tinggi tanpa memperkecil ukuran. | Ubah ukuran gambar menjadi ~300 dpi sebelum OCR; Aspose dapat melakukannya secara otomatis melalui `ocrEngine.setResolution(300)`. |

## Memperluas solusi

Setelah Anda dapat **mengenali teks dari gambar** dan **mengonversi gambar yang dipindai ke spreadsheet**, Anda mungkin bertanya apa lagi yang dapat dilakukan:

* **Pemrosesan batch** – iterasi folder PNG dan menghasilkan ZIP file DOCX/XLSX.
* **Pemrosesan lanjutan** – gunakan ekspresi reguler untuk membersihkan noise OCR (mis., pemisah baris yang tidak diinginkan).
* **Integrasi** – sambungkan kode ke endpoint REST Spring Boot yang menerima unggahan gambar dan mengembalikan DOCX yang dapat diunduh.

Semua ide ini dibangun di atas langkah inti yang baru saja kami bahas.

## Kesimpulan

Anda baru saja mempelajari cara **mengenali teks dari gambar** menggunakan Aspose OCR untuk Java, dan kini Anda tahu cara **mengonversi gambar ke docx**, **mengekstrak teks dari png**, dan **mengonversi gambar yang dipindai ke spreadsheet** dengan hanya beberapa pemanggilan metode. Contoh lengkap yang dapat dijalankan di atas menunjukkan setiap impor, setiap konfigurasi, dan output tepat yang dapat Anda harapkan.

Selanjutnya, coba ganti bahasa ke Inggris, beri file TIFF multi‑halaman, atau rangkaikan output DOCX ke Aspose.Words untuk format lanjutan. Tidak ada batasan ketika Anda menggabungkan OCR dengan perpustakaan pembuatan dokumen.

Ada pertanyaan atau mengalami masalah? Tinggalkan komentar, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Mengonversi Gambar ke Teks dalam Java menggunakan Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Mengekstrak Teks dari Gambar Java dengan Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}