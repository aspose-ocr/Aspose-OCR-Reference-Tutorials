---
category: general
date: 2026-01-15
description: OCR için görüntüyü ön işleme alarak taramayı hızlıca metne dönüştürün.
  Tarama üzerindeki gürültüyü nasıl kaldıracağınızı ve Aspose OCR filtrelerini kullanarak
  OCR doğruluğunu nasıl artıracağınızı öğrenin.
draft: false
keywords:
- preprocess image for ocr
- convert scan to text
- extract text from scan
- remove noise from scan
- improve ocr accuracy
language: tr
og_description: OCR için görüntüyü ön işleme alarak taramayı hızlıca metne dönüştürün.
  Tarama üzerindeki gürültüyü nasıl kaldıracağınızı ve basit C# kodu ile OCR doğruluğunu
  nasıl artıracağınızı keşfedin.
og_title: OCR için Görüntüyü Ön İşleme – Aspose OCR ile Doğruluğu Artırın
tags:
- Aspose OCR
- C#
- Image Preprocessing
title: OCR için Görüntüyü Ön İşleme – Aspose OCR ile Doğruluğu Artırın
url: /tr/net/ocr-optimization/preprocess-image-for-ocr-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntü Ön İşleme – Tam Bir C# Öğreticisi

Hiç **preprocess image for OCR** yapmanız gerektiğinde, hangi filtrelerin gerçekten fark yarattığından emin olmadınız mı? Yalnız değilsiniz—taranmış sayfalar genellikle eğik, lekeli ya da sadece gürültülü olur ve bu da herhangi bir OCR motorunu bozar.  

İyi haber şu ki, birkaç iyi seçilmiş adım **convert scan to text** işlemini güvenilir bir şekilde yapabilir ve tanıma kalitesinde belirgin bir artış göreceksiniz. Bu rehberde eğik bir TIFF dosyasını yüklemeyi, görsel karmaşayı temizlemeyi ve sonunda temiz metni çıkarmayı adım adım göstereceğiz—böylece **remove noise from scan** dosyalarından **improve OCR accuracy** elde edebilirsiniz, sonsuz belgeler arasında dolaşmadan.

## Bu Öğreticide Neler Kapsanıyor

- C#'ta bir Aspose OCR motoru kurma  
- Gerçek dünya taranmış bir görüntüyü yükleme (eğik bir fatura ya da soluk bir form düşünün)  
- **preprocess image for OCR** için Deskew, Denoise ve Binarization filtrelerini uygulama  
- OCR motorunu çalıştırarak **extract text from scan** elde etme ve konsola çıktı verme  
- Çok sayfalı PDF'ler veya düşük kontrastlı belgeler gibi kenar durumlarını ele alma ipuçları  

Sonunda, herhangi bir .NET projesine ekleyebileceğiniz ve anında **convert scan to text** başlatabileceğiniz bağımsız bir programınız olacak.

### Önkoşullar

- .NET 6.0 veya daha yeni bir sürüm (kod .NET Core ve .NET Framework'te de çalışır)  
- Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`)  
- `skewed_scan.tif` adlı örnek bir TIFF, kontrol ettiğiniz bir klasöre yerleştirilmiş  
- Temel C# bilgisi—ileri düzey hileler gerekmez  

Eğer bunlara sahipseniz, başlayalım.

## OCR için Görüntü Ön İşleme – Adım Adım

Aşağıda süreci beş mantıksal adıma bölüyoruz. Her bölüm net bir başlığa, adımın **neden** önemli olduğuna dair kısa bir açıklamaya ve kopyalayıp‑yapıştırabileceğiniz tam bir kod parçacığına sahiptir.

### Adım 1: OCR Motorunu Başlatma

Motor, işlemin kalbidir; onsuz hiçbir şey tanınmaz. Motoru bir kez oluşturup birden fazla görüntüde yeniden kullanmak da daha verimlidir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Create a single OCR engine instance – this is cheap and reusable
        var ocrEngine = new OcrEngine();
```

*Neden bu önemli:* Aspose OCR, `OcrEngine` örneği oluşturulduğunda yüklenecek dil paketleri ve uyarlamalı algoritmalarla birlikte gelir. Erken başlatmak, daha sonra gizli gecikmeleri önler.

### Adım 2: Tarama Belgesini Yükleme ve İnceleme

Motoru gerçek görüntü dosyasına yönlendirmeniz gerekir. `OcrImage.FromFile` kullanmak, filtrelerle zincirlenebilen bir nesne sağlar.

```csharp
        // Load the skewed, noisy scan – adjust the path to match your environment
        var originalImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_scan.tif");
```

*Neden bu önemli:* Ham bir taramayı doğrudan OCR'ye vermek genellikle çöp sonuç verir çünkü motor nispeten temiz bir girdi bekler. Bu, tanımadan önce **remove noise from scan** için mükemmel bir noktadır.

### Adım 3: Deskew, Denoise ve Binarization Filtrelerini Uygulama

İşte gerçek sihrin gerçekleştiği yer. Üç filtreyi zincirliyoruz:

1. **DeskewFilter** – döndürülmüş sayfaları düzleştirir.  
2. **DenoiseFilter** – lekeleri ve grenleri yumuşatır.  
3. **BinarizationFilter** – çoğu OCR motorunun sevdiği siyah‑beyaz bir palet zorlar.  

```csharp
        // Chain the preprocessing filters
        var preprocessedImage = originalImage
            .Apply(new DeskewFilter())          // corrects rotation
            .Apply(new DenoiseFilter())         // reduces visual noise
            .Apply(new BinarizationFilter());   // converts to B/W
```

*Neden bu önemli:* Eğik bir metin satırı ayrı karakterler olarak yorumlanır ve rastgele noktalar noktalama işareti sanılabilir. Bu üç adımla **preprocess image for OCR** yaparak **improve OCR accuracy** büyük ölçüde artırırsınız.

> **Pro ipucu:** Taramalarınız zaten çoğunlukla düzse, birkaç milisaniye tasarruf etmek için `DeskewFilter`'i atlayabilirsiniz.

### Adım 4: Metni Tanıma ve Tarama Metnine Dönüştürme

Şimdi temizlenmiş görüntüyü OCR motoruna veriyoruz. İngilizce isteyeceğiz, ancak desteklenen herhangi bir dil aynı şekilde çalışır.

```csharp
        // Perform OCR on the processed image using English language
        var ocrResult = ocrEngine.Recognize(preprocessedImage, Language.English);
```

*Neden bu önemli:* Motor artık yüksek kontrastlı, gürültüsüz bir bitmap ile çalışıyor, bu yüzden güven skorları çok daha yüksek. Bu, gerçekten **extract text from scan** yaptığınız noktadır.

### Adım 5: Tanınan Metni Çıktılamak ve Sonuçları Doğrulamak

Hızlı bir `Console.WriteLine` ham dizeyi gösterir. Gerçek bir uygulamada bir dosyaya, veritabanına yazabilir veya bir sonraki NLP hattına besleyebilirsiniz.

```csharp
        // Output the recognized text to the console
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

**Beklenen çıktı** (basit bir fatura örneği):

```
Invoice #12345
Date: 01/12/2024
Total Amount: $1,234.56
Thank you for your business!
```

Metin bozuk görünüyorsa, orijinal taramanın çözünürlüğünü (300 dpi iyi bir temel) tekrar kontrol edin ve `DenoiseFilter` gücünü ayarlamayı düşünün.

![OCR için görüntü ön işleme örneği](https://example.com/images/preprocess-ocr.png "OCR için görüntü ön işleme örneği")

*Yukarıdaki resim, üç filtre uygulandıktan sonra taranmış bir sayfanın ön‑ve‑son halini gösterir.*

## Tarama Dosyalarından Gürültüyü Kaldırmak İçin Ek İpuçları

- **Increase DPI before scanning** – 300 dpi veya daha yüksek, filtrelerin daha fazla veri ile çalışmasını sağlar.  
- **Crop margins** – gereksiz beyaz boşluk binarizasyon adımını karıştırabilir.  
- **Use `ContrastFilter`** – belge soluksa; `BinarizationFilter`'den önce eklenebilir.  
- **Batch processing** – yukarıdaki kodu bir `foreach` döngüsü içinde sararak dosyaları otomatik olarak toplu işleyebilirsiniz.

## Yaygın Sorular ve Kenar Durumları

**Belgem birden fazla sayfa içeriyorsa ne olur?**  
Yükleme adımını, her sayfayı ayrı bir `OcrImage` olarak okuyan bir döngü içinde sarın. Aspose OCR doğrudan PDF akışlarını da kabul edebilir.

**İngilizce dışındaki dilleri tanıyabilir miyim?**  
Evet—`Language.English` yerine `Language.French`, `Language.Spanish` vb. değiştirin, dil paketi yüklü olduğu sürece.

**Güven skorlarını almanın bir yolu var mı?**  
`ocrResult` her karakter için bir `Confidence` özelliği içerir. Düşük güvenilirlikli bölgeleri manuel inceleme için kaydetmek üzere `ocrResult.Regions` üzerinde döngü yapabilirsiniz.

**Tarama renkli ise ne olur?**  
Filtreler renkli görüntülerde de çalışır; içsel olarak binarizasyon öncesi gri tonlamaya dönüştürürler. Ancak, kendiniz gri tonlamaya dönüştürmek (`new GrayscaleFilter()`) bazen hız kazandırabilir.

## Sonuç

Artık Aspose OCR ile **preprocess image for OCR**, **remove noise from scan** ve **convert scan to text** yapan eksiksiz, çalıştırmaya hazır bir örneğiniz var. Deskew, Denoise ve Binarization filtrelerini zincirleyerek sürekli **improve OCR accuracy** elde edeceksiniz, bu da sonraki veri çıkarımını çok daha güvenilir kılar.

Bir sonraki adıma hazır mısınız? Çıktıyı bir CSV yazıcıya beslemeyi, bir arama indeksine itmeyi ya da `ContrastFilter` veya `SharpenFilter` gibi diğer Aspose filtreleriyle denemeler yapmayı deneyin. Güçlü bir OCR motoru ile sağlam ön işleme birleştirildiğinde sınır yoktur.

Kodlamaktan keyif alın, ve taramalarınız her zaman net olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}