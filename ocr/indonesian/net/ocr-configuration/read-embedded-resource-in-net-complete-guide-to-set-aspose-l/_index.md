---
category: general
date: 2026-01-10
description: Baca sumber daya yang disematkan dan atur lisensi Aspose di C#. Pelajari
  cara menggunakan GetManifestResourceStream, menyematkan file lisensi, dan mendapatkan
  assembly yang sedang dieksekusi .NET dalam satu tutorial.
draft: false
keywords:
- read embedded resource
- set aspose license
- use getmanifestresourcestream
- how to embed license
- get executing assembly .net
language: id
og_description: Baca sumber daya yang disematkan di .NET dan atur lisensi Aspose dengan
  cepat. Panduan langkah demi langkah yang mencakup GetManifestResourceStream, menyematkan
  lisensi, dan menggunakan assembly yang sedang dijalankan.
og_title: Baca Sumber Daya Tersemat – Atur Lisensi Aspose di .NET
tags:
- C#
- .NET
- Aspose OCR
- Embedded Resources
title: Membaca Sumber Daya Tersemat di .NET – Panduan Lengkap untuk Mengatur Lisensi
  Aspose
url: /id/net/ocr-configuration/read-embedded-resource-in-net-complete-guide-to-set-aspose-l/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Baca Sumber Daya Tersemat – Panduan Lengkap untuk Menetapkan Lisensi Aspose

Pernahkah Anda perlu **read embedded resource** pada runtime dan bertanya-tanya bagaimana cara melisensikan perpustakaan Aspose OCR Anda tanpa menuliskan jalur secara keras? Anda bukan satu-satunya. Dalam banyak aplikasi perusahaan, file lisensi berada di dalam assembly sehingga Anda tidak perlu mengirim file tambahan atau khawatir tentang izin yang hilang. Tutorial ini menunjukkan secara tepat cara membaca sumber daya tersemat dan menetapkan lisensi Aspose menggunakan metode .NET `GetManifestResourceStream`.

Kami akan membahas semua yang Anda perlukan: menyematkan file `.lic`, mengambilnya dengan `GetExecutingAssembly`, dan akhirnya menerapkannya ke kelas `License` Aspose OCR. Pada akhir tutorial, Anda akan memiliki solusi mandiri yang berfungsi pada proyek .NET apa pun—tanpa file eksternal.

## Apa yang Akan Anda Pelajari

- **How to embed a license file** ke dalam proyek .NET sehingga menjadi bagian dari DLL yang dikompilasi.
- Cara yang tepat untuk **use GetManifestResourceStream** untuk membaca sumber daya tersemat tersebut.
- Cara **set Aspose license** secara programatis tanpa menyentuh sistem file.
- Tips untuk menangani jebakan umum seperti nama sumber daya yang salah eja atau aksi build yang hilang.
- Contoh kode lengkap yang dapat dijalankan yang dapat Anda masukkan ke dalam solusi Anda.

### Prasyarat

- .NET 6.0 atau yang lebih baru (kode ini juga berfungsi pada .NET Framework 4.x, cukup sesuaikan file proyeknya).
- Paket NuGet Aspose.OCR terpasang (`dotnet add package Aspose.OCR`).
- Familiaritas dasar dengan C# dan Visual Studio (atau IDE favorit Anda).

Jika Anda sudah memiliki semua itu, bagus—mari kita mulai.

## Langkah 1: Sematkan File Lisensi Aspose ke dalam Assembly Anda

Hal pertama yang Anda butuhkan adalah file lisensi yang sebenarnya (`Aspose.OCR.lic`). Alih-alih menyalinnya di samping executable Anda, Anda akan menyematkannya sebagai **resource**.

1. Tambahkan file `.lic` ke proyek Anda (misalnya, buat folder `Resources` dan letakkan file di sana).
2. Di properti file, atur **Build Action** menjadi `Embedded Resource`.  
   *Pro tip:* pertahankan struktur folder sederhana; nama sumber daya yang sepenuhnya memenuhi syarat akan menjadi `YourNamespace.Resources.Aspose.OCR.lic`.

```text
MyApp/
 └─ Resources/
     └─ Aspose.OCR.lic   ← Build Action = Embedded Resource
```

Mengapa menyematkan? Karena assembly kini membawa lisensi di dalamnya, menghilangkan risiko file yang hilang pada server produksi.

## Langkah 2: Ambil Sumber Daya Tersemat Menggunakan GetExecutingAssembly

Sekarang lisensi berada di dalam DLL, Anda memerlukan cara untuk **read embedded resource** pada runtime. Kelas .NET `Assembly` memberikan hal itu secara tepat.

```csharp
using System.Reflection;

// Get the assembly that contains the embedded resource
Assembly currentAssembly = Assembly.GetExecutingAssembly();
```

Metode `GetExecutingAssembly` mengembalikan assembly yang sedang berjalan—sempurna untuk menemukan sumber daya yang berada berdampingan dengan kode Anda.

## Langkah 3: Buka Stream Lisensi dengan GetManifestResourceStream

Dengan referensi assembly di tangan, Anda dapat memanggil `GetManifestResourceStream`. Metode ini mengembalikan `Stream` yang dapat Anda berikan langsung ke Aspose.

```csharp
// Build the fully qualified resource name
string resourceName = "MyApp.Resources.Aspose.OCR.lic";

// Attempt to open the resource stream
using Stream? licenseStream = currentAssembly.GetManifestResourceStream(resourceName);

if (licenseStream == null)
{
    throw new InvalidOperationException(
        $"Unable to locate embedded resource '{resourceName}'. " +
        "Check the namespace and Build Action settings.");
}
```

Perhatikan kami menggunakan pernyataan `using` **null‑conditional** (`using Stream?`) untuk memastikan stream dibuang secara otomatis. Jika nama salah, kami melempar pengecualian yang jelas—ini menyelamatkan Anda dari kegagalan diam-diam di kemudian hari.

## Langkah 4: Terapkan Lisensi ke Aspose OCR

Kelas `License` Aspose mengharapkan sebuah `Stream`. Kita sudah memilikinya, jadi langkah akhir menjadi sederhana.

```csharp
using Aspose.OCR;

// Create a License instance and set the license from the stream
License ocrLicense = new License();
ocrLicense.SetLicense(licenseStream);
```

Itu saja! Mesin Aspose OCR kini sepenuhnya berlisensi dan siap memproses gambar tanpa watermark percobaan.

## Contoh Kerja Lengkap

Berikut adalah program lengkap yang siap disalin‑tempel yang menunjukkan seluruh proses. Program ini mencakup direktif `using` yang diperlukan, penanganan error, dan panggilan OCR sederhana untuk membuktikan lisensi aktif.

```csharp
// Program.cs
using System;
using System.IO;
using System.Reflection;
using Aspose.OCR;

namespace MyApp
{
    class Program
    {
        static void Main()
        {
            try
            {
                // Step 1: Get the current executing assembly
                Assembly currentAssembly = Assembly.GetExecutingAssembly();

                // Step 2: Build the resource name (adjust namespace/folder as needed)
                const string resourceName = "MyApp.Resources.Aspose.OCR.lic";

                // Step 3: Retrieve the embedded license stream
                using Stream? licenseStream = currentAssembly.GetManifestResourceStream(resourceName);
                if (licenseStream == null)
                {
                    Console.WriteLine($"Failed to locate embedded resource: {resourceName}");
                    return;
                }

                // Step 4: Apply the license
                License ocrLicense = new License();
                ocrLicense.SetLicense(licenseStream);
                Console.WriteLine("Aspose OCR license applied successfully.");

                // Optional: Quick test – recognize text from a sample image
                var ocrEngine = new OcrEngine();
                ocrEngine.Image = ImageStream.FromFile("sample.png"); // replace with your image path
                if (ocrEngine.Process())
                {
                    Console.WriteLine("OCR Result:");
                    Console.WriteLine(ocrEngine.Text);
                }
                else
                {
                    Console.WriteLine("OCR processing failed.");
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

### Output yang Diharapkan

Saat Anda menjalankan program pada mesin dengan lisensi yang valid tersemat, Anda akan melihat:

```
Aspose OCR license applied successfully.
OCR Result:
[Detected text from sample.png]
```

Jika stream lisensi tidak dapat ditemukan, konsol akan melaporkan nama sumber daya yang hilang, mengarahkan Anda untuk memeriksa kembali **Build Action** dan namespace.

## Kesalahan Umum & Cara Menghindarinya

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Resource name mismatch** | .NET membangun nama resource dari namespace default + jalur folder. | Gunakan `Assembly.GetManifestResourceNames()` untuk menampilkan nama yang tersedia dan memverifikasi string yang tepat. |
| **License file not set as Embedded Resource** | Aksi Build default adalah `Content`. | Ubah menjadi `Embedded Resource` di properti file. |
| **Running from a different assembly** | Jika Anda memanggil kode dari pustaka kelas, `GetExecutingAssembly()` mungkin mengembalikan pustaka alih-alih exe utama. | Gunakan `Assembly.GetEntryAssembly()` atau berikan assembly yang tepat secara eksplisit. |
| **Stream disposed before use** | Tidak sengaja menggunakan blok `using` yang menutup stream terlalu cepat. | Pertahankan `using` di sekitar pemanggilan `SetLicense`, seperti yang ditunjukkan di atas. |
| **Aspose.OCR version mismatch** | Versi yang lebih baru mungkin memerlukan format lisensi yang berbeda. | Selalu unduh lisensi terbaru dari akun Aspose Anda dan sematkan kembali. |

## Menggunakan Teknik yang Sama untuk File Tersemat Lainnya

Pola—**read embedded resource**, kemudian **use GetManifestResourceStream**—bekerja untuk jenis file apa pun: konfigurasi JSON, gambar, bahkan DLL native. Cukup sesuaikan `resourceName` dan cara Anda menggunakan stream.

```csharp
// Example: Load an embedded JSON config
string jsonName = "MyApp.Resources.Config.appsettings.json";
using var jsonStream = Assembly.GetExecutingAssembly()
                               .GetManifestResourceStream(jsonName);
using var reader = new StreamReader(jsonStream);
string json = await reader.ReadToEndAsync();
```

## Gambaran Visual

![Diagram yang menggambarkan cara membaca sumber daya tersemat dan menetapkan lisensi Aspose](read-embedded-resource-diagram.png)

*Alt text:* read embedded resource – diagram yang menunjukkan proses penyematan, pengambilan dengan GetManifestResourceStream, dan penerapan lisensi Aspose.

## Ringkasan

Kami telah membahas cara **read embedded resource** dalam assembly .NET, langkah tepat untuk **use GetManifestResourceStream**, dan cara bersih untuk **set Aspose license** tanpa mengekspos file di disk. Dengan menyematkan lisensi, Anda menghilangkan masalah deployment dan menjaga aplikasi tetap portabel.

## Apa Selanjutnya?

- **Automate license updates:** Tulis skrip build‑time kecil yang menggantikan file `.lic` tersemat ketika Anda memperbarui langganan Aspose.
- **Secure the resource:** Pertimbangkan untuk mengenkripsi lisensi sebelum menyematkan dan mendekripsinya pada runtime untuk perlindungan tambahan.
- **Explore other Aspose products:** Pendekatan yang sama bekerja untuk Aspose.Words, Aspose.PDF, dll., masing‑masing dengan kelas `License`nya sendiri.

Silakan bereksperimen—mungkin Anda akan menyematkan beberapa lisensi untuk modul yang berbeda, atau beralih ke nama sumber daya yang dikendalikan oleh konfigurasi. Tidak ada batasnya.

---

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa forum Aspose untuk contoh lebih lanjut.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}