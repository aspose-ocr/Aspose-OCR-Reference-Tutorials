---
category: general
date: 2026-03-28
description: C#'ta toplu OCR nasıl yapılır ve TIFF dosyalarını kolayca metne dönüştürürsünüz
  öğrenin. Bu adım adım rehber, Aspose OCR kullanarak TIFF dosyalarından metin çıkarılmasını
  gösterir.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: tr
og_description: C#'ta toplu OCR nasıl yapılır? Aspose OCR kullanarak çok sayfalı TIFF
  dosyalarını aranabilir metne dönüştürmek için bu kapsamlı öğreticiyi izleyin.
og_title: C#'ta Toplu OCR Nasıl Yapılır – Çok Sayfalı TIFF'i Metne Dönüştürme
tags:
- OCR
- C#
- Aspose
title: C#'ta Toplu OCR Nasıl Yapılır – Çok Sayfalı TIFF'i Metne Dönüştürme
url: /tr/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Toplu OCR Nasıl Yapılır – Çok Sayfalı TIFF'i Metne Dönüştürme

Hiç **toplu OCR**'un bir yığın taranmış sayfayı nasıl işleyebileceğini, her görüntü için ayrı bir döngü yazmadan merak ettiniz mi? Tek başına değilsiniz. Birçok projede—örneğin fatura işleme ya da arşiv dijitalleştirme—**TIFF'i metne dönüştürme** ihtiyacı her gün karşımıza çıkıyor ve tek tek sayfa tek tek işlemek kısa sürede bir kabusa dönüşebiliyor.

İyi haber? Birkaç satır C# ve Aspose OCR ile çok sayfalı bir TIFF'i motorun içine besleyebilir ve sayfa numaralarıyla çıkarılan metinleri eşleyen bir sözlük elde edebilirsiniz. Bu öğreticide, **toplu OCR**'un tam olarak nasıl yapılacağını, **TIFF'ten metin çıkarma** yöntemini ve bu yaklaşımın manuel alternatifi neden geride bıraktığını gösteren çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz.

## Öğrenecekleriniz

- .NET projesine Aspose OCR kütüphanesini nasıl ekleyeceğinizi.  
- `Image.FromMultiPageFile` ile çok sayfalı bir TIFF dosyasını nasıl yükleyeceğinizi.  
- `RecognizeBatch` metodunu çalıştırarak sayfa bazlı sonuçları içeren bir `Dictionary<int,string>` elde etmeyi.  
- Çıktıyı temiz ve okunabilir bir formatta nasıl yazdıracağınızı.  

Bu adımları tamamladığınızda, ekstra bir araç kullanmadan herhangi bir çok sayfalı TIFF'i düz metne dönüştüren hazır bir konsol uygulamanız olacak.  

### Önkoşullar

- .NET 6.0 SDK (veya daha yeni bir .NET sürümü).  
- Visual Studio 2022 ya da VS Code—sevdiğiniz IDE yeterli.  
- Geçerli bir Aspose OCR lisansı ya da ücretsiz deneme anahtarı (API lisanssız çalışır ancak filigran ekler).  
- `multipage.tif` adlı örnek çok sayfalı TIFF dosyasını referans alabileceğiniz bir klasöre yerleştirin.

> **Pro ipucu:** Windows kullanıyorsanız, varsayılan proje klasörü TIFF'i bırakmak için uygun bir yerdir; Linux/macOS'ta ise yolu ona göre ayarlamanız yeterli.

## Adım 1: Aspose OCR NuGet Paketini Yükleyin

Kod yazmaya başlamadan önce OCR kütüphanesine ihtiyacımız var. Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Bu komut, en son kararlı sürümü (Mart 2026 v23.9 itibarıyla) indirir ve gerekli DLL'leri projenize ekler. Basit bir konsol uygulaması için ekstra bir yapılandırma gerekmez.

## Adım 2: Konsol Uygulaması Taslağını Oluşturun

OCR motoruna referans veren minimal bir program iskeleti oluşturalım. `using` yönergeleri çok önemlidir—onlar olmadan derleyici eksik tipler hakkında şikayet eder.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **Neden önemli?** `Image` sınıfı bir alt‑namespace içinde yer alır ve `ImageProcessing` import edilmezse “type or namespace not found” hatası alırsınız; bu da saatler süren bir hata ayıklamaya yol açabilir.

Şimdi `Main` metodunu ve amacını kısaca açıklayan bir yorum satırını ekleyin:

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## Adım 3: OCR Motorunu Başlatın

`OcrEngine` işin bel kemiğidir. Motoru bir kez örnekleyip tüm sayfalar için yeniden kullanmak hem bellek açısından verimli hem de hızlıdır.

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Arka planda ne oluyor?** Motor dil modellerini yükler ve varsayılan ayarları (ör. İngilizce, otomatik döndürme) önceden yapılandırır. Daha sonra bu ayarları değiştirebilirsiniz, ancak varsayılanlar çoğu belge için yeterlidir.

## Adım 4: Çok Sayfalı TIFF'i Yükleyin

Aspose, çok çerçeveli görüntüleri sorunsuz bir şekilde yüklemenizi sağlar. Tam yolu ya da çalıştırılabilir dosyanın çalışma dizininden göreli bir yolu belirtin.

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

Dosya bulunamazsa `FromMultiPageFile` bir `FileNotFoundException` fırlatır. Daha nazik bir hata yönetimi istiyorsanız `try/catch` bloğu ekleyin—bunu bir sonraki adımda göstereceğiz.

## Adım 5: Toplu OCR'ı Gerçekleştirin

Şimdi gösterinin yıldızı: `RecognizeBatch`. Bu metod, anahtarının sayfa indeksi (0'dan başlayan) ve değerinin tanınan metin olduğu bir `Dictionary<int,string>` döndürür.

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **Köşe durumu:** Bazı TIFF'lerde boş sayfalar bulunabilir. Aspose bu sayfalar için boş bir string döndürür; çıktınızda gereksiz kalabalık istemiyorsanız daha sonra filtreleyebilirsiniz.

## Adım 6: Sonuçları Görüntüleyin

Son olarak sözlüğü döngüye alıp her sayfanın metnini ekrana yazdırın. Interpolated string kullanmak kodu temiz tutar.

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı almanız gerekir:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

Eğer bozuk karakterler görürseniz, kaynak TIFF'in bozulmadığını ve metnin dilinin motorun varsayılan dili (İngilizce) ile eşleştiğini kontrol edin. İngilizce dışı belgeler için `ocrEngine.Language = OcrLanguage.Spanish;` gibi bir ayar da yapabilirsiniz.

## Tam Çalışan Örnek

Tüm parçaları bir araya getirdiğimizde, `Program.cs` dosyasına kopyalayıp çalıştırabileceğiniz eksiksiz program aşağıdadır:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Kaydedin, derleyin ve çalıştırın:

```bash
dotnet run
```

Her sayfanın çıkarılmış içeriği konsola yazdırılacaktır. İşte aradığınız **c# ocr tutorial** burada.

## Sık Sorulan Sorular & Köşe Durumları

### TIFF'imde onlarca sayfa varsa ne yapmalıyım?

`RecognizeBatch` tek bir çağrıda tüm çerçeveleri işler, ancak bellek kullanımı sayfa sayısı ile lineer olarak artar. Çok büyük belgeler (yüzlerce sayfa) için parçalar halinde işleme yapmayı düşünün:

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### Çıktıyı dosyalara kaydetmek istersem nasıl yaparım?

Kesinlikle. `Console.WriteLine` bloğunu dosya I/O kodu ile değiştirin:

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

Artık her sayfa için ayrı bir `.txt` dosyası oluşturulur—sonraki indeksleme işlemleri için ideal.

### Çıktı dilini değiştirmek ya da otomatik döndürmeyi etkinleştirmek nasıl olur?

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

Bu ayarlar **RecognizeBatch** çağrılmadan **önce** uygulanmalıdır.

## Sonuç

Aspose OCR kullanarak C# ile çok sayfalı bir TIFF'i **toplu OCR** ile nasıl işleyebileceğinizi ele aldık. Görüntüyü bir kez yükleyip `RecognizeBatch` çağırarak ve elde edilen sözlüğü döngüye alarak **TIFF'i metne dönüştürme** işlemini saniyeler içinde tamamlayabilirsiniz. Örnek aynı zamanda **TIFF'ten metin çıkarma**, hata yönetimi ve isteğe bağlı olarak sonuçları dosyalara yazma konularını da gösteriyor—hepsi temiz, tek dosyalı bir konsol uygulaması içinde.

Bir sonraki adıma hazır mısınız? Bu yaklaşımı bir PDF oluşturma kütüphanesiyle birleştirerek aranabilir PDF'ler üretin ya da çıktıyı bir veritabanına kaydedip arşivlenebilir bir sistem oluşturun. `Image.FromMultiPageFile` yerine `Image.FromFile` kullanarak diğer görüntü formatları (PNG, JPEG) ile de deneyler yapabilirsiniz.

OCR, lisanslama ya da performans ayarlamaları hakkında daha fazla sorunuz varsa aşağıya yorum bırakın, iyi kodlamalar!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}