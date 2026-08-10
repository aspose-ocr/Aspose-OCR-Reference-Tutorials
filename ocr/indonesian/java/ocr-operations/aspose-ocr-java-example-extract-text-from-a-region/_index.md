---
category: general
date: 2026-05-03
description: Contoh Aspose OCR Java menunjukkan cara memuat gambar untuk OCR dan mengekstrak
  teks dari sebuah area hanya dalam beberapa baris kode.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: id
og_description: Contoh Aspose OCR Java menunjukkan cara memuat gambar untuk OCR dan
  mengekstrak teks dari wilayah tertentu, sangat cocok untuk pemrosesan faktur.
og_title: Contoh OCR Aspose Java – Ekstraksi Teks Wilayah
tags:
- Aspose OCR
- Java
- Image Processing
title: 'Contoh OCR Aspose Java: Ekstrak Teks dari Wilayah'
url: /id/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Contoh Aspose OCR Java: Ekstrak Teks dari Sebuah Wilayah

Mencari **contoh Aspose OCR Java** yang memungkinkan Anda mengambil hanya bagian yang Anda butuhkan dari sebuah gambar? Dalam panduan ini kami akan membahas **memuat gambar untuk OCR** dan **mengekstrak teks dari sebuah wilayah**, sempurna untuk nomor faktur, bidang formulir, atau potongan data apa pun yang tersembunyi di dalam gambar yang lebih besar.

Anda mungkin bertanya-tanya mengapa harus membatasi OCR ke sebuah persegi panjang alih-alih memindai seluruh halaman. Jawaban singkatnya: kecepatan dan akurasi. Ketika mesin hanya melihat potongan yang ditentukan, ia melewatkan noise yang tidak relevan, berjalan lebih cepat, dan sering menghasilkan hasil yang lebih bersih. Pada akhir tutorial ini Anda akan memiliki program Java yang berdiri sendiri yang melakukan hal tersebut, plus beberapa tip untuk menghindari jebakan umum yang sering membuat pemula tersandung.

## Apa yang Anda Butuhkan

- **Java Development Kit (JDK) 11** atau yang lebih baru terpasang.
- **Aspose.OCR for Java** library (Anda dapat mengambil JAR terbaru dari repositori Maven Central atau portal unduhan Aspose).
- Sebuah file gambar yang berisi teks yang ingin Anda baca – untuk demo kami akan menggunakan `invoice.png`, yang menyimpan nomor faktur di dekat sudut kanan atas.
- IDE favorit atau editor teks sederhana plus terminal; alat build apa saja (Maven, Gradle, atau plain `javac`) dapat digunakan.

Itu saja. Tidak ada mesin OCR tambahan, tidak ada binary native, hanya Java murni dan Aspose.

![Screenshot contoh Aspose OCR Java](/images/aspose-ocr-java-example.png "Contoh Aspose OCR Java menampilkan ekstraksi wilayah")

## Contoh Aspose OCR Java – Inisialisasi Mesin OCR

Hal pertama yang dibutuhkan dalam alur kerja OCR apa pun adalah sebuah instance mesin. Aspose menyediakan kelas ringan `OcrEngine` yang menangani segala hal mulai dari pemuatan gambar hingga pemilihan bahasa.

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Mengapa ini penting:** Membuat mesin di awal memberi Anda objek bersih untuk dikonfigurasi. Anda dapat menggunakan kembali `OcrEngine` yang sama untuk beberapa gambar jika Anda memproses batch, yang menghemat memori dan waktu inisialisasi.

## Muat Gambar untuk OCR

Selanjutnya kami memberi tahu mesin gambar mana yang akan dipindai. Aspose menyediakan helper `ImageStream.fromFile`, yang menyembunyikan boilerplate `FileInputStream` tingkat rendah.

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Tip:** Ganti `YOUR_DIRECTORY` dengan path absolut atau relatif yang mengarah ke lokasi Anda menyimpan `invoice.png`. Jika file tidak dapat ditemukan, Aspose akan melempar `IOException`, jadi Anda mungkin ingin membungkus ini dalam blok try‑catch untuk kode produksi.

## Definisikan dan Ekstrak Teks dari Sebuah Wilayah

Sekarang masuk bintang pertunjukan: persegi panjang yang memberi tahu mesin di mana harus melihat. Konstruktor `java.awt.Rectangle` menerima `(x, y, width, height)` – semua diukur dalam piksel.

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**Cara kerjanya:** Dengan memanggil `setRegion`, Anda membatasi pemindaian OCR ke potongan selebar 300 piksel yang dimulai 120 piksel dari tepi kiri dan 250 piksel dari atas. Sesuaikan angka-angka ini agar cocok dengan tata letak Anda; cara cepat menemukannya adalah membuka gambar di editor grafis apa pun yang menampilkan koordinat piksel.

## Aktifkan Bahasa dan Jalankan Pengenalan

Aspose OCR mendukung puluhan bahasa, tetapi untuk nomor faktur kami hanya memerlukan Bahasa Inggris. Mengaktifkan bahasa yang tepat secara dramatis mengurangi false positive.

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Mengapa hanya mengaktifkan Bahasa Inggris?** Mesin OCR akan mencoba mencocokkan karakter dari setiap set bahasa yang diaktifkan, yang dapat membingungkannya ketika teks hanya alfanumerik sederhana. Membatasi ruang lingkup bahasa meningkatkan baik kecepatan maupun presisi.

### Output yang Diharapkan

Ketika semuanya selaras, Anda akan melihat sesuatu seperti:

```
Extracted region text: INV-12345
```

Jika persegi panjang berada beberapa piksel di luar posisi yang tepat, output mungkin berantakan atau kosong. Itu adalah pengecekan sanity yang mudah: jalankan program, lihat konsol, dan pastikan teks cocok dengan yang Anda lihat di gambar.

## Jalankan Kode dan Verifikasi Output

Dengan asumsi Anda menggunakan Maven, tambahkan dependensi Aspose OCR ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Kompilasi dan eksekusi:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

Atau, jika Anda lebih suka plain `javac`:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

Anda seharusnya melihat baris **Extracted region text** tercetak di konsol. Jika Anda mendapatkan “OCR recognition failed,” periksa kembali path file dan pastikan wilayah tersebut memang berisi karakter yang dapat dibaca.

## Kasus Tepi & Variasi Umum

| Situation | What to Change |
|-----------|----------------|
| **Multiple languages** (e.g., English + Spanish) | Call `ocrEngine.getLanguage().setSpanish(true);` alongside English. |
| **Region outside image bounds** | Aspose will silently clip the rectangle, but you’ll lose data. Use `ImageInfo` (`ocrEngine.getImage().getWidth()`) to verify dimensions before setting the region. |
| **Dynamic invoices** (different layouts) | Consider running a lightweight pre‑scan on the whole image to locate keywords like “Invoice #” and then compute the rectangle programmatically. |
| **Higher DPI images** | Increase `ocrEngine.getImage().setResolution(300);` for better accuracy on scanned documents. |
| **Performance tuning** | Disable unnecessary languages, keep the region as small as possible, and reuse a single `OcrEngine` instance across many files. |

## Pro Tips Dari Pengalaman

- **Pro tip:** Jika Anda hanya membutuhkan digit (umum untuk nomor faktur), aktifkan mode numerik dengan `ocrEngine.getLanguage().setDigits(true);`. Ini menghilangkan noise alfabetik.
- **Watch out for:** PNG transparan. Aspose kadang‑kadang salah menafsirkan kanal alfa; mengonversi gambar ke JPEG dengan latar belakang solid terlebih dahulu dapat menyelesaikan output kosong yang aneh.
- **Remember:** Persegi panjang menggunakan sistem koordinat asli gambar, bukan skala UI apa pun yang mungkin Anda lihat di layar. Selalu uji dengan file tepat yang akan Anda proses di produksi.

## Apa Selanjutnya?

Sekarang Anda memiliki **contoh Aspose OCR Java** yang solid untuk ekstraksi berbasis wilayah, Anda dapat memperluasnya ke beberapa arah berguna:

- **Batch processing:** Loop over a folder of invoices, reusing the same `OcrEngine` to improve throughput.
- **Data validation:** Pipe the extracted text through a regex like `INV-\\d{5}` to ensure you captured a valid invoice number.
- **Integration with PDF:** Use Aspose.PDF to overlay the extracted text back onto the original document for audit trails.
- **Cloud deployment:** Wrap the code in a lightweight REST service (Spring Boot) so other systems can call it on demand.

Setiap langkah ini secara alami melibatkan konsep inti yang sama—**load image for OCR**, **extract text from a region**, dan menangani hasilnya—sehingga Anda akan menemukan transisinya tanpa hambatan.

---

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa forum Aspose dimana komunitas berbagi penyesuaian dunia nyata untuk tata letak yang rumit.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}