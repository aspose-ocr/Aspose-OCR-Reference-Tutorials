---
category: general
date: 2026-01-01
description: c# OCR öğreticisi, metin çıkarma, OCR için görüntü yükleme ve Aspose.OCR
  kullanarak JSON dosyasına yazma işlemlerini gösterir – adım adım rehber.
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: tr
og_description: c# OCR öğreticisi, görüntülerden metin çıkarmayı, OCR için görüntü
  yüklemeyi ve Aspose.OCR kullanarak JSON'u dosyaya yazmayı adım adım gösterir.
og_title: c# OCR öğretici – Metni Çıkar ve JSON'a Aktar
tags:
- Aspose.OCR
- C#
- Text Extraction
title: c# OCR öğretici – Görüntülerden Metin Çıkar ve JSON'a Aktar
url: /tr/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR öğretici – Görüntülerden Metin Çıkar ve JSON Olarak Dışa Aktar

Hiç taranmış bir faturadan özel ayrıştırıcılar yazarak saatler harcamadan metin çıkarmanın nasıl yapılacağını merak ettiniz mi? Yalnız değilsiniz. Bu **c# OCR tutorial** içinde bir görüntüyü OCR için nasıl yükleyeceğinizi, tanıma motorunu çalıştıracağınızı ve ardından **write JSON to file** yaparak verileri sonraki sistemlere nasıl besleyeceğinizi tam olarak göstereceğiz.

Bir klasörde `receipt1.png`, `receipt2.png` gibi adlandırılmış makbuzlarınız olduğunu ve bunları hızlı bir şekilde aranabilir JSON kayıtlarına dönüştürmek istediğinizi hayal edin. Çözmek üzere olduğumuz problem bu ve sonunda bunu yapan hazır‑çalıştır konsol uygulamasına sahip olacaksınız. Aspose.OCR dışındaki ekstra bağımlılık yok, sihir yok—sadece net, tekrarlanabilir adımlar.

> **What you’ll learn**
> - How to **load image for OCR** using Aspose.OCR.
> - The best way to **how to extract text** and get confidence scores.
> - Converting the OCR result into a nicely structured **OCR image to JSON** payload.
> - Safely **write JSON to file** and verify the output.

## Önkoşullar

- .NET 6 SDK veya daha yeni bir sürüm (kod .NET Core üzerinde de çalışır).  
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir editör.  
- Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`).  
- İşlemek istediğiniz bir görüntü dosyası (PNG, JPG, BMP) – demo için `invoice.png` kullanacağız.

Eğer bunlardan herhangi birine sahip değilseniz, Microsoft sitesinden SDK’yı indirin ve Package Manager Console üzerinden NuGet paketini ekleyin:

```powershell
Install-Package Aspose.OCR
```

Şimdi temel hazırlıklar tamam, gerçek uygulamaya dalalım.

## Step 1: c# OCR tutorial – OCR Motorunu Başlatma

**load image for OCR** yapabilmeden önce tanıma sürecini yönetecek bir motor örneğine ihtiyacımız var. `OcrEngine` sınıfı hafiftir, ancak kaynakların hızlıca serbest bırakılması için bir `using` bloğu içinde sarmalamak iyi bir uygulamadır.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*Pro tip:* Bir toplu işlemde çok sayıda görüntü işleyecekseniz, her seferinde yeni bir `OcrEngine` oluşturmak yerine aynı örneği yeniden kullanın. Bellek kullanımını azaltır ve işlemi hızlandırır.

## Step 2: Load image for OCR

Şimdi gerçekten **load image for OCR** yapıyoruz. Aspose.OCR çeşitli formatları destekler; bir PNG, JPEG ya da çok sayfalı TIFF bile gösterebilirsiniz. `OcrImage.FromFile` metodu dosyayı okur ve tanıma için hazır hâle getirir.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **Why this matters:** Görüntüyü ayrı ayrı yüklemek, boyutlarını, DPI’sını ya da ön‑işleme (ör. ikilileştirme) yapmanızı sağlar; motorun önüne göndermeden önce kontrol edebilirsiniz. Görüntü bozuksa, `FromFile` net bir istisna fırlatır, bunu yakalayıp kaydedebilirsiniz.

## Step 3: How to extract text – Tanıma İşlemini Çalıştırma

Görüntü elimizde olduğuna göre, nihayet **how to extract text** yapabiliriz. `Recognize` metodu, yalnızca düz metni değil, aynı zamanda konumsal veri ve her kelime için güven skorlarını içeren bir `OcrResult` nesnesi döndürür.

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*Edge case:* Bazı PDF’ler görünmez metin katmanları içerir. PDF sayfasını görüntü olarak beslerseniz motor hiçbir şey görmeyebilir. Bu durumlarda önce Aspose.PDF ile gizli katmanı çıkarın, ardından gerektiğinde OCR’a geçin.

## Step 4: OCR image to JSON – Sonucu Dönüştürme

`OcrResult` sınıfı, tüm sonuç kümesini—her kelimenin sınırlama kutusu ve güven skorları dahil—JSON dizesine serileştiren kullanışlı bir `ToJson()` yardımcı metoduna sahiptir. Kendi serileştiricinizi yazmadan **OCR image to JSON** elde etmenin en temiz yoludur.

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

Özel bir şema tercih ederseniz, `ocrResult.Words` üzerinde döngü kurarak kendi nesnenizi oluşturabilirsiniz; ancak çoğu senaryoda yerleşik JSON yeterli ve zaten iyi yapılandırılmıştır.

## Step 5: Write JSON to file

Şimdi bulmacanın son parçası: JSON yükünü kalıcı hâle getirmek. `File.WriteAllText` metodu dosyanın atomik olarak oluşturulmasını (veya üzerine yazılmasını) sağlar. Hedef klasörün var olduğundan emin olun, aksi takdirde `DirectoryNotFoundException` alırsınız.

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*Tip:* UTF‑8 BOM ile ya da farklı bir kodlama gerekiyorsa, `Encoding` argümanını kabul eden aşırı yüklemeyi kullanın.

## Step 6: Verify the output

Kısa bir `Console.WriteLine` işlemin başarıyla tamamlandığını gösterir. Ayrıca JSON dosyasını bir görüntüleyicide açarak yapıyı doğrulayabilirsiniz.

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### Expected JSON snippet

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

JSON, her kelimenin konumunu içerir; bu, daha sonra bir UI’da metni vurgulamak istediğinizde işe yarar.

## Full Working Example

Aşağıda tamamen kopyala‑yapıştır‑hazır program yer alıyor. `YOUR_DIRECTORY` kısmını görüntünüzün bulunduğu gerçek yol ile değiştirin.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

Programı çalıştırın (`dotnet run` proje klasöründen) ve `invoice.json` dosyasını orijinal PNG’nizin yanında bulacaksınız.

## Common Pitfalls & How to Avoid Them

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **FileNotFoundException** görüntü yüklenirken | Yol hatası ya da dosya eksik | `Path.Combine` kullanın ve `FromFile` çağırmadan önce `File.Exists` kontrol edin. |
| **Low confidence scores** | Düşük görüntü kalitesi, düşük DPI | `ocrImage.AdjustContrast` ile ön‑işleme yapın ya da görüntüyü 300 DPI’ye yükseltin. |
| **JSON file empty** | `ocrResult` null döndürdü (motor başarısız) | Görüntü formatının desteklendiğini ve lisansın (varsa) doğru uygulandığını doğrulayın. |
| **Performance bottleneck on large batches** | Her yinelemede `OcrEngine` yeniden oluşturulması | Toplu işlemde tek bir `OcrEngine` örneğini yeniden kullanın, sadece sonunda serbest bırakın. |

## Next Steps

Şimdi **c# OCR tutorial**’ı ustalaştığınıza göre, şunları yapmak isteyebilirsiniz:

- **Batch process** tüm klasörü işleyip JSON dosyalarını tek bir veritabanına toplayabilirsiniz.  
- **Integrate** çıktıyı Azure Cognitive Search ile birleştirerek aranabilir PDF'ler elde edebilirsiniz.  
- **Add language support** `ocrEngine.Language = OcrLanguage.Spanish` (veya desteklenen herhangi bir dil) ayarlayarak ekleyebilirsiniz.  
- **Post‑process** JSON'ı düzenli ifadelerle tablo veya anahtar‑değer çiftlerini çıkarmak için işleyebilirsiniz.  

Bu uzantıların her biri, OCR için görüntü yükleme, metin çıkarma, JSON’a dönüştürme ve JSON’ı diske yazma temel kavramları üzerine inşa edilmiştir.

---

### Conclusion

Bu **c# OCR tutorial**’da **load image for OCR**, **how to extract text** adımlarını, sonucu **OCR image to JSON** yüküne dönüştürmeyi ve sonunda **write JSON to file** işlemini ayrıntılı olarak ele aldık. Tam kod örneği herhangi bir .NET projesine eklenmeye hazır ve açıklamalar, çözümü gerçek dünya senaryolarına uyarlamanız için gereken bağlamı sağlıyor.

Kendi makbuz veya fatura setinizle deneyin—görüntü ön‑işlemeyi ayarlayın, farklı dillerle denemeler yapın ve JSON çıktısının büyümesini izleyin. Bir sorunla karşılaşırsanız, sorunlar tablosuna göz atın ya da aşağıya yorum bırakın. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}