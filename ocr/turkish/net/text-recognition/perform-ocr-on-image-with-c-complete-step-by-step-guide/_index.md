---
category: general
date: 2026-05-21
description: C# kullanarak görüntüde OCR gerçekleştirin. OCR için görüntünün nasıl
  yükleneceğini, PNG’den metin nasıl çıkarılacağını ve küçük bir kod örneğiyle görüntüden
  metnin nasıl tanınacağını öğrenin.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: tr
og_description: C#'ta görüntü üzerinde OCR'ı hızlıca gerçekleştirin. Bu kılavuz, OCR
  için görüntünün nasıl yükleneceğini, PNG'den metnin nasıl çıkarılacağını ve düzen‑bilinçli
  HTML çıktısı ile görüntüden metnin nasıl tanınacağını gösterir.
og_title: C# ile Görüntüde OCR Yapma – Tam Programlama Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: C# ile Görüntüde OCR Yapın – Tam Adım Adım Rehber
url: /tr/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Görüntüde OCR Yapma – Tam Adım‑Adım Kılavuz

Ağır GUI'lerle uğraşmadan **görüntüde OCR gerçekleştirmek** dosyalarını nasıl işleyebileceğinizi hiç merak ettiniz mi? Tek başınıza değilsiniz. Makbuzları dijitalleştiriyor, taranmış formlardan veri çekiyor ya da sadece bir PNG'yi aranabilir metne dönüştürmeniz gerektiğinde, birkaç satır C# işi halledebilir.

Bu öğreticide OCR için bir görüntüyü yüklemeyi, görüntüden metin tanımayı ve sonunda PNG'den temiz HTML olarak metin çıkarmayı adım adım göstereceğiz. Sonunda, **görüntüde OCR gerçekleştiren** dosyaları ve orijinal düzeni koruyan, çalıştırmaya hazır bir konsol uygulamanız olacak.

## Oluşturacağınız Şey

- PNG (veya desteklenen herhangi bir görüntü) okuyan minimal bir konsol programı  
- Bir OCR motoru kullanarak **görüntüden metni tanıma**  
- Sonucu düzen‑duyarlı HTML olarak kaydeder, orijinal resmi gömerek  
- Nasıl **OCR için görüntü yüklenir**, **PNG'den metin çıkarılır** ve yaygın kenar durumları ele alınır gösterir  

> **Önkoşullar**  
> - .NET 6.0 SDK veya daha yeni bir sürüm (aynı zamanda .NET Framework 4.7+ hedefleyebilirsiniz)  
> - NuGet‑uyumlu bir OCR kütüphanesi – örnek *Aspose.OCR* kullanıyor ancak benzer API'ye sahip herhangi bir kütüphane çalışır  
> - Temel C# bilgisi (fazla bir şey yok)  

Bunlar hazır mı? Harika—hadi başlayalım.

## Görüntüde OCR Yapma – Tam Kod İncelemesi

Aşağıda **tam, çalıştırılabilir** program bulunuyor. Yeni bir konsol projesine (`dotnet new console`) kopyalayıp yapıştırın ve **F5** tuşuna basın.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Beklenen çıktı**  
> ```
> HTML with layout saved.
> ```  
> Çalıştırdıktan sonra PNG'nizin yanında `form.html` dosyasını bulacaksınız. Bir tarayıcıda açtığınızda aynı düzeni göreceksiniz, ancak metin artık seçilebilir ve aranabilir olacak.

### OCR için Görüntü Yükleme

`engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` satırı, **OCR için görüntü yükleme** işlemini yaptığımız yerdir. `ImageStream` yardımcı sınıfı dosya formatı detaylarını soyutlar, böylece kodu değiştirmeden JPEG, BMP veya TIFF besleyebilirsiniz.  

**Neden sadece bir `Bitmap` geçmiyoruz?**  
Çünkü birçok OCR SDK'sı DPI meta verilerini de taşıyan bir akış bekler. Kütüphanenin yerleşik yükleyicisini kullanmak, motorun görüntüyü ekranda göründüğü gibi görmesini sağlar ve bu da doğruluğu artırır.

#### Pro ipucu
Eğer bir dosya topluluğunu işliyorsanız, yükleme adımını bir `try/catch` bloğuna sarın ve olası `FileNotFoundException`'ları kaydedin. Bu, tek bir eksik dosya nedeniyle tüm topluluğun çökmesini önler.

### PNG'den Metin Çıkarma

`engine.Recognize()` tamamlandığında, OCR motoru tanınan metni dahili olarak tutar. Yalnızca ham metne ihtiyacınız varsa, bunu bir string olarak alabilirsiniz:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

Bu, **PNG'den metin çıkarma** işlemini, düzenle ilgilenmediğinizde en hızlı yoldur. Çoğu veri girişi işinde, düz metin yeterlidir—CSV'ye aktarmayı planlıyorsanız satır sonlarını kırpmayı unutmayın.

### Görüntüden Metin Tanıma

`Recognize()` çağrısı ağır işi yapar. Motorun içinde:

1. Görüntüyü normalleştirir (eğrileri düzeltir, gürültüyü kaldırır)  
2. Satır ve kelimelere ayırır  
3. Milyonlarca glif üzerinde eğitilmiş bir sinir‑ağ sınıflandırıcısı çalıştırır  

`Language = OcrLanguage.English` olarak ayarladığımız için motor, İngilizce‑özel sözlükleri uygular ve bu da yanlış pozitifleri büyük ölçüde azaltır. Çok dilli desteğe ihtiyacınız varsa, sadece bir dil dizisi geçirin:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Düzen‑Duyarlı HTML Çıktısını Ele Alma

Çoğu geliştirici düz metinde durur, ancak kullandığımız `HtmlSaveOptions` **görüntüde OCR gerçekleştirmeyi** sağlar ve görsel yapıyı bozulmadan tutar. İki bayrak önemlidir:

- `PreserveLayout = true` – sütunları, tabloları ve boşlukları korur.  
- `EmbedImages = true` – orijinal PNG'yi Base64‑kodlu bir `<img>` öğesi olarak ekler, böylece HTML tek başına bulunur.  

Daha hafif bir dosya isterseniz, `EmbedImages = false` olarak ayarlayın ve HTML, PNG'yi diskteki orijinal dosyaya referans verir.

#### Kenar Durumu: Büyük Dosyalar

5 MB'den büyük görüntüler için, gömme HTML boyutunu şişirebilir. Bu gibi durumlarda, dış görüntü referanslarına geçin ve PNG'yi önceden `ImageProcessor.Compress` ile sıkıştırmayı düşünün.

## Yaygın Tuzaklar ve Pro İpuçları

| Semptom | Muhtemel Neden | Çözüm |
|--------|--------------|-----|
| Bozuk karakterler | Yanlış dil ayarı veya eksik dil paketi | Uygun dil veri dosyalarını kurun ve `engine.Language`'ı doğru şekilde ayarlayın |
| Çıktıda metin yok | Görüntü çok karanlık veya düşük çözünürlükte | `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` ile ön işleme yapın |
| HTML'de düzen bozulmuş | `PreserveLayout` varsayılan `false` olarak bırakılmış | `HtmlSaveOptions` içinde `PreserveLayout = true` ayarlayın |
| Birçok sayfada yavaş işleme | Motor her dosyada yeniden başlatılıyor | Aynı `OcrEngine` örneğini yeniden kullanın ve her döngüde sadece `engine.Image`'ı değiştirin |

### Birden Çok Dosyaya Ölçeklendirme

Bir klasördeki **görüntüde OCR gerçekleştirme** dosyalarına ihtiyacınız varsa, temel mantığı basit bir döngüye sarın:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Döngü içinde **OCR için görüntü yükleme** yaptığımızı fark edin, ancak aynı `engine` ve `htmlOptions` nesnelerini tutuyoruz. Bu, bellek tüketimini azaltır ve toplu işleri hızlandırır.

## Ötesine Geçmek: PDF veya DOCX'e Dışa Aktarma

Aynı `engine` diğer formatlara da kaydedebilir:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Eğer sonraki sisteminiz aranabilir PDF'ler bekliyorsa, bu tek satırlık bir değişiklik—ayrı bir dönüşüm hattı yazmanıza gerek yok.

## Sonuç

Sizinle C# ile **görüntüde OCR gerçekleştirme** dosyalarını nasıl yapacağınızı, resmi yüklemekten **PNG'den metin çıkarma** ve sonunda **görüntüden metin tanıma** yoluyla düzen‑duyarlı bir HTML dosyasına dönüştürmeyi gösterdik. Tam örnek çalıştırmaya hazır ve artık her adımın neden önemli olduğunu, farklı diller için nasıl ayarlama yapacağınızı ve hangi tuzaklara dikkat etmeniz gerektiğini anladınız.

Şimdi, İngilizce dilini başka bir yerel ayarla değiştirin, daha hafif bir HTML elde etmek için `PreserveLayout = false` ile deney yapın veya düz metin çıktısını aranabilir arşivler için bir veritabanına yönlendirin. Güçlü bir OCR motorunu birkaç satır C# ile birleştirdiğinizde sınır yoktur.

Çok sayfalı TIFF'leri nasıl ele alacağınız hakkında sorularınız mı var, ya da bunu bir ASP.NET Core API'ye nasıl entegre edeceğinizi öğrenmek mi istiyorsunuz? Aşağıya bir yorum bırakın, iyi kodlamalar!

## İlgili Öğreticiler

- [Aspose.OCR kullanarak dil seçimiyle görüntü metni çıkarma C#](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [OCR'da Dikdörtgen Hazırlayarak Görüntüden Metin Çıkarma](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Görüntüden Metin Çıkarma – Aspose.OCR ile Satır Tanıma](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}