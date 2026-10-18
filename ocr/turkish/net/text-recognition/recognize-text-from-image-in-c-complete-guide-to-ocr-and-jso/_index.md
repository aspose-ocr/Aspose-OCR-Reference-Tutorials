---
category: general
date: 2026-01-10
description: Aspose OCR'i C#'ta kullanarak görüntüden metin tanımayı, metin koordinatlarını
  çıkarmayı ve fişi JSON'a dönüştürmeyi öğrenin. Adım adım öğretici.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: tr
og_description: Aspose OCR kullanarak C#'de görüntüden metin tanıma. Bu kılavuz, metni
  nasıl çıkaracağınızı, koordinatları nasıl alacağınızı ve fişi JSON'a nasıl dönüştüreceğinizi
  gösterir.
og_title: görselden metin tanıma – Tam C# OCR Öğreticisi
tags:
- OCR
- C#
- Aspose
title: C#'ta Görüntüden Metin Tanıma – OCR ve JSON İçin Tam Kılavuz
url: /tr/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# görüntüden metin tanıma – Tam C# OCR Öğreticisi

Görüntüden metin tanıma ihtiyacınız oldu mu ama hangi kütüphaneyi seçeceğinizden emin değildiniz? Yalnız değilsiniz. Gerçek dünyadaki birçok uygulamada—gider takipçileri, fiş tarayıcıları veya belge arşivleyicileri—metni güvenilir bir şekilde çıkarmak ilk engeldir.  

Bu öğreticide **metni nasıl çıkaracağımızı**, sınırlayıcı kutularını nasıl alacağımızı ve sonunda Aspose.OCR for .NET kullanarak **fişi JSON'a dönüştürmeyi** adım adım göstereceğiz. Sonunda, bir fiş fotoğrafını alıp güven puanları ve koordinatlarla düzenli bir JSON dosyası üreten bağımsız bir C# projesine sahip olacaksınız.

## Gerekenler

İlerlemeye başlamadan önce, makinenizde aşağıdakilerin yüklü olduğundan emin olun:

- **.NET 6.0 SDK** (veya daha yeni bir sürüm). Eski framework'ler de çalışır, ancak .NET 6 modern kütüphaneler için ideal noktadır.
- **Visual Studio 2022** veya C# uzantılı VS Code.
- **Aspose.OCR for .NET** NuGet paketi (`Aspose.OCR` ve `Aspose.OCR.Output`). Bunu Package Manager Console üzerinden kurabilirsiniz:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Örnek bir fiş resmi (ör. `receipt.jpg`) daha sonra başvuracağınız bir klasöre yerleştirin.

Hepsi bu—ekstra SDK yok, yerel ikili dosyalar yok, sadece saf yönetilen kod.

## Adım 1: Yeni Bir Konsol Projesi Oluşturun

İlk olarak, bir konsol uygulaması oluşturun. UI yükü olmadan OCR'ı test etmenin en hızlı yoludur.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Pro ipucu:** Proje klasörünü düzenli tutun; `Resources` adlı bir alt klasör oluşturup `receipt.jpg` dosyasını oraya koyun. Böylece yol yönetimi sorunsuz olur.

## Adım 2: Fiş Resmini Yükleyin

Şimdi gerçekten **görüntüden metin tanıma** yapıyoruz. İlk adım OCR motorunu dosyaya yönlendirmektir.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Yüklemeyi basit bir varlık kontrolüyle sarmamızın nedeni nedir? Çünkü üretimde, eksik veya bozuk olabilecek kullanıcı yüklemeleriyle sıkça karşılaşırsınız. Sorunu erken yakalamak, ileride belirsiz istisnalardan sizi korur.

## Adım 3: OCR Gerçekleştir – **görüntüden metin tanıma**

Resim bellekteyken, Aspose'tan **görüntüden metin tanıma** yapmasını istiyoruz. Bu işlem eşzamanlıdır ve zengin bir sonuç kümesi döndürür.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Arka planda Aspose, milyonlarca karakter üzerinde eğitilmiş bir sinir ağı çalıştırır. Motor `ocrEngine.Text`, `ocrEngine.RecognitionResult` ve koordinatları tutan `OcrRegion` nesnelerinin bir koleksiyonunu doldurur. Bu, bir sonraki adım için tam olarak ihtiyacımız olan şeydir.

## Adım 4: **Metni Nasıl Çıkarırız** – Ham Dizeyi Almak

Sadece düz metinle ilgileniyorsanız (belki hızlı bir arama için), motorun sağladığı metni doğrudan alabilirsiniz:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

OCR'ın paragraf sınırlarını algıladığı yerlerde satır sonları göreceksiniz. Birçok fiş tarama senaryosunda ham dize, basit regex'ler kullanarak toplamları, tarihleri veya satıcı adlarını çıkarmak için yeterlidir.

## Adım 5: **Metin Koordinatlarını Çıkarma** – Her Kelime İçin Sınırlayıcı Kutular

Çoğu zaman bir metin parçasının görüntüde *nerede* olduğunu bilmeniz gerekir—örneğin, UI'da toplam tutarı vurgulamak için. Aspose bunu `OcrRegion` nesneleri aracılığıyla sağlar.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Her tanınan segment için **metin koordinatlarını çıkarma** döngüsü yaptığımızı fark edin. Koordinatlar orijinal görüntüye göre görecelidir, bu yüzden bir grafik kanvasına veya HTML `<canvas>` öğesine yerleştirebilirsiniz.

## Adım 6: **Fişi JSON'a Dönüştürme** – Ayrıntılı Sonuçları Kaydetme

Şimdi her şeyi bir araya getiren kısma geliyoruz: metin, güven puanları ve sınırlayıcı kutuları içeren makine‑okunur bir yapı istiyoruz. Aspose, bunu kolaylaştıran `JsonSaveOptions` ile birlikte gelir.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

Oluşan dosya aşağıdaki gibi görünür (kısaltılmıştır):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Artık **fişi JSON'a dönüştürme** artefaktına sahipsiniz; bu, gider‑rapor API'leri, analiz boru hatları veya her kelimenin etrafına dikdörtgen çizen basit bir UI gibi aşağı akış hizmetlerine beslenebilir.

## Tam Çalışan Örnek

Tüm parçaları bir araya getirerek, projenize kopyalayıp yapıştırabileceğiniz tam `Program.cs` dosyasını aşağıda bulabilirsiniz:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Programı çalıştırın (`dotnet run`) ve konsol çıktısını izleyin. Yapıyı doğrulamak için `Resources/receipt.json` dosyasını açın.

## Yaygın Sorular & Kenar Durumları

- **Resim bulanıktaysa ne olur?**  
  Aspose OCR, 300 dpi veya daha yüksek çözünürlükte en iyi performansı gösterir. Düşük güven puanları alırsanız, görüntüyü motorun önüne göndermeden önce bir keskinleştirme filtresi uygulamayı düşünün.

- **Birden fazla dili tanıyabilir miyim?**  
  Evet. `Recognize()` çağırmadan önce `ocrEngine.Language = Language.English | Language.Spanish;` şeklinde ayarlayın.

- **Çıktıyı sadece sayılarla (ör. toplamlar) sınırlamak nasıl yapılır?**  
  Düz metni elde ettikten sonra `ocrEngine.Text` üzerinde `\d+\.\d{2}` gibi bir regex çalıştırın. Zaten koordinatlara sahip olduğumuz için eşleşen dizeyi görsel vurgulama için bölgesine geri haritalayabilirsiniz.

- **JSON formatı özelleştirilebilir mi?**  
  `JsonSaveOptions` sınıfı birkaç bayrak sunar. Tamamen özel bir şema gerekiyorsa, `ocrEngine.RecognitionResult.Regions` üzerinde döngü yapıp nesneleri `System.Text.Json` ile kendiniz serileştirebilirsiniz.

## Sonuç

Aspose.OCR kullanarak C#'ta **görüntüden metin tanıma**, **metni çıkarma**, **metin koordinatlarını çıkarma** ve sonunda **fişi JSON'a dönüştürme** nasıl yapılır gösterdik. Tüm akış tek bir, çalıştırması kolay konsol uygulamasında yer alır; bu da prototipler için ya da daha büyük sistemlerde bir yapı taşı olarak mükemmeldir.

Sonraki adımlar? JSON'ı sınırlayıcı kutuları çizen bir ön‑yüze beslemeyi deneyin veya çıktıyı bir gider‑rapor hizmetine bağlayın. Ayrıca farklı görüntü formatları (PNG, TIFF) ile deney yapabilir veya bir klasördeki fişleri toplu işleyebilirsiniz.

OCR, Aspose veya JSON işleme hakkında daha fazla sorunuz mu var? Aşağıya yorum bırakın, iyi kodlamalar! 

![Görüntüden metin tanıma örnek fiş görüntüsü](receipt.jpg "Fiş görüntüsü örneği")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}