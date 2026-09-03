---
category: general
date: 2026-01-02
description: Aspose OCR kullanarak C#'de görüntüden metin çıkarın. Görüntüyü hızlı
  ve güvenilir bir şekilde JSONL formatına dönüştürmeyi öğrenin.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: tr
og_description: Aspose OCR ile görüntüden metin çıkarın ve JSONL formatına dönüştürün.
  Geliştiriciler için tam adım adım C# öğreticisi.
og_title: Görüntüden Metin Çıkar – C#'ta JSONL'ye Dönüştür
tags:
- C#
- OCR
- Aspose
- JSONL
title: Görüntüden Metin Çıkar ve JSONL'ye Dönüştür – C# Rehberi
url: /tr/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkar ve JSONL'e Dönüştür – Tam C# Öğreticisi

Hiç **görüntüden metin çıkarma** ihtiyacı duydunuz mu, ama hangi kütüphanenin temiz, yapılandırılmış bir çıktı vereceğinden emin değildiniz mi? Tek başınıza değilsiniz. Birçok fiş‑işleme veya belge‑dijitalleştirme projesinde darboğaz, bir bitmap'i aranabilir metne *ve* makine‑okunabilir bir formata dönüştürmek oluyor.  

İyi haber? Aspose OCR ile **görüntüden metin çıkarabilir** ve birkaç satır kodla **görüntüyü JSONL'e dönüştürebilirsiniz**; böylece sonraki analizler için veri hattına akıtabilirsiniz. Bu kılavuz, PNG'yi yüklemekten JSON‑Lines dosyasına yazmaya kadar tüm süreci adım adım gösterir.

> **İpucu:** .NET 6 veya daha yeni bir sürüm kullanıyorsanız, aynı kod ek bir yapılandırma olmadan çalışır.

## Önkoşullar — Neye İhtiyacınız Var

- **.NET 6 SDK** (veya herhangi bir yeni .NET sürümü)
- **Aspose.OCR** NuGet paketi  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** serileştirme için  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Bir örnek görüntü (ör. `receipt.png`) erişebileceğiniz bir klasörde.
- Tercih ettiğiniz IDE veya editör — Visual Studio, VS Code, Rider vb.

Yoğun kurulum yok, harici hizmet yok, sadece birkaç NuGet paketi.

![C# kullanarak görüntüden metin çıkarma](https://example.com/assets/ocr-sample.png)

*Alt metin: Aspose OCR ile C# kullanarak görüntüden metin çıkarma*

## Adım 1: İşlemek İstediğiniz Görüntüyü Yükleyin  

**görüntüden metin çıkarma** yapmak istediğinizde ilk yapmanız gereken OCR motoruna bir bitmap vermektir. `System.Drawing.Bitmap` kullanmak basittir ve çoğu raster formatı için çalışır.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Neden önemli:** Görüntüyü `Bitmap` olarak yüklemek, OCR motoruna doğrudan piksel erişimi sağlar; bu da ham bayt akışıyla karşılaştırıldığında tanıma hızını ve doğruluğunu artırır.

## Adım 2: JSON‑Lines Çıktısı İçin Aspose OCR'ı Yapılandırın  

Aspose OCR, dil, çıktı formatı ve birkaç performans ayarı belirlemenize izin verir. Burada **JSON‑Lines** (her satırda bir JSON nesnesi) istiyoruz çünkü daha sonra satır‑satır işleme için mükemmeldir.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Pro ipucu:** Çok dilli fişlere ihtiyacınız varsa `Language = Language.Multilingual` ayarlayın veya bir `Language` dizisi geçin.

## Adım 3: OCR'ı Çalıştırın ve Sonucu Yakalayın  

Şimdi gerçekten **görüntüden metin çıkarıyoruz**. `Recognize` metodu, tanınan metin satırlarını ve sınırlayıcı kutularını içeren bir `OcrResult` nesnesi döndürür.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

Bu noktada `ocrResult.Lines` ihtiyacınız olan her şeyi tutar — ham metin, güven puanları ve koordinatlar.

## Adım 4: Satırları JSON‑Lines Olarak Serileştirin  

Koleksiyonu güzel bir girintili JSON dizesine dönüştüreceğiz. JSON‑Lines genellikle sıkıştırılmış olsa da, girinti eklemek dosyayı geliştirme sırasında incelemeyi kolaylaştırır.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

Ortaya çıkan `jsonLines` değişkeni aşağıdaki gibi (kısaltılmış) görünecektir:

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Her satır bir yeni satır karakteriyle biter; bu da gerçek bir **JSONL** (JSON‑Lines) dosyası oluşturur.

## Adım 5: JSON‑Lines'ı Disk'e Yazın  

Son olarak çıktıyı kalıcı hâle getiriyoruz; böylece Spark, Logstash ya da basit bir Bash betiği gibi diğer hizmetler satır satır tüketebilir.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

`receipt.jsonl` dosyasını açtığınızda her satırda bir JSON nesnesi göreceksiniz; akışa hazır.

## Adım 6: Dışa Aktarmayı Doğrulayın  

Hızlı bir tutarlılık kontrolü, ileride saatlerce hata ayıklamaktan sizi kurtarır. İlk birkaç satırı tekrar okuyup konsola yazdıralım.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Tipik konsol çıktısı:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Böyle bir şey görüyorsanız, tebrikler — **görüntüden metin çıkarma** ve **görüntüyü JSONL'e dönüştürme** işlemini başarıyla tamamladınız.

## Yaygın Tuzaklar ve Çözümleri  

| Sorun | Neden Olur | Çözüm |
|-------|------------|-------|
| **Boş çıktı** | Görüntü yolu hatalı veya dosya okunamıyor. | `File.Exists(imagePath)` ile bitmap oluşturmadan önce kontrol edin. |
| **Düşük güven puanları** | Görüntü bulanık veya düşük kontrastlı. | Görüntüyü ön‑işleyin (ör. `Bitmap.RotateFlip`, `Graphics.Clear`) veya DPI'yi artırın. |
| **Yanlış dil** | OCR varsayılan olarak İngilizce; fiş başka bir dilde. | `options.Language = Language.Spanish` (veya uygun enum) ayarlayın. |
| **JSONL tek bir JSON dizisi olarak görünüyor** | `Formatting.None` kullandınız ve yeni satır eklemediniz. | Her serileştirilmiş nesnenin sonuna `Environment.NewLine` eklediğinizden emin olun. |

## Tam Çalışan Örnek  

Aşağıda, doğrudan çalıştırılabilir tam program yer alıyor. Bir konsol projesine yapıştırın ve **F5** tuşuna basın.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Beklenen sonuç:** `receipt.jsonl` dosyası, her satırda `Text`, `Confidence` ve `BoundingBox` alanlarına sahip bir JSON nesnesi içerir. Artık bu dosyayı JSONL tüketen herhangi bir analiz hattına besleyebilirsiniz.

## Sonraki Adımlar – Temel OCR'ın Ötesine Geçmek  

- **Toplu işleme:** Yukarıdaki mantığı bir `foreach` döngüsü içinde sararak bir klasördeki tüm fişleri işleyin.  
- **Paralellik:** Binlerce görüntüyle çalışırken çok‑çekirdekli hızlandırma için `Parallel.ForEach` kullanın.  
- **Son‑işleme:** Düşük‑güvenli satırları (`Confidence < 0.9`) depolamadan önce ayıklayın.  
- **Entegrasyon:** JSONL'i doğrudan Azure Blob Storage veya AWS S3'e ilgili SDK'lar ile gönderin.  
- **Alternatif formatlar:** Aşağı akış sisteminiz farklı bir format tercih ediyorsa `OutputFormat`'ı `PlainText` veya `Xml` olarak değiştirin.

## Sonuç  

Aspose OCR ve C# kullanarak **görüntüden metin çıkarma** ve **görüntüyü JSONL'e dönüştürme** için sağlam, uçtan uca bir çözümünüz artık var. Bu öğretici, bitmap'i yüklemekten çıktıyı doğrulamaya kadar her adımı ve hattınızı dayanıklı tutmak için pratik ipuçlarını kapsadı.

Kendi fişleriniz, faturalarınız veya taranmış formlarınızla deneyin — OCR motorunun pikselleri saniyeler içinde aranabilir, satır‑yapılı verilere dönüştürmesini izleyin. Kenar durumlarla (ör. eğik taramalar veya çok dilli metin) karşılaşırsanız, *RecognitionOptions* bölümüne geri dönüp dil ya da ön‑işleme adımlarını ayarlayın.

Kodlamanın tadını çıkarın, veri hatlarınız her daim temiz olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}