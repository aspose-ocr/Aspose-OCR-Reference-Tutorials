---
category: general
date: 2026-01-12
description: c# ocr öğreticisi, metin görüntüsünü nasıl tanıyacağınızı, metin görüntüsünü
  c# ile nasıl çıkaracağınızı ve güven puanlarıyla bir görüntüyü pdf ocr dosyasına
  nasıl dönüştüreceğinizi gösterir.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: tr
og_description: Metin görüntüsünü tanıyan, C# ile metin görüntüsünü çıkaran ve güven
  puanlarıyla bir görüntüyü PDF OCR belgesine dönüştüren eksiksiz bir C# OCR öğreticisini
  öğrenin.
og_title: c# ocr öğretici – Görüntüleri aranabilir PDF'lere dönüştür
tags:
- OCR
- C#
- PDF
title: c# OCR öğreticisi – Görüntüleri aranabilir PDF'lere dönüştür
url: /tr/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Görüntüleri Aranabilir PDF'lere Dönüştürme

Üçüncü taraf hizmetler aramadan bir C# projesinde **metin görüntüsünü tanıma** dosyalarını nasıl tanıyacağınızı hiç merak ettiniz mi? Yalnız değilsiniz. Gerçek dünyadaki birçok uygulamada—fatura tarayıcıları, makbuz izleyicileri veya çok dilli belge arşivleri gibi—geliştiricilerin güvenilir, yerinde bir OCR motoruna ve aynı zamanda güven puanları (confidence scores) üretebilen bir çözüme ihtiyacı vardır.

Bu **c# ocr tutorial** size ihtiyacınız olan her şeyi adım adım gösterecek: bir resmi yüklemekten, dil modellerini seçmeye, GPU hızlandırmasını açıp kapamaya, sonuçları aranabilir bir PDF olarak kaydetmeye kadar. Sonunda, metni çıkaran, OCR güven puanlarını raporlayan ve isteğe bağlı olarak bir *image to pdf ocr* dosyası oluşturan, bir dakikadan az bir kodlama süresiyle çalıştırılabilir bir örnek kodunuz olacak.

## Oluşturacağınız Şey

- Çokk dilli bir görüntüyü yükleyin (`sample_multi_lang.jpg` bir yer tutucu olarak kullanılır).  
- Arapça, Hintçe ve Rusça dil modellerini seçin (daha fazlasını ekleyebilirsiniz).  
- Makineniz destekliyorsa GPU işleme özelliğini etkinleştirin.  
- Ham OCR sonucunu **güven puanlarıyla** alın.  
- Sonucu güzel biçimlendirilmiş JSON'a serileştirin **veya** aranabilir bir PDF olarak yazın.  

## Önkoşullar

- .NET 6.0 veya daha yeni bir sürüm (kod .NET Core ve .NET Framework üzerinde derlenir).  
- Visual Studio 2022 (veya tercih ettiğiniz herhangi bir IDE).  
- Bir Aspose.OCR for .NET lisansı (ücretsiz deneme sürümü test için çalışır).  
- İsteğe bağlı: Tanıma hızını artırmak istiyorsanız CUDA uyumlu bir GPU.  

> **Pro tip:** GPU'nuz yoksa, sadece `UseGpu = false` ayarlayın ve motor kod değişikliği yapmadan CPU'ya geri dönecektir.

## Adım 1: Gerekli NuGet Paketlerini Yükleyin

**Package Manager Console**'u açın ve şu komutu çalıştırın:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Bu üç paket size OCR motorunu, GPU hızlandırmasını ve güven puanı çıktısı için güzel bir JSON serileştiricisini sağlar.

## Adım 2: Proje Yapısını Oluşturun

Yeni bir konsol projesi oluşturun (`dotnet new console -n AsposeOcrDemo`) ve oluşturulan `Program.cs` dosyasını aşağıdaki kodla değiştirin.  
Tüm mantık `Program` sınıfı içinde yer alır; tek ek tip, OCR sonucunu JSON için biçimlendiren küçük bir uzantı metodudur.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Bu Kod Neden Çalışıyor

1. **GPU geçişi** – `GpuOcrEngine` CUDA çekirdeklerini kullanır; ternary operatör (koşul operatörü) geçişi sorunsuz hâle getirir.  
2. **Otomatik dil indirme** – `AutoDownloadResources = true` ayarı, uygulamayı ilk çalıştırdığınızda Arapça, Hintçe ve Rusça modellerinin indirilmesini sağlar.  
3. **Güven puanları** – `result.Words` tanınan her kelime için bir `Confidence` içerir; uzantı metodu bunları temiz bir JSON nesnesine biçimlendirir.  
4. **Aranabilir PDF** – `result.Pdf` zaten tamamen aranabilir bir PDF'dir, bu yüzden bayt dizisini diske yazarız. Ek bir kütüphane gerekmez.  

## Adım 6: Örneği Çalıştırın

Bir terminal açın, proje klasörüne gidin ve şu komutu çalıştırın:

```bash
dotnet run
```

Eğer **JSON** çıktısını seçtiyseniz, aşağıdakine benzer bir şey göreceksiniz:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Eğer **PDF**'ye geçiş yaptıysanız, konsol yolu yazdırır ve kaynak görüntünün hemen yanında aranabilir bir PDF bulursunuz.

## Yaygın Sorular & Kenar Durumları

- **Bir dil modeli mevcut değilse ne olur?**  
  OCR motoru net bir `ResourceNotFoundException` hatası fırlatır. `AutoDownloadResources = true` ayarını yaptığımız için eksik model ilk çalıştırmada otomatik olarak indirilir, bu yüzden üretimde bu istisna nadiren görülür.

- **Bir grup görüntüyü işleyebilir miyim?**  
  Kesinlikle. `engine.Recognize` çağrısını bir dosya dizini üzerinde `foreach` döngüsüyle sarın. Aynı `OcrResultExtensions` her görüntü için çalışır.

- **GPU için lisansa ihtiyacım var mı?**  
  Hayır. Ücretsiz deneme sürümü CPU ve GPU için çalışır. Tam lisans deneme filigranını kaldırır ve sayfa sınırı kısıtlamalarını ortadan kaldırır.

- **Güven puanları ne kadar doğru?**  
  Puanlar 0.0 (güvensiz) ile 1.0 (tam güven) arasında değişir. Pratikte, 0.90 üzerindeki değerler sonraki işlemler için güvenilirdir; daha katı bir doğrulama gerekiyorsa düşük güven puanlı kelimeleri filtreleyebilirsiniz.

## Adım 7: Sonraki Adımlar (OCR Araç Setinizi Genişletin)

1. **Daha fazla dil ekleyin** – `Languages` dizisine sadece `LanguageModel.French` (veya desteklenen başka bir model) ekleyin.  
2. **OCR'ı PDF/A dönüşümüyle birleştirin** – Aspose.PDF, arşivleme için OCR katmanını PDF/A‑2b uyumlu bir belgeye gömebilir.  
3. **Azure Functions ile bütünleştirin** – mantığı anlık yüklemeleri işlemek için sunucusuz bir uç noktaya sarın.  
4. **Güven eşiklerini ince ayarlayın** – `result.Words.Where(w => w.Confidence < 0.85)` kullanarak belirsiz kelimeleri manuel inceleme için işaretleyin.  

### TL;DR

Bu **c# ocr tutorial** size şunları gösterir:

- Bir görüntüyü yükleyin ve birden fazla dil modeli seçin.  
- Tek bir boolean bayrağıyla GPU hızlandırmasını etkinleştirin.  
- OCR sonuçlarını **güven puanlarıyla** alın ve JSON'a serileştirin.  
- İsteğe bağlı olarak aranabilir bir PDF yazın (**image to pdf ocr**).

Bunların hepsi sadece birkaç satır kod, ücretsiz bir Aspose.OCR deneme sürümü ve yukarıdaki kodla mümkündür. Deneyin, dil listesini ayarlayın ve dakikalar içinde üretime hazır bir OCR hattına sahip olun.

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}