---
category: general
date: 2026-02-24
description: Aspose OCR C# örneğinde GPU'yu nasıl etkinleştirirsiniz – görüntüyü hızlıca
  düz metne dönüştürün. GPU cihaz kimliğini ayarlama ve görüntü metnini okuma C# rehberi
  içerir.
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: tr
og_description: Aspose OCR C# örneğinde GPU'yu nasıl etkinleştirirsiniz. GPU cihaz
  kimliğini ayarlamayı ve C# ile görüntü metnini verimli bir şekilde okumayı öğrenin.
og_title: C#'ta Aspose OCR için GPU'yu Nasıl Etkinleştirirsiniz – Hızlı Görüntüden
  Düz Metne
tags:
- Aspose OCR
- C#
- GPU acceleration
title: C#'ta Aspose OCR için GPU'yu Nasıl Etkinleştirirsiniz – Hızlı Görüntüden Düz
  Metne
url: /tr/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

Make sure markdown formatting preserved.

Let's construct final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR için C#'ta GPU Nasıl Etkinleştirilir – Hızlı Görüntüden Düz Metne

Aspose OCR kullanarak bir resmi düzenlenebilir metne dönüştürürken **GPU'nun nasıl etkinleştirileceğini** hiç merak ettiniz mi? Tek başınıza değilsiniz—birçok geliştirici büyük faturalar veya taranmış sözleşmeler işlenirken performans duvarına çarpıyor. İyi haber? Görüntüyü düz metne dönüştürmek, grafik kartınızı kullandığınızda ışık hızında olabilir.

Bu rehberde, GPU'yu nasıl etkinleştireceğinizi, GPU cihaz kimliğini nasıl ayarlayacağınızı ve **C# tarzında görüntü metnini okuma** işlemini gösteren eksiksiz bir **Aspose OCR örneği** üzerinden geçeceğiz. Sonunda, yalnızca CPU kullanan bir yaklaşıma göre çok daha kısa sürede desteklenen herhangi bir görüntüden metin çıkaran çalıştırılabilir bir programınız olacak.

## Gereksinimler

- .NET 6.0 veya daha yenisi (API .NET Core ve .NET Framework ile çalışır)
- En son sürücü yüklü CUDA‑uyumlu bir GPU
- Aspose.OCR for .NET lisansı (veya geliştirme için çalışan ücretsiz deneme sürümü)
- Visual Studio 2022 (veya tercih ettiğiniz herhangi bir C# editörü)

`Aspose.OCR` dışındaki ekstra NuGet paketlerine gerek yok—yalnızca kütüphane yeterli.

## Adım 1 – Aspose OCR NuGet Paketini Yükleyin

İlk olarak, resmi Aspose OCR kütüphanesini projenize ekleyin. Package Manager Console'u açın ve şu komutu çalıştırın:

```powershell
Install-Package Aspose.OCR
```

Bu, `Aspose.OCR.dll` ve tüm bağımlılıklarını getirir. GUI'yi tercih ediyorsanız, projenize sağ‑tıklayın → **Manage NuGet Packages** → *Aspose.OCR* aratın ve **Install**'a tıklayın.  

*Pro tip:* Kurulumdan sonra, Solution Explorer'da **Dependencies** altında `Aspose.OCR` klasörünün göründüğünden emin olun.

## Adım 2 – Basit Bir Konsol Uygulaması Taslağı Oluşturun

Tüm akışı gösteren küçük bir konsol uygulaması oluşturacağız. Yeni bir proje oluşturun:

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

Oluşturulan `Program.cs` dosyasını daha sonra gösterilecek tam kodla değiştirin. Bu taslak temiz bir giriş noktası sağlar ve OCR mantığına odaklanmamıza izin verir.

## Adım 3 – GPU'yu Nasıl Etkinleştirir ve GPU Cihaz Kimliğini Nasıl Ayarlarsınız

Şimdi gösterinin yıldızı: Aspose OCR'de **GPU'nun nasıl etkinleştirileceği**. Kütüphane, `UseGpu` özelliğini açıp kapatabileceğiniz ve isteğe bağlı olarak `GpuDeviceId` ile belirli bir CUDA cihazı seçebileceğiniz bir `OcrSettings` nesnesi sunar. Aşağıda programınıza ekleyeceğiniz tam kod parçacığı bulunuyor:

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Neden GPU Etkinleştirilmeli?

GPU'yu etkinleştirmek, yoğun işlemleri—piksel ön işleme, karakter segmentasyonu ve sinir ağı çıkarımı—grafik kartına devreder. Orta seviye bir GTX 1650'de, özellikle yüksek çözünürlüklü belgelerde CPU‑yalnızca moda göre **2‑3 kat hız artışı** görebilirsiniz.

### Cihaz Kimliği Seçimi

Makinenizde birden fazla GPU varsa, `GpuDeviceId` belirli bir tanesini hedeflemenizi sağlar. `0` ilk cihazı seçer; `1` ikinciyi, vb. Mevcut kimlikleri NVIDIA `nvidia-smi` aracıyla veya Aspose'un `GpuInfo` sınıfını sorgulayarak (kısalık için burada gösterilmemiş) öğrenebilirsiniz.

## Adım 4 – Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda eksiksiz, çalıştırmaya hazır program bulunuyor. `Program.cs` içine yapıştırın, görüntü yolunu diskinizdeki gerçek bir dosyayla değiştirin ve **F5** tuşuna basın.

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### Beklenen Çıktı

Eğer sağlanan görüntü *“Invoice #12345 – Total $1,250.00”* satırını içeriyorsa, konsol şu çıktıyı verir:

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

Sonuç düz metindir ve daha fazla işleme hazırdır (örneğin bir veritabanına ya da doğal dil ayrıştırıcısına beslemek).

## Adım 5 – GPU Kullanımını Doğrulama (İsteğe Bağlı)

GPU'nun gerçekten kullanıldığından emin olmak için program çalışırken GPU izleme aracınızı (örneğin **NVIDIA‑Smi** veya **GPU-Z**) açın. Seçilen cihaz için işlemci kullanımında bir artış görmelisiniz. Sadece CPU aktivitesi görürseniz, şunları tekrar kontrol edin:

- GPU sürücüsü güncel olmalı.
- `UseGpu` bayrağı `true` olarak ayarlanmalı.
- Görüntü formatınız destekleniyor olmalı (PNG, JPEG, TIFF, vb.).

## Yaygın Tuzaklar ve Nasıl Önlenir

| Sorun | Neden Oluşur | Hızlı Çözüm |
|-------|--------------|-------------|
| **GPU algılanmadı** | Güncel olmayan sürücü veya eksik CUDA çalışma zamanı | En son NVIDIA sürücüsü ve CUDA araç setini kurun |
| **`Aspose.OCR` “GPU not supported” hatası veriyor** | CUDA destekli olmayan bir GPU'da çalışıyor (örneğin eski AMD) | `UseGpu = false` olarak ayarlayın veya uyumlu bir GPU'ya geçin |
| **Yanlış görüntü yolu** | Göreceli yol yanlış klasöre işaret ediyor | Mutlak yol kullanın veya yolu komut satırı argümanı olarak geçirin |
| **Lisans uygulanmadı** | Değerlendirme modu GPU kullanımını sınırlayabilir | `License license = new License(); license.SetLicense("Aspose.OCR.lic");` ile lisans kaydedin |

## Örneği Genişletme: GPU ile Toplu İşleme

Eğer onlarca fatura işlemek istiyorsanız, tanıma çağrısını bir döngü içinde sarın. GPU sıcak kaldığı için sonraki görüntüler **ısınma önbelleklemesinden** faydalanır ve her çalıştırmada birkaç milisaniye daha tasarruf sağlar.

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

Aynı `OcrEngine` örneğini tutmayı unutmayın—her dosya için yeni bir motor oluşturmak GPU bağlamını yeniden başlatır ve performansı düşürür.

## Sonuç

Artık **GPU'nun nasıl etkinleştirileceğini**, **GPU cihaz kimliğinin nasıl ayarlanacağını** ve **C# tarzında görüntü metninin nasıl okunacağını** gösteren sağlam, uçtan uca bir **Aspose OCR örneğine** sahipsiniz. `UseGpu`'yu açıp doğru cihaza yönlendirerek, yavaş CPU‑bağlı bir OCR görevini büyük faturalar, makbuzlar veya herhangi bir taranmış belgeyi işleyebilen yüksek verimli bir boru hattına dönüştürürsünüz.

Denemekten çekinmeyin: farklı görüntü formatlarını deneyin, çoklu GPU sistemlerinde `GpuDeviceId`'yi ayarlayın veya PDF oluşturma için diğer Aspose kütüphaneleriyle birleştirin. GPU devreye girdiğinde sınır yoktur.

<img src="gpu-ocr.png" alt="C# ile Aspose OCR'de GPU'yu nasıl etkinleştiririz – görüntüyü hızlıca düz metne dönüştürme">

*Kodlamaktan keyif alın! Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da daha derin incelemeler için Aspose'un resmi forumlarına göz atın.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}