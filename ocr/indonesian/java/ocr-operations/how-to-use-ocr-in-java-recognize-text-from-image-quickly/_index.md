---
category: general
date: 2026-02-17
description: Pelajari cara menggunakan OCR di Java untuk mengenali teks dari file
  gambar, mengekstrak teks dari kwitansi PNG, dan mengonversi kwitansi menjadi JSON
  dengan Aspose OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: id
og_description: Panduan langkah demi langkah tentang cara menggunakan OCR di Java
  untuk mengenali teks dari gambar, mengekstrak teks dari kwitansi PNG, dan mengonversi
  kwitansi menjadi JSON.
og_title: Cara Menggunakan OCR di Java – Mengenali Teks dari Gambar
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Cara Menggunakan OCR di Java – Mengenali Teks dari Gambar dengan Cepat
url: /id/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

preserve the shortcodes at top and bottom.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan OCR di Java – Mengenali Teks dari Gambar dengan Cepat

Pernah bertanya‑tanya **cara menggunakan OCR** untuk mengekstrak teks dari foto struk? Mungkin Anda sudah mencoba beberapa alat daring, namun yang muncul hanya karakter‑karakter kacau atau format yang sulit diproses. Kabar baiknya, dengan beberapa baris kode Java Anda dapat **mengenali teks dari gambar**, **mengekstrak teks dari PNG** struk, bahkan **mengonversi struk ke JSON** untuk pemrosesan lanjutan.  

Dalam tutorial ini kami akan menelusuri alur kerja lengkap—dari melisensikan pustaka Aspose OCR hingga mendapatkan payload JSON bersih yang dapat Anda masukkan ke basis data atau model pembelajaran mesin. Tanpa basa‑basi, hanya contoh praktis yang dapat dijalankan dan Anda dapat menyalin‑tempel ke IDE. Pada akhir tutorial Anda akan memiliki program mandiri yang mengambil `receipt.png` dan menghasilkan string JSON siap pakai.

## Apa yang Anda Butuhkan

- **Java Development Kit (JDK) 8+** – versi terbaru apa pun dapat digunakan.  
- **Aspose OCR for Java** library (artifact Maven: `com.aspose:aspose-ocr`).  
- **File lisensi Aspose OCR yang valid** (`Aspose.OCR.lic`). Versi percobaan gratis cukup untuk pengujian, tetapi lisensi penuh menghilangkan batas evaluasi.  
- File gambar (PNG, JPEG, dll.) yang berisi teks yang ingin Anda baca—misalnya `receipt.png` dan letakkan di folder yang diketahui.  
- IDE favorit Anda (IntelliJ IDEA, Eclipse, VS Code…) – pilih sesuka hati.

> **Pro tip:** Simpan file lisensi di luar folder sumber dan referensikan dengan path absolut atau relatif agar tidak ter‑commit ke kontrol versi.

Setelah prasyarat jelas, mari masuk ke kode sebenarnya.

## Cara Menggunakan OCR – Langkah‑Langkah Inti

Berikut ikhtisar tingkat tinggi dari tindakan yang akan kami lakukan:

1. **Muat pustaka Aspose OCR** dan terapkan lisensi Anda.  
2. **Buat instance `OcrEngine`** – inilah mesin yang melakukan semua pekerjaan berat.  
3. **Siapkan objek `OcrInput`** yang menunjuk ke gambar yang ingin diproses.  
4. **Panggil `recognize` dengan `ResultFormat.JSON`** untuk mendapatkan representasi JSON dari teks yang diekstrak.  
5. **Tangani output JSON** – cetak, simpan ke file, atau parsing lebih lanjut.

Setiap langkah dijelaskan secara detail pada bagian berikut.

## Langkah 1 – Instal Aspose OCR dan Terapkan Lisensi Anda

Pertama, tambahkan dependensi Aspose OCR ke `pom.xml` jika Anda menggunakan Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Sekarang, dalam kode Java Anda, muat lisensinya. Langkah ini penting; tanpa lisensi pustaka berjalan dalam mode evaluasi dan dapat menambahkan watermark pada output.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Mengapa ini penting:** Objek `License` memberi tahu mesin OCR bahwa Anda berhak menggunakan seluruh fitur, termasuk pengenalan akurat dan ekspor JSON. Melewatkan langkah ini tetap memungkinkan Anda **mengenali teks dari gambar**, tetapi hasilnya mungkin dibatasi.

## Langkah 2 – Buat Instance OCR Engine

Kelas `OcrEngine` adalah titik masuk untuk semua operasi OCR. Anggaplah ini sebagai “otak” yang membaca piksel dan menentukan karakter apa yang diwakilinya.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

Anda dapat menyesuaikan mesin (misalnya, mengatur bahasa, mengaktifkan deskew) nanti jika struk Anda mengandung skrip non‑Latin atau dipindai dengan sudut miring. Untuk kebanyakan struk di AS, pengaturan default sudah cukup baik.

## Langkah 3 – Muat Gambar yang Akan Diproses

Sekarang kami akan mengarahkan mesin OCR ke file yang berisi struk. Kelas `OcrInput` dapat menerima banyak gambar, tetapi untuk tutorial ini kami gunakan satu PNG sederhana.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

Jika Anda perlu **mengekstrak teks dari PNG** secara massal, cukup panggil `input.add()` berulang kali atau berikan daftar path file.

## Langkah 4 – Kenali Teks dan Konversi Struk ke JSON

Berikut inti tutorial. Kami meminta mesin untuk mengenali teks dan mengembalikan hasil dalam format JSON. Flag `ResultFormat.JSON` melakukan semua pekerjaan berat untuk kami.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

Payload JSON mencakup setiap baris yang dikenali, kotak pembatasnya, skor kepercayaan, dan teks mentah. Struktur ini memudahkan **mengonversi struk ke JSON** dan selanjutnya mengirimkannya ke API mana pun.

## Langkah 5 – Gabungkan Semua dan Jalankan Program

Berikut kelas Java lengkap yang siap dijalankan. Simpan sebagai `JsonExportDemo.java` (atau nama lain yang Anda suka) dan jalankan dari IDE atau command line.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Output yang Diharapkan

Menjalankan program akan mencetak string JSON serupa dengan berikut (isi tepatnya tergantung pada struk Anda):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

Sekarang Anda dapat mengirim JSON ini ke basis data, endpoint REST, atau pipeline analisis data. Langkah **mengonversi struk ke JSON** sudah selesai untuk Anda.

## Pertanyaan Umum dan Kasus Khusus

### Bagaimana jika gambar diputar?

Aspose OCR secara otomatis mendeteksi dan memperbaiki rotasi ringan. Untuk gambar yang sangat miring, panggil `engine.getImagePreprocessingOptions().setDeskew(true)` sebelum proses pengenalan.

### Bagaimana cara menangani banyak bahasa?

Gunakan `engine.getLanguage()` untuk mengatur bahasa yang diinginkan, misalnya `engine.setLanguage(Language.FRENCH)`. Ini berguna ketika Anda perlu **mengenali teks dari gambar** yang berisi struk multibahasa.

### Bisakah saya menghasilkan teks biasa alih‑alih JSON?

Tentu saja. Ganti `ResultFormat.JSON` dengan `ResultFormat.TEXT` dan panggil `result.getText()`.

### Apakah ada cara membatasi OCR pada area tertentu?

Ya—gunakan `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` untuk memfokuskan pada area struk, yang dapat meningkatkan kecepatan dan akurasi.

## Pro Tips untuk OCR Siap Produksi

- **Cache objek lisensi** jika Anda memproses banyak file dalam loop; membuatnya berulang kali menambah overhead.  
- **Proses batch**: muat semua path struk ke dalam satu `OcrInput` dan panggil `recognize` sekali. JSON akan berisi array halaman, masing‑masing dengan barisnya.  
- **Validasi JSON**: setelah mendapatkan string, parsing dengan pustaka seperti Jackson untuk memastikan formatnya benar sebelum disimpan.  
- **Pantau confidence**: JSON menyertakan field `confidence` per baris. Filter baris dengan nilai di bawah ambang (misalnya 0.85) untuk menghindari data sampah.  
- **Amankan lisensi Anda**: simpan `Aspose.OCR.lic` di vault yang aman atau variabel lingkungan, terutama pada deployment cloud.

## Kesimpulan

Kami telah membahas **cara menggunakan OCR** di Java untuk **mengenali teks dari gambar**, **mengekstrak teks dari PNG** struk, dan **mengonversi struk ke JSON**—semuanya dengan contoh singkat yang dapat dijalankan dari ujung ke ujung. Langkah‑langkahnya sederhana, kodenya siap pakai, dan output JSON memberi Anda representasi terstruktur yang siap dipakai di sistem mana pun.

Selanjutnya, Anda dapat menjelajahi skenario lanjutan: mengirim JSON ke Apache Kafka untuk pemrosesan real‑time, menerapkan pola regex untuk mengekstrak total item, atau mengintegrasikan dengan layanan OCR cloud untuk skalabilitas. Apapun pilihan Anda, dasar‑dasar yang baru saja dipelajari tetap relevan.

Ada pertanyaan, atau mengalami kendala saat mencoba? Tinggalkan komentar di bawah, dan mari kita selesaikan bersama. Selamat coding, dan nikmati mengubah gambar struk berantakan menjadi data bersih yang dapat dicari!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}