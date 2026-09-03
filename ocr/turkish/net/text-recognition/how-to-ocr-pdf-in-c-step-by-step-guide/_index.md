---
category: general
date: 2025-12-29
description: C#'ta PDF dosyalarını OCR'lamak ve PDF sayfalarından metin çıkarmayı
  öğrenin. Bu öğreticide ayrıca PDF'yi metne dönüştürme ve PDF sayfasını C# ile okuma
  teknikleri de ele alınmaktadır.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- extract pdf text c#
- read pdf page c#
language: tr
og_description: C#'ta PDF OCR nasıl yapılır, özlü bir rehberde açıklandı. PDF'den
  metin çıkarmak, PDF'yi metne dönüştürmek ve PDF sayfasını C# ile okumak için tam
  kodu alın.
og_title: C#'ta PDF OCR Nasıl Yapılır – Tam Programlama Rehberi
tags:
- OCR
- C#
- PDF processing
title: C#'ta PDF'yi OCR Nasıl Yapılır – Adım Adım Rehber
url: /tr/net/text-recognition/how-to-ocr-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta PDF OCR Nasıl Yapılır – Adım Adım Kılavuz

C# uygulamanızdan doğrudan **how to OCR PDF** dosyalarını OCR'lamak istediğinizi hiç merak ettiniz mi? Belki taranmış faturalar yığınına sahipsiniz ve metni manuel kopyala‑yapıştır yapmadan çıkarmanız gerekiyor. Bu, PDF'ler görüntü tabanlı olduğunda ve geleneksel metin çıkarma yöntemleri başarısız olduğunda sık karşılaşılan bir sorundur.  

Bu öğreticide, **how to OCR PDF** sadece göstermekle kalmayıp aynı zamanda *extract text from PDF*, *convert PDF to text* ve *read PDF page C#* işlemlerini Aspose.OCR kütüphanesiyle nasıl yapacağınızı adım adım anlatan, çalıştırmaya hazır bir çözüm üzerinden ilerleyeceğiz. Belirsiz referanslar yok – sadece Visual Studio'ya yapıştırıp denemeye başlayabileceğiniz kodlar.

## What You’ll Need

- **.NET 6.0** veya daha yeni bir sürüm (kod .NET Framework 4.7+ üzerinde de çalışır)  
- **Aspose.OCR** NuGet paketi – `dotnet add package Aspose.OCR` komutuyla kurun  
- Bir taranmış PDF (ör. `invoice.pdf`) ve referans verebileceğiniz bir klasör  
- C# konsol uygulamaları hakkında temel bilgi  

Hepsi bu. Zaten bir projeniz varsa sadece paketi ekleyin, hazırsınız.

## Step 1: Set Up the Project and Add Aspose.OCR

İlk olarak yeni bir konsol projesi oluşturun (ya da mevcut bir projeyi kullanın) ve OCR kütüphanesini ekleyin.

```csharp
// Create a new console app (run this in a terminal)
// > dotnet new console -n OcrPdfDemo
// > cd OcrPdfDemo
// > dotnet add package Aspose.OCR
```

Bu adımın önemi: Aspose.OCR, görüntü analizi, düzen algılama ve karakter tanıma işlerini üstlenir. Onsuz rasterizer, Tesseract motoru ve bir sürü bağlayıcı kodu bir araya getirmeniz gerekir.

## Step 2: Import Namespaces and Prepare the OCR Engine

Şimdi `Program.cs` dosyasını (veya tercih ettiğiniz herhangi bir .cs dosyasını) açın ve gerekli `using` yönergelerini ekleyin.

```csharp
using System;
using Aspose.OCR;   // Core OCR classes
```

Motoru oluşturmak oldukça basit, ancak tipik fatura taramaları için doğruluğu artıran birkaç seçeneği de yapılandıracağız.

```csharp
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Enable automatic language detection (optional but handy)
    Language = Language.English,
    // Turn on deskew to correct rotated pages
    ImagePreprocessingOptions = new ImagePreprocessingOptions
    {
        Deskew = true,
        Binarization = true
    }
};
```

**Pro ipucu:** Dili önceden biliyorsanız `Language` özelliğini açıkça ayarlayın; işlem daha hızlı gerçekleşir.

## Step 3: Point to Your PDF File

İşlemek istediğiniz PDF'nin mutlak ya da göreli yolunu belirtin. Bu örnek için dosyanın `Samples` adlı bir klasörde olduğunu varsayacağız.

```csharp
// Path to the PDF you want to OCR
string pdfFilePath = @"Samples/invoice.pdf";

// Verify the file exists early to avoid runtime surprises
if (!System.IO.File.Exists(pdfFilePath))
{
    Console.WriteLine($"File not found: {pdfFilePath}");
    return;
}
```

Dosyanın varlığını kontrol etmek küçük bir adımdır, ancak ileride karşılaşabileceğiniz belirsiz istisnalardan sizi korur.

## Step 4: Choose the Page(s) to Read

Bir PDF'de onlarca sayfa olabilir, ancak çoğu zaman sadece belirli bir sayfaya ihtiyacınız olur – örneğin toplam tutarın bulunduğu ikinci sayfa. `RecognizePdf` metodu tek bir sayfayı ya da tüm belgeyi hedeflemenize olanak tanır.

```csharp
// Extract text from page 2 (page numbers are 1‑based)
int pageNumber = 2;

// The method returns an OcrResult containing the recognized text
OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);
```

Eğer *convert PDF to text* işlemini tüm belge için yapmak istiyorsanız `pageNumber` parametresini atlayın:

```csharp
// OcrResult fullResult = ocrEngine.RecognizePdf(pdfFilePath);
```

## Step 5: Display or Save the Extracted Text

OCR motoru işi bitirdiğinde, metni konsola yazdırabilir, bir `.txt` dosyasına kaydedebilir ya da başka bir sisteme (ör. veritabanı) besleyebilirsiniz.

```csharp
// Show the recognized text in the console
Console.WriteLine("=== OCR Result (Page {0}) ===", pageNumber);
Console.WriteLine(ocrResult.Text);

// Optionally, save to a .txt file
string outputPath = $"output_page{pageNumber}.txt";
System.IO.File.WriteAllText(outputPath, ocrResult.Text);
Console.WriteLine($"Text saved to {outputPath}");
```

**Neden önemli:** Çıktıyı kalıcı hale getirerek yeniden kullanılabilir bir artefakt oluşturursunuz – sonraki analizler ya da arama indekslemesi için ideal.

## Full Working Example

Hepsini bir araya getirdiğimizde, `Program.cs` içine kopyalayıp hemen çalıştırabileceğiniz bağımsız bir program elde edersiniz.

```csharp
using System;
using Aspose.OCR;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine with helpful options
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                ImagePreprocessingOptions = new ImagePreprocessingOptions
                {
                    Deskew = true,
                    Binarization = true
                }
            };

            // 2️⃣ Define the PDF path
            string pdfFilePath = @"Samples/invoice.pdf";
            if (!System.IO.File.Exists(pdfFilePath))
            {
                Console.WriteLine($"Error: File not found -> {pdfFilePath}");
                return;
            }

            // 3️⃣ Choose which page to OCR (change as needed)
            int pageNumber = 2; // read PDF page C# example

            // 4️⃣ Perform OCR on the selected page
            OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);

            // 5️⃣ Output the result
            Console.WriteLine($"--- OCR Result for page {pageNumber} ---");
            Console.WriteLine(ocrResult.Text);

            // 6️⃣ Save to a text file for later use
            string outputPath = $"output_page{pageNumber}.txt";
            System.IO.File.WriteAllText(outputPath, ocrResult.Text);
            Console.WriteLine($"Extracted text saved to: {outputPath}");
        }
    }
}
```

### Expected Output

```
--- OCR Result for page 2 ---
Invoice #12345
Date: 2024‑11‑30
Total: $1,250.00
...
Extracted text saved to: output_page2.txt
```

PDF net, yüksek çözünürlüklü taramalar içeriyorsa çıktı neredeyse kusursuz olur. Düşük kaliteli görüntüler ek ön işleme (ör. DPI artırma veya filtre uygulama) gerektirebilir; Aspose.OCR’nin `ImagePreprocessingOptions` bu senaryolara göre ayarlanabilir.

## Common Questions & Edge Cases

### 1️⃣ What if the PDF is password‑protected?
Aspose.OCR’nin `RecognizePdf` aşırı yüklemesi, şifreyi belirtebileceğiniz bir `PdfLoadOptions` nesnesi alır:

```csharp
var loadOptions = new PdfLoadOptions { Password = "mySecret" };
OcrResult result = ocrEngine.RecognizePdf(pdfFilePath, pageNumber, loadOptions);
```

### 2️⃣ Can I OCR the entire document in one go?
Evet—`RecognizePdf(pdfFilePath)` metodunu sayfa numarası belirtmeden çağırın. Metod, tüm sayfalardan birleştirilmiş metni içeren tek bir `OcrResult` döndürür.

### 3️⃣ How does this differ from “extract text from PDF” using a text‑based library?
Saf metin çıkarma (ör. iTextSharp kullanımı) yalnızca zaten seçilebilir metin içeren PDF'lerde çalışır. **how to OCR PDF** ise PDF esasen bir dizi görüntü (taranmış faturalar gibi) olduğunda gerekir. Bu durumda OCR motoru, resimleri aranabilir metne dönüştürür.

### 4️⃣ What about performance on large PDFs?
İşlem süresi sayfa sayısı ve görüntü çözünürlüğüyle yaklaşık doğrusal artar. Büyük işler için şunları düşünün:
- OCR’ı paralel çalıştırın (`Parallel.ForEach`)  
- OCR’dan önce görüntü DPI’sını düşürün (`Resolution = 150`)  
- Her dosya için yeni bir `OcrEngine` örneği yaratmak yerine aynı örneği önbelleğe alın

### 5️⃣ Is there a way to get the bounding boxes of each word?
`OcrResult`, koordinatları içeren bir `OcrRegion` koleksiyonu sunar. Bunları döngüyle gezerek aranabilir PDF’ler oluşturabilir ya da UI’da sonuçları vurgulayabilirsiniz.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} – ({region.Bounds.X}, {region.Bounds.Y}, {region.Bounds.Width}, {region.Bounds.Height})");
}
```

## Tips for Production‑Ready Implementations

- **Error handling:** OCR çağrılarını try/catch bloklarıyla sararak kütüphane‑özel istisnaları yakalayın.  
- **Logging:** Sayfa numaralarını ve işlem sürelerini kaydedin; sorunlu taramaları tespit etmenize yardımcı olur.  
- **Memory management:** PDF sayfalarını görüntülere dönüştürürken büyük `Bitmap` nesnelerini dispose edin.  
- **Security:** Ham PDF’leri güvensiz disklerde saklamayın; doğrudan OCR motoruna akıtmayı değerlendirin.  

## Conclusion

Artık C# kullanarak **how to OCR PDF** sorusuna tam bir uçtan uca yanıtınız var. Eğitim, Aspose.OCR kurulumu, belirli bir sayfanın seçilmesi, metnin çıkarılması ve yaygın kenar durumlarının ele alınması konularını kapsadı. Bu temelle *extract text from PDF*, *convert PDF to text* ve *read PDF page C#* işlemlerini herhangi bir belge işleme hattına entegre edebilirsiniz.

Bir sonraki adıma hazır mısınız? OCR çıktısını Lucene.NET gibi tam metin arama motoruna besleyin ya da tanınan metni orijinal görüntüler üzerine bindirerek aranabilir PDF’ler oluşturun. Ufkunuz geniş, ve bu araçlarla artık oraya ulaşabilirsiniz.

---

![ocr pdf örneği](image-placeholder.png "PDF sayfasında OCR işleme illüstrasyonu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}