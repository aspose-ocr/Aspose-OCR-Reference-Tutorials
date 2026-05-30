---
category: general
date: 2026-05-06
description: Buat PDF yang dapat dicari dari gambar menggunakan Aspose OCR di Java.
  Pelajari cara mengonversi gambar ke PDF, mengaktifkan koreksi ejaan, dan menggunakan
  OCR GPU untuk hasil yang cepat.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: id
og_description: Buat PDF yang dapat dicari dari gambar menggunakan Aspose OCR di Java.
  Panduan ini menunjukkan cara mengonversi gambar ke PDF, mengaktifkan koreksi ejaan,
  dan menggunakan OCR GPU.
og_title: Buat PDF yang Dapat Dicari dari Gambar dengan OCR Java
tags:
- OCR
- Java
- PDF
title: Buat PDF yang Dapat Dicari dari Gambar dengan Java OCR
url: /id/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF yang Dapat Dicari dari Gambar dengan Java OCR

Pernah membutuhkan untuk **create searchable PDF** dari gambar yang dipindai tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—kebanyakan pengembang mengalami kebuntuan itu saat pertama kali menangani PDF berbasis gambar. Untungnya, dengan Aspose OCR for Java Anda dapat **convert image to PDF**, mengubah teks menjadi konten yang dapat dipilih, dan bahkan menambahkan koreksi ejaan untuk hasil yang rapi.

Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang menunjukkan cara **use OCR GPU** ketika tersedia, cara **process image OCR** secara efisien, dan mengapa mengaktifkan koreksi ejaan penting untuk pencarian downstream. Pada akhir tutorial Anda akan memiliki cara satu‑klik untuk menghasilkan PDF yang dapat dicari yang dapat Anda kirim ke pengguna atau arsipkan untuk kepatuhan.

> **Pro tip:** Jika Anda menjalankan pada mesin tanpa GPU, kode secara elegan akan beralih ke CPU, sehingga Anda tidak perlu menulis ulang apa pun.

## Apa yang Anda Butuhkan

- **Java 8+** (kode ini dikompilasi dengan JDK 8 dan yang lebih baru)
- **Aspose OCR for Java** library (unduh JAR terbaru dari situs Aspose)
- Sebuah **input image** (JPEG, PNG, TIFF, dll.) yang ingin Anda ubah menjadi PDF yang dapat dicari
- (Opsional) Sebuah **GPU** dengan dukungan CUDA jika Anda menginginkan pengenalan secepat mungkin

Tidak ada kerangka kerja tambahan, tidak ada sihir Maven/Gradle—hanya satu JAR pada classpath dan Anda siap melanjutkan.

## Langkah 1: Inisialisasi OCR Engine – Jantung Proses  

Pertama kami membuat instance `OcrEngine` dan menunjukkannya ke file sumber. Objek ini adalah mesin kerja yang akan membaca gambar, menjalankan jaringan saraf, dan mengembalikan teks kepada kami.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*Mengapa ini penting:* Menginisialisasi engine sekali dan menggunakannya kembali menghindari beban memuat pustaka native berulang‑ulang—sebuah peningkatan kinerja kecil yang bertambah ketika Anda memproses puluhan file secara batch.

## Langkah 2: Pilih Perangkat Pemrosesan – Gunakan OCR GPU Jika Memungkinkan  

Jika workstation Anda memiliki GPU yang kompatibel, Anda dapat memberi tahu Aspose untuk menjalankan beban kerja berat di atasnya. Jika tidak, engine secara otomatis beralih ke CPU.

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*Apa manfaatnya?* Akselerasi GPU dapat mengurangi beberapa detik per halaman, terutama untuk pemindaian resolusi tinggi. Fallback memastikan kode yang sama bekerja di mana saja, itulah mengapa kami merekomendasikan **use OCR GPU** sebagai pengaturan default.

## Langkah 3: Percepat Pemindaian – Manfaatkan Semua Core CPU  

Bahkan ketika GPU sibuk, langkah-langkah pra‑pemrosesan di sekitarnya dapat diparalelkan. Menetapkan jumlah thread ke jumlah prosesor yang tersedia memberi engine kesempatan untuk memproses beberapa bagian secara bersamaan.

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*Catatan:* Pada laptop 4‑core ini akan memulai empat thread; pada workstation 16‑core Anda mendapatkan manfaat penuh. Hanya perlu diingat bahwa lebih banyak thread berarti penggunaan memori yang lebih tinggi.

## Langkah 4: Bersihkan Gambar – Filter Pra‑pemrosesan  

Pemindaian yang buram atau berisik akan menghasilkan teks sampah. Menambahkan beberapa filter bawaan secara dramatis meningkatkan akurasi.

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*Mengapa filter ini?* `DeskewFilter` memperbaiki rotasi yang sering terjadi ketika dokumen dimasukkan ke pemindai dengan sudut. `NoiseRemovalFilter` menghilangkan piksel stray yang sebaliknya akan ditafsirkan sebagai karakter. Anggap saja ini memberi OCR engine selembar kertas bersih untuk dibaca.

## Langkah 5: Aktifkan Fitur Cerdas – Aktifkan Spell Correction & Auto Language Detection  

Jika Anda menangani dokumen multibahasa, atau hanya ingin mengurangi typo, aktifkan pemeriksa ejaan bawaan dan biarkan engine menebak bahasa.

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*Kapan ini berguna?* Misalkan pemindaian Anda berisi bagian Bahasa Inggris dan Spanyol. Fitur auto‑detect beralih kamus secara dinamis, sementara spell correction membersihkan karakter yang salah dibaca seperti “0” untuk “O”. Langkah ini penting untuk menghasilkan **searchable PDF** yang benar‑benar mengembalikan hasil yang tepat.

## Langkah 6: Simpan Hasil – Convert Image to PDF dan Jadikan Dapat Dicari  

Akhirnya kami meminta engine menulis PDF di mana gambar asli berada di belakang lapisan teks tak terlihat. Ini adalah alur kerja klasik **convert image to PDF**, tetapi PDF kini dapat dicari.

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

File output (`output-searchable.pdf`) dapat dibuka di penampil PDF apa pun; Anda akan dapat memilih, menyalin, dan mencari teks seperti PDF asli. Tidak diperlukan alat tambahan.

## Contoh Lengkap yang Berjalan – Salin‑dan‑Jalankan  

Berikut seluruh program, siap untuk dikompilasi. Ganti `YOUR_DIRECTORY` dengan folder yang berisi `input.jpg`.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**Output yang diharapkan:** Saat Anda menjalankan program, Anda akan melihat baris konsol *“Searchable PDF generated successfully.”* Membuka `output-searchable.pdf` di Adobe Reader memungkinkan Anda mengetik kata dari gambar asli ke kotak pencarian dan langsung melompat ke lokasinya.

## Pertanyaan Umum & Kasus Tepi  

- **What if the GPU isn’t detected?**  
  Panggilan `setDeviceType(OcrDeviceType.GPU)` tidak melempar pengecualian; ia hanya memberi instruksi pada engine untuk mencoba GPU terlebih dahulu. Jika gagal, engine beralih ke CPU secara diam‑diam.

- **Can I process multiple images in one run?**  
  Ya. Bungkus kode dalam loop, ubah nama file setiap iterasi, dan gunakan kembali instance `OcrEngine` yang sama untuk menjaga penggunaan memori tetap rendah.

- **My PDF is huge—how do I shrink it?**  
  Setelah OCR Anda dapat menjalankan API optimisasi PDF Aspose, atau cukup turunkan skala gambar sumber sebelum memberi ke engine (`ImageStream.fromFile(...).setResolution(150)` untuk 150 DPI).

- **I need to keep the original image resolution for legal compliance.**  
  Format `PDF_SEARCHABLE` mempertahankan bitmap asli secara persis; lapisan teks tak terlihat ditambahkan di atas tanpa mengubah kualitas visual.

## Ringkasan Visual  

![contoh membuat pdf yang dapat dicari](placeholder-image.png "contoh membuat pdf yang dapat dicari")

*Alt text:* *contoh membuat pdf yang dapat dicari – mesin Java OCR mengubah JPG yang dipindai menjadi PDF yang dapat dicari.*

## Kesimpulan  

Anda kini memiliki **solusi lengkap, end‑to‑end** untuk mengubah gambar apa pun menjadi **searchable PDF** menggunakan Aspose OCR for Java. Dengan **converting image to PDF**, **enabling spell correction**, dan **using OCR GPU** bila memungkinkan, Anda mendapatkan hasil yang cepat, akurat, dan dapat dicari yang bekerja di semua platform.

Apa selanjutnya? Cobalah bereksperimen dengan:

- **Different output formats** (`PDF`, `DOCX`, `HTML`) untuk melihat bagaimana lapisan teks berperilaku.
- **Custom dictionaries** jika Anda memproses jargon khusus domain.
- **Batch processing** untuk menangani ribuan pemindaian secara otomatis.

Silakan ubah jumlah thread, ganti filter, atau sambungkan pipeline pra‑pemrosesan Anda sendiri. Pola inti tetap sama: load → preprocess → configure → OCR → save.

Selamat coding, dan semoga PDF Anda selalu dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}