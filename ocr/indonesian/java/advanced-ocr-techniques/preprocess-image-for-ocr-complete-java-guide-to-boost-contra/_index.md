---
category: general
date: 2026-02-17
description: Pra-proses gambar untuk OCR dengan Aspose OCR di Java. Pelajari cara
  meningkatkan kontras gambar, mengatur tingkat kontras, dan mengenali teks dari gambar
  dalam hitungan menit.
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: id
og_description: Pra-proses gambar untuk OCR menggunakan Aspose OCR Java. Panduan ini
  menunjukkan cara meningkatkan kontras gambar, mengatur tingkat kontras, dan mengenali
  teks dari gambar dengan cepat.
og_title: Pra-proses Gambar untuk OCR – Tutorial Java untuk Meningkatkan Kontras &
  Mengekstrak Teks
tags:
- Java
- OCR
- Image Processing
title: Pra-proses Gambar untuk OCR – Panduan Java Lengkap untuk Meningkatkan Kontras
  & Mengekstrak Teks
url: /id/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pra‑proses Gambar untuk OCR – Panduan Java Lengkap

Pernah membutuhkan **preprocess image for OCR** tetapi tidak yakin pengaturan mana yang benar‑benar berpengaruh? Anda tidak sendirian. Kebanyakan pengembang melemparkan gambar ke mesin OCR dan berharap keajaiban terjadi, hanya untuk mendapatkan output yang berantakan. Dalam tutorial ini kami akan membahas contoh praktis end‑to‑end yang **boosts image contrast**, menyesuaikan **contrast level**, dan akhirnya **recognizes text from image** menggunakan Aspose OCR untuk Java.

Setelah selesai, Anda akan memiliki potongan kode yang dapat digunakan kembali yang **extracts text using OCR** secara andal, bahkan pada pemindaian yang berisik. Tidak ada trik tersembunyi, hanya langkah‑langkah yang jelas dan alasan di balik masing‑masing.

## Apa yang Anda Butuhkan

- Java 17 atau yang lebih baru (kode dapat dikompilasi dengan JDK terbaru apa pun)
- Perpustakaan Aspose OCR untuk Java (unduh dari situs resmi Aspose)
- File lisensi Aspose OCR yang valid (`Aspose.OCR.lic`)
- Gambar input (`input.jpg`) yang ingin Anda baca
- IDE favorit atau setup baris perintah sederhana

Jika Anda sudah memiliki semua ini, bagus—mari langsung masuk.

## Langkah 1: Muat Lisensi Aspose OCR (Pengaturan Utama)

Sebelum mesin OCR melakukan apa pun, ia harus mengetahui bahwa Anda memiliki lisensi. Jika tidak, Anda akan melihat watermark percobaan.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Mengapa ini penting:** Tanpa lisensi yang tepat, mesin berjalan dalam mode evaluasi, yang dapat memotong hasil atau menambahkan watermark. Menetapkan lisensi lebih awal juga memastikan bahwa opsi pra‑pemrosesan selanjutnya diterapkan dalam mode penuh‑fitur.

## Langkah 2: Inisialisasi Mesin OCR

Membuat instance `OcrEngine` memberi Anda akses ke pipeline pengenalan dan pra‑pemrosesan.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Tip pro:** Simpan mesin sebagai singleton jika Anda berencana memproses banyak gambar dalam satu batch; ia menyimpan cache sumber daya internal dan mempercepat panggilan berikutnya.

## Langkah 3: Konfigurasikan Pra‑pemrosesan – Deskew, Denoise, dan Peningkatan Kontras

Di sinilah kami **preprocess image for OCR**. Tiga pengaturan yang akan kami ubah adalah:

1. **Deskew** – memperbaiki rotasi ringan.
2. **Denoise** – menghilangkan bintik‑bintik yang membingungkan segmentasi karakter.
3. **Contrast enhancement** – membuat teks gelap lebih menonjol dibandingkan latar belakang.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### Mengapa Menyesuaikan Contrast Level?

Menambah contrast level memperluas histogram gambar, membuat piksel gelap menjadi lebih gelap dan piksel terang menjadi lebih terang. Dalam praktiknya, **contrast level** sebesar `1.3f` sering memberikan keseimbangan terbaik untuk dokumen cetak, sementara nilai di atas `1.5f` dapat menyebabkan goresan tipis terlalu terang. Silakan bereksperimen; pengaturan ini murah untuk diubah dan dapat secara dramatis meningkatkan tingkat keberhasilan **recognize text from image**.

## Langkah 4: Siapkan Gambar Input

Kelas `OcrInput` menyederhanakan penanganan file. Anda dapat menambahkan beberapa gambar jika memerlukan pemrosesan batch.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Kasus khusus:** Jika gambar Anda dalam format non‑standar (mis., TIFF dengan beberapa halaman), Anda dapat memuat tiap halaman secara terpisah atau mengonversinya ke PNG/JPEG terlebih dahulu.

## Langkah 5: Lakukan Pengenalan

Sekarang mesin menjalankan pipeline pra‑pemrosesan yang baru saja kami konfigurasikan, kemudian menyerahkan gambar yang telah dibersihkan ke algoritma inti OCR.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Apa yang terjadi di balik layar?** Aspose OCR pertama‑tama menerapkan transformasi deskey, kemudian menjalankan filter denoise, dan akhirnya menyesuaikan kontras sebelum memberi gambar ke recognizer berbasis jaringan sarafnya. Urutan ini disengaja; mengubahnya dapat menghasilkan hasil yang kurang optimal.

## Langkah 6: Keluarkan Teks yang Dikenali

Akhirnya, kami mencetak string yang diekstrak ke konsol. Dalam aplikasi nyata Anda mungkin menuliskannya ke file atau mengirimnya melalui jaringan.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Output yang Diharapkan

Jika `input.jpg` berisi frasa “Hello World!”, konsol harus menampilkan:

```
Hello World!
```

Jika output terlihat berantakan, periksa kembali nilai pra‑pemrosesan—terutama **contrast level** dan **denoise mode**—dan coba format gambar lain.

## Bonus: Visualisasi Gambar Pra‑diproses (Opsional)

Kadang‑kadang Anda ingin melihat apa yang dilihat mesin setelah deskew, denoise, dan peningkatan kontras. Aspose OCR memungkinkan Anda mengekspor bitmap menengah:

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

Buka `processed.png` berdampingan dengan yang asli; Anda akan melihat horizon yang lebih lurus dan teks yang lebih tajam. Langkah ini berguna saat Anda menelusuri mengapa pemindaian tertentu gagal.

![contoh preprocess image for OCR](/images/ocr-preprocess-example.png "preprocess image for OCR – sebelum dan sesudah peningkatan kontras")

*Gambar di atas menggambarkan bagaimana peningkatan kontras dan denoising mengubah pemindaian yang buram menjadi gambar bersih yang siap OCR.*

## Kesalahan Umum & Cara Menghindarinya

| Pitfall | Why it Happens | Fix |
|---------|----------------|-----|
| **Over‑contrasting** (`setContrastLevel` terlalu tinggi) | Latar belakang yang terang menjadi putih, menghapus karakter yang samar | Pertahankan level antara 1.1 dan 1.4 untuk kebanyakan teks cetak |
| **Deskew tolerance terlalu rendah** | Rotasi kecil tidak terkoreksi | Naikkan `setDeskewAngleTolerance` menjadi 0.2 atau 0.3 untuk buku yang dipindai |
| **Menggunakan GAUSSIAN denoise pada gambar biner** | Memburamkan tepi, menggabungkan karakter | Gunakan `DenoiseMode.MEDIAN` untuk pemindaian hitam‑putih |
| **Lisensi hilang** | Mesin kembali ke mode percobaan, memotong output | Verifikasi jalur ke `Aspose.OCR.lic` dan pastikan file dapat dibaca |

## Langkah Selanjutnya: Melampaui Pra‑pemrosesan Dasar

Sekarang Anda dapat **preprocess image for OCR** dan **extract text using OCR**, pertimbangkan ekstensi berikut:

- **Language packs** – memuat kamus bahasa spesifik untuk meningkatkan akurasi pada teks non‑English.
- **Region‑of‑interest (ROI) cropping** – memfokuskan pada sub‑bagian gambar jika Anda hanya membutuhkan bagian tertentu dari halaman.
- **Batch processing** – mengulangi direktori gambar, menggunakan kembali instance `OcrEngine` yang sama untuk kecepatan.
- **Integrate with PDF** – menggabungkan Aspose OCR dengan Aspose PDF untuk mengonversi PDF yang dipindai menjadi PDF yang dapat dicari dalam satu pipeline.

Setiap topik ini secara alami menggabungkan kata kunci sekunder kami: Anda masih akan **boost image contrast**, **set contrast level**, dan terus **recognize text from image** dalam banyak skenario.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **preprocess image for OCR** menggunakan Aspose OCR untuk Java: memuat lisensi, mengonfigurasi deskew, denoise, dan peningkatan kontras, memberi gambar, dan akhirnya **recognizing text from image**. Dengan contoh lengkap yang dapat dijalankan di atas, Anda kini dapat **extract text using OCR** pada gambar apa pun yang telah dipersiapkan dengan tepat.

Jalankan kode tersebut, sesuaikan **contrast level**, dan saksikan akurasi meningkat. Saat Anda siap, jelajahi model bahasa‑spesifik atau pipeline batch untuk mengubah demo satu‑gambar ini menjadi solusi tingkat produksi.

*Selamat coding, semoga pemindaian Anda selalu tajam!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}