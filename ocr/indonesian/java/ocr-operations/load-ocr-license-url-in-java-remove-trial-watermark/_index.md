---
category: general
date: 2026-06-28
description: Muat URL lisensi OCR di Java dan hapus watermark percobaan dengan contoh
  kode sederhana. Pelajari langkah demi langkah cara menerapkan lisensi Aspose OCR
  jarak jauh.
draft: false
keywords:
- load OCR license URL
- remove trial watermark
- Aspose OCR Java
- remote license loading
- Java OCR setup
language: id
og_description: Muat URL lisensi OCR di Java untuk menghapus watermark percobaan.
  Ikuti panduan lengkap ini untuk lisensi Aspose OCR.
og_title: Muat URL Lisensi OCR di Java – Hapus Watermark Percobaan
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Load OCR license URL in Java and remove trial watermark with a simple
    code example. Learn step‑by‑step how to apply a remote Aspose OCR license.
  headline: Load OCR License URL in Java – Remove Trial Watermark
  type: TechArticle
- description: Load OCR license URL in Java and remove trial watermark with a simple
    code example. Learn step‑by‑step how to apply a remote Aspose OCR license.
  name: Load OCR License URL in Java – Remove Trial Watermark
  steps:
  - name: Setting up the Aspose OCR library in a Maven/Gradle project.
    text: Setting up the Aspose OCR library in a Maven/Gradle project.
  - name: Loading the OCR license from a remote URL (the **load OCR license URL**
      part).
    text: Loading the OCR license from a remote URL (the **load OCR license URL**
      part).
  - name: Disabling trial mode to **remove trial watermark**.
    text: Disabling trial mode to **remove trial watermark**.
  - name: Instantiating the `OcrEngine` and performing a quick test scan.
    text: Instantiating the `OcrEngine` and performing a quick test scan.
  - name: The URL is correct and returns the exact `.lic` file (no redirects to an
      HTML page).
    text: The URL is correct and returns the exact `.lic` file (no redirects to an
      HTML page).
  - name: The license file matches the product version you’re using.
    text: The license file matches the product version you’re using.
  - name: '`setTrialMode(false)` was called *after* `fromUrl`.'
    text: '`setTrialMode(false)` was called *after* `fromUrl`.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Muat URL Lisensi OCR di Java – Hapus Watermark Percobaan
url: /id/java/ocr-operations/load-ocr-license-url-in-java-remove-trial-watermark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Muat URL Lisensi OCR di Java – Hapus Watermark Percobaan

Pernahkah Anda perlu **load OCR license URL** dalam proyek Java tetapi terus melihat watermark percobaan yang mengganggu pada setiap output? Anda bukan satu-satunya. Dalam banyak skenario perusahaan, watermark tidak hanya terlihat tidak profesional—bahkan dapat mengganggu alur kerja hilir.  

Berita baik? Dengan beberapa baris kode Anda dapat mengambil lisensi Aspose OCR Anda dari endpoint HTTPS yang aman dan **remove trial watermark** sekali untuk selamanya. Di bawah ini Anda akan mendapatkan contoh siap‑jalankan, plus “mengapa” di balik setiap langkah, sehingga Anda tidak akan kebingungan nanti.

## Apa yang Dibahas dalam Tutorial Ini

Kami akan membahas:

1. Menyiapkan pustaka Aspose OCR dalam proyek Maven/Gradle.  
2. Memuat lisensi OCR dari URL remote (bagian **load OCR license URL**).  
3. Menonaktifkan mode percobaan untuk **remove trial watermark**.  
4. Membuat instance `OcrEngine` dan melakukan pemindaian tes cepat.  

Tidak diperlukan dokumentasi eksternal—semua yang Anda butuhkan ada di sini. Pada akhir tutorial Anda akan memiliki pipeline OCR bersih tanpa watermark yang dapat Anda masukkan ke layanan Java mana pun.  

*Prasyarat*: Java 8+, lingkungan build Maven atau Gradle, dan file lisensi Aspose OCR yang valid yang dihosting di server HTTPS (misalnya `https://yourcompany.com/licenses/asp-ocr.lic`). Jika Anda belum memiliki lisensi, Anda dapat meminta percobaan dari situs web Aspose—hanya ingat untuk menggantinya dengan lisensi produksi nanti.

---

## Langkah 1: Tambahkan Dependensi Aspose OCR

Pertama, pastikan JAR Aspose OCR ada di classpath Anda. Jika Anda menggunakan Maven, tambahkan cuplikan berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Untuk Gradle, tampilannya seperti ini:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Perhatikan nomor versi; rilis terbaru sering menyertakan perbaikan bug untuk penanganan lisensi.

---

## Langkah 2: **Load OCR License URL** – Ambil Lisensi dari Cloud

Sekarang masuk ke inti tutorial. Kita akan membuat objek `License` dan memberinya URL remote. Ini adalah tempat tepat di mana aksi **load OCR license URL** terjadi.

```java
import com.aspose.ocr.*;

public class CloudLicenseDemo {
    public static void main(String[] args) throws Exception {
        // 2.1: Initialize the License object
        License license = new License();

        // 2.2: Load the license from a secure HTTPS location
        // Replace the URL with the actual path to your .lic file
        license.fromUrl("https://yourcompany.com/licenses/asp-ocr.lic");

        // 2.3: Turn off trial mode – this is what actually **remove trial watermark**
        license.setTrialMode(false);

        // 2.4: Create the OCR engine – ready for real work
        OcrEngine ocrEngine = new OcrEngine();

        // 2.5: Quick sanity check – run OCR on a sample image
        ocrEngine.setImage("sample.png");
        if (ocrEngine.process()) {
            System.out.println("OCR succeeded, output:");
            System.out.println(ocrEngine.getText());
        } else {
            System.err.println("OCR failed – check the license and image path.");
        }
    }
}
```

### Mengapa Ini Berfungsi

* `License.fromUrl(...)` menghubungi server remote, mengunduh file `.lic`, dan memvalidasinya terhadap kunci publik produk. Selama URL dapat dijangkau melalui **HTTPS**, koneksi terenkripsi dan aman dari serangan man‑in‑the‑middle.  
* `setTrialMode(false)` memberi tahu Aspose untuk memperlakukan lisensi sebagai lisensi penuh. Jika Anda melewatkan pemanggilan ini, perpustakaan menganggapnya sebagai percobaan dan secara otomatis menambahkan logika **remove trial watermark**—artinya Anda masih akan melihat watermark meskipun file lisensi ada.  

> **Edge case:** Beberapa firewall perusahaan memblokir panggilan HTTPS keluar. Jika Anda mendapatkan `java.net.ConnectException`, pertimbangkan untuk menempatkan lisensi di server internal atau menyertakannya dalam JAR Anda dan menggunakan `license.setLicense("aspose.lic")` sebagai gantinya.

---

## Langkah 3: Verifikasi Watermark Sudah Hilang

Tes cepat adalah cara terbaik untuk memastikan Anda benar‑benar **remove trial watermark**. Jalankan program dengan gambar yang diketahui mengandung teks terlihat. Jika lisensi aktif, output akan bersih, dan tidak ada teks “Aspose OCR – Trial Version” yang muncul pada gambar atau di konsol.

**Output konsol yang diharapkan (jika berhasil):**

```
OCR succeeded, output:
Hello, World!
```

Jika Anda masih melihat watermark, periksa kembali:

1. URL sudah benar dan mengembalikan file `.lic` yang tepat (tidak ada pengalihan ke halaman HTML).  
2. File lisensi cocok dengan versi produk yang Anda gunakan.  
3. `setTrialMode(false)` dipanggil *setelah* `fromUrl`.  

---

## Langkah 4: Tips Siap‑Produksi & Kesalahan Umum

| Situasi | Apa yang Harus Dilakukan |
|-----------|------------|
| **License expires** | Pantau tanggal kedaluwarsa `License` (tersedia via `license.getExpirationDate()`) dan otomatisasi peringatan perpanjangan. |
| **Network latency** | Cache lisensi secara lokal setelah unduhan pertama untuk menghindari panggilan HTTP berulang. |
| **Multiple JVMs** | Muat lisensi sekali per JVM; panggilan selanjutnya murah tetapi tidak diperlukan. |
| **Running in Docker** | Pastikan kontainer dapat menjangkau endpoint HTTPS; tambahkan CA perusahaan ke trust store Java jika diperlukan. |
| **File not found** | Gunakan URL absolut dan verifikasi bahwa server mengembalikan `200 OK` dengan `application/octet-stream`. |

---

## Langkah 5: Contoh Kerja Penuh (Semua Langkah Digabungkan)

Berikut adalah program akhir yang siap disalin‑tempel yang menggabungkan semua rekomendasi dari panduan ini:

```java
import com.aspose.ocr.*;

public class CloudLicenseDemo {
    public static void main(String[] args) {
        try {
            // ---------- Load OCR license from a remote URL ----------
            License license = new License();
            // Make sure the URL points directly to the .lic file and uses HTTPS
            license.fromUrl("https://yourcompany.com/licenses/asp-ocr.lic");
            // Disable trial mode – this is the key to **remove trial watermark**
            license.setTrialMode(false);

            // ---------- Initialize OCR engine ----------
            OcrEngine ocrEngine = new OcrEngine();

            // ---------- Optional: set language, DPI, etc. ----------
            ocrEngine.getLanguage().setLanguage(Language.English);
            ocrEngine.getImageProperties().setResolution(300);

            // ---------- Perform a quick OCR test ----------
            ocrEngine.setImage("sample.png"); // replace with your image path
            if (ocrEngine.process()) {
                System.out.println("OCR succeeded, output:");
                System.out.println(ocrEngine.getText());
            } else {
                System.err.println("OCR failed – verify the license and image.");
            }
        } catch (Exception e) {
            // ---------- Robust error handling ----------
            System.err.println("An error occurred while loading the OCR license or processing the image:");
            e.printStackTrace();
        }
    }
}
```

**Jalankan:** `mvn compile exec:java -Dexec.mainClass=CloudLicenseDemo` (atau perintah Gradle yang setara). Jika semuanya sudah dikonfigurasi dengan benar, Anda akan melihat teks OCR tercetak tanpa watermark percobaan yang muncul.

---

## Kesimpulan

Kami baru saja menunjukkan cara **load OCR license URL** di Java dan **remove trial watermark** hanya dengan beberapa baris kode. Dengan mengambil lisensi dari lokasi remote yang aman, menonaktifkan mode percobaan, dan menginisialisasi `OcrEngine`, Anda mendapatkan pipeline OCR kelas produksi siap diintegrasikan ke micro‑services, pekerjaan batch, atau aplikasi desktop.  

Langkah selanjutnya? Coba beri engine PDF melalui `PdfInput`, bereksperimen dengan paket bahasa yang berbeda, atau buat endpoint REST yang menerima gambar dan mengembalikan teks biasa—pilihan Anda. Dan ingat, menjaga lisensi tetap terbaru dan menangani gangguan jaringan dengan elegan akan menyelamatkan Anda dari sakit kepala di masa depan.

Selamat coding, semoga hasil OCR Anda tetap bersih dan bebas watermark!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Set License and Verify Aspose.OCR License in Java](/ocr/english/java/ocr-basics/set-license/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)
- [Beräkna snedvinkel med Aspose OCR Java – Fullständig guide](/ocr/swedish/java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}