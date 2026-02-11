---
category: general
date: 2026-02-11
description: C#'ta Arapça bir görüntüden aranabilir PDF oluşturun. Görüntüyü PDF'ye
  dönüştürmeyi, Arapça metni çıkarmayı ve Aspose OCR kullanarak gizli metin eklemeyi
  öğrenin.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract arabic text
- pdf with hidden text
- ocr arabic image
language: tr
og_description: Aspose OCR kullanarak C#'ta Arapça bir görüntüden aranabilir PDF oluşturun.
  Görüntüyü PDF'ye dönüştürmek, Arapça metni çıkarmak ve gizli metni gömmek için bu
  rehberi izleyin.
og_title: Arapça Görüntüden Aranabilir PDF Oluştur – Adım Adım
tags:
- Aspose
- OCR
- PDF
- C#
- Arabic
title: Arapça Görüntüden Aranabilir PDF Oluşturma – Tam Kılavuz
url: /tr/net/text-recognition/create-searchable-pdf-from-arabic-image-complete-guide/
---

0}} etc. Keep them unchanged.

Also need to translate the blockquote lines.

Let's translate.

Title: "Create Searchable PDF from Arabic Image – Complete Guide" => "Arapça Görüntüden Aranabilir PDF Oluşturma – Tam Kılavuz"

Paragraphs.

We'll translate naturally.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Arapça Görüntüden Aranabilir PDF Oluşturma – Tam Kılavuz

Tarayıcıdan alınmış bir Arapça faturadan **aranabilir PDF** oluşturmanız gerektiğinde, orijinal görünümü korurken metnin seçilebilir olmasını nasıl sağlayacağınızı hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok belge‑otomasyon projesinde zorluk sadece bir resmi PDF’ye dönüştürmek değil, aynı zamanda görsel düzeni korumak ve arama motorlarının indeksleyebileceği gizli bir metin katmanı eklemektir.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: **görseli PDF’ye dönüştürme**, **Aspose OCR ile Arapça metni çıkarma** ve sonunda bu metni **gizli metinli PDF** olarak gömme, böylece ortaya çıkan dosya tamamen aranabilir olur. Sonunda, herhangi bir .NET çözümüne ekleyebileceğiniz hazır bir C# kod parçacığına sahip olacaksınız. Harici hizmetlere gerek yok, sadece zaten sahip olduğunuz Aspose kütüphaneleri yeterli.

## Gerekenler

- .NET 6 veya üzeri (kod .NET Core ile de çalışır)  
- **Aspose.OCR** ve **Aspose.Pdf** NuGet paketleri (Şubat 2026 itibarıyla en yeni sürümler)  
- Aranabilir PDF’ye dönüştürmek istediğiniz bir Arapça görüntü dosyası (ör. `arabic_invoice.jpg`)  
- Biraz C# bilgisi – kavramlar basit, ancak her satırın “neden”ini açıklayacağız.

> **Pro ipucu:** NuGet paketlerini henüz eklemediyseniz, proje klasörünüzden şu komutları çalıştırın  
> `dotnet add package Aspose.OCR` ve  
> `dotnet add package Aspose.Pdf`.

Şartlar halledildiğine göre, adım adım uygulamaya geçelim.

## Adım 1 – OCR Motorunu Arapça Metin İçin Ayarlama

İlk yapmamız gereken, Aspose OCR’u Arapça karakterleri tanıyacak şekilde yapılandırmak. Arapça sağ‑dan‑sol bir yazı sistemi olduğundan, motorun hangi dili yükleyeceğini belirtmeli ve dil verileri makinede yoksa otomatik kaynak indirmeyi etkinleştirmeliyiz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Configure OCR for Arabic and let Aspose fetch the language pack if needed
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic,
    AutomaticResourceDownload = true
};
```

**Neden önemli:**  
`Language = OcrLanguage.Arabic` ayarını atlamanız durumunda motor varsayılan olarak İngilizceyi kullanır ve karakterler bozuk çıkar. `AutomaticResourceDownload` özelliği, dil dosyalarını sunucuya manuel olarak yerleştirmenizi engeller.

## Adım 2 – Kaynak Görüntüyü Yükleme

Şimdi Arapça metni içeren görüntüyü yüklüyoruz. `Image.FromFile` kullanmak, görüntünün bir GDI+ `Image` nesnesine okunmasını sağlar; bu, Aspose OCR’un beklediği formattır.

```csharp
using System.Drawing;          // For Image
using System.IO;                // For MemoryStream

// Replace with the actual path to your Arabic invoice
string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";

using (var inputImage = Image.FromFile(imagePath))
{
    // The rest of the workflow lives inside this using block
```

**Köşe durumu:** Görüntü çok büyükse (ör. taranmış bir A3 sayfa), performansı artırmak için önce ölçek küçültmeyi düşünün. OCR motoru büyük dosyaları işleyebilir, ancak bellek kullanımı hızla artar.

## Adım 3 – Arapça Metni Tanıma ve Sonucu Yakalama

Şimdi OCR’u çalıştırıyoruz. `Recognize` metodu, tespit edilen metin, güven skorları ve (gelişmiş düzen analizi için ihtiyaç duyarsanız) sınırlayıcı kutuları içeren bir `OcrResult` nesnesi döndürür.

```csharp
    // Perform OCR on the loaded image
    OcrResult ocrResult = ocrEngine.Recognize(inputImage);
    string extractedText = ocrResult.Text;

    // Quick sanity check: print the first 200 characters to the console
    Console.WriteLine("Extracted Arabic text (preview):");
    Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Ön izlemeyi neden tutmalısınız?**  
Çıkarılan metnin bir kısmını görmek, dil paketinin doğru yüklendiğini PDF oluşturma sürecine zaman harcamadan doğrulamanıza yardımcı olur.

## Adım 4 – Yeni Bir PDF Belgesi Oluşturma ve Boş Sayfa Ekleme

Metin elimizde olduğuna göre PDF’i oluşturmaya başlayabiliriz. Aspose PDF bize tüm dosyayı temsil eden bir `Document` nesnesi sağlar. Bir sayfa eklemek, hem orijinal görüntüyü hem de gizli metin katmanını yerleştireceğimiz bir tuval oluşturur.

```csharp
    // Initialize a new PDF document
    var pdfDocument = new Aspose.Pdf.Document();

    // Add a blank page – this will become the background for our image
    var pdfPage = pdfDocument.Pages.Add();
```

**Not:** Çok sayfalı bir TIFF veya PDF işliyorsanız birden fazla sayfa ekleyebilirsiniz; tek görüntülü senaryoda bir sayfa yeterlidir.

## Adım 5 – Orijinal Görüntüyü Arka Plan Öğesi Olarak Eklemek

Son PDF’nin taranmış faturayla tamamen aynı görünmesini istiyoruz; bu yüzden görüntüyü görünür bir arka plan olarak gömüyoruz. Aspose PDF’den `Image` sınıfı bir akış (stream) beklediği için dosyayı bir `MemoryStream` içine okuruz.

```csharp
    // Load the same image bytes for the PDF background
    var backgroundImage = new Aspose.Pdf.Image
    {
        ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
    };

    // Add the image to the page's paragraph collection
    pdfPage.Paragraphs.Add(backgroundImage);
```

**Neden arka plan resmi?**  
Görüntüyü doğrudan sayfaya yerleştirmek, orijinal düzeni, renkleri ve OCR motorunun göz ardı edebileceği damga ya da logoları korur.

## Adım 6 – OCR Metnini Gizli Katman Olarak Eklemek

**Aranabilir PDF** için gizli metin katmanı, görüntünün üstünde yer alır. Yazı tipinin boyutunu `0` yaparak metni insan gözüyle görünmez hâle getirir, ancak hâlâ seçilebilir ve aranabilir kalır.

```csharp
    // Create a TextFragment with the extracted Arabic text
    var searchableText = new Aspose.Pdf.Text.TextFragment(extractedText)
    {
        // Hide the visible text; only the text layer remains searchable
        TextState = { FontSize = 0 }
    };

    // Add the hidden text fragment to the same page
    pdfPage.Paragraphs.Add(searchableText);
```

**Önemli bir nüans:**  
Gizli metnin görüntüyle mükemmel hizalanması gerekiyorsa (ör. OCR koordinatlar döndürdüğünde), `TextFragmentAbsorber` kullanıp her parçayı manuel konumlandırabilirsiniz. Çoğu fatura için basit bir tam‑sayfa kaplama yeterli olur.

## Adım 7 – Aranabilir PDF’yi Kaydetme

Son olarak PDF’yi diske yazıyoruz. Çıktı dosyası hem görsel resmi hem de gizli Arapça metni içerir; böylece Adobe Reader, Google Drive ya da OCR‑bilinçli herhangi bir görüntüleyicide tamamen aranabilir olur.

```csharp
    // Define the output path
    string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";

    // Save the document
    pdfDocument.Save(outputPath);

    Console.WriteLine($"Searchable PDF created at: {outputPath}");
}
```

### Tam Çalışan Örnek

Tüm parçaları bir araya getirerek, işte çalıştırmaya hazır tam program:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic,
            AutomaticResourceDownload = true
        };

        // 2️⃣ Load the source image
        string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";
        using (var inputImage = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR and get the text
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);
            string extractedText = ocrResult.Text;

            // Optional preview
            Console.WriteLine("Extracted Arabic text (preview):");
            Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));

            // 4️⃣ Create PDF document
            var pdfDocument = new Document();
            var pdfPage = pdfDocument.Pages.Add();

            // 5️⃣ Add original image as background
            var backgroundImage = new Aspose.Pdf.Image
            {
                ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
            };
            pdfPage.Paragraphs.Add(backgroundImage);

            // 6️⃣ Add hidden searchable text
            var searchableText = new TextFragment(extractedText)
            {
                TextState = { FontSize = 0 }
            };
            pdfPage.Paragraphs.Add(searchableText);

            // 7️⃣ Save the searchable PDF
            string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";
            pdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Beklenen sonuç:** Oluşturulan `arabic_invoice_searchable.pdf` dosyasını herhangi bir PDF görüntüleyicide açın, **Ctrl + F** tuşlarına basın ve orijinal faturada yer alan bir Arapça kelimeyi yazın. Görüntüleyici, metin katmanı görünmese bile kelimeyi bulmalıdır.

## Yaygın Sorular & Dikkat Edilmesi Gerekenler

- **Diğer dillerle de çalışır mı?**  
  Kesinlikle. Sadece `Language = OcrLanguage.YourLanguage` satırını değiştirin ve ilgili dil paketinin mevcut olduğundan emin olun. Geri kalan akış aynı kalır.

- **OCR güveni düşük olduğunda ne yapmalı?**  
  `ocrResult.Confidence` değerini (0‑1 arası) inceleyebilirsiniz. Eğer bir eşik değerinin (ör. 0.75) altına düşerse, görüntüyü ön‑işleme tabi tutun—düzeltme, kontrast artırma veya gri tonlamaya çevirme—motorun önüne göndermeden önce.

- **Bir PDF’ye birden fazla görüntü ekleyebilir miyim?**  
  Evet. Görüntü yollarının bir koleksiyonunu döngüye alıp her biri için yeni bir sayfa ekleyin ve adım 5‑6’yı tekrarlayın. Her görüntü için `using` bloğunu korumayı unutmayın; böylece GDI kaynakları serbest bırakılır.

- **Gizli metin gerçekten görünmez mi?**  
  `FontSize = 0` çoğu görüntüleyicide metni görünmez kılar. Eğer bir görüntüleyici hâlâ hafif bir glif gösteriyorsa, metin rengini tamamen şeffaf yapabilirsiniz (`TextState.FillColor = Color.Transparent`).

## Sonraki Adımlar

Artık **Arapça bir görüntüden aranabilir PDF** oluşturmayı bildiğinize göre, aşağıdaki konuları keşfetmek isteyebilirsiniz:

- **Toplu işleme** – bir klasördeki tüm görüntüleri okuyup her dosya için tek bir aranabilir PDF oluşturma.  
- **OCR koordinatlarını ekleme** – `OcrResult.Regions` kullanarak her metin parçasını tam olarak göründüğü konuma yerleştirme, karmaşık düzenlerde arama doğruluğunu artırır.  
- **PDF şifreleme** – Aspose PDF, ek güvenlik ihtiyacınız varsa parola veya dijital imza eklemenize olanak tanır.  
- **Azure Blob Storage entegrasyonu** – oluşturulan PDF’leri doğrudan buluta kaydedip sonraki iş akışları için kullanılabilir hâle getirme.

Bu konular doğal olarak ikincil anahtar kelimeler **convert image to pdf**, **extract** ile de ilişkilidir.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}