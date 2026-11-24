---
category: general
date: 2026-05-06
description: C#'ta toplu OCR nasıl yapılır ve Aspose OCR Batch kullanarak taramalardan
  metni hızlıca nasıl çıkarılır öğrenin. Kod, ipuçları ve uç durum yönetimiyle eksiksiz
  adım adım bir rehberi izleyin.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: tr
og_description: C#'ta toplu OCR nasıl yapılır? Bu rehber, Aspose OCR, GPU desteği
  ve paralel işleme ile taramalardan metni verimli bir şekilde çıkarmayı gösterir.
og_title: C#'ta Toplu OCR Nasıl Yapılır – Taramalardan Metin Çıkarma
tags:
- C#
- OCR
- Aspose
title: C#'ta Toplu OCR Nasıl Yapılır – Taramalardan Metin Çıkarma
url: /tr/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Toplu OCR Nasıl Yapılır – Taramalardan Metin Çıkarma

Ever wondered **how to batch OCR** when you have a folder full of scanned PDFs or JPEGs? You're not the only one staring at a mountain of images and thinking, “There has to be a faster way to pull the text out.” In this tutorial we’ll walk through a practical solution that not only lets you **extract text from scans** but also speeds things up with GPU acceleration and parallelism.

Şöyle ki: OCR'yi tek tek dosya üzerinde yapmak büyük bir zaman kaybı, özellikle onlarca ya da yüzlerce sayfa ile uğraşıyorsanız. Bu rehberin sonunda, tek bir komutla tüm bir dizini işleyen, indeksleme, arama veya sonraki adımlar için hazır temiz metin dosyaları üreten çalıştırmaya hazır bir C# konsol uygulamanız olacak.

## Önkoşullar

- **.NET 6.0 veya üzeri** (kod modern C# özelliklerini kullanır).
- **Aspose.OCR lisansı** (ücretsiz deneme testi için çalışır).
- **`UseGpu`** özelliğini etkinleştirmek istiyorsanız GPU uyumlu bir makine; aksi takdirde kütüphane CPU'ya geri dönecektir.
- **C# konsol uygulamaları** hakkında temel bilgi.

Harici hizmetler yok, gizli yapılandırma dosyaları yok—sadece SDK ve bir resim klasörü.

## Adım 1: Aspose.OCR NuGet Paketini Yükleyin

İlk olarak, Aspose OCR kütüphanesini projenize ekleyin. Çözüm klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

> **Pro ipucu:** Visual Studio kullanıyorsanız, paketi NuGet Package Manager UI üzerinden de ekleyebilirsiniz.

## Adım 2: Konsol Uygulaması Taslağını Oluşturun

Toplu işlemcimizi barındıracak minimal bir konsol uygulaması ayarlayalım. `Program.cs` adlı yeni bir dosya oluşturun ve aşağıdaki taslağı yapıştırın:

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

`Main` içinde mantığı neden sarıyoruz? Çünkü bir konsol uygulaması `Console.WriteLine` aracılığıyla anlık geri bildirim sağlar, **toplu OCR** işinin gerçekten tamamlandığını hızlıca doğrulamak için mükemmeldir.

## Adım 3: OcrBatchProcessor'ı Yapılandırın

Şimdi çözümün özüne geliyoruz. `OcrBatchProcessor`'ı örnekleyecek, giriş klasörümüzü gösterecek, sonuçların nereye kaydedileceğini belirtecek ve birkaç performans ayarını ince ayar yapacağız.

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### Bu ayarların önemi

| Setting | What it does | When you might change it |
|---------|--------------|--------------------------|
| `InputFolder` | İşlemek istediğiniz taramaların yolu. | Taşınabilirlik için göreceli bir yol kullanın. |
| `OutputFolder` | Her resmin çıkarılan metninin `.txt` dosyası olarak kaydedileceği yer. | Merkezi depolama gerekiyorsa bir ağ paylaşımına yönlendirin. |
| `Language` | OCR dil modeli; çok dilli desteği göstermek için İspanyolca seçtik. | `OcrLanguage.English` veya desteklenen başka bir dile geçin. |
| `UseGpu` | Yoğun matris hesaplamalarını GPU'ya devreder. | GPU'su olmayan başsız sunucularda `false` olarak ayarlayın. |
| `MaxDegreeOfParallelism` | Aynı anda kaç resmin işleneceğini kontrol eder. | Düşük CPU'lu makinelerde sınırlamayı azaltın. |

## Adım 4: Hata Yönetimiyle Toplu İşlemi Çalıştırın

Toplu işlemi çalıştırmak `Execute()` çağrısı kadar basittir, ancak bir try‑catch bloğu içinde saracağız, böylece bir şeyler ters gittiğinde (ör. eksik klasör, desteklenmeyen görüntü formatı) faydalı bir mesaj alırsınız.

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

İşlemci bitince, konsolda **Batch completed.** mesajını göreceksiniz ve her kaynak görüntünün `OcrResults` içinde eşleşen bir `.txt` dosyası olacak. Dosya adları orijinal ile aynı olduğundan, orijinal taramaya geri dönmek kolaydır.

## Adım 5: Çıktıyı Doğrulayın – Ne Beklenir

Program çalıştıktan sonra, `YOUR_DIRECTORY/OcrResults` içindeki herhangi bir dosyayı açın. İlgili görüntüden çıkarılmış düz metin içeriğini görmelisiniz, örneğin:

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

Çıktı bozuk görünüyorsa, `Language` ayarının taramalarınızın diliyle eşleştiğini iki kez kontrol edin. Aspose OCR 100'den fazla dili destekler, bu yüzden `OcrLanguage.Spanish` yerine ihtiyacınıza uygun bir dili kullanabilirsiniz.

## Kenar Durumları ve Yaygın Tuzakların Ele Alınması

### 1. GPU Mevcut Değil

Makinenizde uyumlu bir GPU yoksa, `UseGpu = true` sessizce CPU moduna geri dönecek, ancak hız artışını kaybedeceksiniz. Açık olmak için GPU yeteneğini şu şekilde algılayabilirsiniz:

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. Belleği Aşan Büyük Dosyalar

Devasa TIFF'ler veya PDF'lerle çalışırken, onları daha küçük görüntülere önceden bölmeyi düşünün. Aspose OCR çok sayfalı PDF'leri işleyebilir, ancak bellek tüketimi sayfa sayısıyla artar. `Aspose.Imaging` kullanarak basit bir ön işleme adımı, belgeyi yönetilebilir parçalara bölerek çözüm sağlar.

### 3. Giriş Klasöründeki Görüntü Olmayan Dosyalar

Toplu işlemci işleyemediği dosyaları görmezden gelir, ancak klasörü temiz tutmak iyi bir uygulamadır. Uzantıya göre filtreleyebilirsiniz:

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*(Not: `FileFilter` varsayımsal bir özelliktir; mevcutsa gerçek API ile değiştirin.)*

## Tam Çalışan Örnek

Aşağıda, tamamen kopyala‑yapıştır hazır program bulunmaktadır. `YOUR_DIRECTORY` ifadesini makinenizdeki tam yol ile değiştirin.

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Beklenen Konsol Çıktısı

```
Batch completed.
```

Ve `C:\OcrResults` içinde `C:\MyScans` içindeki her görüntü için bir `.txt` dosyası bulacaksınız.

## Sonuç

Artık C#'ta **toplu OCR nasıl yapılır** ve **taramalardan metin çıkarma** işlemini manuel olarak her dosyayı açmadan yapabileceğiniz sağlam, üretim‑hazır bir yönteme sahipsiniz. Aspose'un toplu API'si, GPU hızlandırması ve yapılandırılabilir paralellik sayesinde çözüm birkaç sayfadan binlerce sayfaya ölçeklenebilir.

Sonraki adım ne? Şu fikirleri deneyin:

- **Bir arama indeksiyle bütünleştirin** (ör. Elasticsearch) böylece çıkarılan metin aranabilir olur.
- **Yazım denetimi veya dil tespiti** gibi son‑işlem ekleyin.
- **Konsol uygulamasını bir Windows Servisi** olarak paketleyin, böylece bir bırakma klasörünü sürekli izleyebilirsiniz.

Paralellik seviyesini değiştirmek, dil modelini takas etmek ya da başka deneyler yapmakta özgürsünüz. Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın—iyi OCRlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}