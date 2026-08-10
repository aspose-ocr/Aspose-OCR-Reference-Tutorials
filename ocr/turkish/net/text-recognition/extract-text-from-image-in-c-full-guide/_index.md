---
category: general
date: 2026-03-23
description: Aspose OCR kullanarak C#'ta görüntüden metin çıkarın ve gerçek zamanlı
  geri bildirim için konsol günlüğü eklemeyi öğrenin.
draft: false
keywords:
- extract text from image
- add console logger
language: tr
og_description: Aspose OCR ile görüntüden metin çıkarın ve süreci izlemek için konsol
  günlüğü ekleyin. Adım adım C# öğreticisi.
og_title: C#'ta Görüntüden Metin Çıkarma – Tam Programlama Rehberi
tags:
- OCR
- C#
- logging
title: C#'ta Görüntüden Metin Çıkarma – Tam Rehber
url: /tr/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkarma C# ile – Tam Kılavuz

Görüntüden **metin çıkarmak** için hızlı ve güvenilir bir çözüm mü arıyorsunuz? Aspose OCR ile bunu birkaç satır C# koduyla yapabilirsiniz.  
**add console logger**'ı nasıl ekleyeceğinizi de göstereceğiz, böylece OCR motorunun ilerlemesini doğrudan terminalinizde izleyebilirsiniz.

Tarayıcıdan alınmış bir makbuz, el yazısı bir not ya da PNG olarak kaydedilmiş bir PDF sayfanız olduğunu hayal edin. Yoğun bir kullanıcı arayüzü açmadan ham karakterleri elde etmek istiyorsunuz. Bu öğretici, .NET 6+ ve en yeni Aspose OCR kütüphanesiyle çalışan eksiksiz, kopyala‑yapıştır çözümünü adım adım gösterir.

Bu kılavuzun sonunda şunları yapabilecek duruma geleceksiniz:

* Bir görüntü dosyasını yükleyip OCR çalıştırarak **görüntüden metin çıkarma** verisini elde edebilirsiniz.  
* Aspose AI'ye bir console logger ekleyerek kütüphanenin arka planda neler yaptığını görebilirsiniz.  
* OCR hatalarını temizlemek için yerleşik yazım denetimi post‑processor'ını uygulayın.  

> **Prerequisites** – Çalışan bir .NET geliştirme ortamı (Visual Studio 2022, VS Code veya Rider), .NET 6 SDK veya daha yeni bir sürüm ve bir Aspose OCR lisansı (veya ücretsiz deneme). Başka üçüncü‑taraf paketine gerek yok.

---

## İhtiyacınız Olanlar

| Öğe | Neden Önemli |
|------|----------------|
| **Aspose.OCR** NuGet package | `OcrEngine` sınıfını sağlayarak görüntüyü okur. |
| **Aspose.OCR.AI** NuGet package | `AsposeAI` post‑processor çerçevesini, yazım denetimi dahil, size sunar. |
| **Microsoft.Extensions.Logging** (optional) | `ILogger` arayüzünü **add console logger** adımı için sağlar. |
| **An input image** (`input.png`) | `**extract text from image**` işlemini yapacağımız kaynak dosya. |

Paketleri terminal üzerinden kurabilirsiniz:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

## Adım 1 – Aspose OCR ile Görüntüden Metin Çıkarma

İlk olarak görüntüyü OCR motoruna veriyoruz. Bu blok, ağır işi yapar ve hâlâ yazım hataları içerebilecek ham bir dize döndürür.

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**Neden bu çalışır:** `OcrEngine` tüm düşük seviyeli görüntü ön işleme (ikilileştirme, eğrilik düzeltme vb.) işlemlerini soyutlar. `Recognize()` `true` döndürdüğünde, `Text` özelliği zaten en iyi tahmin edilen karakterleri içerir.  

> **İpucu:** Görüntünüz büyükse, motorun işleme alması öncesinde en uzun kenarını ≤ 2000 px olacak şekilde yeniden boyutlandırmayı düşünün. Bu, doğruluğu etkilemeden işleme süresini hızlandırır.

## Adım 2 – Gerçek‑Zamanlı İçgörü İçin Console Logger Ekleme

Şimdi **add console logger** parçasını ekliyoruz. Günlükleme sadece hata ayıklama için değildir; model indirmeleri, AI‑processor adımları ve kütüphanenin verebileceği uyarılar hakkında görünürlük sağlar.

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

Bu logger'ı artık Aspose AI'ye bağlayabilirsiniz:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**Gördükleriniz:** Yazım denetimi modeli otomatik indirildiğinde, konsol şu satırı benzeri bir şey yazdırır:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

Bu, **add console logger** avantajıdır – arka plan işleminin başarılı olup olmadığını asla merak etmezsiniz.

## Adım 3 – Yazım Denetimi Post‑Processor'ını Yapılandırma ve Kaydetme

Aspose AI, yaygın OCR hatalarını (ör. “rec0gn1ze” → “recognize”) temizleyen kullanışlı bir yazım denetimi post‑processor'ı ile birlikte gelir. Bunu yapılandıracağız, isteğe bağlı olarak kütüphaneye modeli nerede saklayacağını söyleyeceğiz ve ardından kaydedeceğiz.

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**Neden özel bir yol isteyebilirsiniz:** CI/CD boru hatlarında modelleri tekrar indirmeleri önlemek için bilinen bir dizinde önbelleğe almak isteyebilirsiniz. `AllowAutoDownload` bayrağı, kodu ilk çalıştırdığınızda modelin indirilmesini sağlar.

## Adım 4 – OCR Sonucunda Post‑Processor'ı Çalıştırma

OCR metni elimizde ve yazım denetimi işlemcisi hazır olduğunda, ham dizeyi `AsposeAI`'ye veririz. Motor modeli çalıştırır ve işlemci düzeltilmiş metni dahili olarak saklar.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Bu çağrıdan sonra, `spellProcessor` temizlenmiş sürümü içeren `RecognitionText` özelliğine sahip `RecognitionResult` nesnelerinin bir koleksiyonunu tutar.

## Adım 5 – Düzeltlenmiş Metni Alıp Görüntüleme

Son olarak, işlemciden düzeltilmiş dizeyi alıp ekrana yazdırıyoruz. Bu, OCR ve **add console logger** iş akışının faydasını gerçekten gördüğünüz an.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Beklenen çıktı** (görüntünün “Aspose OCR demo” ifadesini birkaç OCR hatasıyla içerdiğini varsayarsak):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Logger'ın modelin hazır olduğunu bildirdiğine ve düzeltilmiş satırın temiz bir şekilde okunduğuna dikkat edin.

## Adım 6 – Kaynakları Temizleme

`AsposeAI` ve `OcrEngine` her ikisi de `IDisposable` uygular. Onları dispose etmek, yerel belleği ve dosya tutucularını serbest bırakır; bu, uzun süre çalışan hizmetlerde özellikle önemlidir.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

## Tam Çalışan Örnek

Aşağıda, yeni bir console projesine (`dotnet new console`) kopyalayıp yapıştırabileceğiniz tam program bulunmaktadır. `"YOUR_DIRECTORY"` ifadesini makinenizdeki gerçek bir klasörle değiştirin.

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}