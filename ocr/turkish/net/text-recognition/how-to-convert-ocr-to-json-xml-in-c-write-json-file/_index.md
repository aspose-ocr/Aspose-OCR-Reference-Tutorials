---
category: general
date: 2026-04-01
description: OCR çıktısını C#'ta JSON ve XML'e nasıl dönüştürülür – Aspose.OCR kullanarak
  görüntüden metin çıkarma ve C# ile JSON dosyası yazmayı öğrenin.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: tr
og_description: OCR sonuçlarını C# ile yapılandırılmış JSON ve XML dosyalarına nasıl
  dönüştüreceksiniz? Görüntüden metin çıkarma ve C# ile JSON dosyası yazma adım adım
  rehberi.
og_title: C#'ta OCR'yi JSON ve XML'e Dönüştürme – JSON Dosyası Yazma
tags:
- OCR
- C#
- Aspose
title: C#'ta OCR'yi JSON ve XML'e Nasıl Dönüştürürsünüz – JSON Dosyası Yazma
url: /tr/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR'yi JSON ve XML'e Dönüştürme – C# ile JSON Dosyası Yazma

**OCR'yi nasıl dönüştürürsünüz** sonuçlarını gerçekten kullanabileceğiniz bir şeye dönüştürmek, birçok geliştiricinin sorduğu bir sorudur. Bu rehberde, bir görüntüden metin nasıl çıkarılır, OCR çıktısı nasıl güzel biçimlendirilmiş JSON ve XML'e dönüştürülür ve ardından bu dosyalar C# ile diske nasıl yazılır, göstereceğiz.

Eğer hiç ham bir OCR dizesine bakıp “Bunu saklamanın daha iyi bir yolu olmalı” diye düşündüyseniz, doğru yerdesiniz. Sonunda **görüntü dosyalarından metin çıkaran** ve **JSON dosyası C#** ile **XML dosyası C#** yazmayı bilen eksiksiz, çalıştırılabilir bir programınız olacak.

## Gereksinimler

- **.NET 6.0** veya daha yeni (kod .NET Framework 4.6+ ile de çalışır).  
- **Aspose.OCR** NuGet paketi – `dotnet add package Aspose.OCR` komutuyla kurun.  
- Metin içeren bir görüntü (ör. `invoice.png`).  
- İstediğiniz herhangi bir IDE – Visual Studio, Rider veya VS Code yeterlidir.

> **Pro tip:** Görüntü dosyalarınızı ayrı bir klasörde tutun (ör. `Resources/`) böylece yollar düzenli kalır.

## Adım 1: OCR Motorunu Kurun – OCR'yi Nasıl Dönüştürürsünüz

İlk olarak bir `OcrEngine` örneği oluşturur ve hangi dili arayacağını belirtiriz. Çoğu durumda İngilizce yeterlidir, ancak `Language.English` yerine desteklenen herhangi bir dili kullanabilirsiniz.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Neden önemli:** Motoru doğru dil ile başlatmak, özellikle Latin dışı yazı sistemleri için doğruluğu büyük ölçüde artırır.

## Adım 2: Metni Tanıma – Görüntüden Metin Çıkarma

Şimdi görüntüyü motora besliyoruz. `Recognize` metodu, ham metni ve konum verilerini içeren bir `OcrResult` nesnesi döndürür.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Görüntü bulunamazsa, `Recognize` bir `FileNotFoundException` fırlatır. Demo'yu basit tutmak için yolu doğru varsayıyoruz, ancak üretimde bunu bir try‑catch bloğu içinde ele almanız gerekir.

## Adım 3: Sonucu JSON'a Dönüştürme – JSON Dosyası Yazma C#

Aspose.OCR serileştirmeyi çok kolaylaştırır. `ToJson` metodu, güzel biçimlendirilmiş çıktı üretmek için bir `indent` bayrağı kabul eder; bu, dosyayı bir metin düzenleyicide açmayı planlıyorsanız mükemmeldir.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Beklenen JSON Örneği

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **Metni nasıl çıkarırsınız:** `Text` özelliği, diğer hizmetlere (arama indeksleri, veritabanları vb.) besleyebileceğiniz düz metni verir.

## Adım 4: JSON'ı Saklama – JSON Dosyası Yazma C# (Devam)

JSON dizesi hazır olduğunda, `File.WriteAllText` kullanarak bir dosyaya yazıyoruz. Bu, varsayılan olarak UTF‑8 kodlamasını sağlar.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Artık `invoice.json` dosyanız görüntünün yanında duruyor ve sonraki işlemler için hazır.

## Adım 5: Sonucu XML'e Dönüştürme – XML Dosyası Yazma C#

Eğer eski sistemler için XML tercih ediyorsanız, `ToXml` metodu işi halleder. `ToJson` gibi, güzel biçimlendirmeyi de destekler.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Beklenen XML Örneği

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Adım 6: XML'i Saklama – XML Dosyası Yazma C# (Devam)

XML'i kaydetmek JSON adımına tamamen benzer; sadece `.xml` uzantısına işaret edin.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Tam Çalışan Örnek

Hepsini bir araya getirerek, bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz tam program aşağıdadır:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Programı çalıştırın, ve `invoice.json` ile `invoice.xml` adlı iki yeni dosyanın belirttiğiniz konumda oluştuğunu göreceksiniz. Dosyaları açarak yapının örneklerle eşleştiğini doğrulayın.

## Yaygın Sorular ve Kenar Durumları

| Soru | Cevap |
|------|-------|
| **Görüntü birden fazla dil içeriyorsa ne olur?** | Her dil için ayrı `OcrEngine` örnekleri oluşturun veya destekleniyorsa `Language.Multi` kullanın. |
| **Çıktı formatını kontrol edebilir miyim (ör. bölge verisini dışarıda bırakmak)?** | Evet. Hem `ToJson` hem `ToXml` isteğe bağlı parametreler alır ve alanları filtrelemenize izin verir; `ExportOptions` için Aspose.OCR belgelerine bakın. |
| **Birçok sayfaya sahip büyük PDF'leri nasıl işleyebilirim?** | Her sayfayı ayrı ayrı işleyin, sonuçları birleştirin ve ardından tek seferde serileştirin. |
| **Çıktı UTF‑8 güvenli mi?** | Kesinlikle—Aspose.OCR dahili olarak Unicode kullanır ve `File.WriteAllText` varsayılan olarak UTF‑8 yazar. |
| **Performans ne durumda?** | OCR CPU‑yoğun bir işlemdir. Toplu işler için çekirdekler arasında paralelleştirmeyi veya Aspose'un bulut API'sini kullanmayı düşünün. |

## Sonuç

Artık **OCR'yi nasıl dönüştürürsünüz** sonuçlarını JSON ve XML olarak C# ile elde edebileceğinizi biliyorsunuz. Yukarıdaki adımları izleyerek **görüntüden metin çıkarabilir**, ardından **JSON dosyası C#** ve **XML dosyası C#** sadece birkaç satır kodla yazabilirsiniz. Bu yaklaşım hızlı, güvenilir ve Aspose.OCR'un desteklediği herhangi bir görüntü türüyle çalışır.

Bir sonraki meydan okumaya hazır mısınız? Şimdi deneyin:

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}