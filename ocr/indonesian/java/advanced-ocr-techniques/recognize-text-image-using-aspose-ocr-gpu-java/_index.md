---
category: general
date: 2026-02-17
description: Mengenali teks pada gambar dengan cepat menggunakan dukungan GPU Aspose
  OCR di Java. Pelajari cara mengekstrak teks dari gambar dan mengatur ID perangkat
  GPU untuk kinerja optimal.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: id
og_description: Mengenali teks gambar dengan cepat menggunakan dukungan GPU Aspose
  OCR di Java. Panduan ini menunjukkan cara mengekstrak teks dari gambar dan mengatur
  ID perangkat GPU.
og_title: Mengenali gambar teks menggunakan Aspose OCR GPU – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: Mengenali gambar teks menggunakan Aspose OCR GPU – Java
url: /id/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengenali gambar teks menggunakan Aspose OCR GPU – Java

Pernah membutuhkan untuk **recognize text image** dalam aplikasi Java tetapi CPU kesulitan dengan file besar? Anda bukan satu-satunya—banyak pengembang mengalami hal yang sama saat memproses pemindaian resolusi tinggi. Kabar baik? Aspose OCR memungkinkan Anda **extract text from image** pada GPU, memotong waktu pemrosesan secara dramatis.  

Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang menunjukkan secara tepat cara menyiapkan lisensi, mengaktifkan percepatan GPU, dan **set gpu device id** ketika Anda memiliki beberapa kartu grafis. Pada akhir tutorial Anda akan memiliki program mandiri yang mencetak teks yang dikenali ke konsol—tanpa langkah tambahan.

## Apa yang Anda Butuhkan

- **Java 17** atau lebih baru (API kompatibel dengan Java 8+, tetapi LTS terbaru memberikan kinerja yang lebih baik).  
- **Aspose OCR for Java** library (unduh JAR dari situs web Aspose).  
- File lisensi **Aspose OCR** yang valid (`Aspose.OCR.lic`). Versi percobaan gratis berfungsi, tetapi fitur GPU terkunci di versi berlisensi.  
- File gambar (`sample-image.png`) yang berisi teks yang jelas dan dapat dibaca mesin.  
- Lingkungan yang mendukung GPU (kartu NVIDIA CUDA‑compatible bekerja paling baik).  

Jika ada yang belum familiar, jangan khawatir—setiap poin akan dijelaskan seiring berjalan.

## Langkah 1: Tambahkan Aspose OCR ke Proyek Anda

Pertama, sertakan Aspose OCR JAR pada classpath Anda. Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml`:

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

> **Pro tip:** Jaga nomor versi tetap sinkron dengan catatan rilis library; versi yang lebih baru sering membawa perbaikan kinerja untuk pemrosesan GPU.

## Langkah 2: Muat Lisensi Aspose OCR (diperlukan untuk penggunaan GPU)

Tanpa lisensi pemanggilan `setEnableGpu(true)` akan diam-diam beralih ke mode CPU. Muat lisensi tepat di awal `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Ganti `YOUR_DIRECTORY` dengan path absolut atau relatif tempat Anda menyimpan file `.lic`. Jika path salah, Aspose akan melempar `FileNotFoundException`, jadi periksa kembali ejaannya.

## Langkah 3: Buat mesin OCR dan aktifkan percepatan GPU

Sekarang kita menginstansiasi `OcrEngine` dan memberitahukannya untuk menggunakan GPU. Metode `setGpuDeviceId` memungkinkan Anda memilih kartu tertentu ketika lebih dari satu tersedia.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Mengapa harus mengatur device ID? Pada server multi‑GPU Anda mungkin menyisihkan satu kartu untuk pra‑pemrosesan gambar dan kartu lain untuk OCR. Mengatur ID memastikan perangkat keras yang tepat melakukan pekerjaan berat.

## Langkah 4: Siapkan gambar input

Aspose OCR bekerja dengan berbagai format (PNG, JPG, BMP, TIFF). Bungkus file Anda dalam objek `OcrInput`:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Jika Anda perlu memproses aliran (misalnya file yang di‑upload), gunakan `ocrInput.add(InputStream)` sebagai gantinya.

## Langkah 5: Jalankan proses pengenalan dan ambil hasilnya

Metode `recognize` mengembalikan `OcrResult` yang berisi teks polos, skor kepercayaan, dan bahkan informasi tata letak bila diperlukan.

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

Jika gambar blur atau bahasa tidak didukung, hasilnya mungkin kosong. Dalam kasus tersebut, periksa nilai `ocrResult.getConfidence()` (0‑100) untuk memutuskan apakah harus mencoba lagi dengan pra‑pemrosesan.

## Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semua bagian memberikan satu kelas Java yang dapat Anda salin‑tempel ke IDE:

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

> **Expected output:** Konsol mencetak teks persis yang muncul di `sample-image.png`. Jika GPU aktif, Anda akan melihat waktu pemrosesan turun dari beberapa detik (CPU) menjadi kurang dari satu detik untuk pemindaian 300 dpi tipikal.

## Pertanyaan Umum & Kasus Tepi

### Apakah ini bekerja pada server tanpa tampilan (headless)?

Ya. Driver GPU harus terinstal, tetapi tidak diperlukan tampilan. Pastikan toolkit `CUDA` (atau yang setara untuk GPU Anda) berada di `PATH` sistem.

### Bagaimana jika saya memiliki lebih dari satu GPU dan ingin menggunakan GPU 1?

Ubah device ID:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### Bagaimana cara mengekstrak teks dari gambar dalam bahasa lain?

Atur bahasa sebelum memanggil `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose mendukung lebih dari 30 bahasa; lihat dokumentasi API untuk enumerasi lengkapnya.

### Bagaimana jika gambar berisi beberapa halaman (misalnya PDF yang dikonversi menjadi gambar)?

Buat entri `OcrInput` terpisah untuk setiap halaman, atau lakukan loop pada file-file tersebut:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Mesin akan menggabungkan hasil secara berurutan.

### Bagaimana menangani hasil dengan kepercayaan rendah?

Periksa skor kepercayaan:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Langkah pra‑pemrosesan umum meliputi binarisasi, pengurangan noise, atau mengubah ukuran ke 300 dpi.

## Tips Kinerja

- **Batch processing:** Menambahkan banyak gambar ke satu `OcrInput` mengurangi overhead inisialisasi konteks GPU berulang.  
- **Warm‑up:** Jalankan pengenalan tiruan sekali setelah memulai JVM; panggilan pertama menimbulkan latensi inisialisasi driver.  
- **Memory management:** Buang objek `OcrInput` besar (`ocrInput.clear()`) setelah selesai untuk membebaskan memori GPU.  

## Kesimpulan

Anda kini tahu cara **recognize text image** secara efisien dengan mesin GPU Aspose OCR di Java, cara **extract text from image** dalam bahasa apa pun yang didukung, dan cara **set gpu device id** saat bekerja dengan beberapa kartu grafis. Kode lengkap yang dapat dijalankan di atas seharusnya langsung berfungsi—cukup ganti lisensi dan path gambar Anda.

Siap untuk langkah berikutnya? Coba proses folder PDF yang dipindai, bereksperimen dengan opsi `setLanguage` yang berbeda, atau gabungkan OCR dengan model machine‑learning untuk pasca‑pemrosesan. Kemungkinannya tak terbatas, dan peningkatan kinerja dari percepatan GPU membuat proyek berskala besar menjadi layak.

Selamat coding, dan silakan tinggalkan komentar jika Anda mengalami kendala!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}