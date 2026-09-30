---
category: general
date: 2026-02-22
description: Aspose OCR kullanarak aranabilir PDF oluşturun ve görüntüden metin çıkarın.
  Tek bir öğreticide görüntüyü PDF'ye dönüştürmeyi ve düz metin çıktısı almayı öğrenin.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: tr
og_description: Aspose OCR ile taranmış görüntülerden aranabilir PDF oluşturun. Bu
  kılavuz, görüntüden metin çıkarmayı, düz metin olarak çıktı almayı ve görüntüyü
  PDF'ye dönüştürmeyi gösterir.
og_title: Görüntülerden Aranabilir PDF Oluşturma – Tam C# Öğreticisi
tags:
- C#
- OCR
- PDF generation
- Aspose
title: C#'ta Görüntülerden Aranabilir PDF Oluşturma – Adım Adım Rehber
url: /tr/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerden Aranabilir PDF Oluşturma C# – Tam Kılavuz

Hiç taranmış bir fotoğraftan **aranabilir PDF** oluşturmanız gerekti ama nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—çoğu geliştirici OCR ile ilk karşılaştıklarında bu duvara çarpar. İyi haber? Aspose OCR ile sadece birkaç C# satırıyla **extract text from image**, **output plain text** ve **convert image to PDF** yapabilirsiniz.

Bu rehberde, bir PNG dosyasını yüklemekten aranabilir PDF ve düz metin dosyası kaydetmeye kadar tüm süreci adım adım inceleyeceğiz. Sonunda, herhangi bir .NET projesine yapıştırabileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız. Gereksiz ayrıntı yok, sadece işi halleder.

## Öğrenecekleriniz

- Bir .NET console uygulamasında **Aspose.OCR**'yi nasıl kuracağınız.  
- **output plain text** ve **searchable PDF** modları arasındaki fark.  
- **extract text from image** yapıp bir `.txt` dosyasına nasıl yazacağınız.  
- Orijinal bitmap'i korurken gizli bir metin katmanı ekleyen **convert image to PDF** nasıl yapılır.  
- Büyük toplu işlemler, yaygın hatalar ve doğruluğu artırmak için ayarları nerede değiştirileceği ipuçları.

> **Prerequisites** – .NET 6+ (veya .NET Framework 4.7+), Visual Studio 2022 (veya herhangi bir editör) ve bir Aspose OCR lisansı (veya ücretsiz deneme) gerekir. Başka üçüncü‑taraf kütüphane gerekmez.

![generate searchable pdf example](image-placeholder.png "Example of a generated searchable PDF")

## Adım 1: Aspose  OCR'yi Yükleyin ve Motoru Oluşturun

İlk iş olarak NuGet paketini projenize ekleyin:

```bash
dotnet add package Aspose.OCR
```

Şimdi OCR motorunu başlatıp hangi dilde çalıştığını söyleyebiliriz. İngilizce varsayılan, ancak `Language` enum'ını değiştirerek Fransızca, İspanyolca vb. dilleri seçebilirsiniz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Neden önemli:** Motor, tüm yapılandırmayı—dil, çıktı formatı ve isteğe bağlı ön işleme bayraklarını—tutar. Bir kez ayarlayıp yeniden kullanmak, her dosya için yeni bir örnek oluşturmanın getirdiği yükü azaltır.

## Adım 2: Metni Çıkarın ve Düz Metin Olarak Kaydedin

Sadece ham karakterlere ihtiyacınız varsa motoru `OutputFormat.Text` olarak ayarlayın. Bu, Aspose OCR'yi PDF üretimini tamamen atlamaya ve bir string döndürmeye zorlar.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Pro tip:** `plainTextResult.Text` zaten OCR düzenine ait satır sonlarını temizler. Orijinal boşlukları korumak isterseniz `plainTextResult.TextBlocks`'a bakın.

### Beklenen Sonuç

`output.txt` dosyasını açın; aşağıdakine benzer bir şey görmelisiniz:

```
Hello, world!
This is a sample scanned document.
```

Bu, öğreticinin **output plain text** kısmıdır—hızlı, hafif ve sonraki işlemler (ör. indeksleme) için mükemmel.

## Adım 3: Aranabilir PDF Moduna Geçiş

Şimdi bir **searchable PDF** oluşturalım. Motor, orijinal bitmap'i gömüp OCR‑oluşturulan metni alt katmana ekleyecek, böylece belge herhangi bir PDF görüntüleyicide aranabilir olacak.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Neden yeniden tanıma yapıyoruz:** OCR motoru son görüntüyü önbelleğe alır, ancak çıktı formatı hangi veriyi döndüreceğini belirler. Formatı değiştirmek, gizli metin katmanını içeren yeni bir geçişi zorunlu kılar.

### PDF Nasıl Görünür

`output.pdf` dosyasını Adobe Reader veya başka bir görüntüleyicide açın ve metni seçmeye çalışın. Görsel hâlâ orijinal bitmap olsa da içeriği kopyalayabilir, arayabilir ve vurgulayabilirsiniz. İşte **convert scanned image pdf**'in özelliği bu.

## Adım 4: Birden Fazla Dosya İşleme (Opsiyonel)

Gerçek dünyada projeler nadiren tek bir görüntüyle çalışır. Aşağıdaki döngü, bir klasördeki tüm PNG dosyalarını işleyerek eşleşen `.txt` ve `.pdf` dosyalarını üretir.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Köşe durum notu:** Büyük görüntüler bellek tüketebilir. `OutOfMemoryException` alırsanız, tanıma öncesinde `Image.Resize` ile küçültmeyi veya dosyaları daha küçük partilerde işlemeyi düşünün.

## Adım 5: OCR Doğruluğunu İnce Ayar Yapma

Aspose OCR birkaç ayar sunar:

| Setting | What it does | When to use |
|---------|--------------|-------------|
| `ocrEngine.PageSegmentationMode` | Engine'in görüntüyü metin bloklarına nasıl böleceğini kontrol eder. | Çok sütunlu düzenlerde faydalıdır. |
| `ocrEngine.Deskew` | Hafif eğimli sayfaları otomatik döndürür. | Tam olarak hizalanmamış taranmış belgeler. |
| `ocrEngine.RemoveNoise` | Lekeleri ve arka plan artefaktlarını temizlemeye çalışır. | Düşük kalite taramalar veya faks sayfaları. |

Örnek:

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

Bu seçenekleri etkinleştirmek işlem süresini artırabilir, ancak **extract text from image** kalitesindeki artış genellikle buna değerdir.

## Adım 6: Çıktıyı Programlı Olarak Doğrulama

Bazen PDF'in gerçekten aranabilir metin içerdiğini (ör. otomatik testlerde) doğrulamanız gerekir. En basit kontrol, PDF bayt dizisinin boş olmaması ve `RawData` uzunluğunun görüntü boyutundan büyük olmasıdır.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

Daha derin bir doğrulama için bir PDF kütüphanesi (iTextSharp gibi) kullanarak metin akışını çıkarıp `plainTextResult.Text` ile karşılaştırabilirsiniz.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

- **Missing License** – Geçerli bir Aspose lisansı olmadan kütüphane değerlendirme modunda çalışır ve PDF'lere filigran ekler. Lisansınızı erken kaydedin (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Incorrect Path** – Mutlak yolları sabit kodlamak kendi makinenizde çalışır ama başka bir yerde kırılır. Taşınabilirlik için `Path.Combine` ve `AppDomain.CurrentDomain.BaseDirectory` kullanın.  
- **Unsupported Image Formats** – GIF ve çok sayfalı TIFF'ler özel işleme (`Image.LoadMultiPage`) gerektirir. Sadece ilk sayfaya ihtiyacınız varsa önce PNG/JPEG'e dönüştürün.  
- **Performance Bottlenecks** – Döngü içinde `OcrEngine` yeniden oluşturmak maliyetlidir. Tek bir örnek tutun ve sadece `OutputFormat`'u gerektiği gibi değiştirin.

## Özet

Aspose OCR kullanarak taranmış bir görüntüden **generate searchable PDF** oluşturma sürecini baştan sona ele aldık:

1. NuGet paketini kurun ve bir `OcrEngine` oluşturun.  
2. `OutputFormat.Text` ile **output plain text** elde edip `.txt` dosyasına yazın.  
3. `OutputFormat.SearchablePdf` ile **convert image to PDF** yapıp gizli bir metin katmanı ekleyin.  
4. PDF baytlarını kaydedin ve toplu işleme için klasör döngüsü ekleyin.  
5. Deskew, noise removal ve page segmentation gibi ayarlarla doğruluğu ince ayar yapın.  

Tüm bunlar, Visual Studio'ya kopyalayıp yapıştırabileceğiniz kompakt, bağımsız bir programda toplanmıştır.

## Bir Sonraki Denemeniz Gerekenler?

- **Batch processing** ile bir UI ön yüz (WinForms veya WPF) ekleyerek kullanıcıların dosyaları sürükle‑bırak yapmasını sağlayın.  
- **Language detection** – Aspose OCR otomatik dil algılayabilir; `ocrEngine.Language = Language.AutoDetect` deneyin.  
- **Post‑processing** – Çıkarılan metni bir arama indeksine (ElasticSearch, Azure Cognitive Search) göndererek anlık belge bulma sağlayın.  
- **Alternative outputs** – Web ön izlemeleri için `OutputFormat.Hocr` kullanarak HTML‑tabanlı OCR sonuçları alın.

Farklı görüntü çözünürlükleri, renk modları ve OCR ayarlarıyla denemeler yapmaktan çekinmeyin. Ne kadar çok oynarsanız, hız ve doğruluk arasındaki dengeyi o kadar iyi kavrarsınız.

---

**Kodlamaktan keyif alın!** Herhangi bir sorunla karşılaşırsanız aşağıya yorum bırakın ya da daha derin bilgiler için Aspose OCR dokümantasyonuna göz atın. İster fatura, arşivleme, ister aranabilir bilgi tabanı oluşturma projesi olsun, bir sonraki projeniz çok daha kolay olacak.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}