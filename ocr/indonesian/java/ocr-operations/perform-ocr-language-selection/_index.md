---
date: 2026-02-12
description: Pelajari cara melakukan OCR teks gambar dengan pilihan bahasa menggunakan
  Aspose.OCR untuk Java. Panduan langkah demi langkah ini mencakup ekstraksi teks
  Java, koreksi kemiringan OCR, dan lainnya.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR
url: /id/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara OCR Teks Gambar dengan Bahasa Menggunakan Aspose.OCR

## Pendahuluan

Mengekstrak teks dari file gambar adalah kebutuhan umum, baik Anda mendigitalkan dokumen yang dipindai, memproses kwitansi, atau membangun arsip yang dapat dicari. Dalam tutorial ini kami akan memandu Anda melalui contoh lengkap, hands‑on, yang menunjukkan **cara OCR teks gambar** dengan pengaturan bahasa tertentu, sehingga Anda dapat mengintegrasikan OCR yang handal ke dalam aplikasi Java Anda hari ini. Anda juga akan melihat cara menangani koreksi kemiringan OCR dan pengenalan berbasis wilayah untuk akurasi optimal.

## Jawaban Cepat
- **Perpustakaan apa yang menangani OCR di Java?** Aspose.OCR untuk Java  
- **Pengaturan mana yang memilih bahasa?** `settings.setLanguage(Language.Eng)` (atau bahasa lain yang didukung)  
- **Apakah saya memerlukan lisensi untuk pengembangan?** Lisensi evaluasi gratis cukup untuk pengujian; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya membatasi OCR ke wilayah tertentu pada gambar?** Ya, gunakan `RecognitionSettings.setRecognitionAreas()` dengan persegi panjang.  
- **Berapa lama waktu eksekusi biasanya?** Beberapa detik per halaman pada laptop standar, tergantung ukuran gambar dan kompleksitas bahasa.

## Cara OCR Teks Gambar dengan Pemilihan Bahasa
Pada bagian ini kami menjawab pertanyaan inti **bagaimana cara OCR** sebuah gambar ketika Anda mengetahui bahasa teksnya. Memilih bahasa yang tepat secara dramatis meningkatkan akurasi pengenalan karena mesin OCR dapat menerapkan kamus dan model karakter yang spesifik bahasa.

### Mengapa ini penting
- **Akurasi lebih tinggi** – model khusus bahasa mengurangi kesalahan pengenalan.  
- **Peningkatan performa** – mesin melewati pemeriksaan bahasa yang tidak diperlukan.  
- **Penanganan diakritik yang lebih baik** – bahasa Prancis, Spanyol, Jerman, dll., dikenali dengan benar ketika enum `Language` yang cocok digunakan.

## Apa itu “ekstrak teks dari gambar”?
Mengekstrak teks dari gambar (OCR) mengubah representasi visual karakter menjadi string yang dapat dibaca mesin. Ini memungkinkan pencarian, analitik, dan alur kerja ekstraksi data yang sebaliknya memerlukan transkripsi manual.

## Mengapa menggunakan Aspose.OCR dengan pemilihan bahasa?
- **Dukungan multibahasa** – Pilih bahasa yang tepat(s) yang ada pada gambar Anda untuk meningkatkan akurasi.  
- **Kontrol terperinci** – Sesuaikan kemiringan, definisikan wilayah pengenalan, dan atur perilaku auto‑skew.  
- **API Java murni** – Tanpa ketergantungan native, mudah diintegrasikan ke proyek Java apa pun.  
- **Data hasil yang kaya** – Dapatkan teks polos, JSON, persegi panjang pembatas, dan peringatan dalam satu panggilan.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- **Java Development Kit (JDK)** terpasang (JDK 8 atau lebih baru).  
- **Aspose.OCR untuk Java** library – unduh dari situs resmi [di sini](https://reference.aspose.com/ocr/java/).  
- Sebuah file gambar yang berisi teks yang ingin Anda ekstrak, misalnya `p3.png`.

## Impor Paket

Di file sumber Java Anda, sertakan kelas Aspose.OCR yang diperlukan serta utilitas Java standar:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Panduan Langkah‑per‑Langkah

### Langkah 1: Siapkan Direktori Dokumen Anda

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Ganti `"Your Document Directory"` dengan jalur absolut tempat `p3.png` berada.

### Langkah 2: Tentukan Jalur Gambar

```java
// The image path
String file = dataDir + "p3.png";
```

Pastikan variabel `file` mengarah ke gambar tepat yang ingin Anda proses.

### Langkah 3: Buat Instansi API Aspose.OCR

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Objek `AsposeOCR` memberi Anda akses ke semua operasi OCR.

### Langkah 4: Atur Opsi Pengenalan (Pemilihan Bahasa)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Di sini kami:

1. Menonaktifkan auto‑skew karena kami menyediakan nilai skew manual.  
2. Mendefinisikan wilayah persegi panjang (`RecognitionAreas`) untuk membatasi OCR hanya pada bagian gambar yang memang berisi teks.  
3. Menetapkan **bahasa** ke Inggris (`Language.Eng`). Ubah ini menjadi `Language.Fra`, `Language.Spa`, dll., tergantung pada gambar sumber Anda.

### Langkah 5: Jalankan OCR dan Dapatkan Hasil

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Pemanggilan `RecognizePage` menjalankan mesin OCR menggunakan gambar dan pengaturan yang Anda definisikan. Hasilnya disimpan dalam objek `RecognitionResult`.

### Langkah 6: Cetak dan Manfaatkan Hasil

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Output konsol menampilkan:

- Teks lengkap yang diekstrak (`recognitionText`).  
- Teks untuk setiap persegi panjang yang didefinisikan (`recognitionAreasText`).  
- Koordinat persegi panjang pembatas.  
- Representasi JSON untuk pemrosesan lebih lanjut yang mudah.  
- Sudut kemiringan yang terdeteksi dan setiap peringatan.

Sekarang Anda dapat memasukkan `result.recognitionText` ke dalam logika bisnis Anda—menyimpannya, mengindeksnya, atau mengirimnya ke layanan lain.

## Masalah Umum dan Solusinya

| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| **Karakter sampah** | Bahasa yang dipilih salah | Atur enum `Language` yang benar (misalnya `Language.Fra` untuk bahasa Prancis). |
| **Tidak ada teks yang dikembalikan** | Area pengenalan tidak mencakup teks | Sesuaikan koordinat `Rectangle` atau hapus `RecognitionAreas` untuk memproses seluruh gambar. |
| **Performa lambat** | Gambar sangat besar atau resolusi tinggi | Turunkan skala gambar sebelum OCR atau tingkatkan alokasi memori untuk JVM. |
| **Peringatan tentang format yang tidak didukung** | Format gambar tidak dikenali | Konversi gambar ke PNG, JPEG, atau TIFF sebelum diproses. |

## FAQ

**T: Dapatkah saya mengenali banyak bahasa dalam satu panggilan OCR?**  
J: Ya. Gunakan `settings.setLanguage(Language.Eng \| Language.Fra)` untuk mengaktifkan pengenalan multibahasa.

**T: Format gambar apa yang didukung Aspose.OCR?**  
J: PNG, JPEG, BMP, TIFF, GIF, dan beberapa lainnya. Cukup berikan jalur file yang tepat.

**T: Apakah ada batas ukuran untuk gambar?**  
J: Tidak ada batas keras, tetapi gambar yang sangat besar meningkatkan penggunaan memori dan waktu pemrosesan. Pertimbangkan untuk mengubah ukuran file besar.

**T: Bagaimana cara mendapatkan lisensi produksi?**  
J: Beli lisensi dari situs Aspose dan terapkan melalui kelas `License` seperti yang ditunjukkan dalam dokumentasi Aspose.

**T: Dapatkah saya mengekstrak teks dari halaman PDF secara langsung?**  
J: Tidak secara langsung dengan Aspose.OCR. Konversi halaman PDF ke gambar terlebih dahulu (misalnya, menggunakan Aspose.PDF) lalu jalankan OCR.

## Kesimpulan

Anda kini telah melihat cara **mengekstrak teks dari gambar** menggunakan Aspose.OCR untuk Java sambil memilih bahasa yang tepat dan membatasi pengenalan ke wilayah tertentu. Pendekatan ini memberikan OCR yang akurat dan berperforma tinggi yang dapat disematkan ke dalam alur kerja berbasis Java apa pun—dari sistem manajemen dokumen hingga pipeline penangkapan data. Siap melanjutkan? Coba ganti enum bahasa, eksperimen dengan wilayah pengenalan yang berbeda, dan integrasikan hasilnya ke dalam logika aplikasi Anda sendiri.

---

**Terakhir Diperbarui:** 2026-02-12  
**Diuji Dengan:** Aspose.OCR 24.11 untuk Java  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}