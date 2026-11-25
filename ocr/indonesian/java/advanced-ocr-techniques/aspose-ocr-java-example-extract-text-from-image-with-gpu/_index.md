---
category: general
date: 2026-06-28
description: Pelajari contoh Aspose OCR Java untuk mengekstrak teks dari gambar pada
  proyek Java dan mengatur batas memori GPU untuk hasil yang lebih cepat.
draft: false
keywords:
- aspose ocr java example
- extract text from image java
- set gpu memory limit
- gpu accelerated OCR Java
- Aspose OCR licensing
language: id
og_description: Contoh OCR Aspose Java yang menunjukkan cara mengekstrak teks dari
  gambar menggunakan kode Java sambil mengatur batas memori GPU untuk kinerja optimal.
og_title: Contoh OCR Aspose Java – Ekstraksi Teks Cepat dengan GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn an Aspose OCR Java example to extract text from image Java projects
    and set GPU memory limit for faster results.
  headline: Aspose OCR Java Example – Extract Text from Image with GPU
  type: TechArticle
tags:
- Aspose OCR
- Java
- GPU
title: Contoh OCR Aspose Java – Ekstrak Teks dari Gambar dengan GPU
url: /id/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Contoh Aspose OCR Java – Ekstrak Teks dari Gambar dengan GPU

Pernah bertanya-tanya bagaimana cara **extract text from image Java** aplikasi tanpa membuat CPU Anda melambat? Anda tidak sendirian. Dalam banyak skenario dunia nyata—seperti pemindaian struk, verifikasi ID, atau pengarsipan dokumen massal—bottlenecknya adalah mesin OCR itu sendiri.  

Berita baik: **Aspose OCR Java example** ini memandu Anda melalui program lengkap yang siap dijalankan yang memanfaatkan akselerasi GPU, dan bahkan menunjukkan cara **set GPU memory limit** sehingga server Anda tetap stabil. Pada akhir panduan ini Anda akan memiliki kelas Java yang berfungsi, yang membaca file gambar, menjalankan OCR pada GPU, dan mencetak teks yang dikenali ke konsol. Tanpa referensi yang samar, hanya kode konkret dan penjelasan yang jelas.

Kami akan membahas semuanya mulai dari lisensi hingga penyetelan GPU, jadi apakah Anda pengembang Java berpengalaman atau baru mencoba computer‑vision, Anda akan menemukan nilai di sini. Satu-satunya prasyarat adalah lingkungan pengembangan Java (JDK 8 atau lebih baru) dan akses ke GPU yang kompatibel dengan CUDA atau OpenCL.

---

## Prasyarat

- **Java Development Kit (JDK) 8+** – Anda dapat mengunduhnya dari Oracle atau mengadopsi OpenJDK.  
- **Aspose.OCR for Java** library – dapatkan JAR-nya dari situs web Aspose atau Maven Central.  
- **A valid Aspose OCR license file** (`Aspose.OCR.Java.lic`). Versi percobaan gratis dapat digunakan untuk pengujian, tetapi lisensi menghilangkan watermark evaluasi.  
- **GPU with CUDA or OpenCL support** – demo secara otomatis mendeteksi mode terbaik, tetapi Anda perlu menginstal driver.  
- **An image to test** – PNG atau JPEG yang jelas dari struk, tanda, atau teks cetak apa pun.  

Jika ada yang terdengar tidak familiar, jangan panik. Langkah-langkah di bawah ini akan mengarahkan Anda ke tautan unduhan yang tepat dan menunjukkan di mana menempatkan file-file tersebut.

---

## Langkah 1: Aspose OCR Java Example – Menyiapkan Proyek

Pertama, buat proyek Maven baru (atau folder sederhana jika Anda lebih suka `javac` biasa). Tambahkan dependensi Aspose OCR ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** Maven akan mengunduh semua dependensi transitif, termasuk pustaka dukungan GPU, sehingga Anda tidak perlu mencari JAR tambahan.

Letakkan file `Aspose.OCR.Java.lic` Anda di root proyek (atau folder apa pun yang akan Anda referensikan nanti). **aspose ocr java example** yang kami bangun mengharapkan jalur lisensi menjadi `"Aspose.OCR.Java.lic"`.

## Langkah 2: Terapkan Lisensi Aspose OCR

Langkah lisensi sangat penting—tanpa itu, mesin OCR berjalan dalam mode evaluasi dan menambahkan watermark pada output. Berikut kode minimal yang Anda perlukan:

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense() throws Exception {
        License license = new License();
        // Adjust the path if your license file lives elsewhere
        license.setLicense("Aspose.OCR.Java.lic");
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

Menjalankan ini sekali di awal aplikasi Anda menjamin bahwa **all subsequent OCR calls** sepenuhnya berlisensi.

## Langkah 3: Konfigurasikan Akselerasi GPU – Set GPU Memory Limit

Sekarang bagian yang menyenangkan: memberi tahu Aspose untuk menggunakan GPU dan secara opsional **set GPU memory limit**. Pustaka ini menyertakan `GpuEngineOptions`, yang memungkinkan Anda mengaktifkan mode GPU, memilih perangkat, dan membatasi penggunaan memori. Membatasi memori berguna pada server bersama di mana Anda tidak ingin pekerjaan OCR Anda menghabiskan seluruh GPU.

```java
import com.aspose.ocr.gpu.*;

public class GpuConfig {
    public static GpuEngineOptions createOptions() {
        GpuEngineOptions gpuOptions = new GpuEngineOptions();
        gpuOptions.setEnableGpu(true);          // turn on GPU acceleration
        gpuOptions.setDeviceId(0);              // use the first GPU device
        gpuOptions.setMemoryLimitMb(2048);      // **set GPU memory limit** to 2 GB
        System.out.println("GPU options configured (memory limit = 2048 MB).");
        return gpuOptions;
    }
}
```

> **Why set a memory limit?** Jika tugas OCR Anda melibatkan gambar sangat besar atau Anda menjalankan banyak pekerjaan bersamaan, GPU dapat dengan cepat kehabisan VRAM, menyebabkan crash. Dengan membatasi alokasi, Anda menjaga proses tetap dalam batas aman dan memungkinkan beban kerja lain berco‑exist secara damai.

## Langkah 4: Ekstrak Teks dari Gambar Java – Memuat Gambar

Dengan lisensi dan pengaturan GPU selesai, kita akhirnya dapat **extract text from image Java** kode. Potongan berikut membuat `OcrEngine` menggunakan opsi GPU, memuat file gambar, dan menjalankan pengenalan.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense();

        // 2️⃣ Set up GPU options (including memory limit)
        GpuEngineOptions gpuOptions = GpuConfig.createOptions();

        // 3️⃣ Create the OCR engine with GPU acceleration
        OcrEngine ocrEngine = new OcrEngine(gpuOptions);

        // 4️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // Replace the placeholder with your actual image path
        ocrInput.add("YOUR_DIRECTORY/receipt.png");

        // 5️⃣ Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized Text (GPU):");
        System.out.println(ocrResult.getText());
    }
}
```

**Poin penting** dalam **aspose ocr java example** ini:

- `OcrInput.add()` dapat menerima banyak gambar; mesin akan memprosesnya secara berurutan.  
- `ocrResult.getText()` mengembalikan string teks biasa, mempertahankan jeda baris tetapi tidak informasi tata letak.  
- Seluruh pipeline berjalan pada GPU, yang dapat menjadi **5‑10× lebih cepat** dibandingkan pemrosesan hanya CPU untuk gambar resolusi tinggi.

## Langkah 5: Jalankan Demo dan Verifikasi Output

Kompilasi dan jalankan program:

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrDemo
```

Jika semuanya terhubung dengan benar, Anda akan melihat sesuatu seperti:

```
Aspose OCR license applied successfully.
GPU options configured (memory limit = 2048 MB).
Recognized Text (GPU):
Item   Qty   Price
Apple   2    $1.20
Banana  5    $0.75
Total          $5.85
```

Teks tepat tergantung pada gambar Anda, tetapi hal pentingnya adalah konsol mencetak **the recognized text** tanpa watermark “Evaluation version”. Jika Anda menemukan error `CUDA driver not found`, periksa kembali bahwa driver GPU Anda terbaru dan toolkit CUDA berada di path sistem.

## Kesalahan Umum & Cara Menghindarinya

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| `OutOfMemoryError: CUDA out of memory` | Memori GPU terlampaui | Turunkan `setMemoryLimitMb` (misalnya, 1024) atau proses potongan gambar yang lebih kecil. |
| `LicenseException` | File lisensi tidak ada atau path salah | Pastikan `Aspose.OCR.Java.lic` dapat diakses dan path-nya cocok. |
| No text returned | Gambar terlalu buram atau ruang warna salah | Pra‑proses gambar (tingkatkan kontras, konversi ke grayscale) sebelum memberi ke OCR. |
| GPU not used | `setEnableGpu(false)` atau driver tidak ada | Verifikasi `gpuOptions.setEnableGpu(true)` dan instal ulang driver GPU. |

## Memperluas Contoh

Sekarang Anda memiliki **aspose ocr java example** yang solid, Anda mungkin ingin:

- **Batch process a folder** – iterasi file dan simpan hasilnya ke database.  
- **Detect language** – gunakan `ocrEngine.setLanguage(OcrLanguage.English)` atau tambahkan beberapa bahasa.  
- **Apply post‑processing** – bersihkan string mentah dengan regex atau kirim ke pemeriksa ejaan.  

Semua ekstensi ini menggunakan kembali kode lisensi dan konfigurasi GPU yang sama, jadi Anda hanya perlu menambahkan logika bisnis.

## Pemikiran Akhir

Anda baru saja melihat **aspose ocr java example** lengkap yang **extracts text from image Java** aplikasi sambil **setting GPU memory limit** untuk kinerja yang kuat. Ide inti—lisensi lebih awal, konfigurasi GPU, memuat gambar, membaca teks—dapat digunakan kembali di banyak proyek, mulai dari pemindai struk hingga sistem entri formulir otomatis.

Mulai dari sini, silakan bereksperimen dengan nilai `GpuEngineOptions` yang berbeda, coba gambar yang lebih besar, atau integrasikan langkah OCR ke dalam microservice Spring Boot. Langit adalah batasnya, dan berkat akselerasi GPU, batasnya jauh lebih tinggi daripada sebelumnya.

Ada pertanyaan atau butuh bantuan menyesuaikan pengaturan memori untuk perangkat keras spesifik Anda? Tinggalkan komentar di bawah, dan selamat coding!

![Diagram Contoh Aspose OCR Java yang menunjukkan alur dari input gambar → OCR dipercepat GPU → output teks](https://example.com/images/aspose-ocr-java-example-diagram.png "diagram contoh aspose ocr java")

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengatur Lisensi dan Memverifikasi Lisensi Aspose.OCR di Java](/ocr/english/java/ocr-basics/set-license/)
- [Ekstrak Teks dari Gambar Java dengan Mode Deteksi Area Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Konversi Gambar ke Teks di Java menggunakan Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}