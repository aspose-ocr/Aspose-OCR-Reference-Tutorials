---
category: general
date: 2026-04-06
description: Cara mengatur lisensi di Aspose OCR menggunakan C# – pelajari cara menyematkan
  sumber daya, mengambil sumber daya yang disematkan, dan memuat lisensi dari file
  atau aliran dalam beberapa langkah saja.
draft: false
keywords:
- how to set license
- how to embed resource
- get embedded resource
- how to load license
- use license stream
language: id
og_description: Cara mengatur lisensi di Aspose OCR dijelaskan langkah demi langkah.
  Pelajari cara menyematkan lisensi, mengambilnya, dan menggunakan aliran lisensi
  untuk integrasi yang mulus.
og_title: Cara Mengatur Lisensi di Aspose OCR – Panduan Lengkap C#
tags:
- Aspose OCR
- C#
- .NET licensing
title: Cara Mengatur Lisensi di Aspose OCR – Panduan Lengkap C#
url: /id/net/ocr-configuration/how-to-set-license-in-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengatur Lisensi di Aspose OCR – Panduan Lengkap C#

Mengatur lisensi di Aspose OCR adalah tantangan umum bagi pengembang. Dalam tutorial ini kami akan menjelaskan langkah‑langkah tepat untuk mengatur lisensi, menyematkannya sebagai sumber daya, dan memuatnya dari stream—sehingga Anda dapat mulai melakukan OCR tanpa watermark mode percobaan yang mengganggu.

Pernah mencoba menjalankan pekerjaan OCR hanya untuk melihat banner “Evaluation version”? Itu merupakan gejala lisensi yang hilang atau tidak diterapkan dengan benar. Pada akhir panduan ini Anda akan memiliki instance Aspose OCR yang berlisensi penuh, baik Anda menyimpan file `.lic` berdampingan dengan binary Anda atau menyembunyikannya di dalam assembly.

## Apa yang Anda Butuhkan

- **Aspose.OCR for .NET** (paket NuGet terbaru pada saat penulisan – 23.10)
- **file lisensi Aspose OCR yang valid** (`Aspose.OCR.lic`)
- Visual Studio 2022 atau IDE kompatibel C# apa pun
- Familiaritas dasar dengan penyematan sumber daya .NET (kami akan membahasnya)

Tidak diperlukan pustaka pihak ketiga tambahan; semuanya berada di dalam paket Aspose.

![Ilustrasi cara mengatur lisensi](image.png "Cara mengatur lisensi")

## Langkah 1: Instal Paket NuGet Aspose.OCR

Sebelum Anda dapat menulis kode lisensi apa pun, pastikan pustaka sudah direferensikan:

```bash
dotnet add package Aspose.OCR
```

Atau, melalui NuGet manager di Visual Studio, cari **Aspose.OCR** dan klik *Install*. Ini akan mengunduh `Aspose.OCR.dll` beserta dependensinya.

> **Pro tip:** Target .NET 6 atau yang lebih baru untuk menikmati API terbaru dan kinerja yang lebih baik.

## Langkah 2: Buat Objek License – Inti dari “Cara Mengatur Lisensi”

Aspose menggunakan kelas `License` sederhana untuk menerapkan kunci komersial. Membuat instance-nya adalah baris pertama dalam alur kerja berlisensi apa pun:

```csharp
using Aspose.OCR;

// Step 2: Create a License object
var ocrLicense = new License();
```

Mengapa ini penting: instance `License` membaca konten `.lic` dan mendaftarkannya secara global untuk AppDomain saat ini. Setelah terdaftar, setiap `OcrEngine` yang Anda buat akan beroperasi dalam mode penuh fitur.

## Langkah 3: Terapkan Lisensi dari File (“Cara Memuat Lisensi” Klasik)

Jika Anda lebih suka menyimpan file lisensi di samping executable Anda, panggil `SetLicense` dengan jalur file:

```csharp
// Step 3: Apply the license from a file (replace with your actual path)
ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

### Hal-hal yang Perlu Diwaspadai

- **Absolute vs. relative paths:** Jalur relatif diresolusikan terhadap *working directory* proses, yang biasanya adalah folder bin.
- **File permissions:** Akun yang menjalankan aplikasi harus memiliki akses baca ke file `.lic`.
- **Exception handling:** `SetLicense` melempar `FileNotFoundException` jika jalur salah, jadi bungkus dalam `try/catch` jika Anda memerlukan penurunan yang elegan.

## Langkah 4: Cara Menyematkan Resource – Menyimpan Lisensi di Dalam Assembly Anda

Menyematkan lisensi menghilangkan kebutuhan mengirim file terpisah. Berikut cara **menyematkan resource** ke dalam proyek .NET:

1. Tambahkan file `.lic` ke proyek Anda (misalnya, di dalam folder bernama `Resources`).
2. Klik kanan file → *Properties* → atur **Build Action** menjadi **Embedded Resource**.
3. Build proyek; lisensi menjadi bagian dari DLL yang dikompilasi.

Sekarang Anda dapat mengambilnya dengan logika **get embedded resource**.

## Langkah 5: Dapatkan Stream Resource yang Disematkan

Potongan kode berikut menunjukkan **get embedded resource** menggunakan refleksi. Sesuaikan namespace dan nama resource agar cocok dengan struktur proyek Anda:

```csharp
using System.Reflection;

// Step 5: Load the embedded license stream
using var licenseStream = Assembly.GetExecutingAssembly()
                                 .GetManifestResourceStream("MyApp.Resources.Aspose.OCR.lic");

if (licenseStream == null)
{
    throw new InvalidOperationException("Embedded license not found. Check the resource name.");
}
```

> **Mengapa refleksi?** `Assembly.GetExecutingAssembly()` mengacu pada assembly yang sedang berjalan, memastikan kode berfungsi baik di aplikasi console, situs web, atau Azure Function.

## Langkah 6: Gunakan Stream Lisensi – Pola “use license stream”

Setelah Anda memiliki stream, **use license stream** untuk menerapkan lisensi tanpa menyentuh sistem file:

```csharp
// Step 6: Apply the license using the stream
ocrLicense.SetLicense(licenseStream);
```

Ketika `SetLicense` menerima sebuah `Stream`, Aspose membaca byte secara langsung, mendaftarkan lisensi, dan membuang stream ketika Anda keluar dari blok `using`. Ini adalah cara paling bersih untuk menyembunyikan lisensi Anda.

### Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program mandiri yang menunjukkan ketiga pendekatan (file, resource yang disematkan, dan stream). Komentari bagian yang tidak Anda perlukan.

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

namespace LicenseDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣  Create the License object – core of how to set license
            // -------------------------------------------------
            var ocrLicense = new License();

            // -------------------------------------------------
            // 2️⃣  Option A: Load from external .lic file (how to load license)
            // -------------------------------------------------
            // Replace with your actual path or use a relative path.
            // ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // -------------------------------------------------
            // 3️⃣  Option B: Load from an embedded resource (how to embed resource)
            // -------------------------------------------------
            // Ensure the .lic file is added as an Embedded Resource.
            // string resourceName = "LicenseDemo.Resources.Aspose.OCR.lic";
            // using var licenseStream = Assembly.GetExecutingAssembly()
            //                                   .GetManifestResourceStream(resourceName);
            // if (licenseStream == null)
            // {
            //     Console.WriteLine("Embedded license not found.");
            //     return;
            // }
            // ocrLicense.SetLicense(licenseStream); // use license stream

            // -------------------------------------------------
            // 4️⃣  Verify the license – no exception means success
            // -------------------------------------------------
            Console.WriteLine("License applied successfully!");

            // -------------------------------------------------
            // 5️⃣  Run a quick OCR test to prove it works
            // -------------------------------------------------
            var engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample.png"); // replace with your image
            engine.Recognize();

            Console.WriteLine("Recognized text:");
            Console.WriteLine(engine.Text);
        }
    }
}
```

**Output yang Diharapkan**

```
License applied successfully!
Recognized text:
[Your OCR result here]
```

Jika lisensi tidak diterapkan, Aspose akan melempar `LicenseException` atau Anda akan melihat watermark evaluasi pada hasil OCR.

## Kesalahan Umum & Cara Menghindarinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| “Evaluation version” banner masih muncul | Lisensi tidak dimuat atau jalur salah | Periksa kembali jalur file atau nama resource yang disematkan. |
| `NullReferenceException` pada `GetManifestResourceStream` | Nama resource typo atau Build Action tidak diatur ke Embedded Resource | Verifikasi nama dengan namespace yang lengkap dan atur Build Action dengan benar. |
| Lisensi berfungsi secara lokal tetapi gagal setelah deployment | Tidak ada izin baca pada server | Berikan identitas app pool izin baca ke file `.lic`, atau sematkan lisensi untuk menghindari masalah sistem file. |
| Beberapa objek `License` tidak memberikan efek | Anda memanggil `SetLicense` pada instance *berbeda* setelah yang pertama | Gunakan satu instance `License` per AppDomain; gunakan kembali atau panggil `SetLicense` sekali saat startup. |

## Kapan Memilih Setiap Pendekatan

- **File‑based** – Prototipe cepat, mudah diganti tanpa rebuild.
- **Embedded resource** – Ideal untuk distribusi desktop atau library dimana Anda tidak ingin lisensi tersebar.
- **Stream‑based** – Sempurna untuk lingkungan cloud (Azure Functions, AWS Lambda) dimana Anda dapat mengambil lisensi dari vault aman dan memberikannya secara langsung.

## Langkah Selanjutnya – Memperluas Pengetahuan Lisensi Anda

Setelah Anda menguasai **cara mengatur lisensi**, Anda mungkin ingin menjelajahi:

- **How to embed resource** dalam solusi multi‑project yang lebih kompleks.
- **Get embedded resource** dari satellite assemblies untuk skenario lokalisasi.
- **How to load license** secara dinamis dari Azure Key Vault atau AWS Secrets Manager.
- **Use license stream** bersama dependency injection untuk kode startup yang lebih bersih.

Setiap topik ini membangun di atas dasar yang dibahas di sini dan membantu Anda menjaga strategi lisensi tetap aman dan dapat dipelihara.

---

### TL;DR

Kami telah menunjukkan **cara mengatur lisensi** di Aspose OCR menggunakan tiga teknik handal: memuat dari file, menyematkan `.lic` sebagai resource, dan menerapkannya melalui stream. Ikuti kode, perhatikan jebakan, dan mesin OCR Anda akan berjalan dengan kecepatan penuh—tanpa watermark percobaan, tanpa kejutan.

Selamat coding, semoga hasil OCR Anda jernih seperti kristal!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}