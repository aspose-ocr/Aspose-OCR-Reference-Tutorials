---
date: 2026-02-20
description: Pelajari cara mengenali persegi panjang halaman menggunakan Aspose.OCR
  untuk Java, mengekstrak proyek gambar teks Java, dan ikuti tutorial Aspose OCR Java
  ini untuk OCR yang akurat.
linktitle: How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Cara Mengenali Persegi Panjang Halaman untuk Pengenalan Teks OCR di Aspose.OCR
url: /id/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengenali Persegi Panjang Halaman untuk Pengenalan Teks OCR di Aspose.OCR

Dalam pipeline otomatisasi dokumen modern, **recognize page rectangles** adalah teknik kunci yang memungkinkan Anda memberi tahu mesin OCR secara tepat di mana harus mencari. Dengan membatasi Aspose.OCR pada area yang memang berisi teks, Anda meningkatkan kecepatan, mengurangi noise, dan mendapatkan hasil yang lebih bersih. Dalam tutorial ini kami akan membahas setiap langkah—menyiapkan pustaka, lisensi, mendefinisikan persegi panjang, dan akhirnya memanggil API OCR—sehingga Anda dapat mengekstrak teks dari gambar apa pun dengan percaya diri.

## Jawaban Cepat
- **Perpustakaan apa yang menangani pengenalan teks OCR di Java?** Aspose.OCR for Java.  
- **Apakah saya memerlukan lisensi untuk penggunaan produksi?** Ya – lisensi Aspose.OCR yang valid membuka semua fungsi.  
- **Bisakah saya membatasi OCR pada bagian tertentu gambar?** Tentu; Anda mendefinisikan persegi panjang yang membatasi zona target.  
- **Apa saja prasyarat utama?** JDK 17+, Aspose.OCR untuk Java, dan IDE Java.  
- **Apakah pendekatan ini cocok untuk mengekstrak teks dari gambar?** Ya, ini cara yang efisien untuk **extract text image java** projects.

## Apa itu “recognize page rectangles”?
Istilah ini merujuk pada praktik memberikan daftar objek `java.awt.Rectangle` ke mesin OCR sehingga hanya memproses wilayah‑wilayah tertentu pada halaman. Pendekatan terfokus ini mengurangi waktu pemrosesan dan meningkatkan akurasi, terutama pada dokumen kompleks seperti faktur atau formulir.

## Mengapa Menyiapkan Persegi Panjang untuk Pengenalan Teks OCR?
Mendefinisikan persegi panjang memfokuskan mesin pada wilayah yang memang berisi teks, yang:
* Mengurangi waktu pemrosesan.  
* Meningkatkan akurasi dengan mengabaikan latar belakang yang berisik.  
* Memungkinkan Anda mengekstrak hanya data yang dibutuhkan—sempurna untuk formulir, faktur, dan kwitansi.  

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- **Java Development Kit (JDK)** – Aspose.OCR untuk Java bekerja dengan JDK 17 atau lebih baru. Unduh dari situs Oracle.  
- **Aspose.OCR for Java library** – Dapatkan JAR terbaru dari halaman unduhan resmi [di sini](https://releases.aspose.com/ocr/java/). Ikuti panduan instalasi [di sini](https://reference.aspose.com/ocr/java/).  
- **Lingkungan Pengembangan** – IDE Java apa saja (IntelliJ IDEA, Eclipse, VS Code, dll.) dapat digunakan.

## Import Packages

Di file sumber Java Anda, impor kelas Aspose.OCR yang diperlukan serta utilitas standar Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *Kami mengimpor `java.awt.Rectangle` karena API OCR mengharapkan persegi panjang yang mendefinisikan wilayah yang akan dipindai.*

## Langkah 1: Menyiapkan Lisensi

```java
SetLicense.main(null);
```

Memanggil `SetLicense` mengaktifkan lisensi Aspose.OCR Anda, menghapus batas evaluasi, dan mengaktifkan pengenalan teks OCR dengan semua fitur.

## Langkah 2: Menentukan Direktori Dokumen dan Path Gambar

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

Ganti `"Your Document Directory"` dengan path absolut tempat gambar Anda (`p.png`) berada. Ini adalah gambar yang akan diproses.

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

Setiap `Rectangle(x, y, width, height)` memberi tahu Aspose.OCR secara tepat di mana harus mencari teks. Sesuaikan koordinat agar cocok dengan tata letak gambar sumber Anda.

## Langkah 5: Melakukan Pengenalan OCR

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

Pemanggilan `RecognizePage` memproses hanya persegi panjang yang telah didefinisikan dan mengembalikan string yang diekstrak. Output konsol memungkinkan Anda memverifikasi hasil **ocr text recognition** secara langsung.

## Masalah Umum dan Tips

| Masalah | Penyebab | Solusi |
|-------|-------|----------|
| **Tidak ada output** | Koordinat persegi panjang atau path gambar yang salah | Periksa kembali nilai `dataDir` dan pastikan persegi panjang benar‑benar menutupi area teks. |
| **Karakter sampah** | Gambar beresolusi rendah atau font tidak didukung | Gunakan sumber beresolusi lebih tinggi atau terapkan pra‑pemrosesan gambar (mis., binarisasi). |
| **Lisensi tidak diterapkan** | `SetLicense` tidak dipanggil sebelum OCR | Pastikan `SetLicense.main(null);` dijalankan sebelum panggilan API apa pun. |
| **Keterlambatan performa** | Terlalu banyak persegi panjang besar | Batasi jumlah persegi panjang dan buat sekecil mungkin di sekitar teks. |

## Pertanyaan yang Sering Diajukan

**Q:** *Apakah Aspose.OCR kompatibel dengan bahasa pemrograman lain?*  
**A:** Ya, Aspose.OCR juga mendukung .NET, C++, dan Python. Lihat dokumentasi resmi untuk contoh khusus bahasa.

**Q:** *Bisakah saya menggunakan Aspose.OCR dalam proyek komersial?*  
**A:** Tentu. Beli lisensi komersial melalui [Aspose store](https://purchase.aspose.com/buy).

**Q:** *Apakah tersedia versi percobaan gratis?*  
**A:** Ya, Anda dapat mengunduh versi percobaan [di sini](https://releases.aspose.com/).

**Q:** *Bagaimana cara mendapatkan lisensi sementara untuk evaluasi?*  
**A:** Lisensi sementara disediakan melalui [Aspose temporary‑license portal](https://purchase.aspose.com/temporary-license/).

**Q:** *Di mana saya dapat mendapatkan dukungan komunitas?*  
**A:** Kunjungi forum Aspose.OCR [di sini](https://forum.aspose.com/c/ocr/16) untuk pertanyaan, tips, dan contoh kode.

## Kesimpulan

Anda kini telah mempelajari cara **recognize page rectangles** dengan Aspose.OCR untuk Java, menyiapkan lisensi, menentukan path gambar, dan—yang paling penting—menyiapkan persegi panjang yang ketat untuk memfokuskan OCR pada bagian gambar yang tepat yang Anda butuhkan. Teknik ini ideal untuk setiap **aspose ocr java tutorial** yang menuntut ekstraksi teks yang presisi dan berperforma tinggi.

---

**Last Updated:** 2026-02-20  
**Tested With:** Aspose.OCR for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}