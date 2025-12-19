---
date: 2025-12-06
description: Pelajari cara menggunakan Aspose.OCR untuk Java untuk melakukan pengenalan
  teks OCR, mengekstrak teks dari gambar, dan menyiapkan persegi panjang untuk pengenalan
  yang ditargetkan.
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Menyiapkan Persegi Panjang untuk Pengakuan Teks OCR di Aspose.OCR
url: /id/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyiapkan Persegi Panjang untuk Pengakuan Teks OCR di Aspose.OCR

## Pendahuluan

Di dunia yang didorong oleh data saat ini, **ocr text recognition** menjadi fondasi untuk mengubah dokumen yang dipindai, tangkapan layar, dan foto menjadi konten yang dapat dicari dan diedit. Aspose.OCR untuk Java membuat proses ini cepat dan dapat diandalkan, terutama ketika Anda perlu fokus pada area tertentu dari sebuah gambar. Dalam tutorial ini kami akan membimbing Anda melalui setiap langkah yang diperlukan untuk menyiapkan persegi panjang yang membatasi OCR ke wilayah yang Anda inginkan, memberikan kontrol yang tepat dan kinerja yang lebih baik.

## Jawaban Cepat
- **Perpustakaan apa yang menangani pengenalan teks OCR di Java?** AsposeCR for Java.  
- **Apakah saya memerlukan lisensi untuk penggunaan produksi?** Ya – lisensi Aspose.OCR yang valid membuka semua fungsi.  
- **Bisakah saya membatasi OCR ke bagian tertentu dari gambar?** Tentu saja; Anda mendefinisikan persegi panjang yang membatasi zona target.  
- **Apa saja prasyarat utama?** JDK 17+, Aspose.OCR for Java, dan IDE Java.  
- **Apakah pendekatan ini cocok untuk mengekstrak teks dari gambar?** Ya, ini cara yang efisien untuk proyek **extract text image java**.

## Apa itu Pengakuan Teks OCR?
OCR (Optical Character Recognition) mengubah gambar berbasis piksel menjadi karakter yang dapat dibaca mesin. Ini memungkinkan Anda mencari, mengedit, dan menganalisis konten yang awalnya hanya berupa gambar.

## Mengapa Menyiapkan Persegi Panjang untuk Pengakuan Teks OCR?
Mendefinisikan persegi panjang memfokuskan mesin pada wilayah yang benar‑benar berisi teks, yang:
* Mengurangi waktu pemrosesan.  
* Meningkatkan akurasi dengan mengabaikan latar belakang yang berisik.  
* Memungkinkan Anda mengekstrak hanya data yang diperlukan—sempurna untuk formulir, faktur, dan kwitansi.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- **Java Development Kit (JDK)** – Aspose.OCR untuk Java bekerja dengan JDK 17 atau yang lebih baru. Unduh dari situs Oracle.  
- **Aspose.OCR untuk Java library** – Dapatkan JAR terbaru dari halaman unduhan resmi [di sini](https://releases.aspose.com/ocr/java/). Ikuti panduan instalasi [di sini](https://reference.aspose.com/ocr/java/).  
- **Lingkungan Pengembangan** – IDE Java apa pun (IntelliJ IDEA, Eclipse, VS Code, dll.) dapat digunakan.

## Impor Paket

Di file sumber Java Anda, impor kelas Aspose.OCR yang diperlukan serta utilitas Java standar:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *Kami mengimpor `java.awt.Rectangle` karena API OCR mengharapkan persegi panjang yang menentukan wilayah yang akan dipindai.*

## Langkah 1: Mengatur Lisensi

```java
SetLicense.main(null);
```

Memanggil `SetLicense` mengaktifkan lisensi Aspose.OCR Anda, menghapus batas evaluasi dan mengaktifkan pengakuan teks OCR dengan semua fitur.

## Langkah 2: Menentukan Direktori Dokumen dan Jalur Gambar

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

Ganti `"Your Document Directory"` dengan jalur absolut tempat gambar Anda (`p.png`) berada. Inilah gambar yang akan diproses.

## Langkah 3: Membuat Instance Aspose.OCR

```java
AsposeOCR api = new AsposeOCR();
```

Membuat instance `AsposeOCR` memberi Anda akses ke metode `RecognizePage`, yang melakukan OCR sebenarnya.

## Langkah 4: Menyiapkan Persegi Panjang dengan Teks

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

Setiap `Rectangle(x, y, width, height)` memberi tahu Aspose.OCR tepat di mana mencari teks. Sesuaikan koordinat agar cocok dengan tata letak gambar sumber Anda.

## Langkah 5: Melakukan Pengakuan OCR

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

Pemanggilan `RecognizePage` memproses hanya persegi panjang yang telah didefinisikan dan mengembalikan string yang diekstrak. Output konsol memungkinkan Anda memverifikasi hasil **ocr text recognition** secara instan.

## Masalah Umum dan Tips

| Masalah | Penyebab | Solusi |
|-------|-------|----------|
| **Tidak ada output** | Koordinat persegi panjang atau jalur gambar tidak tepat | Periksa kembali nilai `dataDir` dan pastikan persegi panjang benar‑benar menutupi wilayah teks. |
| **Karakter sampah** | Gambar beresolusi rendah atau font tidak didukung | Gunakan sumber beresolusi lebih tinggi atau terapkan pra‑pemrosesan gambar (misalnya, binarisasi). |
| **Lisensi tidak diterapkan** | `SetLicense` tidak dipanggil sebelum OCR | Pastikan `License.main(null);` dijalankan sebelum pemanggilan API apa pun. |
| **Keterlambatan kinerja** | Terlalu banyak persegi panjang besar | Batasi jumlah persegi panjang dan buatlah sekecil mungkin mengelilingi teks. |

## Kesimpulan

Anda kini telah mempelajari cara mengintegrasikan Aspose.OCR untuk Java, mengatur lisensi, menentukan jalur gambar, dan—yang paling penting—menyiapkan persegi panjang untuk memfokuskan **ocr text recognition** pada bagian tertentu gambar. Teknik ini ideal untuk setiap **java ocr tutorial** yang memerlukan ekstraksi teks yang tepat dan berperforma tinggi.

## Pertanyaan yang Sering Diajukan

**Q: Apakah Aspose.OCR kompatibel dengan bahasa pemrograman lain?**  
A: Ya, Aspose.OCR juga mendukung .NET, C++, dan Python. Lihat dokumentasi resmi untuk contoh spesifik bahasa.

**Q: Bisakah saya menggunakan Aspose.OCR dalam proyek komersial?**  
A: Tentu saja. Beli lisensi komersial melalui [Aspose store](https://purchase.aspose.com/buy).

**Q: Apakah ada percobaan gratis yang tersedia?**  
A: Ya, Anda dapat mengunduh versi percobaan [di sini](https://releases.aspose.com/).

**Q: Bagaimana cara mendapatkan lisensi sementara untuk evaluasi?**  
A: Lisensi sementara disediakan melalui [portal lisensi sementara Aspose](https://purchase.aspose.com/temporary-license/).

**Q: Di mana saya dapat mendapatkan dukungan komunitas?**  
A: Kunjungi [forum](https://forum.aspose.com/c/ocr/16) Aspose.OCR untuk pertanyaan, tips, dan contoh kode.

---

**Terakhir Diperbarui:** 2025-12-06  
**Diuji Dengan:** Aspose.OCR for Java 24.12  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
