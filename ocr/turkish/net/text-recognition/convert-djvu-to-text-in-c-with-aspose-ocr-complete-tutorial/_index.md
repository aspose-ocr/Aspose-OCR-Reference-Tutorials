---
category: general
date: 2026-02-28
description: Aspose OCR C# kullanarak Djvu'yu hızlıca metne dönüştürün. Görüntüden
  metin tanımayı ve Djvu dosyalarından metin çıkarmayı birkaç kolay adımda öğrenin.
draft: false
keywords:
- convert djvu to text
- recognize text from image
- extract text from djvu
- aspose ocr c# tutorial
language: tr
og_description: Aspose OCR C# ile Djvu'yu metne dönüştürün. Görüntüden metin tanıma
  ve Djvu dosyalarından metin çıkarma için bu adım adım kılavuzu izleyin.
og_title: Djvu'yu C#'ta Metne Dönüştür – Tam Aspose OCR Rehberi
tags:
- Aspose OCR
- C#
- DjVu
- Text Extraction
title: Aspose OCR ile C#'ta Djvu'yu Metne Dönüştürme – Tam Kılavuz
url: /tr/net/text-recognition/convert-djvu-to-text-in-c-with-aspose-ocr-complete-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose OCR Kullanarak Djvu'yu Metne Dönüştürme – Tam Kılavuz

Hiç **Djvu'yu metne dönüştürmek** gerektiğinde, hangi kütüphanenin bunu yapabileceğinden emin olmadınız mı? Yalnız değilsiniz. Birçok geliştirici, taranmış DjVu belgelerinden aranabilir metinler çıkarmaya çalışırken bu engelle karşılaşıyor. İyi haber? Aspose OCR tüm süreci çocuk oyuncağı haline getiriyor ve **görüntüden metin tanıma** dosyalarını—DjVu dahil—düşük seviyeli piksel manipülasyonuyle uğraşmadan yapmanızı sağlıyor.

Bu kılavuzda, C# kullanarak **Djvu'dan metin çıkarma** işlemini tam olarak nasıl yapacağınızı gösteren gerçek bir örnek üzerinden ilerleyeceğiz. Sonunda çalıştırılabilir bir program, her satırın neden önemli olduğuna dair net bir anlayış ve yaygın tuzaklardan kaçınmanıza yardımcı olacak birkaç ipucu elde edeceksiniz. Harici referanslara gerek yok—sadece saf, kopyala‑yapıştır‑hazır kod.

## Gerekenler

* .NET 6.0 SDK veya daha yenisi (API .NET Core ve .NET Framework ile de çalışır)
* Aktif bir Aspose.OCR for .NET lisansı (ücretsiz deneme sürümü test için çalışır)
* İşlemek istediğiniz bir DjVu dosyası (referans alabileceğiniz bir klasöre koyun)
* Visual Studio 2022 veya tercih ettiğiniz herhangi bir C# editörü

Hepsi bu—hiçbir şey egzotik değil. Bu temellere sahipseniz, Djvu'yu metne dönüştürmeye hazırsınız.

![Djvu'yu metne dönüştürme örneği](image-placeholder.png "Aspose OCR'un bir DjVu dosyasından metin çıkardığını gösteren ekran görüntüsü")

## Adım 1: Aspose.OCR NuGet Paketini Yükleyin

İlk olarak, Aspose OCR kütüphanesini projenize ekleyin. Çözüm klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

> **Pro ipucu:** NuGet CLI kullanmak, yazım anında en yeni kararlı sürümü (`23.10`) almanızı sağlar. Paketi güncel tutmak, zaten düzeltilmiş hatalarla karşılaşma olasılığını azaltır.

## Adım 2: OCR Motorunu Başlatın

`OcrEngine` örneği oluşturmak, herhangi bir **görüntüden metin tanıma** işleminin giriş noktasıdır. Motoru, piksel verilerini yorumlayan ve karakterlere dönüştüren bir beyin olarak düşünün.

```csharp
using Aspose.OCR;
using System.Drawing;

class DjvuDemo
{
    static void Main()
    {
        // Step 2: Create an OCR engine instance – this object holds all the settings.
        OcrEngine ocrEngine = new OcrEngine();
```

Motoru bir kez örneklememizin nedeni nedir? Aynı `OcrEngine` nesnesini birden çok dosya arasında yeniden kullanmak, dil verilerini tekrar tekrar yükleme yükünü ortadan kaldırır ve toplu DjVu dosyaları işlediğinizde performansı artırır.

## Adım 3: DjVu Görüntüsünü Yükleyin

Aspose OCR, DjVu dosyalarını görüntü olarak ele alır; bu yüzden `Image.Load` ile doğrudan yükleyebilirsiniz. `using` ifadesi, görüntünün düzgün bir şekilde serbest bırakılmasını garanti eder ve bellek sızıntılarını önler.

```csharp
        // Step 3: Load the DjVu image you want to process.
        // Replace the path with the actual location of your .djvu file.
        using var djvuImage = Image.Load(@"C:\Docs\input.djvu");
```

> **Köşe durumu:** Bazı DjVu dosyaları birden çok sayfa içerir. `Image.Load` varsayılan olarak ilk sayfayı yükler. Her sayfayı işlemek istiyorsanız `Image.LoadMultiple` kullanın ve oluşan koleksiyonu döngüyle işleyin.

## Adım 4: OCR Tanımasını Gerçekleştirin

İşte sihir burada. `Recognize` metodu bitmap'i tarar ve çıkarılan metin, güven puanları ve daha fazlasını içeren bir `OcrResult` nesnesi döndürür.

```csharp
        // Step 4: Perform OCR recognition on the loaded image.
        var ocrResult = ocrEngine.Recognize(djvuImage);
```

Şöyle düşünebilirsiniz: *Djvu düşük çözünürlüklü bir tarama içeriyorsa ne olur?* `Recognize` çağrısından önce motorun `Resolution` özelliğini ayarlamak doğruluğu artırabilir:

```csharp
        // Optional: improve accuracy for low‑dpi images.
        ocrEngine.RecognitionSettings.Resolution = 300; // DPI
```

## Adım 5: Tanınan Metni Çıktılayın

Son olarak, çıkarılan dizeyi konsola—ya da isterseniz bir dosyaya—yazın. İşte **Djvu'yu metne dönüştürme** işleminin gerçek anlamda gerçekleştiği an.

```csharp
        // Step 5: Output the recognized text to the console.
        System.Console.WriteLine("=== Extracted Text ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Programı (`dotnet run`) çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Çıktı bozuk görünüyorsa, kaynak DjVu kalitesini, dil ayarlarını ve `ocrEngine.Language = OcrLanguage.English;` gibi belirli bir dil paketinin etkinleştirilip etkinleştirilmediğini iki kez kontrol edin.

## Aspose OCR Kullanarak Görüntüden Metin Tanıma – Gelişmiş Ayarlar

Temel akış çoğu durumda işe yarasa da, Aspose OCR **görüntüden metin tanıma** adımını ince ayar yapmanızı sağlayan bir dizi seçenek sunar:

| Ayar | Ne İşe Yarar | Ne Zaman Kullanılır |
|------|--------------|---------------------|
| `ocrEngine.RecognitionSettings.DetectOrientation` | Eğimli sayfaları otomatik döndürür | Tam olarak hizalanmamış taranmış belgeler |
| `ocrEngine.RecognitionSettings.Language` | Belirli bir dil modelini zorlar | Varsayılan İngilizce modelinin yetersiz kaldığı çok dilli PDF'ler |
| `ocrEngine.RecognitionSettings.UsePreProcessing` | OCR'dan önce filtreler uygular (gürültü azaltma, ikilileştirme) | Düşük kontrastlı veya gürültülü DjVu taramaları |
| `ocrEngine.RecognitionSettings.OutputFormat` | Düz metin, hOCR veya PDF döndürür | Ham metin yerine aranabilir PDF'lere ihtiyaç duyulduğunda |

Bu bayraklarla, temel işlevi çalıştırdıktan sonra deneme yapın. Küçük ayarlamalar, zor belgelerde doğruluğunuzu %85'ten %95'in üzerine çıkarabilir.

## Djvu Dosyalarından Metin Çıkarma – Çoklu Sayfaları İşleme

DjVu dosyanız birden fazla sayfa içeriyorsa, her birini döngüyle işleyip sonuçları birleştirmek isteyeceksiniz. İşte kompakt bir örnek:

```csharp
using Aspose.OCR;
using System.Drawing;

class DjvuMultiPageDemo
{
    static void Main()
    {
        OcrEngine engine = new OcrEngine();
        var images = Image.LoadMultiple(@"C:\Docs\book.djvu");

        foreach (var page in images)
        {
            var result = engine.Recognize(page);
            System.Console.WriteLine($"--- Page {page.PageNumber} ---");
            System.Console.WriteLine(result.Text);
        }
    }
}
```

`LoadMultiple` kullanımına dikkat edin; her `page` nesnesi kendi `PageNumber` değerini bilir, bu da çıktıyı etiketlemeyi kolaylaştırır. Bu desen, **Djvu'dan metin çıkarma** işlemini indeksleme veya tam metin arama için yaparken yaygındır.

## Aspose OCR C# Kılavuzu – Yaygın Tuzaklar ve Nasıl Kaçınılır

1. **Lisansın ayarlanmayı unutması** – Geçerli bir lisans olmadan kütüphane değerlendirme modunda çalışır ve çıktıya bir filigran ekler. `Main` metodunun başında `License license = new License(); license.SetLicense("Aspose.OCR.lic");` çağrısını yapın.
2. **Yanlış görüntü formatının kullanılması** – DjVu yerel bir bitmap değildir; bozuk bir akış gönderildiğinde `ArgumentException` fırlatır. Her zaman `Image.Load` veya `LoadMultiple` ile yükleyin.
3. **Serbest bırakmanın ihmal edilmesi** – Büyük DjVu dosyaları gigabaytlarca RAM tüketebilir. Önceden gösterilen `using` deseni, yerel kaynakların hızlıca serbest bırakılmasını sağlar.
4. **Dil ayarlarının uyumsuzluğu** – Belgeniz Fransızca ise, `engine.RecognitionSettings.Language = OcrLanguage.French;` ayarlayarak bozuk karakterlerin önüne geçin.

Bu sorunları erken aşamada ele almak, sayısız hata ayıklama saatinden tasarruf sağlar.

## Uygulamanızı Test Etme

Dönüşümün beklendiği gibi çalıştığını doğrulamak için:

1. Bilinen bir DjVu dosyasıyla programı çalıştırın (ör. kamu malı bir kitabın taranmış sayfası).
2. Konsol çıktısını, orijinal metinle bir diff aracı kullanarak karşılaştırın.
3. `Resolution` ve `UsePreProcessing` ayarlarını, fark tolerans sınırının altına düşene kadar ayarlayın.

Otomatik test ihtiyacınız varsa, OCR çağrısını bir string döndüren bir metoda sarın ve ardından beklenen alt dizelerle birim testleri yazın.

## Özet ve Sonraki Adımlar

Aspose OCR kullanarak C# içinde tam bir **Djvu'yu metne dönüştürme** iş akışını adım adım inceledik. Paketi yükleme, `OcrEngine` başlatma, DjVu'yu yükleme, içeriği tanıma ve sonucu çıktıya yazma adımları, doğrudan projenize kopyalayabileceğiniz kodlarla kapsandı.

Bundan sonra şunları yapabilirsiniz:

* **Toplu işleme**: Bir klasördeki tüm DjVu dosyalarını işleyip her bir sonucu bir `.txt` dosyasına yazın.
* **Aranabilir PDF'ler oluşturma**: OCR metnini Aspose.PDF'e geri besleyerek PDF'leri aranabilir hâle getirin.
* **Azure Functions ile bütünleştirme**: Bulutta isteğe bağlı OCR için Azure Functions kullanın.
* **Dil algılamayı keşfetme**: OCR dil paketlerini otomatik olarak değiştirmek için dil algılamayı araştırın.

**Görüntüden metin tanıma** ve **Djvu'dan metin çıkarma** temellerini kavradığınızda, olanaklar sınırsızdır.

---

*Kodlamaktan keyif alın! Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın—birlikte çözüm bulalım.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}