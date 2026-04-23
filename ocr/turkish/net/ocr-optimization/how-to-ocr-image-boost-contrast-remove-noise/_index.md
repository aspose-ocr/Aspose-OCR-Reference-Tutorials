---
category: general
date: 2026-02-22
description: Aspose OCR ile görüntüyü OCR'lamak nasıl yapılır – görüntü gürültüsünü
  kaldır, kontrastı artır ve C#'ta metin görüntüsünü hızlıca çıkar.
draft: false
keywords:
- how to ocr image
- remove image noise
- boost image contrast
- extract text image
- recognize image text
language: tr
og_description: Aspose OCR kullanarak görüntüyü OCR yapmayı, gürültüyü temizlemeyi,
  kontrastı artırmayı ve C#'ta tam, çalıştırmaya hazır bir örnekle metin görüntüsü
  çıkarmayı öğrenin.
og_title: Görüntüyü OCR nasıl yaparız – Kontrastı artır ve gürültüyü kaldır
tags:
- OCR
- C#
- Image Processing
title: 'görüntüyü OCR yapma: kontrastı artır, gürültüyü kaldır'
url: /tr/net/ocr-optimization/how-to-ocr-image-boost-contrast-remove-noise/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü OCR Yapma – Kontrastı Artırma ve Gürültüyü Kaldırma C#'ta

Hiç **görüntüyü OCR yapma** dosyalarının eğik, grenli ya da sadece okunması zor olduğunu merak ettiniz mi? Yalnız değilsiniz. Gerçek dünyadaki birçok projede—örneğin makbuz tarama veya eski belgeleri dijitalleştirme—ham resim nadiren mükemmeldir. İyi haber? Birkaç C# satırı ve Aspose OCR ile **görüntü gürültüsünü kaldırabilir**, **görüntü kontrastını artırabilir** ve sonunda **görüntü metnini çıkarabilirsiniz** zahmetsizce.

Bu öğreticide, baştan sona bir çözüm üzerinden adım adım ilerleyeceğiz. Sonuna geldiğinizde OCR motorunu nasıl kuracağınızı, gürültülü bir resmi nasıl temizleyeceğinizi ve **görüntü metnini tanıyacağınızı** tam olarak bilecek ve sonucu ihtiyacınız olan yere yönlendirebileceksiniz. Belirsiz referanslar yok, sadece çalıştırılabilir bir kod örneği ve her seçimin ardındaki mantık var.

## Gereksinimler

- .NET 6+ (veya .NET Core 3.1+ – API aynı)
- Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`)
- Eğik ve gürültülü bir örnek resim (ör. `skewed_noisy.jpg`)
- İstediğiniz herhangi bir IDE – Visual Studio, Rider veya VS Code yeterli

Hepsi bu. Bunlara sahipseniz doğrudan koda geçebiliriz.

![how to ocr image example](/images/ocr-demo.png){alt="görüntüyü ocr yapma örneği"}

## Adım 1: OCR Motorunu Başlatma – görüntüyü ocr doğru şekilde

İlk yapmanız gereken bir `OcrEngine` örneği oluşturup hangi dili bekleyeceğini belirtmektir. İngilizce en yaygın dildir, ancak Aspose kutudan çıkar çıkmaz onlarca dili destekler.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Create the OCR engine and set the language to English.
        var ocrEngine = new OcrEngine { Language = Language.English };
```

**Neden önemli:** Motorun karakter setini bilmesi gerekir; aksi takdirde tahmin etmeye çalışarak zaman harcar ve doğruluğunuz düşer. Dili önceden ayarlamak ayrıca bellek kullanımını azaltır çünkü motor yalnızca gerekli dil verilerini yükler.

## Adım 2: Resmi Yükleme ve Görüntü Gürültüsünü Kaldırmaya Başlama

Şimdi resmi diskinizden alıyoruz. Çoğu durumda dosya, çok fazla gren içeren bir JPEG veya PNG olur. Bunu bir `Image` nesnesine yüklemek, filtrelerden geçirebileceğimiz bir tutamaç sağlar.

```csharp
        // Load the input image (skewed and noisy)
        var inputImage = Image.Load(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

**İpucu:** Resminiz bir bulut deposunda bulunuyorsa, `Image.Load(Stream)` ile doğrudan akış olarak yükleyebilirsiniz. Böylece geçici bir dosya oluşturmanın önüne geçersiniz.

## Adım 3: Filtre Zinciri Uygulama – görüntü kontrastını artırma ve gürültüyü temizleme

Aspose OCR, kullanışlı bir filtre boru hattı ile gelir. Burada üç filtreyi zincirliyoruz:

1. **DeskewFilter** – metnin yatay oturması için dönüşü düzelterek rotasyonu sabitler.  
2. **DenoiseFilter** – harfleri bulanıklaştırmadan grenleri kaldırır.  
3. **ContrastFilter** – ön plan ve arka plan arasındaki farkı artırarak soluk karakterlerin ortaya çıkmasını sağlar.

```csharp
        // Pre‑process the image with a chain of filters
        var processedImage = inputImage
            .Apply(new DeskewFilter())          // correct rotation
            .Apply(new DenoiseFilter())         // reduce grain
            .Apply(new ContrastFilter(1.5f));   // boost contrast
```

**Neden bu filtreler?**  
- **Deskew**, doğru OCR için vazgeçilmezdir; birkaç derece sapma bile tanıma oranınızı yarıya indirebilir.  
- **Denoise**, telefon kamerası taramalarında sıkça gördüğünüz “görüntü gürültüsünü kaldır” sorununu çözer.  
- **Contrast**, düşük kontrastlı belgeler için gizli sos gibidir—solmuş makbuzları düşünün.  

`ContrastFilter` faktörünü (`1.0f` varsayılan) ayarlayabilirsiniz. `1.5f` üzerindeki değerler resmi aşırı aydınlatabilir, bu yüzden birkaç deneme yapın.

## Adım 4: Görüntü Metnini Tanıma – görüntüyü ocr yapmanın kalbi

Resim temizlendikten sonra OCR motoruna teslim ediyoruz.

```csharp
        // Recognize text from the processed image
        var ocrResult = ocrEngine.Recognize(processedImage);
```

`Recognize` metodu, çıkarılan dizeyi, güven skorlarını ve isterseniz vurgulama için sınırlayıcı kutuları içeren bir `OcrResult` nesnesi döndürür.

**Köşe durumu:** Resim birden fazla dil içeriyorsa, `ocrEngine.Language = Language.English | Language.Spanish;` şeklinde ayarlayabilirsiniz. Motor her iki sözlüğü de deneyecektir.

## Adım 5: Görüntüyü Göster ve Doğrula – uygulamanız için metin çıkarma

Son olarak metni konsola yazdırıyoruz. Gerçek bir uygulamada bunu bir veritabanına, bir dosyaya yazabilir ya da aşağı akış bir NLP borusuna besleyebilirsiniz.

```csharp
        // Display the extracted text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Beklenen çıktı:**  

```
=== OCR Result ===
Invoice #12345
Date: 2024‑01‑15
Total: $256.78
Thank you for your business!
```

Eğer bozuk karakterler görürseniz, Adım 3'e geri dönüp filtre parametrelerini ayarlayın. Çoğu zaman daha yüksek bir kontrast faktörü ya da ek bir `SharpenFilter` sorunu çözer.

## Yaygın Sorular & İpuçları

### Resmim zaten siyah‑beyaz ise ne yapmalıyım?  
`ContrastFilter`'ı atlayıp sadece `DenoiseFilter` kullanabilirsiniz. İkili bir görüntüyü aşırı kontrastlamak artefaktlara yol açabilir.

### Çok büyük dosyalar (>10 MB) nasıl yönetilir?  
Filtrelemeden önce resmi daha düşük bir çözünürlükte yükleyin (`Image.Load(path, new LoadOptions { DesiredWidth = 2000 })`). OCR motoru, metin okunaklı olduğu sürece ölçeklendirilmiş sürümlerle sorunsuz çalışır.

### Bunu bir web API içinde çalıştırabilir miyim?  
Kesinlikle. Aynı mantığı bir ASP.NET Core denetleyicisinde paketleyin, bir `IFormFile` kabul edin ve OCR sonucunu JSON olarak döndürün. `Image` nesnelerini dispose etmeyi unutmayın.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}