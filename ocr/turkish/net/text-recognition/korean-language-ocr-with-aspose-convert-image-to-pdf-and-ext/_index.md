---
category: general
date: 2026-05-28
description: C#'ta Aspose kullanarak Korece Dil OCR öğreticisi. Görüntüyü akıştan
  nasıl yükleyeceğinizi, düz metni nasıl çıkaracağınızı, görüntüyü PDF'ye nasıl dönüştüreceğinizi
  ve aranabilir PDF olarak nasıl dışa aktaracağınızı öğrenin.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: tr
og_description: Aspose kullanarak C#'de Korece Dil OCR'ı. Akıştan görüntü yükleme,
  düz metin çıkarma, görüntüyü PDF'ye dönüştürme ve aranabilir PDF dışa aktarma adım
  adım rehberi.
og_title: Kore Dili OCR – Görüntüyü PDF'ye Dönüştür ve Metni Çıkar (C# Rehberi)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'Aspose ile Korece Dil OCR: Görüntüyü PDF''ye Dönüştür ve C#''ta Metni Çıkar'
url: /tr/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose ile Korece Dil OCR'ı: Görüntüyü PDF'ye Dönüştürme ve C#'ta Metin Çıkarma

Hiç **Korece Dil OCR**'ını bir resimde, hiçbir şeyi buluta göndermeden çalıştırmayı düşündünüz mü? Tek başınıza değilsiniz. Sokak işaretlerini dijitalleştiriyor, fişleri işliyor ya da çok dilli bir arama indeksi oluşturuyorsanız, Korece karakterleri yerel olarak tanıyabilmek zaman, para ve gizlilik sorunlarından tasarruf sağlar.

Bu öğreticide, **akıştan görüntü yükleme**, **düz metin çıkarma**, **görüntüyü PDF'ye dönüştürme** ve son olarak **arama yapılabilir PDF dışa aktarma** işlemlerini gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz—hepsi Aspose.OCR ve birkaç satır C# ile. Harici hizmetler, gizli sihir yok—herhangi bir konsol uygulamasına ekleyebileceğiniz saf .NET kodu.

## Neler Öğreneceksiniz

- Bir JPEG dosyasını dosya akışı üzerinden okuyan çalışan bir konsol programı.  
- Korece metnin düz Unicode dizgileri olarak çıkarılması.  
- Hata ayıklama veya analiz için OCR çalışmasının ayrıntılı JSON raporu.  
- Herhangi bir PDF okuyucusunda açabileceğiniz ve Korece kelimeleri gerçekten seçebileceğiniz bir arama yapılabilir PDF.  

**Önkoşullar**  
- .NET 6.0 veya üzeri (kod .NET Framework 4.7+ üzerinde de çalışır).  
- Aspose.OCR for .NET NuGet paketi yüklü (`Install-Package Aspose.OCR`).  
- `korean_sign.jpg` dosyasını içeren bir klasör ve çıktı dosyaları için yazılabilir bir konum.  

Bu bileşenler zaten hazırsa, harika—hadi işe koyulalım.

## Adım 1: Korece Dil OCR'ı için OCR Motorunu Başlatma

İhtiyacınız olan ilk şey bir `OcrEngine` örneği. GPU'yu etkinleştirmek (varsa) tanıma süresini büyük ölçüde hızlandırır ve otomatik kaynak indirmeyi kapatmak, kütüphanenin sağladığınız çevrim dışı dil paketlerini kullanmasını sağlar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Neden önemli:**  
> *GPU hızlandırması*, büyük toplularda işleme süresini saniyelerden milisaniyelere indirebilir. `AutomaticResourceDownload` değerini `false` yapmak, demoyu çevrim dışı çalıştırır—bu, birçok kurumsal ortam için kritik bir gereksinimdir.

## Adım 2: Akıştan Görüntü Yükleme

Görüntüyü bir akış üzerinden okumak esneklik sağlar: dosyaları diskten, ağ paylaşımlarından ya da hatta bellek‑önbellekli blob'lardan alabilirsiniz. Burada yerel bir JPEG dosyası açıyoruz, ancak aynı desen herhangi bir `Stream` için geçerlidir.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Pro ipucu:** Web API üzerinden yüklenen görüntüleri işlemek isterseniz, sadece `File.OpenRead` yerine gelen `IFormFile.OpenReadStream()` ile değiştirin—geri kalan aynı kalır.

## Adım 3: Korece Dilini Seçme ve Ön‑İşleme Filtrelerini Uygulama

Aspose.OCR, tanımadan önce görüntüyü temizleyen birkaç ön‑işleme adımını destekler. Korece işaretler için genellikle deskew (eğikliği düzeltme) ve denoise (gürültü azaltma) yeterlidir.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Arka planda ne oluyor?**  
> `Deskew` filtresi döndürülmüş metni düzeltirken, `Denoise` karakter sınıflandırıcısını şaşırtabilecek taneleri temizler. Bu adımlar atlandığında, özellikle düşük çözünürlüklü fotoğraflarda bozuk çıktı alınması sık görülür.

## Adım 4: Düz Metni Asenkron Olarak Çıkarma

Şimdi gerçek an—motoru karakterleri tanıması ve bize temiz bir dize vermesi için çağırma zamanı. `RecognizeAsync` kullanmak, bu kodu bir masaüstü ya da web uygulamasına entegre ettiğinizde UI'nın yanıt vermesini sağlar.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
OCR complete. Extracted text:
서울시청
```

> **Neden async?**  
> OCR CPU‑yoğun olabilir. Asenkron yürütme, iş parçacığının bloke olmasını önler; bu özellikle ASP.NET Core’da iş parçacığı açlığının gerçek bir sorun olduğu durumlarda çok yararlıdır.

## Adım 5: Ayrıntılı Tanıma Sonucunu Alın ve JSON Olarak Kaydedin

Bazen sadece ham dize yeterli olmaz—belki güven skorları, sınırlayıcı kutular ya da orijinal görüntü verisi gerekir. `RecognizeDetailed` metodu, daha sonra analiz için JSON’a serileştirilebilen bir `RecognitionResult` nesnesi döndürür.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

`korean_ocr.json` dosyasını açtığınızda aşağıdaki gibi bir yapı göreceksiniz:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Ne zaman kullanılır?**  
> Bir arama indeksi oluşturuyorsanız, güven değerleri düşük‑kaliteli sonuçları filtrelemenize yardımcı olur. UI’da metni vurgulamanız gerekiyorsa, sınırlayıcı kutular haritanız olur.

## Adım 6: Görüntüyü PDF'ye Dönüştürme ve Arama Yapılabilir PDF Dışa Aktarma

Aspose, raster’dan vektöre geçişi zahmetsiz kılar. `OutputFormat` değerini `SearchablePdf` olarak ayarladığınızda, kütüphane orijinal görüntüyü gömüp OCR çıktısını içeren görünmez bir metin katmanı ekler. Ortaya çıkan PDF, yerel bir PDF gibi aranabilir, kopyalanabilir ve indekslenebilir.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

`korean_searchable.pdf` dosyasını Adobe Reader ya da herhangi bir PDF görüntüleyicide açın, **Ctrl+F** tuşlarına basın, bir Korece kelime yazın ve sayfadaki tam konuma atlayışını izleyin. İşte arama yapılabilir PDF’in gücü.

> **Ek ipucu:** Görünür bir PDF yeterli ise ve gizli metin katmanı istemiyorsanız, `OutputFormat` değerini `Pdf` olarak değiştirin.

## Tam Çalışan Örnek

Aşağıda tam program yer alıyor—kopyalayıp yapıştırın, `YOUR_DIRECTORY` kısmını gerçek bir yol ile değiştirin ve **F5** tuşuna basın.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Beklenen Konsol Çıktısı

```
OCR complete. Extracted text:
서울시청
```

Ve kaynak görüntünüzün yanına üç yeni dosya oluşacak:

- `korean_ocr.json` – tam tanıma verileri.  
- `korean_searchable.pdf` – arama yapabileceğiniz bir PDF.  
- (isteğe bağlı) eklemek istediğiniz ara günlük dosyaları.

## Yaygın Sorular & Kenar Durumları

**GPU'm yoksa ne yapmalıyım?**  
`EnableGpu = false` olarak ayarlayın; CPU geri dönüşü küçük toplular için gayet yeterlidir.

**Bir çalıştırmada birden fazla görüntüyü işleyebilir miyim?**  
Kesinlikle. Çekirdek mantığı `foreach (var file in Directory.GetFiles(...))` döngüsü içine alın ve her yinelemede `ocrEngine.Image` değerini yeniden atayın.

**Korece ile birlikte başka dilleri nasıl işleyebilirim?**  
Aspose.OCR, `Language = Language.AutoDetect` ayarına izin verir ya da bitwise OR operatörü ile dilleri birleştirmenizi sağlar (ör. `Language.Korean | Language.English`).

**OCR güveni düşük olduğunda ne yapmalıyım?**  
`detailedResult.Pages[0].Words` koleksiyonunu inceleyin ve `Confidence < 0.7` olan girdileri filtreleyin. Ayrıca ön‑işleme filtrelerini ayarlayabilirsiniz—`PreprocessFilter.ContrastEnhancement` eklemeyi deneyin.

## Sonuç

**Korece Dil OCR**'ını uçtan uca nasıl gerçekleştireceğinizi gördünüz; **akıştan görüntü yükleme**, **düz metin çıkarma**, **görüntüyü PDF'ye dönüştürme** ve sonunda **arama yapılabilir PDF dışa aktarma** adımlarını tamamladınız. Yaklaşım modüler olduğundan, görüntü kaynağını değiştirebilir, çıktı formatını değiştirebilir ya da JSON çıktısını herhangi bir sonraki işlem hattına bağlayabilirsiniz.

What’s next


## İlgili Öğreticiler

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}