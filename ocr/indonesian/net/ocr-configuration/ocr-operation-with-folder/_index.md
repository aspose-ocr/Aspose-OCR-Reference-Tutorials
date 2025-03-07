---
title: Operasi OCRO dengan Folder dalam Pengenalan Gambar OCR
linktitle: Operasi OCRO dengan Folder dalam Pengenalan Gambar OCR
second_title: Aspose.OCR .NET API
description: Buka kekuatan pengenalan gambar OCR di .NET dengan Aspose.OCR. Ekstrak teks dengan mudah dari gambar.
weight: 11
url: /id/net/ocr-configuration/ocr-operation-with-folder/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Operasi OCRO dengan Folder dalam Pengenalan Gambar OCR

## Perkenalan

Selamat datang di dunia Pengenalan Karakter Optik (OCR) menggunakan Aspose.OCR untuk .NET! Jika Anda ingin mengekstrak teks dari gambar dengan lancar dalam aplikasi .NET, Anda berada di tempat yang tepat. Tutorial ini akan memandu Anda melalui proses pengenalan gambar OCR dengan folder, memanfaatkan kemampuan Aspose.OCR yang canggih.

## Prasyarat

Sebelum masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:

- Pengetahuan tentang pengembangan C# dan .NET.
- Visual Studio diinstal pada mesin Anda.
-  Aspose.OCR untuk perpustakaan .NET, yang dapat Anda unduh[Di Sini](https://releases.aspose.com/ocr/net/).
- Pemahaman dasar tentang konsep OCR.

## Impor Namespace

Dalam kode C# Anda, pastikan untuk mengimpor namespace yang diperlukan untuk menggunakan Aspose.OCR. Sertakan yang berikut ini di awal skrip Anda:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Langkah 1: Atur Direktori Dokumen

```csharp
// MantanMulai:1
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```

Pastikan Anda mengganti "Direktori Dokumen Anda" dengan jalur sebenarnya tempat gambar Anda disimpan.

## Langkah 2: Inisialisasi Aspose.OCR

```csharp
// Inisialisasi instance AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Buat instance kelas AsposeOcr untuk memanfaatkan fungsinya.

## Langkah 3: Tentukan Jalur Gambar

```csharp
//Jalur Gambar
string fullPath = dataDir + "OCR";
```

Gabungkan jalur direktori dokumen dengan folder spesifik yang berisi gambar Anda.

## Langkah 4: Kenali Gambar

```csharp
// Kenali gambar
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //default atau kustom
});
```

Manfaatkan metode RecognizeMultipleImages untuk melakukan OCR pada beberapa gambar dalam folder yang ditentukan.

## Langkah 5: Cetak Hasil

```csharp
// Hasil cetak
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

Ulangi hasilnya dan cetak teks yang dikenali untuk setiap gambar.

## Langkah 6: Kesimpulan

```csharp
// ExEnd:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

Pastikan kesimpulan skrip Anda tercapai untuk menandakan keberhasilan pelaksanaan operasi OCR dengan folder.

## Kesimpulan

Selamat! Anda telah berhasil mempelajari cara menerapkan pengenalan gambar OCR dengan folder menggunakan Aspose.OCR untuk .NET. Alat canggih ini membuka segudang kemungkinan untuk mengekstraksi teks dari gambar di aplikasi .NET Anda.

## FAQ

### Q1: Dapatkah saya menggunakan Aspose.OCR untuk .NET dalam proyek komersial?

 A1: Ya, Aspose.OCR untuk .NET adalah produk komersial. Untuk informasi perizinan, kunjungi[Di Sini](https://purchase.aspose.com/buy).

### Q2 :. Apakah ada uji coba gratis yang tersedia?

 A2: Ya, Anda dapat menjelajahi uji coba gratis[Di Sini](https://releases.aspose.com/).

### Q3: Di mana saya dapat menemukan dokumentasinya?

 A3: Dokumentasi tersedia[Di Sini](https://reference.aspose.com/ocr/net/).

### Q4: Bagaimana cara mendapatkan lisensi sementara?

 A4: Lisensi sementara dapat diperoleh[Di Sini](https://purchase.aspose.com/temporary-license/).

### Q5: Butuh dukungan atau punya pertanyaan?

 A5: Kunjungi[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) untuk dukungan masyarakat.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
