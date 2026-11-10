---
category: general
date: 2026-02-13
description: Cara membaca struk dengan cepat menggunakan Aspose OCR dan mengekstrak
  jumlah menggunakan regex. Pelajari pemrosesan struk langkah demi langkah dengan
  OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: id
og_description: Cara membaca struk dalam C# menggunakan Aspose OCR dan regex. Panduan
  ini menunjukkan cara memproses struk dengan OCR dan mengekstrak jumlah total.
og_title: Cara Membaca Resi di C# – Tutorial Lengkap OCR & Regex
tags:
- OCR
- C#
- Regex
- Aspose
title: Cara Membaca Resi di C# – Panduan OCR + Regex
url: /id/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membaca Struk di C# – Panduan OCR + Regex

Pernah bertanya-tanya **cara membaca struk** tanpa harus mengetik setiap baris secara manual? Di banyak aplikasi usaha kecil Anda perlu mengambil total jumlah dari foto struk, dan melakukannya secara manual menghilangkan manfaat otomatisasi. Kabar baik? Dengan Aspose OCR Anda dapat membiarkan mesin melakukan pekerjaan berat, kemudian ekspresi reguler sederhana akan menemukan totalnya. Dalam tutorial ini kami akan membahas **proses struk dengan OCR**, mengekstrak jumlah menggunakan regex, dan menghasilkan nilai total yang siap pakai.

Anda akan melihat contoh lengkap yang dapat dijalankan, mempelajari mengapa model bahasa struk penting, serta mendapatkan tips untuk menangani kasus tepi seperti simbol mata uang yang berbeda atau label “Total” yang hilang. Tidak diperlukan dokumen eksternal—semua yang Anda butuhkan ada di sini.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan Aspose OCR untuk pengenalan khusus struk (model bahasa `Receipt` secara otomatis meluruskan dan membersihkan gambar).  
- Cara menerapkan ekspresi reguler yang **mengekstrak jumlah menggunakan regex** yang bekerja untuk kebanyakan struk gaya AS.  
- Cara menangani variasi umum seperti “TOTAL”, “Total:”, atau “Grand Total – $12.34”.  
- Cara mengeluarkan hasil dengan aman dan apa yang harus dilakukan ketika pola tidak ditemukan.  

**Prasyarat**: .NET 6+ (atau .NET Framework 4.7+), lisensi Aspose OCR yang valid atau trial, dan gambar struk yang disimpan secara lokal. Itu saja—tidak ada paket NuGet tambahan selain Aspose.OCR.

---

## Langkah 1 – Instal Aspose OCR dan Siapkan Proyek

### Mengapa ini penting

Aspose OCR menyediakan model **proses struk dengan OCR** yang dirancang khusus untuk meluruskan kertas kusut dan mengabaikan noise latar belakang. Menggunakan model teks umum akan menghasilkan lebih banyak kesalahan, terutama pada pemindaian beresolusi rendah.

### Code

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Pro tip:** Simpan file lisensi di luar folder kontrol sumber Anda untuk menghindari commit tidak sengaja.

---

## Langkah 2 – Konfigurasikan Mesin OCR untuk Pengenalan Struk

### Mengapa ini penting

Model bahasa `Receipt` mencakup de‑skew dan de‑noise bawaan, yang secara dramatis meningkatkan akurasi pada struk dunia nyata yang sering terlipat atau kusut.

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Langkah 3 – Kenali Teks dari Gambar Struk

### Mengapa ini penting

Anda memerlukan teks mentah sebelum dapat menerapkan regex apa pun. Metode `RecognizeImage` mengembalikan `OcrResult` yang berisi string lengkap, skor kepercayaan, dan lainnya jika Anda membutuhkannya nanti.

### Code

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Output OCR yang Diharapkan (contoh)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Langkah 4 – Bangun Regex untuk **Mengekstrak Jumlah Menggunakan Regex**

### Mengapa ini penting

Struk hadir dalam banyak format, tetapi kata “Total” (atau varian serupa) diikuti oleh jumlah dolar merupakan jangkar yang dapat diandalkan. Pola di bawah ini toleran terhadap spasi opsional, titik dua, tanda hubung, dan tanda `$` opsional.

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Penjelasan pola**

| Bagian | Arti |
|--------|------|
| `Total` | Mencari kata “Total” (tidak peka huruf). |
| `\s*[:\-]?` | Mengizinkan spasi apa pun, lalu titik dua atau tanda hubung opsional. |
| `\s*\$?` | Spasi opsional dan tanda dolar opsional. |
| `(\d+(\.\d{2})?)` | Menangkap satu atau lebih digit, opsional diikuti desimal dan dua angka sen. |

---

## Langkah 5 – Keluarkan Total yang Diekstrak atau Tangani Data yang Hilang

### Mengapa ini penting

Bahkan OCR terbaik dapat melewatkan kata, terutama pada struk yang blur. Menyediakan fallback yang elegan mencegah crash dan memberi Anda titik masuk untuk logika khusus (mis., meminta pengguna mengonfirmasi).

### Code

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Contoh output konsol**

```
Total: $12.25
```

---

## Contoh Kerja Lengkap – Semua Langkah dalam Satu File

Berikut adalah program tunggal yang dapat Anda salin‑tempel ke proyek konsol. Program ini mencakup komentar, penanganan error, dan pemuatan lisensi opsional.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Menjalankan program**

1. Buat proyek konsol baru (`dotnet new console -n ReceiptReader`).  
2. Tambahkan paket NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
3. Ganti `YOUR_DIRECTORY/receipt.jpg` dengan path aktual ke gambar struk.  
4. Build dan jalankan (`dotnet run`).  

Anda akan melihat dump OCR diikuti oleh `Total: $xx.xx` jika semuanya cocok.

---

## Menangani Kasus Tepi & Variasi Umum

### 1. Simbol Mata Uang Berbeda

Jika Anda menangani euro (€) atau pound (£), perpanjang pola:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Label “Total” Hilang

Beberapa struk hanya menampilkan “Grand Total”. Tambahkan alternatif:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Beberapa Total (mis., “Subtotal” dan “Total”)

Jika regex mencocokkan kemunculan pertama, Anda mungkin menginginkan **cocokan terakhir**:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Gambar Resolusi Rendah

- Tingkatkan DPI saat memindai (`300 DPI` adalah titik optimal).  
- Pra‑proses gambar dengan filter pengurang blur sederhana sebelum memberi ke Aspose (di luar lingkup panduan ini, tetapi patut dieksplorasi).

---

## Tips Pro untuk Proyek Dunia Nyata

- **Cache hasil OCR** jika Anda perlu mengekstrak beberapa bidang (pajak, item, dll.) – Anda hanya membayar biaya OCR sekali.  
- **Log teks OCR mentah** ke basis data; ini menjadi jejak audit berharga untuk pengeluaran yang diperselisihkan.  
- Saat membangun API web, **jalankan OCR di worker latar belakang**; proses ini dapat memakan beberapa ratus milidetik, yang cukup baik secara asinkron tetapi tidak ideal untuk permintaan sinkron.  
- **Validasi jumlah yang diekstrak** terhadap aturan bisnis (mis., jumlah harus > 0) sebelum disimpan.

---

## Kesimpulan

Kami telah membahas **cara membaca struk** dalam C# menggunakan Aspose OCR, lalu **mengekstrak jumlah menggunakan regex** untuk menemukan baris total secara andal. Dengan memanfaatkan model bahasa `Receipt` Anda mendapatkan teks yang telah diluruskan dan dibersihkan, dan ekspresi reguler yang ringkas menangani sebagian besar keanehan format. Potongan kode lengkap di atas siap disisipkan ke proyek .NET konsol atau layanan apa pun, dan saran kasus tepi tambahan memberi Anda fondasi kuat untuk penggunaan produksi.

Siap untuk langkah selanjutnya? Cobalah memperluas solusi untuk mengambil item baris individual, menghitung pajak secara otomatis, atau mengintegrasikan dengan API pelacakan pengeluaran. Dan jika Anda menemukan struk yang mematahkan pola, ingat bahwa pendekatan **regex temukan total** hanyalah titik awal—Anda selalu dapat menyesuaikan pola agar cocok dengan locale spesifik Anda.

Selamat coding, semoga proses struk Anda cepat, akurat, dan sepenuhnya otomatis!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}