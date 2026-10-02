---
category: general
date: 2026-02-20
description: Aspose OCR'un GPU hızlandırmasıyla görüntüden metni hızlıca tanıyın.
  C# ile taramadan metin çıkarmayı, eksiksiz ve çalıştırılabilir bir örnekle öğrenin.
draft: false
keywords:
- recognize text from image
- extract text from scan
- Aspose OCR GPU
- C# OCR tutorial
- image to text conversion
language: tr
og_description: GPU hızlandırmasıyla görüntüden metin tanıma. Bu öğreticide, Aspose
  OCR kullanarak C#’ta taramadan metin nasıl çıkarılacağını, kod ve ipuçlarıyla birlikte
  gösteriyoruz.
og_title: Aspose OCR GPU kullanarak görüntüden metin tanıma – C# Rehberi
tags:
- Aspose
- OCR
- C#
- GPU
title: C#'ta Aspose OCR GPU kullanarak görüntüden metin tanıma
url: /tr/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU kullanarak C#'ta görselden metin tanıma

Görselden **metin tanıma** ihtiyacınız hiç oldu mu ama dosya çok büyüktü ve CPU'nuz zorlandı? Belki eski bir OCR kütüphanesini denediniz ve sonsuza kadar sürdü ya da sonuçlar eksikti. İyi haber? Aspose OCR'nun GPU hızlandırmasıyla devasa bir taranmış TIFF'i saniyeler içinde temiz, aranabilir metne dönüştürebilirsiniz.

Bu rehberde, GPU destekli bir makinede **tarama dosyalarından metin çıkarma** işlemini gösteren tam, kopyala‑yapıştır‑hazır bir örnek üzerinden adım adım ilerleyeceğiz. Belirsiz referanslar yok, sadece ihtiyacınız olan kod, her satırın önemi ve sizi sinir bozucu hatalardan koruyacak birkaç ipucu.

## Gereksinimler

- **.NET 6+** (veya .NET Framework 4.7+ – API aynı şekilde çalışır)
- **Aspose.OCR for .NET** NuGet paketi (versiyon 23.12 veya sonrası)
- **CUDA** desteğine sahip bir **GPU** (isteğe bağlı, ancak çok daha hızlı)
- Yüksek çözünürlüklü taranmış bir görüntü (ör. `large_doc.tif`)

GPU'nuz yoksa, motor otomatik olarak CPU'ya geçer—bu yüzden örneği hâlâ çalıştırabilirsiniz, sadece biraz daha yavaş.

## Adım 1 – Aspose.OCR Paketini Yükleyin

Terminalinizi veya Package Manager Console'ı açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Ya da Visual Studio'nun NuGet arayüzünde **Aspose.OCR**'ı aratıp *Install* (Yükle) düğmesine tıklayın. Bu, temel OCR kütüphanesini ve isteğe bağlı GPU hızlandırma derlemesini getirir.

> **Pro ipucu:** Yükledikten sonra `packages` klasöründe `Aspose.OCR.Acceleration.dll` dosyasını kontrol edin. GPU desteği için gereklidir; eğer başsız (headless) bir sunucuda çalışıyorsanız, bunu atlayabilirsiniz ve kod yine derlenecektir.

## Adım 2 – GPU Hızlandırmalı OCR Motorunu Başlatın

`GpuOcrEngine` sınıfı uyumlu bir GPU'yu otomatik olarak algılar. Birden fazla cihazınız varsa belirli bir tanesini seçebilirsiniz, ancak çoğu geliştirici motorun kendisinin karar vermesine izin verir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration;   // <-- enables GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Create the OCR engine. It will look for a CUDA‑compatible GPU.
        GpuOcrEngine ocrEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Force a particular GPU device.
        // Uncomment the line below if you know the device ID you want to use.
        // ocrEngine.Device = GpuDevice.GetById(0);
```

**Neden önemli:** GPU motorunu bir kez başlatmak, ek yükü düşük tutar. Motoru bir döngü içinde tekrar tekrar oluşturup yok ederseniz, performans kazanımlarını kaybedersiniz.

## Adım 3 – Yüksek Çözünürlüklü Taranmış Görüntünüzü Yükleyin

Aspose OCR, `System.Drawing.Image` ile çalışır. Dosya yolunun gerçek bir görüntüye işaret ettiğinden emin olun; aksi takdirde `FileNotFoundException` alırsınız.

```csharp
        // Step 3: Load the image you want to process.
        // Replace YOUR_DIRECTORY with the actual folder on your machine.
        var scannedImage = Image.FromFile(@"YOUR_DIRECTORY/large_doc.tif");
```

> **Köşe durum:** Görüntü 10 000 × 10 000 px'den büyükse, önce ölçek küçültmeyi düşünün. GPU belleği sınırlıdır ve devasa bir bitmap yüklemeye çalışmak `OutOfMemoryException` oluşturabilir.

## Adım 4 – Varsayılan (Latin) Dil Ayarlarıyla OCR Gerçekleştirin

`Recognize` metodu düz bir string döndürür. Farklı bir dil veya özel ön işleme ihtiyacınız varsa bir `OcrOptions` nesnesi geçirebilirsiniz.

```csharp
        // Step 4: Run OCR. By default it assumes Latin script.
        string recognizedText = ocrEngine.Recognize(scannedImage);
```

**Neden varsayılan çalışır:** Çoğu taranmış belge—sözleşmeler, faturalar, raporlar—Latin temelli alfabelerdedir. Eğer Kiril, Arapça veya Çinceye ihtiyacınız varsa, `Recognize` çağırmadan önce `ocrEngine.Language = "ru"` (veya uygun ISO kodu) olarak ayarlayın.

## Adım 5 – Çıkarılan Metni Görüntüle veya Sakla

Hızlı bir doğrulama için sonucu sadece konsola yazdıracağız. Gerçek bir uygulamada bunu bir veritabanına, bir `.txt` dosyasına kaydedebilir veya bir arama indeksine besleyebilirsiniz.

```csharp
        // Step 5: Output the OCR result.
        Console.WriteLine(recognizedText);

        // Optional: Save to a file.
        // File.WriteAllText(@"output.txt", recognizedText);
    }
}
```

### Beklenen Çıktı

`large_doc.tif` basit bir paragraf, örneğin “Hello, world!” içeriyorsa, şu çıktıyı görürsünüz:

```
Hello, world!
```

Çok sayfalı taramalarda motor, metni okuma sırasına göre birleştirir. Sayfa sınırlarına ihtiyacınız varsa, daha sonra satır sonları (`\n`) ile bölüştürebilirsiniz.

## Yaygın Sorunlarla Baş Etme

| Sorun | Belirti | Çözüm |
|-------|---------|-----|
| **GPU bulunamadı** | `ocrEngine.Device` `null` ve işlem yavaş. | En son NVIDIA sürücüsünü ve CUDA Toolkit'i (v11+) kurun. `nvidia-smi` ile doğrulayın. |
| **Garbage collection gecikmeleri** | Birçok görüntü işledikten sonra bellek dalgalanması. | OCR sonrası `scannedImage.Dispose()` çağırın veya görüntüyü bir `using` bloğuna alın. |
| **Yanlış dil** | Latin dışı metinlerde bozuk karakterler. | `Recognize` çağırmadan önce `ocrEngine.Language`'ı doğru ISO 639‑1 koduna ayarlayın. |
| **Çok büyük dosyalar** | `OutOfMemoryException`. | `Image.GetThumbnailImage` ile ölçek küçültün veya taramayı parçalara bölün. |

## Tam, Çalıştırmaya Hazır Örnek

Aşağıda tüm program yer alıyor—`using` yönergeleri, hata yönetimi ve görüntü için düzenli bir `using` bloğu dahil:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration; // GPU support

class GpuOcrDemo
{
    static void Main()
    {
        try
        {
            // Initialize the GPU‑accelerated OCR engine.
            GpuOcrEngine ocrEngine = new GpuOcrEngine();

            // OPTIONAL: Choose a specific GPU device.
            // ocrEngine.Device = GpuDevice.GetById(0);

            // Load the high‑resolution scanned image.
            string imagePath = @"YOUR_DIRECTORY/large_doc.tif";
            if (!File.Exists(imagePath))
                throw new FileNotFoundException($"Image not found: {imagePath}");

            using (Image scannedImage = Image.FromFile(imagePath))
            {
                // Perform OCR (defaults to Latin script).
                string text = ocrEngine.Recognize(scannedImage);

                // Output the extracted text.
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(text);

                // Save to a text file (optional).
                string outputPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(outputPath, text);
                Console.WriteLine($"Text saved to {outputPath}");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Bu Kod Ne Yapıyor

1. **Oluşturur** en iyi GPU'yu otomatik seçen bir `GpuOcrEngine`.
2. **Yükler** hedef TIFF'i bir `using` bloğu içinde, atık oluşmasını garantileyerek.
3. **Çağırır** `Recognize` metodunu, bitmap'i string'e dönüştürmek için.
4. **Yazar** sonucu hem konsola hem de kaynak görüntünün yanındaki bir `.txt` dosyasına.
5. **Yakalar** herhangi bir istisna ve dostça bir hata mesajı yazdırır.

## İleri Adımlar – “görselden metin tanıma”dan Tam Ölçekli Belge Boru Hatlarına

Artık **tarama dosyalarından metin çıkarabildiğinize** göre, şu sonraki adımları düşünün:

- **Toplu işleme:** TIFF klasörünü döngüyle gezerek sonuçları tek bir aranabilir indeks içinde birleştirin.
- **Dil tespiti:** `ocrEngine.DetectLanguage()` (varsa) kullanarak dilleri otomatik değiştirin.
- **Son işleme:** Çıktıyı bir yazım denetleyicisi veya regex filtresiyle çalıştırarak OCR artefaktlarını temizleyin.
- **Azure Cognitive Search ile entegrasyon:** Çıkarılan metni anında sorgulanabilir bir bulut indeksine gönderin.

Bunların her biri, az önce gördüğünüz aynı temel desen üzerine kuruludur—bir kez başlat, görüntüleri besle, metni topla.

## Sonuç

Aspose OCR'nun GPU hızlandırmalı motorunu C#'ta kullanarak **görselden metin tanıma** yöntemini yeni öğrendiniz. Tam, çalıştırılabilir örnek, motoru nasıl kuracağınızı, yüksek çözünürlüklü bir taramayı nasıl yükleyeceğinizi, OCR'ı nasıl gerçekleştireceğinizi ve çıktıyı nasıl yöneteceğinizi gösteriyor. Yukarıdaki ipuçlarını ve köşe durumlarını izleyerek, yaygın sorunlardan kaçınacak ve geliştirici dizüstü bilgisayarında ya da üretim sunucusunda çalışırken güvenilir sonuçlar elde edeceksiniz.

Daha fazla taramayı aranabilir veri haline getirmeye hazır mısınız? Tüm bir klasörü işleyin, Latin dışı dillerle deney yapın veya sonuçları tam metin arama motoruna besleyin. Gökyüzü sınırdır ve az önce yazdığınız kod, ihtiyacınız olan sağlam temeldir.

Kodlamanın tadını çıkarın! 🚀

![recognize text from image example](/images/ocr-gpu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}