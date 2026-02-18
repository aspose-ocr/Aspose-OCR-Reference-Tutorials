---
category: general
date: 2026-02-17
description: Aspose OCR kullanarak C#'ta birden fazla PDF ve görüntüyü toplu OCR nasıl
  yapılır. PDF'den metin çıkarma, PDF'yi metne dönüştürme ve görüntülerden metin tanıma
  öğrenin.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: tr
og_description: Aspose OCR ile C#’ta birden fazla belgeyi toplu OCR nasıl yapılır.
  PDF’den metin çıkarmak, PDF’yi metne dönüştürmek ve görüntülerden metin tanımak
  için adım adım kodu alın.
og_title: C#'ta OCR Dosyalarını Toplu İşleme – Tam Kılavuz
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: C#'ta OCR dosyalarını toplu işleme – Tam Kod Örneği
url: /tr/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

alarını işleme – Tam Kılavuz". Keep same heading level.

Paragraphs: translate.

Need to keep **bold** formatting.

Also code block placeholders remain unchanged.

Tables: translate column headers and content but keep pipe formatting. Need to translate text inside table cells.

Let's translate.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta toplu OCR dosyalarını işleme – Tam Kılavuz

Hiç **toplu OCR** yaparak bir yığın PDF ve görüntü taramasını ayrı ayrı döngü yazmadan işleyebileceğinizi merak ettiniz mi? Yalnız değilsiniz. Çoğu geliştirici, bir kerede onlarca sayfadan metin çekmeleri gerektiğinde bu duvara çarpar. İyi haber? Aspose OCR ile dosyalar koleksiyonunu tek bir motora besleyebilir ve ağır işi ona bırakabilirsiniz.  

Bu öğreticide, **pdf'den metin çıkarma**, **pdf'yi metne dönüştürme** ve **görüntülerden metin tanıma** işlemlerini tek bir toplu çalıştırmada yapmanızı sağlayan pratik bir çözümü adım adım inceleyeceğiz. Sonunda, her sayfa için OCR sonucunu yazdıran hazır bir konsol uygulamanız olacak ve her adımın nedenini anlayarak projelerinize uyarlayabileceksiniz.

## Gereksinimler – Başlamadan Önce Neye İhtiyacınız Var

- **.NET 6.0 veya üzeri** (kod .NET Framework'ta da çalışır, ancak .NET 6+ önerilir)
- **Aspose.OCR NuGet paketi** – `dotnet add package Aspose.OCR` komutuyla kurun
- Birkaç örnek dosya: çok sayfalı bir PDF (`doc1.pdf`) ve taranmış bir TIFF (`doc2.tif`). Bunları `C:\OCRSamples` gibi bir klasöre koyun.
- Temel C# bilgisi – `using` ifadeleri ve koleksiyonlarla rahat olmalısınız.

> Pro ipucu: Lisansınız yoksa, Aspose geliştirme sırasında 100 sayfa sınırını kaldıran ücretsiz geçici bir anahtar sunar.

## Adım 1: Projeyi Oluşturun ve Ad Alanlarını İçe Aktarın

İlk olarak yeni bir konsol projesi oluşturun (veya mevcut bir projeye ekleyin) ve gerekli ad alanlarını ekleyin.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Neden önemli:** `Aspose.OCR.Image`'i içe aktarmak, PDF sayfalarını otomatik olarak ayrı görüntü akışlarına bölen `ImageStream.FromFile` metodunu sağlar. Bu, toplu işleme sorunsuz çalışan gizli sostur.

## Adım 2: OCR Motorunu Başlatın

Motor, temel OCR motoruyla iletişim kuran iş gücüdür. Tüm toplu işlem için yalnızca bir örnek yeterlidir.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Açıklama:** Aynı `OcrEngine` örneğini yeniden kullanmak, bellek tüketimini azaltır ve sayfalar arasında yerel kütüphanelerin yüklü kalması sayesinde işleme hızını artırır.

## Adım 3: Görüntü Akışları Listesini Oluşturun

Burada işlemek istediğimiz tüm belgeleri toplarız. `ImageStream.FromFile` bir PDF'i bireysel sayfalara ayıracak kadar akıllıdır; üç sayfalı bir PDF, sahne arkasında üç ayrı akışa dönüşür.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Köşe durumu:** PDF, TIFF, JPEG veya PNG karışımı varsa, aynı listeye ekleyin – Aspose format algılamasını otomatik olarak yapar.

## Adım 4: Toplu OCR İşlemini Çalıştırın

Şimdi listeyi motora veriyoruz. `RecognizeBatch` her sayfa için bir `OcrResult` nesnesi içeren bir koleksiyon döndürür.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Neden toplu?** OCR'ı sayfa sayfa manuel bir döngüde çalıştırmak, motorun her seferinde yeniden başlatılmasına neden olur ve işlem süresini iki katına çıkarabilir. `RecognizeBatch` motoru sıcak tutar ve sonuçları mevcut oldukça akış olarak geri gönderir.

## Adım 5: Tanınan Metni Çıktılayın

Son olarak, sonuçlar üzerinden döngü kurup her sayfanın metnini konsola yazarız. Burada `Console.WriteLine` yerine dosya yazma, veritabanı ekleme veya başka bir downstream eylem koyabilirsiniz.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Beklenen Konsol Çıktısı

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Programı örnek dosyalarla çalıştırdığınızda, her sayfa için bir metin bloğu görmeli ve **taralı pdf'den metin çıkarma** işlemini tek geçişte başarıyla tamamladığınızı doğrulamalısınız.

## Yaygın Sorunlarla Baş Etme

| Sorun | Neden Oluşur | Hızlı Çözüm |
|-------|--------------|------------|
| **Bellek yetersizliği hataları** | Büyük PDF'ler yüksek çözünürlüklü çok sayıda görüntü üretir. | PDF yüklerken DPI'yi sınırlayın: `ocrEngine.Settings.ImageDpi = 200;` |
| **Garip karakterler** | Kaynak tarama düşük kaliteli veya desteklenmeyen bir dilde. | Dili açıkça ayarlayın: `ocrEngine.Language = Language.English;` |
| **Kısmi sonuçlar** | Toplu listede bozuk bir dosya var. | `RecognizeBatch`'i try/catch içinde sarın ve sorunlu dosya için `e.Message`'ı kaydedin. |
| **Performans darboğazı** | Çok çekirdekli bir makinede tek iş parçacığıyla çalışıyor. | Her iş parçacığı için ayrı `OcrEngine` örnekleriyle `Parallel.ForEach` kullanın (ileri seviye). |

## Bonus: OCR Sonuçlarını Metin Dosyalarına Kaydetme

Her sayfa için ayrı bir `.txt` dosyası tutmak isterseniz, döngü içine küçük bir yazma bloğu ekleyin:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Artık **pdf'yi metne dönüştürme** işlemini düzenli bir düz‑metin dosyaları klasörüne dönüştürdünüz—sonraki indeksleme veya arama işlemleri için mükemmel.

## Tam Çalışan Örnek

Aşağıda kopyala‑yapıştır yapmaya hazır tam program yer alıyor. Gizli bağımlılık yok, harici betik yok.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Projeyi klasörden `dotnet run` komutuyla çalıştırın ve konsolda çıkarılan metinle dolduğunu izleyin. İşte **toplu OCR** işlemini sadece birkaç C# satırıyla nasıl yapacağınız.

## Özet – Hızlı Tekrar

- .NET konsol uygulaması kuruldu ve Aspose.OCR yüklendi.  
- İşlem verimliliği için tek bir `OcrEngine` örneği oluşturuldu.  
- PDF'leri sayfalara otomatik bölerek `ImageStream` nesneleri listelendi.  
- `RecognizeBatch` ile **pdf'den metin çıkarma** ve diğer görüntü formatlarından tek seferde metin alındı.  
- Sonuçlar yazdırıldı ve isteğe bağlı olarak ayrı `.txt` dosyalarına kaydedildi; böylece **pdf'yi metne dönüştürme** iş akışı tamamlandı.  

## Sonraki Adımlar ve İlgili Konular

- **Ölçeklendirme**: Yüzlerce dosyayı aynı anda işlemek için `Parallel.ForEach` ve bir `OcrEngine` havuzu kullanın.  
- **Dil paketleri**: `Language.English` yerine `Language.French` kullanın veya **görüntülerden metin tanıma** için özel bir sözlük yükleyin.  
- **Son‑işleme**: OCR çıktısını bir yazım denetleyiciden veya doğal dil ayrıştırıcıdan geçirerek taranmış sözleşmelerin doğruluğunu artırın.  
- **Alternatif kütüphaneler**: Açık kaynak bir seçenek arıyorsanız Aspose OCR'ı Tesseract.NET ile karşılaştırın—her ikisi de **taralı pdf'den metin çıkarma** yapabilir, ancak lisanslama ve kutudan çıkan doğruluk açısından farklılık gösterir.

---

![how to batch OCR example](alt="toplu OCR örneği")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}