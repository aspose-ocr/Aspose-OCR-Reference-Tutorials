---
description: Pelajari cara menyimpan hasil OCR dengan Aspose.OCR untuk .NET – mengonversi
  gambar ke PDF, mengekstrak teks dari PNG, dan menyimpan teks yang dikenali ke DOCX,
  TXT, PDF, atau XLSX.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: Cara Menyimpan Hasil OCR sebagai Dokumen
url: /id/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menyimpan Hasil OCR sebagai Dokumen

## Pendahuluan

Dalam tutorial ini Anda akan menemukan **cara menyimpan OCR** output menggunakan Aspose.OCR untuk .NET. Kami akan memandu Anda melalui proses mengenali teks dalam sebuah gambar, kemudian mengonversi teks tersebut ke dalam format dokumen populer seperti DOCX, TXT, PDF, dan XLSX. Pada akhirnya, Anda akan dapat mengotomatisasi ekstraksi data dari gambar dan menyimpannya sebagai file yang dapat dicari dan diedit—sempurna untuk pengarsipan, pelaporan, atau pemrosesan lanjutan.

## Jawaban Cepat
- **Apa arti “cara menyimpan ocr”?** Ini merujuk pada penyimpanan teks yang dikenali dari gambar ke dalam format file seperti DOCX, PDF, dll.  
- **Format apa yang dapat saya ekspor?** DOCX, TXT, PDF, dan XLSX didukung secara bawaan.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi komersial diperlukan untuk penggunaan produksi.  
- **Bisakah saya mengonversi gambar ke PDF secara langsung?** Ya—simpan hasil OCR sebagai PDF untuk mendapatkan dokumen PDF yang dapat dicari.  
- **Apakah PNG didukung?** Tentu saja; Anda dapat **mengekstrak teks dari PNG** gambar dengan API yang sama.

## Apa itu OCR dan Mengapa Menyimpan Hasil sebagai Dokumen?

Optical Character Recognition (OCR) mengubah teks cetak atau tulisan tangan di dalam gambar menjadi string yang dapat dibaca mesin. Menyimpan string tersebut sebagai dokumen memungkinkan Anda:

* Membuat PDF yang dapat dicari untuk kepatuhan.  
* Mengisi spreadsheet (XLSX) untuk analisis data.  
* Menghasilkan laporan yang dapat diedit (DOCX).  
* Mengarsipkan log teks biasa (TXT) untuk pencarian cepat.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- Aspose.OCR untuk .NET terinstal. Anda dapat mengunduhnya **[di sini](https://releases.aspose.com/ocr/net/)**.  
- Sebuah folder di mesin Anda yang akan menyimpan gambar sumber dan dokumen output. Perbarui variabel `dataDir` dalam kode untuk mengarah ke folder ini.

## Impor Namespace

Kita memerlukan beberapa namespace .NET untuk mengakses I/O file dan kelas Aspose OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### Langkah 1: Inisialisasi Aspose.OCR

Atur path ke direktori kerja Anda dan buat instance mesin OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Langkah 2: Kenali Gambar

Berikan file gambar (mis., PNG) ke pengenalan. Di sini kita **mengenali gambar teks** dan mengubahnya menjadi `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Langkah 3: Simpan Hasil dalam Berbagai Format

Sekarang kita mengekspor teks yang dikenali. Pilih format yang sesuai dengan alur kerja Anda—apakah Anda perlu **mengonversi gambar ke PDF**, **mengekstrak teks dari PNG**, atau menghasilkan spreadsheet.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Langkah 4: Tampilkan Pesan Sukses

Pesan konsol sederhana mengonfirmasi bahwa proses selesai tanpa error.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Kesalahan Umum & Tips

- **Path file:** Selalu gunakan path absolut atau pastikan `dataDir` diakhiri dengan pemisah path (`\` atau `/`).  
- **Kualitas gambar:** Gambar dengan resolusi lebih tinggi meningkatkan akurasi; pertimbangkan pra‑pemrosesan (menghilangkan kemiringan, mengurangi noise) untuk hasil yang lebih baik.  
- **Mode lisensi:** Dalam mode evaluasi output mungkin berisi watermark; terapkan lisensi yang valid untuk menghilangkannya.

## Pertanyaan yang Sering Diajukan

**Q1. Apakah Aspose.OCR kompatibel dengan berbagai format gambar?**  
A1: Ya, Aspose.OCR mendukung berbagai format gambar, memastikan fleksibilitas dalam tugas OCR Anda.

**Q2: Bisakah saya menyesuaikan pengaturan pengenalan untuk akurasi yang lebih baik?**  
A2: Tentu saja! Aspose.OCR menyediakan `RecognitionSettings` untuk menyesuaikan proses OCR sesuai dengan kebutuhan spesifik Anda.

**Q3: Apakah ada versi percobaan gratis?**  
A3: Ya, Anda dapat memulai dengan versi percobaan gratis **[di sini](https://releases.aspose.com/)**.

**Q4: Bagaimana saya dapat memperoleh lisensi sementara untuk Aspose.OCR?**  
A4: Lisensi sementara dapat diperoleh **[di sini](https://purchase.aspose.com/temporary-license/)**.

**Q5: Di mana saya dapat mencari bantuan atau terhubung dengan komunitas?**  
A5: Bergabunglah dengan komunitas Aspose.OCR di **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** untuk dukungan dan diskusi.

---

**Terakhir Diperbarui:** 2026-02-12  
**Diuji Dengan:** Aspose.OCR 24.11 untuk .NET  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}